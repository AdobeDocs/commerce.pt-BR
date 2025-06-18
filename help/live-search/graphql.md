---
title: GraphQL
description: O  [!DNL Live Search] espaço de trabalho do GraphQL permite criar consultas com seus dados dinâmicos.
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

O espaço de trabalho *GraphQL* permite que os administradores criem e testem consultas do GraphQL usando seus próprios dados.

Este espaço de trabalho dá suporte às consultas [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) e [`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/).

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
