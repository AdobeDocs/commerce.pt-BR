---
title: '[!DNL SaaS Data Export Guide]'
description: Saiba mais sobre como usar a extensão  [!DNL data export]  para serviços SaaS do Adobe Commerce que sincroniza dados entre o Adobe Commerce e os serviços Commerce conectados.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 2a09ef51939649a12b72c45cbb8b0dc0d0a4c8ad
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 0%

---

# Guia do [!DNL SaaS Data Export]

[!DNL SaaS data export] sincroniza dados entre uma instância do Adobe Commerce e o Commerce Services conectado. Ao adicionar o Live Search, as Recomendações de Produto, o Serviço de Catálogo ou o [!DNL Adobe Commerce Optimizer Connector] a uma instalação do Adobe Commerce, a extensão [!DNL Data export] é instalada automaticamente.

>[!NOTE]
>
>Se você instalar o [!DNL Adobe Commerce Optimizer Connector], a mesma extensão do [!DNL Data Export] coletará o catálogo e os feeds de preço de [!DNL Adobe Commerce]. Em seguida, o conector mapeia e envia esses feeds para [!DNL Adobe Commerce Optimizer] usando o Modelo de Dados de Catálogo de Composição (CCDM). Consulte a [[!DNL Adobe Commerce Optimizer Connector] visão geral](../aco-connector/overview.md) da instalação e arquitetura e o [Pipeline de sincronização do conector](../aco-connector/connector-sync-pipeline.md) para conhecer o comportamento de sincronização após a exportação.

A exportação de dados SaaS coleta e exporta vários tipos de dados, chamados de _feeds_, que agregam tipos específicos de informações. Dependendo dos serviços Commerce instalados, os feeds de exportação de dados SaaS incluem:

- **Feeds de entidade de catálogo** agregam dados de produto. Os dados incluem produtos, atributos de produto, preços de produto, variações de produto, categorias, permissões de categoria e permissões de produto.
- O **feed de Escopos** agrega dados para grupos de clientes, sites, lojas e visualizações de loja.
- O **feed de Ordem de Venda** agrega dados de pedidos, incluindo suas entidades relacionadas, como faturas, remessas, avisos de crédito e assim por diante.
- O **feed de Inventário MultisSource** agrega dados sobre os itens de status do estoque do estoque.

A exportação de dados SaaS é fornecida como uma extensão PHP. Ela é compatível com vários métodos para iniciar e gerenciar o processo de sincronização de dados.

- **Sincronização manual do Administrador ou da linha de comando**

   - O [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) no Administrador do Commerce fornece uma exibição gráfica do status de sincronização que mostra os dados do produto sincronizados com êxito com os commerce services. Você pode usar o painel para executar uma ressincronização completa (_sincronização completa_) de todos os feeds. No entanto, a Adobe recomenda apenas executar uma sincronização completa na primeira vez que você conecta o Adobe Commerce a um serviço do Commerce. Consulte [Processo de sincronização](data-synchronization.md).

     {{aco-data-sync-verification}}

   - A página [Status de sincronização do feed de dados](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) fornece insights em tempo real sobre a integridade e o desempenho dos feeds de exportação de dados que transferem dados de produto e categoria do Commerce para serviços externos, como Recomendações de produto, Live Search e Serviço de catálogo ou Adobe Commerce Optimizer.

   - A [ferramenta de linha de comando do Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) fornece comandos para sincronizar feeds específicos e inclui opções adicionais para personalizar o processamento do feed.

- **Sincronização automatizada com trabalhos cron**

   - [Sincronização de dados parciais](data-synchronization.md#partial-sync) — Os trabalhos do Cron acionam uma sincronização de dados parcial quando um usuário administrador do Commerce atualiza uma entidade. O processo de exportação de dados envia apenas essas atualizações para os serviços conectados da Commerce. O processo de sincronização parcial é baseado no mecanismo MView e não requer nenhuma ação do usuário administrador ou do integrador de sistema.

   - [Nova tentativa automática para erros de sincronização](data-synchronization.md#retry-failed-items-sync)—Os trabalhos do Cron acionam uma nova tentativa automática do processo de sincronização quando ocorrem erros durante o processo de sincronização de dados.

- **Exportar agendamento e desempenho**

   - Desenvolvedores e integradores de sistemas podem estimar o tempo necessário para a exportação de dados SaaS sincronizar dados entre o Adobe Commerce e os serviços conectados. Essa estimativa pode ajudar a agendar o processamento da exportação de dados para evitar a interrupção do site. Consulte [Estimar volume de dados e tempo de transmissão](estimate-data-volume-sync-time.md).

   - Nos casos em que a sincronização precisa ocorrer mais rapidamente, a exportação de dados do SaaS fornece opções de personalização para melhorar o desempenho do processamento da exportação. Consulte [Melhorar o desempenho da exportação de dados](customize-export-processing.md).

- **Rastrear e solucionar problemas de atividades de exportação de dados**—Use os logs de exportação de dados e de exportação de saas para revisar o status da sincronização e as cargas do feed durante o processo de sincronização e indexação. Consulte [Logs e solução de problemas](troubleshooting-logging.md).
