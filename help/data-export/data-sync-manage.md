---
title: Exibir e Gerenciar o Processo de Sincronização
description: Saiba como exibir e gerenciar o processo de sincronização do  [!DNL SaaS Data Export]  usando o painel Gerenciamento de dados e a página Status de sincronização do feed de dados.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: d3cdead0-685a-4489-9250-4bb709942f66
last-update: 2026-06-23
source-git-commit: 7ce47d7abf7519a7e3ecd436faabf4089005cd63
workflow-type: tm+mt
source-wordcount: 557
ht-degree: 0%

---

# Exibir e gerenciar o processo de sincronização

A maioria das atividades de sincronização é processada automaticamente usando a sincronização completa, a sincronização parcial ou a sincronização de itens com falha de nova tentativa. Consulte [Tipos de sincronização](sync-overview.md#synchronization-types) para obter detalhes sobre quando cada tipo é executado. O [!DNL SaaS Data Export] também fornece ferramentas para monitorar, gerenciar e solucionar problemas do processo. Você pode visualizar o status da sincronização e gerenciar o processo de sincronização de dados usando os painéis da sua implantação.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

Para implantações do Adobe Commerce na nuvem, no local ou no Adobe Commerce as a Cloud Service, visualize e gerencie o processo de sincronização a partir destes recursos de administrador do Commerce:

- **[Página Status da Sincronização do Feed de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** — Verifique o status de exportação do feed para implantações conectadas a [!DNL Live Search], [!DNL Product Recommendations] ou [!DNL Catalog Service]. Este painel mostra o status de exportação de feed de cada feed, incluindo os erros encontrados. Uma exibição detalhada mostra o status de exportação do feed de itens de feed individuais.

- **[Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** — Os usuários administradores podem exibir e rastrear dados exportados e sincronizados com êxito com o Commerce Services conectado. Este painel mostra os dados do produto sincronizados com os Serviços da Commerce.

>[!NOTE]
>
>O painel Gerenciamento de dados e a página Status de sincronização do feed de dados só estarão disponíveis se você tiver o [!DNL Live Search], o [!DNL Product Recommendations] ou o [!DNL Catalog Service] instalado.

>[!TAB Adobe Commerce com Commerce Optimizer]

Para implantações locais ou na nuvem do Commerce integradas com o [!DNL Commerce Optimizer], exiba e gerencie o processo de sincronização usando os seguintes recursos:

- **[Página Status de Sincronização do Feed de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** — Monitore o status de exportação do feed do conector do Administrador do Commerce. Esta página mostra se os dados do catálogo foram exportados com êxito do [!DNL Adobe Commerce], incluindo detalhes de erro por feed e por item.

- **[Página Sincronização de Dados](../optimizer/setup/data-sync.md)** — A página Sincronização de Dados fornece uma visão geral do status de sincronização dos dados do produto provenientes da sua fonte de catálogo upstream no [!DNL Commerce Optimizer].

Para obter detalhes sobre como usar esses painéis para verificar se a sincronização de dados está funcionando e para ressincronizar os dados manualmente, consulte [Gerenciar sincronização](../aco-connector/data-sync-manage.md) no _Guia do Conector do Adobe Commerce Optimizer_.

>[!ENDTABS]

## Verifique se a sincronização de dados está funcionando {#verify-that-the-data-sync-is-working}


{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

## Ressincronizar dados manualmente

Quando a sincronização parcial e a repetição automática não resolvem os problemas de sincronização, é possível ressincronizar os dados manualmente pelo administrador do Commerce ou usando comandos da CLI do Commerce. As opções disponíveis dependem da implantação.

### Opções de ressincronização manual disponíveis {#manual-resync-options-commerce}

Use as opções a seguir para ressincronizar manualmente os dados do feed.

| Tarefa | Opção | Notas |
| --- | --- | --- |
| Ressincronizar itens de feed com falha ou problemáticos selecionados | **[!UICONTROL Data Feed Sync Status]página** | Monitore e ressincronize os itens de feed selecionados do administrador do Commerce. Consulte [Verificar se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working). |
| Ressincronização completa de todos os feeds | **[!UICONTROL Data Management Dashboard]** | Executar uma ressincronização completa de todos os feeds do Administrador do Commerce. A Adobe recomenda isso principalmente ao se conectar pela primeira vez a um serviço do Commerce. Os itens cujo hash de conteúdo não foi alterado desde a última exportação são ignorados. Consulte [Verificar se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working). |
| Ressincronização de feed direcionado com controle operacional | **CLI DO Commerce** | Use o comando `saas:resync` para ressincronizações de feed direcionadas. Consulte [Sincronizar feeds usando a CLI do Commerce](data-export-cli-commands.md). |

>[!MORELIKETHIS]
>
> - [Como a sincronização funciona](sync-overview.md) — Saiba mais sobre os modos de sincronização, sincronização completa, sincronização parcial e tente novamente os itens com falha.
> - [Sincronizar feeds usando a CLI do Commerce](data-export-cli-commands.md) — Use o comando `saas:resync` para ressincronizações de feed direcionadas.
> - [Revisar logs e solucionar problemas](troubleshooting/logging.md) — Diagnosticar erros de exportação de dados e exportação de SaaS.
> - [Gerenciar sincronização com [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md) — Verifique a sincronização de dados do catálogo e ressincronize manualmente os feeds do conector.
