---
title: Itens de linha para  [!DNL Payment Services]
description: Saiba mais sobre os itens de linha do  [!DNL Payment Services]  e como exibi-los no painel de comerciantes.
feature: Payments, Paas, Saas
role: User
exl-id: f690ff94-f83d-4525-9d52-1dea25a71060
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Itens de linha para [!DNL Payment Services]

Os itens de linha para [!DNL Payment Services] são os itens incluídos em um pedido. Esses itens de linha fornecem informações como:

* Detalhes do produto
* Quantidade
* Preço (incluindo impostos, descontos e outras informações relevantes)

Essas informações são úteis para o atendimento ao cliente, gerenciamento de pedidos e faturamento adequado.

Este recurso é habilitado por padrão para [!DNL Payment Services]. Para exibir itens de linha:

1. Navegue até seu [painel de comerciantes do PayPal](https://www.paypal.com/merchant/){target=_blank}.

1. Clique em **Atividade** > **Todas as transações**.

1. Selecione a ordem desejada e exiba seus itens de linha:

   > Exemplo de itens de linha na visualização de painel do comprador

   ![Exibição de itens de linha](assets/paypal-shopper-dashboard-line-items-view.png){width="500" zoomable="yes"}

## Atributos de itens de linha

Os itens de linha são gerados quando o pedido é feito por meio do Adobe Commerce e as informações são enviadas ao PayPal, com os seguintes atributos:

| Atributo | Tipo de dados | Descrição |
| --- | --- | --- |
| `name` | String! | O nome do item. Se um item tiver mais de uma linha devido a várias quantidades ou a uma emissão de arredondamento de imposto, o nome do item permanecerá o mesmo para todas as linhas, mas o preço exibido poderá variar um pouco devido ao arredondamento. |
| `unit_amount` | Objeto! | O preço ou a taxa do item por unidade. Inclui os seguintes atributos: `currency_code` e `value`. |
| `tax` | Objeto | O imposto do item para cada unidade. Inclui os seguintes atributos: `currency_code` e `value`. |
| `quantity` | String! | A quantidade do item. Será um número inteiro. |
| `description` | String | A descrição detalhada do item. |
| `sku` | String | A unidade de manutenção de estoque (ou SKU) do item. |
| `url` | String | O `URL` para o item que está sendo comprado. Visível para o comprador e usado nas experiências do comprador. |
| `upc` | Objeto | O Código Universal de Produto (ou UPC) do item. |
| `category` | String | O tipo de categoria do item. |

### `unit_amount` atributos

O objeto `unit_amount` contém os seguintes atributos:

| Atributo | Tipo de dados | Descrição |
| --- | --- | --- |
| `currency_code` | String! | O [código de moeda ISO-4217 de três caracteres](https://developer.paypal.com/api/rest/reference/currency-codes/) que identifica a moeda. |
| `value` | String! | Indica o valor do item. O `currency_code` determina o número necessário de casas decimais, se houver. |

### `tax` atributos

O objeto `tax` contém os seguintes atributos:

| Atributo | Tipo de dados | Descrição |
| --- | --- | --- |
| `currency_code` | String! | O [código de moeda ISO-4217 de três caracteres](https://developer.paypal.com/api/rest/reference/currency-codes/) que identifica a moeda. |
| `value` | String! | Indica o valor do item. Depende de cada `currency_code` para o número necessário de casas decimais. |

### `upc` atributos

O objeto `upc` contém os seguintes atributos:

| Atributo | Tipo de dados | Descrição |
| --- | --- | --- |
| `type` | sequência de caracteres! | O tipo de UPC. |
| `code` | sequência de caracteres! | O código de produto UPC do item. |

+++Exemplo de itens de linha

```json
{
    "name": "Crown Summit Backpack - 1",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD"
        "value": "3.13"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
},
{
    "name": "Crown Summit Backpack - 2",
    "unit_amount": {
        "currency_code": "USD",
        "value": "38.50"
    },
    "tax": {
        "currency_code": "USD",
        "value": "3.14"
    },
    "quantity": "1",
    "description": "The Crown Summit Backpack is equally at home in a gym locker, study cube or a pup tent, so be sure yours is packed with books,",
    "sku": "24-MB03",
    "url": "https://magento.test/crown-summit-backpack.html",
    "upc": {
        "type": "UPC-A",
        "code": "000003"
    },
    "category": "PHYSICAL_GOODS"
}
```

+++

Consulte a [documentação do desenvolvedor do PayPal sobre os itens de linha](https://developer.paypal.com/docs/api/orders/v2/#definition-line_item){target=_blank} para obter mais informações sobre esses campos e suas limitações.

## Gerenciar itens de linha

O Adobe Commerce [calcula o imposto com base no valor total de cada linha](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/site-store/taxes/taxes#warning-messages){target=_blank}, o que pode causar problemas de arredondamento se várias quantidades do mesmo item forem solicitadas ou se preços com imposto incluído forem exibidos no catálogo. Nesses casos, a quantidade total pode ser dividida em duas linhas, mas a quantidade será igual ao total de itens solicitados.

> Exemplo de itens de linha com problemas de arredondamento na exibição do painel do comerciante

![Exibição de itens de linha](assets/line-items-example.png){width="600" zoomable="yes"}

+++Como o Adobe Commerce calcula um problema de arredondamento em itens de linha

Os itens de linha para [!DNL Payment Services] equilibram esse problema de arredondamento de forma que o valor `unit_amount` ou `unit_tax` corresponda ao valor total do pedido. Um item pode ser dividido em duas linhas para resolver este problema de arredondamento:

* Quando o problema de arredondamento aparecer no `unit_amount`, o comerciante deverá ver uma diferença no preço dessa linha adicional.
* Quando o problema de arredondamento aparecer na `unit_tax`, nenhuma diferença será vista nos itens de linha individuais porque a `tax` não é exibida na grade, mas somente como um total na parte inferior.

+++
