---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Use consultas do GraphQL para recuperar os dados do catálogo e potencializar as experiências do Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
source-git-commit: 935f34a8b4317686e67e33b50df3301d746fbd25
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Recuperar dados do catálogo com o GraphQL {#graphql-queries}

Use consultas do GraphQL para recuperar dados de produto, preço e outros dados do espaço de dados SaaS do catálogo do Adobe Commerce e use-os para renderizar experiências do Commerce com mais rapidez do que as consultas nativas do Adobe Commerce GraphQL.

O Serviço de Catálogo fornece as seguintes consultas:

| Query | Descrição | Uso |
|-------|-------------|-------|
| `categories` | Retorna dados de categoria. Se o objeto de entrada da subárvore for especificado, a consulta retornará detalhes sobre subcategorias. | Útil para renderizar a navegação da loja e as páginas de categoria. [Veja o exemplo.](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) |
| `products` | Retorna detalhes sobre as SKUs especificadas como entrada. | Usado principalmente para renderizar conteúdo nas páginas de detalhes e comparação de produtos. [Veja o exemplo.](https://developer.adobe.com/commerce/services/graphql/catalog-service/categories/) |
| `productSearch` | Retorna uma lista de produtos que correspondem aos critérios de pesquisa. | Útil para renderizar resultados de pesquisa e páginas de lista de produtos com base na entrada de pesquisa. [Veja o exemplo.](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/) |
| `refineProduct` | Restringe os resultados de uma execução de consulta de produtos em um produto complexo para retornar informações específicas sobre uma variante de produto. | Útil para renderizar páginas atualizadas de detalhes do produto quando os compradores selecionam uma opção de produto. [Veja o exemplo.](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) |
| `variants` | Retorna detalhes sobre todas as variações de um produto. | Útil para mostrar imagens variantes em páginas de detalhes do produto ou listagem sem enviar várias solicitações de API. [Veja o exemplo.](https://developer.adobe.com/commerce/services/graphql/catalog-service/product-variants/) |


Consulte o [Guia da API do Serviço de Catálogo](https://developer.adobe.com/commerce/services/graphql/catalog-service/) para obter mais informações sobre o uso dessas consultas

