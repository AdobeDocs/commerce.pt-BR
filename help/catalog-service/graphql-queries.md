---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Use consultas do GraphQL para recuperar os dados do catálogo e potencializar as experiências do Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: null
workflow-type: tm+mt
source-wordcount: 268
ht-degree: 0%

---

# Recuperar dados do catálogo com o GraphQL {#graphql-queries}

Use consultas do GraphQL para recuperar dados de produto, preço e outros dados do espaço de dados SaaS do catálogo do Adobe Commerce e use-os para renderizar experiências do Commerce com mais rapidez do que as consultas nativas do Adobe Commerce GraphQL.

{{aco-merchandising-services}}

O Serviço de Catálogo fornece as seguintes consultas:

| Query | Descrição | Uso |
|-------|-------------|-------|
| `categories` | Retorna dados de categoria. Se o objeto de entrada da subárvore for especificado, a consulta retornará detalhes sobre subcategorias. | Útil para renderizar a navegação da loja e as páginas de categoria. [Veja o exemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Retorna detalhes sobre as SKUs especificadas como entrada. | Usado principalmente para renderizar conteúdo nas páginas de detalhes e comparação de produtos. [Veja o exemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Retorna uma lista de produtos que correspondem aos critérios de pesquisa. | Útil para renderizar resultados de pesquisa e páginas de lista de produtos com base na entrada de pesquisa. [Veja o exemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Restringe os resultados de uma execução de consulta de produtos em um produto complexo para retornar informações específicas sobre uma variante de produto. | Útil para renderizar páginas atualizadas de detalhes do produto quando os compradores selecionam uma opção de produto. [Veja o exemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Retorna detalhes sobre todas as variações de um produto. | Útil para mostrar imagens variantes em páginas de detalhes do produto ou listagem sem enviar várias solicitações de API. [Veja o exemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

Consulte [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) para obter mais informações sobre como usar essas consultas.
