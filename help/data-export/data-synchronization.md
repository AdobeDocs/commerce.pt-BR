---
title: Sincronizar dados com a exportação de dados SaaS
description: Saiba como o  [!DNL SaaS Data Export]  coleta e sincroniza dados entre instâncias do Adobe Commerce e serviços SaaS conectados.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 2a09ef51939649a12b72c45cbb8b0dc0d0a4c8ad
workflow-type: tm+mt
source-wordcount: 1104
ht-degree: 0%

---

# Sincronizar dados com a exportação de dados SaaS

Quando você instala um serviço do Commerce que requer exportação de dados, como Serviço de catálogo, Live Search ou Recomendações de produto, uma coleção de módulos de exportação de dados do Saas é instalada para gerenciar o processo de coleta e sincronização de dados.

A exportação de dados SaaS move os dados do produto de uma instância do Adobe Commerce para a plataforma de serviços da Commerce de forma contínua para manter os dados atualizados. Por exemplo, as Recomendações de produto exigem informações atuais do catálogo para retornar com precisão as recomendações com nomes, preços e disponibilidade corretos. Para obter detalhes sobre o monitoramento do processo de sincronização, consulte [Exibir e gerenciar o processo de sincronização](#view-and-manage-the-synchronization-process).


O diagrama a seguir mostra o fluxo de exportação de dados SaaS.

![Coleta de exportação de dados SaaS e fluxo de sincronização para Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Os principais componentes do fluxo de exportação de dados SaaS incluem:

- Módulos de exportação de dados SaaS que coletam os dados para feeds do Adobe Commerce, montam itens de feed, aguardam atualizações e persistem o status do feed.
- Módulos de exportação SaaS que exportam dados, configuram o roteamento e publicam os feeds para serviços conectados.
- O Serviço do Adobe Commerce gerencia o processo de assimilação de dados para validar feeds recebidos e atualizações persistentes nos serviços conectados.

>[!NOTE]
>
>Para [!DNL Adobe Commerce Optimizer Connector] implantações, [!DNL SaaS Data Export] manipula a detecção de alteração de entidade e o assembly de feed. O conector mapeia os feeds para o formato [!DNL Catalog Data Ingestion API] e os envia para [!DNL Adobe Commerce Optimizer]. Consulte [Pipeline de sincronização do conector](../aco-connector/connector-sync-pipeline.md) para controle de escopo, envio e tratamento de erros.

>[!NOTE]
>
>Para garantir uma programação perfeita e evitar interrupções nas operações do site, a Adobe recomenda estimar o volume de dados e o tempo de sincronização antes de iniciar qualquer sincronização do feed de dados. Essa estimativa é importante ao planejar sincronizações iniciais ou atualizações de catálogos em larga escala, como alterações de preço em massa. Para obter detalhes, consulte [Estimar volume de dados e tempo de transmissão para sincronização de dados](estimate-data-volume-sync-time.md)

## Modos de sincronização

A exportação de dados SaaS tem dois modos para processar feeds de entidade:

- **Modo de exportação imediata** — Neste modo, os dados são coletados e enviados imediatamente para o Commerce Service em uma única iteração. Esse modo acelera a entrega de atualizações de entidades ao serviço do Commerce e reduz o tamanho do armazenamento das tabelas de feed.

- **Modo de exportação herdado** — Neste modo, os dados são coletados em um único processo. Em seguida, um trabalho cron envia os dados coletados para os serviços de comércio conectados. Nas entradas do log de exportação de dados, os feeds que usam o modo herdado são rotulados como `(legacy)`.

## Tipos de sincronização

A exportação de dados SaaS suporta três tipos de sincronização - sincronização completa, sincronização parcial e nova tentativa de sincronização de itens com falha.

### Sincronização completa

Depois de conectar uma instância do Adobe Commerce ao Commerce Service, execute uma sincronização completa para enviar dados de feed de entidade do Adobe Commerce para o serviço conectado.

>[!NOTE]
>
>A sincronização completa é principalmente para a fase de integração. Evite o uso regular para evitar a sobrecarga do banco de dados. Após a sincronização inicial, as alterações em andamento são sincronizadas automaticamente usando a sincronização parcial.

### Sincronização parcial

Com a sincronização parcial, a exportação de dados SaaS envia automaticamente as atualizações do aplicativo Commerce, como alterações de nome de produto ou atualizações de preço, para os serviços de comércio conectados.

O processo de exportação de dados usa os seguintes trabalhos cron para automatizar a operação de sincronização parcial.

- trabalhos do grupo cron &quot;index&quot;:
   - O trabalho `indexer_reindex_all_invalid` reindexa todos os feeds inválidos. É um trabalho cron padrão do Adobe Commerce.
   - O trabalho `saas_data_exporter` é para feeds de exportação herdados.
   - O trabalho `sales_data_exporter` é específico ao feed de exportação de dados de vendas.

Esses trabalhos são executados a cada minuto.

Os mesmos trabalhos cron de sincronização parcial são executados para feeds [!DNL Adobe Commerce Optimizer Connector]. Para envio específico do conector e tratamento de erros, consulte [Pipeline de sincronização do conector](../aco-connector/connector-sync-pipeline.md).

Para que a sincronização parcial funcione, o aplicativo Commerce requer a seguinte configuração:

- [O agendamento de tarefas é habilitado através de trabalhos cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=pt-BR)

- Todos os indexadores de exportação de dados SaaS estão configurados no modo `Update by Schedule`.

  Na versão de exportação de dados SaaS 103.1.0 e posterior, o modo `Update by Schedule` é habilitado por padrão. Você pode verificar a configuração de índice no servidor usando o comando da CLI do Commerce, `bin/magento indexer:show-mode | grep -i feed`

### Repetir sincronização de itens com falha

A sincronização Repetir itens com falha usa um processo separado para reenviar itens que não foram sincronizados devido a erros durante o processo de sincronização, por exemplo, um erro de aplicativo, uma interrupção de rede ou um erro de serviço SaaS. A implementação desta sincronização também se baseia em trabalhos cron.

- `resync_failed_feeds_data_exporter` trabalhos do grupo cron:
   - O trabalho `<feed name>_feed_resend_failed_feeds_items` reenvia itens com falha de sincronização, por exemplo `products_feed_resend_failed_items`.

### Exibir e gerenciar o processo de sincronização

A maioria das atividades de sincronização é processada automaticamente com base na configuração do aplicativo. No entanto, a exportação de dados SaaS também fornece ferramentas para monitorar e gerenciar o processo.

- [!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."} **[Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**—Os usuários administradores podem exibir e rastrear dados sincronizados com os Serviços Commerce e disponíveis para os serviços de vitrine. Este painel mostra o produto sincronizado com os Serviços da Commerce.

  {{aco-data-sync-verification}}

- [!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a projetos da Adobe Commerce integrados ao Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} **[Página Status da Sincronização de Feed de Sincronização de Dados](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/setup/data-sync)** — Para projetos do Commerce que usam o [!DNL Adobe Commerce Optimizer], verifique a disponibilidade de dados de catálogo para sua loja na página Status da Sincronização de Feed de Dados no Adobe Commerce Optimizer. Este painel mostra o status de sincronização dos feeds de exportação de dados.

>[!NOTE]
>
>O painel Gerenciamento de dados só estará disponível se você tiver o Live Search, o Product Recommendations ou o Serviço de catálogo instalado. O painel Status de sincronização do feed de dados estará disponível se você tiver esses serviços ou se o [Adobe Commerce Optimizer Connector](../aco-connector/overview.md) estiver instalado. Para conhecer o comportamento do pipeline do conector do Otimizer, incluindo erros de controle de escopo e envio, consulte [Pipeline de sincronização do conector](../aco-connector/connector-sync-pipeline.md).

### Verificar a configuração do aplicativo do Commerce

A sincronização parcial e a sincronização de itens com falha de Repetir funcionam somente se a instância do Commerce tiver sido configurada corretamente. Normalmente, a configuração é concluída ao configurar o serviço do Commerce. Se a exportação de dados não estiver funcionando corretamente, verifique a seguinte configuração.

- [Confirme se os trabalhos cron estão em execução](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Verifique se os indexadores estão sendo executados do [Admin](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/index-management) ou usando o comando `bin/magento indexer:info` da CLI do Commerce.

- Verifique se os indexadores dos seguintes feeds estão definidos como `Update by Schedule`: Atributos do Catálogo, Produto, Substituições de Produto e Variante de Produto. Você pode verificar os indexadores do [Gerenciamento de Índice](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/index-management) no Administrador ou usando a CLI (`bin/magento indexer:show-mode | grep -i feed`).

### Notificações do gerenciador de eventos para o log de transferência de dados

Na versão 103.3.4 e posterior, a Exportação de dados SaaS despacha o evento `data_sent_outside` quando os dados são enviados da instância do Commerce para os serviços da Adobe Commerce.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>Para obter informações sobre eventos e como se inscrever neles, consulte [Eventos e Observadores](https://developer.adobe.com/commerce/php/development/components/events-and-observers) na Documentação do desenvolvedor do Adobe Commerce.
