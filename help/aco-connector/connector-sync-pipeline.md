---
title: Pipeline de sincronização de catálogo
description: Saiba como o pipeline de sincronização  [!DNL Adobe Commerce Optimizer Connector]  funciona, incluindo transformação de feed, agendamentos cron, controle de escopo e tratamento de erros.
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: c18ed297-2187-4aec-affb-9d9654eca6fcid: c32adafa-ed01-4b31-997e-2413013911b0id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: cc250cf1-34eb-4863-80d0-d170d45ea067id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 662
ht-degree: 1%

---

# Pipeline de sincronização do conector

Criado em [[!DNL SaaS Data Export]](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview), o **[!DNL Adobe Commerce Optimizer Connector]** mapeia os dados coletados pelos indexadores [!DNL SaaS Data Export] para o formato exigido pelo [!DNL Adobe Commerce Optimizer] [!DNL Catalog Data Ingestion API] e manipula a autenticação, o envio em lote e o controle de sincronização baseado em escopo. As seções abaixo descrevem como essa sincronização funciona.

Contexto relacionado:

- Saiba mais sobre o valor comercial, os principais recursos e a arquitetura da integração no tópico [[!DNL Commerce Optimizer Connector] visão geral](overview.md).

- Para obter os nomes dos pacotes de módulo, pontos de extremidade da API de feed e caminhos de chave de configuração, consulte a [Referência do conector](reference/connector-reference.md)

## Como a sincronização funciona

O diagrama a seguir mostra a sincronização de dados de [!DNL Adobe Commerce] a [!DNL Commerce Optimizer] através de [!DNL Adobe I/O Gateway].

![Diagrama de sincronização de alto nível do Commerce Optimizer Connector](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

Quando os dados do catálogo são alterados no [!DNL Adobe Commerce], a sincronização percorre esses estágios.

1. **Detecção de Alteração de Entidade** — (a cada 1 min) Um trabalho cron (`indexer_reindex_all_invalid`) detecta [!DNL Adobe Commerce] alterações de entidade e aciona [!DNL SaaS Data Export], que monta itens de feed.
1. **Transformação** — A [!DNL Commerce Optimizer Connector] seleciona os feeds agrupados, mapeia entidades e escopos de [!DNL Adobe Commerce] para os formatos exigidos pela API [!DNL Commerce Optimizer] e prepara a carga para transmissão.
1. **Transmissão** — Os dados transformados são enviados via HTTP POST (`/v1/catalog/<feed name>`) por meio de [!DNL Adobe I/O Gateway] para [!DNL Commerce Optimizer], que valida e mantém os feeds de entrada.
1. **Persistir resultados** — Persistir status de resposta da API nas [tabelas de feed](reference/connector-reference.md#supported-feeds).
1. **Nova tentativa com falha** (a cada 5 min) — um trabalho cron separado (`*_resend_failed_items`) detecta itens de feed com falha e os reenvia pelo mesmo pipeline.

### Trabalhos cron agendados

Os trabalhos cron a seguir automatizam o pipeline em uma programação fixa.

| Grupo Cron | Trabalho do Cron | Finalidade | Cronograma |
|-------------------------------------|-------------------------------|------------------------------------------------------------------------------|----------------|
| `index` | `indexer_update_all_views` | Acompanha atualizações de entidade, monta itens de feed, mantém o status do feed | A cada 1 minuto |
| `index` | `indexer_reindex_all_invalid` | Executar ressincronização completa para índices de feed marcados como &quot;Reindexação necessária&quot; | A cada 1 minuto |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Verifica itens de feed com falha e os reenvia para [!DNL Commerce Optimizer] | A cada 5 minutos |
| `commerce_data_export` | `cleanup_deleted_feed_items` | Limpa itens de feed excluídos sincronizados após o período de retenção (7 dias) | Todos os dias às 2:00 AM |

A extensão **[!DNL SaaS Data Export]** lida com a coleta de feeds e o rastreamento de status. A camada do conector mapeia entidades e escopos para o formato exigido pela API [!DNL Commerce Optimizer] e os envia por meio de `POST /v1/catalog/<feed name>`.

#### Requisitos

- [cron do Commerce deve estar em execução](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}.
- Os indexadores de feed devem usar o modo **[!UICONTROL Update by Schedule]**. Consulte [Sincronização parcial](../data-export/sync-overview.md#partial-sync){target="_blank"}.

## Controle de sincronização baseado em escopo

O módulo `CommerceOptimizerScopeMapper` lê as configurações de exportação por site e por armazenamento e as impõe durante a coleta e o envio do feed.

- **Escopos habilitados** para exportar dados no agendamento delta normal.
- **Escopos desabilitados** foram excluídos do pipeline.
As entidades sincronizadas anteriormente serão removidas de [!DNL Commerce Optimizer] na próxima execução do cron.

Se os problemas de sincronização afetarem apenas uma origem de catálogo ou catálogo de preços, consulte [Dados não sincronizados](troubleshooting.md#data-not-syncing).

Para obter detalhes sobre como personalizar o escopo de sincronização, consulte [Personalizar a configuração de exportação de escopos do Commerce](get-started.md#customize-the-commerce-scopes-export-configuration).

## Calendário e monitoramento

| Cenário | Tempo típico |
| -------- | -------------- |
| Atualizações de catálogo de rotina | 1 a 2 ciclos de sincronização delta (aproximadamente 1 a 2 minutos para indexação, além do envio) |
| Falhas transitórias | Repetido a cada 5 minutos |
| Sincronização completa ou catálogos grandes | Minutos a horas |

Monitorar status por feed da página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) no Administrador do Commerce. Consulte [Verificar se a sincronização de dados está funcionando](./data-sync-manage.md#verify-that-the-data-sync-is-working).

## Envio de feed e tratamento de erros

O processo `FeedSubmitter` lida com [!DNL Catalog Data Ingestion API] chamadas.

1. Separa os itens de atualização dos itens de exclusão (diferentes pontos de extremidade de API).
1. Chama, atualiza e exclui pontos de extremidade independentemente.
1. Mescla os resultados de status por item novamente em uma única resposta.

### Mesclagem de código do status HTTP

Quando as chamadas de atualização e exclusão retornam códigos de status diferentes, `FeedSubmitter` combina os resultados da seguinte maneira.

| Atualizar resultado | Exclui o resultado | Resultado final |
| --------------- | --------------- | ------------- |
| 200 | 200 ou nenhum | Sucesso 200 |
| 200 | 400 | 200 com erros de exclusão |
| 400 | 400 | 400 erros mesclados |
| outro | outro | REPETÍVEL |

| Tipo de erro | Comportamento |
| ---------- | -------- |
| **400** | Os itens listados no campo de resposta `errors` são exibidos no Administrador e exigem atenção. Outros itens no lote são repetidos. |
| **5xx** | Repetido pelos trabalhos de cron `*_feed_resend_failed_items` específicos do feed no grupo `resync_failed_feeds_data_exporter`. |

>[!MORELIKETHIS]
>
> - [Visão geral do conector](overview.md) — Saiba mais sobre mapeamento de escopo e contexto comercial
> - [Referência do conector](reference/connector-reference.md) — Revisar módulos, pontos de extremidade de API e chaves de configuração
> - [Personalizar a configuração de exportação de escopos do Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration) — Configurar feeds por nível de escopo, habilitar e desabilitar comportamento e etapas de Administrador
> - [Solução de problemas](troubleshooting.md) — Diagnosticar falhas de sincronização
