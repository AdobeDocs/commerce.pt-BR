---
title: GraphQL
description: O  [!DNL Live Search] espaço de trabalho do GraphQL permite criar consultas com seus dados dinâmicos.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

O espaço de trabalho *GraphQL* permite que os administradores criem e testem consultas do GraphQL usando seus próprios dados.

Este espaço de trabalho dá suporte às consultas [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) e [`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/).

![espaço de trabalho do GraphQL](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
		name
      }
    }
    facets {
      title
    }
  }
}
```

Variáveis:

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```

