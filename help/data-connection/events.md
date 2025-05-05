---
title: Eventos comportamentais
description: Saiba quais dados cada evento comportamental captura.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '4516'
ht-degree: 0%

---

# [!DNL Data Connection] Eventos comportamentais

Veja a seguir uma lista dos eventos comportamentais do Commerce disponíveis ao instalar a extensão [!DNL Data Connection]. Os dados que esses eventos coletam são enviados para a Adobe Experience Platform. Você também pode criar [eventos personalizados](custom-events.md) para coletar dados adicionais não fornecidos imediatamente.

Além dos dados coletados pelos eventos a seguir, você também obtém [outros dados](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=pt-BR) fornecidos pelo Adobe Experience Platform Web SDK.

Os eventos comportamentais coletam dados comportamentais anônimos dos compradores enquanto eles navegam pelo site. Você pode usar os dados que esses eventos coletam para criar promoções e campanhas direcionadas a um conjunto específico de compradores.

>[!NOTE]
>
>Todos os eventos comportamentais incluem o campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=pt-BR), que inclui o endereço de email do comprador, quando disponível, e a ECID.

## Eventos da loja

Os eventos da vitrine eletrônica capturam dados das interações dos compradores no site e incluem eventos como [`addToCart`](#addtocart), [`pageView`](#pageview), [`createAccount`](#createaccount), [`editAccount`](#editaccount), [`startCheckout`](#startcheckout), [`completeCheckout`](#completecheckout), [`signIn`](#signin), [`signOut`](#signout), e assim por diante. Os eventos da vitrine eletrônica se aplicam apenas a produtos simples e configuráveis.

### addToCart

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um produto é adicionado ao carrinho ou quando a quantidade de um produto no carrinho é incrementada. | `commerce.productListAdds` |

#### Dados coletados de addToCart

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListAdds` | Indica se um produto foi adicionado a um carrinho de compras. Um valor de `1` indica que um produto foi adicionado. |
| `commerce.cart.cartID` | A ID exclusiva que identifica o carrinho do cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### openCart

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um novo carrinho é criado, ou seja, quando um produto é adicionado a um carrinho vazio. | `commerce.productListOpens` |

#### Dados coletados do openCart

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListOpens` | Indica se um carrinho foi criado. Um valor de `1` indica que um carrinho foi criado. |
| `commerce.cart.cartID` | A ID exclusiva que identifica o carrinho do cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### removeFromCart

| Descrição | Nome do evento XDM |
|---|---|
| Acionado sempre que um produto é removido ou sempre que a quantidade de um produto no carrinho é reduzida. | `commerce.productListRemovals` |

#### Dados coletados de removeFromCart

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListRemovals` | Indica se um produto foi removido do carrinho. Um valor de `1` indica que um produto foi removido do carrinho. |
| `commerce.cart.cartID` | A ID exclusiva que identifica o carrinho do cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### shoppingCartView

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando qualquer página do carrinho é carregada. | `commerce.productListViews` |

#### Dados coletados de shoppingCartView

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productListViews` | Indica se uma lista de produtos foi exibida. |
| `commerce.cart.cartID` | A ID exclusiva que identifica o carrinho do cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `commerce.order` | Contém informações sobre o pedido pendente de um ou mais produtos. |
| `commerce.order.discountAmount` | Indica o valor do desconto aplicado a todo o pedido. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### pageView

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando qualquer página é carregada. | `web.webpagedetails.pageViews` |

#### Dados coletados de pageView

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `web.webPageDetails.pageViews` | Indica se uma página foi carregada. Um `value` de `1` indica que a página foi carregada. |
| `web.webPageDetails.URL` | O URL normativo ou usual da página da Web. Esta pode ser a URL real usada para acessar a página, que seria registrada usando `Web Link`. |
| `web.webPageDetails.name` | O nome normativo da página da Web. Esse nome não é necessariamente o título da página ou diretamente associado ao conteúdo da página, mas é usado para organizar as páginas de um site para fins de classificação. |
| `web.webReferrer.URL` | O URL da página da Web que um comprador visitou antes de clicar em um link para seu site. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### productPageView

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando qualquer página de produto é carregada. | `commerce.productViews` |

#### Dados coletados de productPageView

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.productViews` | Indica se o produto foi visualizado. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### startCheckout

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando o comprador clica em um botão de check-out. | `commerce.checkouts` |

#### Dados coletados de startCheckout

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.checkouts` | Indica se uma ação ocorreu durante o processo de check-out. |
| `commerce.cart.cartID` | A ID exclusiva que identifica o carrinho do cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### completeCheckout

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando o comprador faz um pedido. | `commerce.purchases` |

#### Dados coletados de completeCheckout

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.purchases` | Indica se um pedido foi aceito. |
| `commerce.order` | Contém informações sobre o pedido feito de um ou mais produtos. |
| `commerce.order.purchaseID` | Identificador exclusivo atribuído pelo vendedor para esta compra ou contrato. Não há garantia de que a ID seja exclusiva. |
| `commerce.order.payments` | A lista de pagamentos deste pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador exclusivo desta transação de pagamento. |
| `commerce.order.payments.paymentAmount` | O valor do pagamento. |
| `commerce.order.payments.paymentType` | O método de pagamento deste pedido. Opções: `cash`, `credit_card`, `debit_card`, `gift_card`, `check`, `paypal`, `wire_transfer`, `credit_card_reference`, `other`. |
| `commerce.order.payments.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.order.taxAmount` | O valor do imposto pago pelo comprador como parte do pagamento final. |
| `commerce.order.discountAmount` | Indica o valor do desconto aplicado a todo o pedido. |
| `commerce.order.createdDate` | A hora e a data em que um novo pedido é criado no sistema de comércio. Por exemplo, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Detalhes de remessa de um ou mais produtos. |
| `commerce.shipping.shippingMethod` | O método de entrega escolhido pelo cliente, como entrega padrão, entrega expressa, retirada na loja e assim por diante. |
| `commerce.shipping.shippingAmount` | O valor que o cliente teve de pagar pelo envio. |  | `shipping` | Detalhes de remessa de um ou mais produtos. |
| `commerce.shipping.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

## Eventos de perfil do cliente

Os eventos de perfil capturados da loja incluem informações da conta, como `signIn`, `signOut`, `createAccount` e `editAccount`. Esses dados são usados para ajudar a preencher os principais detalhes do cliente necessários para definir melhor os segmentos ou executar campanhas de marketing, como enviar ofertas de desconto de inscrição, confirmações de alterações de conta etc. Há eventos de perfil semelhantes capturados no [lado do servidor](events-backoffice.md#customer-profile-events).

### signIn

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um comprador tenta entrar. | `userAccount.login` |

>[!NOTE]
>
> Esse evento é acionado quando uma ação específica é tentada. Não indica que a ação tenha sido julgada procedente.

#### Dados coletados do logon

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Um ator, contato ou proprietário individual. |
| `person.accountID` | Registra a ID da conta do usuário. |
| `person.accountType` | Registra o tipo de conta de usuário, como `Personal` ou `Company`, se aplicável. |
| `person.personalEmailID` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `personalEmail` | Captura detalhes de contato - um email e informações associadas. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `userAccount` | Indica detalhes de fidelidade, preferências, processos de logon e outras preferências de conta. |
| `userAccount.login` | Indica se um visitante tentou fazer logon. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### signOut

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando um comprador tenta sair. | `userAccount.logout` |

>[!NOTE]
>
> Esse evento é acionado quando uma ação específica é tentada. Não indica que a ação tenha sido julgada procedente.

#### Dados coletados da saída

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `userAccount` | Indica detalhes de fidelidade, preferências, processos de logon e outras preferências de conta. |
| `userAccount.logout` | Indica se um visitante tentou fazer logoff. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### createAccount

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador tenta criar uma conta. | `userAccount.createProfile` |

>[!NOTE]
>
> Esse evento é acionado quando uma ação específica é tentada. Não indica que a ação tenha sido julgada procedente.

#### Dados coletados de createAccount

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Um ator, contato ou proprietário individual. |
| `person.accountID` | Registra a ID da conta do usuário. |
| `person.accountType` | Registra o tipo de conta de usuário, como `Personal` ou `Company`, se aplicável. |
| `person.personalEmailID` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `personalEmail` | Captura detalhes de contato - um email e informações associadas. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `userAccount` | Indica detalhes de fidelidade, preferências, processos de logon e outras preferências de conta. |
| `userAccount.updateProfile` | Indica se um usuário atualizou seu perfil de conta. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### editAccount

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador tenta editar uma conta. | `userAccount.updateProfile` |

>[!NOTE]
>
> Esse evento é acionado quando uma ação específica é tentada. Não indica que a ação tenha sido julgada procedente.

#### Dados coletados de editAccount

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Um ator, contato ou proprietário individual. |
| `person.accountID` | Registra a ID da conta do usuário. |
| `person.accountType` | Registra o tipo de conta de usuário, como `Personal` ou `Company`, se aplicável. |
| `person.personalEmailID` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `personalEmail` | Captura detalhes de contato - um email e informações associadas. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `userAccount` | Indica detalhes de fidelidade, preferências, processos de logon e outras preferências de conta. |
| `userAccount.updateProfile` | Indica se um usuário atualizou seu perfil de conta. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

## Pesquisar eventos

Os eventos de pesquisa fornecem dados relevantes para a intenção do comprador. O insight sobre a intenção do comprador ajuda os comerciantes a ver como eles estão procurando por itens, em que clicam e, em última análise, compram ou abandonam os produtos. Um exemplo de como você pode usar esses dados é se quiser direcionar os compradores existentes que pesquisam pelo seu produto principal, mas nunca compram o produto. Você deve instalar a extensão [[!DNL Live Search]](../live-search/install.md) para acessar esses eventos.

Use os campos `searchRequest.id` e `searchResponse.id` encontrados nos eventos `searchRequestSent` e `searchResponseReceived` para fazer referência cruzada de uma solicitação de pesquisa para a resposta de pesquisa correspondente.

### searchRequestSent

| Descrição | Nome do evento XDM |
|---|---|
| Acionado pelos seguintes eventos no popover &quot;pesquisar ao digitar&quot;:<br><br>Pressione Enter, Clique em _Exibir Todos_<br><br> Acionado pelos seguintes eventos nas páginas de resultados da pesquisa:<br><br>Selecione um filtro, Altere a ordem de classificação (_Classificar por_), Altere a direção de classificação (crescente ou decrescente), Altere o número de resultados por página (_Mostrar # por página_), Navegue até a próxima página, Navegue até a página anterior, Navegue até uma página diferente | `searchRequest` |

>[!NOTE]
>
>Os eventos de pesquisa não são suportados em uma Adobe Commerce Enterprise Edition com a extensão B2B instalada.

#### Dados coletados de searchRequestSent

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchRequest` | Indica se uma solicitação de pesquisa foi enviada. |
| `searchRequest.id` | O identificador exclusivo para esta solicitação de pesquisa específica. |
| `searchRequest.value` | O valor quantificável da solicitação. |
| `siteSearch` | Contém informações sobre a pesquisa. |
| `siteSearch.filter` | Indica se algum filtro foi aplicado para limitar os resultados da pesquisa. |
| `siteSearch.filter.attribute` (filtro) | A faceta de um item usada para determinar se ele deve ser incluído nos resultados da pesquisa. |
| `siteSearch.filter.isRange` | Quando verdadeiro, os valores indicam pontos de extremidade de um intervalo aceitável de valores. |
| `siteSearch.filter.value` | Valor de atributo usado para determinar quais itens são incluídos nos resultados da pesquisa. |
| `siteSearch.sort` | Indica como os resultados da pesquisa devem ser classificados. |
| `siteSearch.sort.attribute` (classificar) | Um atributo usado para classificar itens nos resultados da pesquisa. |
| `siteSearch.sort.order` | A ordem na qual retornar os resultados da pesquisa. |
| `siteSearch.query` | Os termos procurados. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### searchResponseReceived

| Descrição | Nome do evento XDM |
|---|---|
| Acionado quando o Live Search retorna resultados para o pop-over &quot;pesquisar ao digitar&quot; ou para a página de resultados da pesquisa. | `searchResponse` |

>[!NOTE]
>
>Os eventos de pesquisa não são suportados em uma Adobe Commerce Enterprise Edition com a extensão B2B instalada.

#### Dados coletados de searchResponseReceived

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `searchResponse` | Indica se uma resposta de pesquisa foi recebida. |
| `searchResponse.id` | O identificador exclusivo para esta resposta de pesquisa específica. |
| `searchResponse.value` | O valor quantificável da resposta. |
| `siteSearch.numberOfResults` | O número de produtos devolvidos. |
| `siteSearch.suggestions` | Uma matriz de strings que inclui os nomes de produtos e categorias existentes no catálogo que são semelhantes à consulta de pesquisa. |
| `productListItems` | Uma variedade de produtos que foram adicionados ao carrinho de compras. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.productImageUrl` | URL da imagem principal do produto. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

## Eventos B2B

![B2B para Adobe Commerce](../assets/b2b.svg) Para comerciantes B2B, você deve [instalar](install.md#install-the-b2b-extension) a extensão `experience-platform-connector-b2b` para acessar esses eventos.

Os eventos B2B contêm informações de [lista de requisições](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=pt-BR), como se uma lista de requisições tivesse sido criada, adicionada ou excluída de. Ao rastrear eventos específicos para listas de requisição, você pode ver quais produtos seus clientes compram frequentemente e criar campanhas com base nesses dados.

### createRequisitionList

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador cria uma lista de requisições. | `commerce.requisitionListOpens` |

#### Dados coletados de createRequisitionList

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListOpens` | Indica a inicialização de uma nova lista de requisições. |
| `commerce.requisitionList` | As propriedades da lista de requisições criada pelo cliente. |
| `commerce.requisitionList.ID` | Identificador exclusivo da lista de requisições. |
| `commerce.requisitionList.name` | Nome da lista de requisições especificada pelo cliente. |
| `commerce.requisitionList.description` | Descrição da lista de requisições especificada pelo cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |

### addToRequisitionList

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador adiciona um produto a uma lista de requisições existente ou ao criar uma lista. | `commerce.requisitionListAdds` |

#### Dados coletados de addToRequisitionList

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListAdds` | Indica a adição de um ou mais produtos a uma lista de requisições. |
| `commerce.requisitionList` | As propriedades da lista de requisições criada pelo cliente. |
| `commerce.requisitionList.ID` | Identificador exclusivo da lista de requisições. |
| `commerce.requisitionList.name` | Nome da lista de requisições especificada pelo cliente. |
| `commerce.requisitionList.description` | Descrição da lista de requisições especificada pelo cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma matriz de produtos que foram adicionados à lista de requisições. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### removeFromRequisitionList

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador remove um produto de uma lista de requisições. | `commerce.requisitionListRemovals` |

#### Dados coletados de removeFromRequisitionList

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requsitionListRemovals` | Indica a remoção de um ou mais produtos de uma lista de requisições. |
| `commerce.requisitionList` | As propriedades da lista de requisições criada pelo cliente. |
| `commerce.requisitionList.ID` | Identificador exclusivo da lista de requisições. |
| `commerce.requisitionList.name` | Nome da lista de requisições especificada pelo cliente. |
| `commerce.requisitionList.description` | Descrição da lista de requisições especificada pelo cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
| `productListItems` | Uma matriz de produtos que foram adicionados à lista de requisições. |
| `productListItems.SKU` | Unidade de manutenção de estoque. O identificador exclusivo do produto. |
| `productListItems.name` | O nome de exibição ou o nome legível do produto. |
| `productListItems.priceTotal` | O preço total do item de linha do produto. |
| `productListItems.quantity` | O número de unidades de produto no carrinho. |
| `productListItems.discountAmount` | Indica o valor de desconto aplicado. |
| `productListItems.currencyCode` | Código monetário [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` ou `EUR`. |
| `productListItems.selectedOptions` | Campo usado para um produto configurável. |
| `productListItems.selectedOptions.attribute` | Identifica um atributo do produto configurável, como `size` ou `color`. |
| `productListItems.selectedOptions.value` | Identifica o valor do atributo, como `small` ou `black`. |

### deleteRequisitionList

| Descrição | Nome do evento XDM |
|---|---|
| Disparado quando um comprador exclui uma lista de requisições. | `commerce.requisitionListDeletes` |

#### Dados coletados de deleteRequisitionList

A tabela a seguir descreve os dados coletados para esse evento.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/namespaces.html?lang=pt-BR). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `commerce.requisitionListDeletes` | Indica que uma lista de requisições foi deletada. |
| `commerce.requisitionList` | As propriedades da lista de requisições criada pelo cliente. |
| `commerce.requisitionList.ID` | Identificador exclusivo da lista de requisições. |
| `commerce.requisitionList.name` | Nome da lista de requisições especificada pelo cliente. |
| `commerce.requisitionList.description` | Descrição da lista de requisições especificada pelo cliente. |
| `commerce.commerceScope` | Indica onde um evento ocorreu (exibição de loja, loja, site e assim por diante). |
| `commerce.commerceScope.environmentID` | A ID do ambiente. Uma ID alfanumérica de 32 dígitos separada por hifens. |
| `commerce.commerceScope.storeCode` | O código de armazenamento exclusivo. Você pode ter muitas lojas por site. |
| `commerce.commerceScope.storeViewCode` | O código exclusivo de exibição da loja. Você pode ter muitas exibições de loja por loja. |
| `commerce.commerceScope.websiteCode` | O código exclusivo do site. Você pode ter muitos sites em um ambiente. |
