---
title: Integração da loja headless [!DNL Adobe Commerce Optimizer Connector]
description: Saiba como integrar vitrines headless à  [!DNL Adobe Commerce Optimizer Connector] API do GraphQL, IDs da tabela de preços e codificação de pacotes de add-to-cart.
feature: Storefront, Integration, GraphQL
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# Integração com a loja headless

O módulo `CommerceAdapter` estende [!DNL Adobe Commerce] para preencher a lacuna entre uma loja headless e [!DNL Adobe Commerce Optimizer]. Ela fornece uma consulta GraphQL para resolver o contexto do catálogo de preços do cliente e impõe a codificação do produto do pacote esperada pela API do GraphQL [!DNL Adobe Commerce Optimizer].

Para obter instruções de configuração de vitrine de alto nível, consulte [Configurar merchandising e vitrines](./overview.md#merchandising-storefronts) na visão geral do [!DNL Adobe Commerce Optimizer Connector].

## GraphQL: consulta `commerceOptimizer` {#graphql-commerceoptimizer-query}

As vitrines headless chamam a consulta do GraphQL `commerceOptimizer` para recuperar o `priceBookId` da sessão de cliente atual. Transmita este valor para a [[!DNL Adobe Commerce Optimizer] API do GraphQL](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"} ao buscar preços.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

Exemplo de resposta:

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

Como `priceBookId` é resolvido:

| Estado da sessão | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| Convidado (sem logon) | `websiteCode::sha1(0)`, onde `0` é a ID do grupo de clientes convidados |
| Cliente conectado | `websiteCode::sha1(customerGroupId)` |

O cabeçalho de solicitação `Store` determina o escopo do site e, portanto, o componente `websiteCode`. O componente `sha1(customerGroupId)` corresponde à fórmula de ID do catálogo de preços usada durante a sincronização de dados. Consulte [Price books](reference/field-mapping.md#price-books).

## Produtos do pacote: formato de adição ao carrinho {#bundle-products-add-to-cart-format}

Permitir que os compradores adicionem produtos de pacote ao carrinho de uma loja headless com apenas a `SKU` e `qty` para cada opção de pacote selecionada.

Cada valor de opção selecionado ou inserido deve ser codificado na base64 no seguinte formato:

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

O mesmo SKU filho pode aparecer apenas uma vez em todas as opções.

Exemplo ([!DNL JavaScript]):

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
