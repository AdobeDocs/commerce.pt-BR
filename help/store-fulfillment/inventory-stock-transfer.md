---
title: Transferência do Inventory management Source
description: Configure os estoques do  [!DNL Store Fulfillment solution]  com o Adobe Commerce Inventory management. Configure um novo estoque e transfira o estoque do estoque padrão para que você possa atribuí-lo às fontes configuradas para habilitar os recursos de Retirada da Loja exigidos pela solução de Atendimento da Loja.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Transferência do Inventory management Source

A solução [!DNL Store Fulfillment] usa o Adobe Commerce Inventory management nativo. Por padrão, a configuração [!DNL Commerce] atribui todo o inventário da Web ao estoque padrão, que não pode ter fontes adicionais atribuídas. Como um site só pode ter um único estoque atribuído, um comerciante deve configurar um novo estoque e, opcionalmente, transferir seu inventário de origem padrão para uma origem atribuída ao escopo apropriado. Em seguida, a origem pode ser atribuída ao novo estoque.

>[!IMPORTANT]
>
>Os comerciantes devem manter a fonte padrão para todos os produtos incluídos em grupos e tipos de produtos de pacote. Esses produtos precisam de uma quantidade de estoque que atenda ao limite de quantidade mínima para itens de estoque e inclua um status de estoque de [!UICONTROL In Stock].

Essas alterações de configuração ajudam você a realizar três coisas:

1. [Transferir estoque para origem](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/quantities/inventory-transfer) para mover o estoque padrão/origem para o novo estoque/origem.

1. [Atribuir fontes](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/quantities/bulk-assignment) em massa para adicionar as novas fontes para todos os seus produtos.

1. [Conclua as atualizações em massa dos atributos de produto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update) para adicionar os atributos `Allow Store Pickup` e `Allow Home Delivery` aos produtos existentes. Quando a solução é instalada, os atributos têm os *valores padrão* ideais. No entanto, esses atributos não são aplicados aos produtos existentes até que você conclua o processo de updaContes em massa.

O estoque é deduzido da origem selecionada (localização da loja de varejo ou depósito de comércio eletrônico). As origens usadas como depósitos de comércio eletrônico devem ser atribuídas ao mesmo estoque que o local de retirada da loja e priorizadas antes dos locais de varejo. Para obter informações adicionais, consulte [Priorizando fontes para um estoque](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources).

Para obter mais informações sobre gerenciamento de inventário, estoques e fontes, consulte a documentação do usuário do Adobe Commerce:

- [Gerenciando o inventário](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/introduction)

- [Gerenciando Quantidades de Inventário](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/quantities/quantities-manage)

- [Gerenciando o Stock](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/stocks/stocks-manage)

- [Gerenciando fontes](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/sources/sources-manage)

- [Priorizando fontes para um estoque](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- [Atualizações em massa para atributos de produto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>A alteração da configuração para fontes de estoque e estoque também pode ter impacto downstream nos sistemas integrados. Certifique-se de entender como as alterações na configuração do inventário afetam esses sistemas.
