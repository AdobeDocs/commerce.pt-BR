---
title: Gerenciar [!DNL Adobe Commerce Optimizer Connector] Sincronização
description: Saiba como verificar a sincronização de dados do catálogo e ressincronizar manualmente os feeds do conector entre [!DNL Adobe Commerce] e [!DNL Adobe Commerce Optimizer].
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 0bfd368c50707692c7a0adda6e70e3776bd9692a
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# Gerenciar sincronização com [!DNL Commerce Optimizer]

Após configurar o [!DNL Adobe Commerce Optimizer Connector], a maioria das atualizações de catálogo sincroniza automaticamente por meio de trabalhos cron agendados. Para obter detalhes sobre como a sincronização automática funciona, consulte [Pipeline de sincronização do conector](connector-sync-pipeline.md). Use as ferramentas neste tópico para verificar se os dados atingem [!DNL Adobe Commerce Optimizer] e para ressincronizar manualmente os feeds quando necessário.

## Verifique se a sincronização de dados está funcionando {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Ressincronizar dados manualmente {#manually-resync-data}

Quando a sincronização parcial e a repetição automática não resolvem os problemas de sincronização, é possível ressincronizar manualmente os dados do catálogo. A opção escolhida depende do local de origem do problema e do controle necessário.

| Tarefa | Opção | Notas |
| --- | --- | --- |
| Verifique o status de sincronização e ressincronize a partir do sistema upstream quando os produtos estiverem ausentes | **Ressincronização do sistema upstream** | Em [!DNL Commerce Optimizer], selecione **[!UICONTROL Data Sync]** e verifique se as fontes de catálogo, os produtos, os preços e os atributos esperados são exibidos. Quando os produtos estiverem ausentes, faça a ressincronização a partir da instância [!DNL Adobe Commerce] upstream usando a página **[!UICONTROL Data Feed Sync Status]** ou a CLI do Commerce (consulte as linhas a seguir). |
| Ressincronizar itens de feed de conector com falha ou problemáticos selecionados | **[!UICONTROL Data Feed Sync Status]página no Administrador do Commerce** | Monitore o status da exportação e ressincronize os itens de feed do conector selecionados do administrador do Commerce. Consulte [Verificar se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working). |
| Ressincronização de feed do conector direcionado com controle operacional | **CLI DO Commerce** | Execute `saas:resync` a partir da instância do Adobe Commerce para feeds de conector. Consulte [Sincronizar feeds usando a CLI do Commerce](../data-export/data-export-cli-commands.md) e [Feeds com suporte](reference/connector-reference.md#supported-feeds). |

>[!MORELIKETHIS]
>
> - [Pipeline de sincronização do conector](connector-sync-pipeline.md) — Saiba como a sincronização automatizada, as agendas de cron e a manipulação de erros funcionam
> - [Estimar volume de dados e tempo de sincronização](reference/estimate-data-volume-sync-time.md) — Calcular duração de sincronização esperada
> - [Solução de problemas](troubleshooting.md) — Diagnosticar problemas de exportação de credencial, sincronização e escopo
> - [Módulos de conector e pontos de extremidade de feed](reference/connector-reference.md) — Revise módulos, pontos de extremidade de API e feeds com suporte
> - [Página Status da sincronização do feed de dados no Administrador do Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} — Saiba mais sobre os campos e recursos disponíveis para monitorar o status do feed
> - Painel de Sincronização de Dados [&#x200B; em  [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce-optimizer/data-sync/data-sync){target="_blank"} — Documentação de referência para campos e ações disponíveis para monitorar a sincronização de dados do catálogo
