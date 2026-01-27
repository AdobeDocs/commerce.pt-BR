---
title: Eventos de back-office
description: Saiba quais dados cada evento de back office captura.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 6ffa18a9f66b6be8cd40bda5aedc911b26fe0e1d
workflow-type: tm+mt
source-wordcount: '3619'
ht-degree: 0%

---

# [!DNL Data Connection] Eventos de Back Office

Veja a seguir uma lista dos eventos de back office do Commerce disponíveis quando você instala a extensão [!DNL Data Connection]. Os dados que esses eventos coletam são enviados para a Adobe Experience Platform. Você também pode criar [eventos personalizados](custom-events.md) para coletar dados adicionais não fornecidos imediatamente.

Além dos dados coletados pelos eventos a seguir, você também obtém [outros dados](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=pt-BR) fornecidos pelo Adobe Experience Platform Web SDK.

Os eventos de back office contêm dados do lado do servidor. Estes dados incluem [status do pedido](#order-status) informações como se um pedido foi feito, cancelado, reembolsado, remetido ou concluído. Os dados do lado do servidor também incluem [informações sobre eventos de perfil do cliente](#customer-profile-events), como se uma conta foi criada, atualizada ou excluída.

>[!NOTE]
>
>Todos os eventos de back office incluem o campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=pt-BR), que inclui o endereço de email do comprador, quando disponível, e a ECID.

## Status do pedido

Os dados de status do pedido mostram uma visualização 360 do pedido do comprador. Essa visualização ajuda os comerciantes a direcionar ou analisar melhor todo o status do pedido ao desenvolver campanhas de marketing. Por exemplo, você pode detectar tendências em determinadas categorias de produtos que apresentam um bom desempenho em diferentes épocas do ano. Tais como roupas de inverno que vendem melhor durante os meses mais frios ou certas cores do produto que os compradores estão interessados ao longo dos anos. Além disso, os dados de status do pedido podem ajudar você a calcular o valor vitalício do cliente, entendendo a propensão do comprador para converter com base em pedidos anteriores.

### orderPlaced

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um comprador faz um pedido. | `commerce.backofficeOrderPlaced` |

#### Dados coletados de orderPlaced

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.payments` | A lista de pagamentos deste pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador exclusivo desta transação de pagamento. |
| `commerce.order.payments.paymentAmount` | O valor do pagamento. |
| `commerce.order.payments.paymentType` | O método de pagamento deste pedido. Contado, valores personalizados permitidos. |
| `commerce.order.payments.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.order.taxAmount` | O valor do imposto pago pelo comprador como parte do pagamento final. |
| `commerce.order.discountAmount` | Indica o valor do desconto aplicado a todo o pedido. |
| `commerce.order.createdDate` | A hora e a data em que um novo pedido é criado no sistema de comércio. Por exemplo, `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | O código de moeda ISO 4217 usado para os totais do pedido. |
| `commerce.shipping` | Detalhes de remessa de um ou mais produtos. |
| `commerce.shipping.shippingMethod` | O método de entrega escolhido pelo cliente, como entrega padrão, entrega expressa, retirada na loja e assim por diante. |
| `commerce.shipping.shippingAmount` | O valor que o cliente teve de pagar pelo envio. |
| `commerce.shipping.currencyCode` | O código de moeda ISO 4217 usado para o total de remessa. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `commerce.billing.address` | Endereço postal para cobrança. |
| `commerce.billing.address.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua |
| `commerce.billing.address.street2` | Campo adicional para informações no nível da rua. |
| `commerce.billing.address.city` | O nome da cidade. |
| `commerce.billing.address.state` | O nome do estado. Este é um campo de forma livre. |
| `commerce.billing.address.postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `commerce.billing.address.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.id` | O identificador de item de linha para esta entrada de produto. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |

### orderInvoiced

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um comerciante envia uma NFF para solicitar pagamento. | `commerce.backofficeOrderInvoiced` |

#### Dados coletados de orderInvoiced

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.priceTotal` | O preço total deste pedido após a aplicação de todos os descontos e impostos. |
| `commerce.order.currencyCode` | O código de moeda ISO 4217 usado para os totais do pedido. |
| `commerce.order.purchaseOrderNumber` | Identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |
| `commerce.order.payments` | A lista de pagamentos deste pedido. |
| `commerce.order.payments.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.order.payments.paymentType` | O método de pagamento deste pedido. Contado, valores personalizados permitidos. |
| `commerce.order.payments.paymentAmount` | O valor do pagamento. |
| `commerce.shipping` | Detalhes de remessa de um ou mais produtos. |
| `commerce.shipping.shippingMethod` | O método de entrega escolhido pelo cliente, como entrega padrão, entrega expressa, retirada na loja e assim por diante. |
| `commerce.shipping.shippingAmount` | O valor que o cliente teve de pagar pelo envio. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.id` | O identificador de item de linha para esta entrada de produto. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |

### orderItemsShipped

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um item da ordem é entregue. | `commerce.backofficeOrderItemsShipped` |

#### Dados coletados de orderItemsShipped

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.payments` | A lista de pagamentos deste pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador exclusivo desta transação de pagamento. |
| `commerce.order.payments.paymentAmount` | O valor do pagamento. |
| `commerce.order.payments.paymentType` | O método de pagamento deste pedido. Contado, valores personalizados permitidos. |
| `commerce.order.payments.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.order.priceTotal` | O preço total deste pedido após a aplicação de todos os descontos e impostos. |
| `commerce.order.purchaseOrderNumber` | Identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |
| `commerce.order.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.order.lastUpdatedDate` | A hora em que um determinado registro de pedido foi atualizado pela última vez no sistema de comércio. |
| `commerce.shipping` | Detalhes de remessa de um ou mais produtos. |
| `commerce.shipping.shippingMethod` | O método de entrega escolhido pelo cliente, como entrega padrão, entrega expressa, retirada na loja e assim por diante. |
| `commerce.shipping.shippingAmount` | O valor que o cliente teve de pagar pelo envio. |
| `commerce.shipping.address` | O endereço físico de entrega. |
| `commerce.shipping.address.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua. |
| `commerce.shipping.address.street2` | Segunda linha opcional de informações da rua. |
| `commerce.shipping.address.city` | O nome da cidade. |
| `commerce.shipping.address.state` | O nome do Estado. Este é um campo de forma livre. |
| `commerce.shipping.address.postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `commerce.shipping.address.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `commerce.shipping.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.shipping.trackingNumber` | O número de rastreamento fornecido pela transportadora para uma remessa de item de pedido. |
| `commerce.shipping.trackingURL` | O URL para rastrear o status de envio de um item do pedido. |
| `commerce.shipping.shipDate` | A data em que um ou mais itens de uma ordem são entregues. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `commerce.billing.address` | Endereço postal para cobrança. |
| `commerce.billing.address.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua |
| `commerce.billing.address.street2` | Campo adicional para informações no nível da rua. |
| `commerce.billing.address.city` | O nome da cidade. |
| `commerce.billing.address.state` | O nome do estado. Este é um campo de forma livre. |
| `commerce.billing.address.postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `commerce.billing.address.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |

### orderCanceled

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um comprador cancela um pedido. | `commerce.backofficeOrderCancelled` |

#### Dados coletados de orderCanceled

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.purchaseOrderNumber` | Identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |
| `commerce.order.cancelDate` | A data e a hora em que um comprador cancela um pedido. |
| `commerce.order.lastUpdatedDate` | A hora em que um determinado registro de pedido foi atualizado pela última vez no sistema de comércio. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |

### orderLineItemReembolsado

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um comprador é reembolsado por um item devolvido. | `commerce.backofficeCreditMemoIssued` |

#### Dados coletados de orderLineItemRefund

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.lastUpdatedDate` | A hora em que um determinado registro de pedido foi atualizado pela última vez no sistema de comércio. |
| `commerce.order.purchaseOrderNumber` | Identificador exclusivo atribuído pelo comprador para esta compra ou contrato. |
| `commerce.refunds` | A lista de reembolsos para este pedido. |
| `commerce.refunds.transactionID` | Identificador exclusivo deste reembolso. |
| `commerce.refunds.refundAmount` | O valor da restituição. |
| `commerce.refunds.refundPaymentType` | O método de pagamento deste pedido. Contado, valores personalizados permitidos. |
| `commerce.refunds.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |

### orderItemsReturnInitiated

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador solicita o retorno de um item. | `commerce.backofficeOrderItemsReturnInitiated` |

#### Dados coletados de orderItemsReturnInitiated

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.returns` | As informações de RMA (Autorização para devolução de produto) deste pedido. |
| `commerce.order.returns.returnID` | O identificador exclusivo desta RMA (Autorização para devolução de produto). |
| `commerce.order.returns.returnStatus` | O status da RMA (Autorização para devolução de produto), como Pendente, Fechado etc. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |
| `productListItems.returnItem` | As informações de RMA (Autorização para Devolução de Mercadoria) para este item. |
| `productListItems.returnItem.returnStatus` | O status do item devolvido, como Pendente, Aprovado, etc. |
| `productListItems.returnItem.returnReason` | O motivo pelo qual uma devolução é solicitada para este item. |
| `productListItems.returnItem.returnItemCondition` | A condição do item para o qual a devolução é solicitada. |
| `productListItems.returnItem.returnResolution` | A resolução solicitada do item que está sendo devolvido, como Reembolso, Troca, etc. |
| `productListItems.returnItem.returnQuantityRequested` | O número deste item que o comprador solicitou devolução. |
| `productListItems.returnItem.returnQuantityAuthorized` | O número deste item que está autorizado a ser devolvido. |
| `productListItems.returnItem.eturnQuantityReceived` | O número de itens devolvidos recebidos. |
| `productListItems.returnItem.returnQuantityApproved` | O número deste item com devolução totalmente concluída e aprovada. |

### orderItemReturnCompleted

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um item que um comprador solicitou devolver é concluído. | `commerce.backofficeOrderItemsReturnCompleted` |

#### Dados coletados de orderItemReturnCompleted

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.returns` | As informações de RMA (Autorização para devolução de produto) deste pedido. |
| `commerce.order.returns.returnID` | O identificador exclusivo desta RMA (Autorização para devolução de produto). |
| `commerce.order.returns.returnStatus` | O status da RMA (Autorização para devolução de produto), como Pendente, Fechado etc. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |
| `productListItems.returnItem` | As informações de RMA (Autorização para Devolução de Mercadoria) para este item. |
| `productListItems.returnItem.returnStatus` | O status do item devolvido, como Pendente, Aprovado, etc. |
| `productListItems.returnItem.returnReason` | O motivo pelo qual uma devolução é solicitada para este item. |
| `productListItems.returnItem.returnItemCondition` | A condição do item para o qual a devolução é solicitada. |
| `productListItems.returnItem.returnResolution` | A resolução solicitada do item que está sendo devolvido, como Reembolso, Troca, etc. |
| `productListItems.returnItem.returnQuantityRequested` | O número deste item que o comprador solicitou devolução. |
| `productListItems.returnItem.returnQuantityAuthorized` | O número deste item que está autorizado a ser devolvido. |
| `productListItems.returnItem.eturnQuantityReceived` | O número de itens devolvidos recebidos. |
| `productListItems.returnItem.returnQuantityApproved` | O número deste item com devolução totalmente concluída e aprovada. |

### orderShippingCompleted

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando uma remessa é concluída. | `commerce.backofficeOrderShipmentCompleted` |

#### Dados coletados de orderShippingCompleted

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `commerce.order` | Contém informações sobre o pedido. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.payments` | A lista de pagamentos deste pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador exclusivo desta transação de pagamento. |
| `commerce.order.payments.paymentAmount` | O valor do pagamento. |
| `commerce.order.payments.paymentType` | O método de pagamento deste pedido. Contado, valores personalizados permitidos. |
| `commerce.order.payments.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.order.taxAmount` | O valor do imposto pago pelo comprador como parte do pagamento final. |
| `commerce.order.createdDate` | A hora e a data em que um novo pedido é criado no sistema de comércio. Por exemplo, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Detalhes de remessa de um ou mais produtos. |
| `commerce.shipping.shippingMethod` | O método de entrega escolhido pelo cliente, como entrega padrão, entrega expressa, retirada na loja e assim por diante. |
| `commerce.shipping.shippingAmount` | O valor que o cliente teve de pagar pelo envio. |
| `commerce.shipping.shipDate` | A data em que um ou mais itens de uma ordem são entregues. |
| `commerce.shipping.address` | O endereço físico de entrega. |
| `commerce.shipping.address.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua. |
| `commerce.shipping.address.street2` | Segunda linha opcional de informações da rua. |
| `commerce.shipping.address.city` | O nome da cidade. |
| `commerce.shipping.address.state` | O nome do Estado. Este é um campo de forma livre. |
| `commerce.shipping.address.postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `commerce.shipping.address.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `commerce.billing.address` | Endereço postal para cobrança. |
| `commerce.billing.address.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua |
| `commerce.billing.address.street2` | Campo adicional para informações no nível da rua. |
| `commerce.billing.address.city` | O nome da cidade. |
| `commerce.billing.address.state` | O nome do estado. Este é um campo de forma livre. |
| `commerce.billing.address.postalCode` | O código postal da localização. Os códigos postais não estão disponíveis para todos os países. Em alguns países, conterá apenas parte do código postal. |
| `commerce.billing.address.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos no pedido. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |
| `productListItems.categories` | Contém informações sobre a categoria de um produto. |
| `productListItems.categories.id` | O identificador exclusivo da categoria. |
| `productListItems.categories.name` | O nome da categoria. |
| `productListItems.categories.path` | O caminho para a categoria. |

## Eventos de perfil do cliente

Os eventos de perfil capturados do lado do servidor incluem informações de conta, como `accountCreated`, `accountUpdated` e `accountDeleted`. Esses dados são usados para ajudar a preencher os principais detalhes do cliente necessários para definir melhor os segmentos ou executar campanhas de marketing, como enviar ofertas de desconto de inscrição, confirmações de alterações de conta etc. Há eventos de perfil semelhantes capturados da [vitrine](events.md#customer-profile-events).

>[!NOTE]
>
>Cada evento de perfil de cliente também inclui o campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=pt-BR), que inclui a ID de cliente da Commerce gerada pelo sistema como o identificador principal do perfil e uma ID de email usada como um identificador secundário. [Saiba](custom-identities.md) como criar atributos de identidade personalizados para aprimorar a identificação do perfil do cliente.

### accountCreated

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador tenta criar uma conta. | `userAccount.backofficeCreateProfile` |

#### Dados coletados de accountCreated

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `person` | Contém informações sobre o cliente. |
| `person.name` | Contém informações sobre o nome do cliente. |
| `person.name.firstName` | Contém o nome do cliente. |
| `person.name.lastName` | Contém o sobrenome do cliente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### accountUpdated

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador tenta editar uma conta. | `userAccount.backofficeUpdateProfile` |

#### Dados coletados de accountUpdated

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `person` | Contém informações sobre o cliente. |
| `person.name` | Contém informações sobre o nome do cliente. |
| `person.name.firstName` | Contém o nome do cliente. |
| `person.name.lastName` | Contém o sobrenome do cliente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### accountDeleted

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador tenta excluir uma conta. | `userAccount.backofficeDeleteProfile` |

#### Dados coletados de accountDeleted

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `person` | Contém informações sobre o cliente. |
| `person.name` | Contém informações sobre o nome do cliente. |
| `person.name.firstName` | Contém o nome do cliente. |
| `person.name.lastName` | Contém o sobrenome do cliente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
