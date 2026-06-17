---
title: '[!DNL SaaS Data Export Guide]'
description: Saiba mais sobre como usar a extensão  [!DNL data export]  para serviços SaaS do Adobe Commerce que sincroniza dados entre o Adobe Commerce e os serviços Commerce conectados.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# Guia do [!DNL SaaS Data Export]

[!DNL SaaS data export] sincroniza dados entre uma instância do Adobe Commerce e o Commerce Services conectado. Ao adicionar o Live Search, as Recomendações de Produto, o Serviço de Catálogo ou o [!DNL Adobe Commerce Optimizer Connector] a uma instalação do Adobe Commerce, a extensão [!DNL Data Export] é instalada automaticamente.

>[!NOTE]
>
>Se você instalar o [!DNL Adobe Commerce Optimizer Connector], a mesma extensão do [!DNL Data Export] coletará o catálogo e os feeds de preço de [!DNL Adobe Commerce]. Em seguida, o conector mapeia e envia esses feeds para [!DNL Adobe Commerce Optimizer] usando o Modelo de Dados de Catálogo de Composição (CCDM). Consulte a [[!DNL Adobe Commerce Optimizer Connector] visão geral](../aco-connector/overview.md) da instalação e arquitetura e o [Pipeline de sincronização do conector](../aco-connector/connector-sync-pipeline.md) para conhecer o comportamento de sincronização após a exportação.

A exportação de dados SaaS coleta e exporta vários tipos de dados, chamados de _feeds_, que agregam tipos específicos de informações. Dependendo dos serviços Commerce instalados, os feeds de exportação de dados SaaS incluem:

- **Feeds de entidade de catálogo** agregam dados de produto. Os dados incluem produtos, atributos de produto, preços de produto, variações de produto, categorias, permissões de categoria e permissões de produto.
- O **feed de Escopos** agrega dados para grupos de clientes, sites, lojas e visualizações de loja.
- O **feed de Ordem de Venda** agrega dados de pedidos, incluindo suas entidades relacionadas, como faturas, remessas, avisos de crédito e assim por diante.
- O **feed de Inventário MultisSource** agrega dados sobre os itens de status do estoque do estoque.

A exportação de dados SaaS é fornecida como uma extensão PHP que oferece suporte à sincronização automática e manual:

- **Sincronização automatizada** — Após a sincronização completa inicial quando você conecta um serviço do Commerce, os trabalhos do cron mantêm os serviços conectados atualizados usando a sincronização parcial e a repetição automática de itens com falha, sem nenhuma ação necessária do usuário Administrador ou do integrador de sistemas.

- **Sincronização manual**—Execute uma ressincronização completa ou ressincronize os feeds selecionados do Administrador do Commerce ou da [CLI do Commerce](data-export-cli-commands.md).

- **Monitoramento**—Rastreie a integridade, o status e a entrega do feed da página [!UICONTROL Data Feed Sync Status] e do painel de Gerenciamento de Dados no Administrador do Commerce. Consulte [Gerenciar sincronização](data-sync-manage.md) para ver as etapas de verificação e ressincronização.

Para conhecer o comportamento da sincronização, os modos e o diagrama do fluxo de exportação, consulte [Como a sincronização funciona](sync-overview.md).

A exportação de dados SaaS também fornece ferramentas para planejar e solucionar problemas do processo de sincronização:

- **Agendamento e desempenho** — Estime o tempo de sincronização para agendar o processamento e evitar a interrupção do site, e personalize o processamento de exportação para melhorar o desempenho. Consulte [Estimar volume de dados e tempo de transmissão](estimate-data-volume-sync-time.md) e [Melhorar desempenho da exportação de dados](customize-export-processing.md).

- **Rastreamento e solução de problemas**—Revise o status da sincronização e as cargas do feed usando os logs de exportação de dados e exportação de saas. Consulte [Revisar logs e solucionar problemas](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Estender e personalizar feeds de exportação de dados SaaS](extensibility-and-customizations.md) — Adicionar ou modificar dados de feed.
> - [Cenários de solução de problemas](troubleshooting/troubleshooting-scenarios.md) — Diagnostique configurações incorretas e resultados de sincronização inesperados.
> - [Notas de versão](release-notes.md) — Atualizações de extensão e problemas conhecidos.
