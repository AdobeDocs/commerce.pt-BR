---
title: Mapeamento de campos para  [!DNL Adobe Commerce Optimizer Connector] Feeds
description: Saiba mais sobre o  [!DNL Adobe Commerce Optimizer Connector] mapeamento de campos de  [!DNL Adobe Commerce] dados de catálogo para  [!DNL Adobe Commerce Optimizer] formatos de API de assimilação para todos os feeds.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---


# Mapeamento de campos para feeds de conector

Esta página documenta como o [!DNL Adobe Commerce Optimizer Connector] transforma campos de catálogo [!DNL Adobe Commerce] no formato exigido pelo [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. Consulte a [referência do conector](connector-reference.md#supported-feeds) para obter a lista de feeds com suporte e seus pontos de extremidade de API.

## Produtos

O feed `products` envia dados para o [ponto de extremidade de produtos](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Notas |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin` corrigido para `"AdobeCommerce"` |
| `status` | `status` | Maiúscula; definida como `DISABLED` para produtos compostos sem filhos atribuídos |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | Valor separado por vírgulas dividido e mapeado: `Catalog`→`CATALOG`, `Search`→`SEARCH`; valores não mapeados descartados |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | String delimitada por nova linha dividida em matriz |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Objeto codificado em JSON `{inStock, lowStock, weight, weightType}`; sempre presente como a primeira entrada de atributo |
| `attributes[]` | `attributes[]` | Cada entrada mapeada para `{code, values[], variantReferenceId}`; `inStock`, `lowStock`, `weight`, `weightType` são excluídas (entram em `aco_ac_attributes`) |
| `images[]` | `images[]` | `url`, `label`; funções padrão mapeadas: `image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH`; funções fora do padrão vão para `customRoles[]` |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type` em maiúsculas; entradas sem `sku` descartadas |
| `parents[].productType` + `parents[].sku` | `links[]` | Tipo mapeado: `configurable`→`VARIANT_OF`, `bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`, `label`; tipo de opção `SWATCH` quando `swatchType` é definido, senão `CONFIGURABLE`; variante padrão de `isDefault`; os valores incluem `variantReferenceId`, `label`, `colorHex`, `imageUrl` |
| `bundle options` | `bundles[]` | `label`→`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; SKUs padrão de `isDefault`; os itens incluem `sku`, `qty`, `userDefinedQty` (`qtyMutability`) |

## Metadados de atributos do produto

O feed `productAttributes` envia dados para o [ponto de extremidade de metadados](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.


| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Notas |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Consulte a tabela de conversão abaixo |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | Adicionado à matriz quando `true` |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | Adicionado à matriz quando `true` |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | Adicionado à matriz quando `true` |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | Adicionado à matriz quando `true` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversão do tipo de dados

O conector deriva a API `dataType` dos campos `dataType` e `frontendInput` do Commerce na tabela de mapeamento acima. A tabela a seguir mostra as regras de conversão que o conector aplica.

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | API [!DNL Commerce Optimizer] `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` ou `select` | `TEXT` |
| `int` | qualquer outro | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| qualquer outro | - | `TEXT` |

>[!NOTE]
>
>Quando o `dataType` de um atributo é definido como `OBJECT`, a [API de produtos](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} trata o valor do atributo como um objeto estruturado em vez de uma cadeia de caracteres simples. No momento da consulta, a API tenta analisar o valor armazenado como JSON. Se a análise for bem-sucedida, o resultado será retornado como um objeto aninhado na resposta. **Esse comportamento é particularmente útil** quando você fornece atributos personalizados dinamicamente, por exemplo, para carregar dados estruturados ou de vários campos que não podem ser representados como um valor escalar. Para obter instruções, consulte [Adicionar atributos de produto dinamicamente](../../data-export/add-attribute-dynamically.md).

## Catálogos de preços

O feed `priceBooks` envia dados para o [ponto de extremidade de catálogos de preços](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

Ao contrário dos outros feeds de conector, o feed `priceBooks` não é coletado por um indexador [!DNL SaaS Data Export] em [!DNL Adobe Commerce]. O conector gera esse feed a partir do site e da configuração do grupo de clientes no Administrador.

Um **catálogo de preços base** é criado por site, mais um **catálogo de preços filho** por par de grupo de site-cliente.

**Fórmula da ID do catálogo de preços:**

- **Base** (preços normais): `priceBookId = websiteCode`
- **Filho** (grupo de clientes ou catálogo compartilhado): `priceBookId = websiteCode::sha1(customerGroupId)` onde `sha1(customerGroupId)` é o resumo hexadecimal SHA-1 da ID de inteiro do grupo de clientes

O feed de preços usa a mesma fórmula ao resolver a qual catálogo de preços uma entrada de preço pertence. Para saber como as vitrines resolvem o `priceBookId` de uma sessão de cliente, consulte [Integração de vitrines headless](../headless-storefront.md#graphql-commerceoptimizer-query).

| Campo gerado | Campo de API [!DNL Commerce Optimizer] | Notas |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| Nome do site | `name` | Catálogo de preços base: nome do site. Filho: `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | Presente somente em catálogos de preços filhos; aponta para o catálogo de preços base |
| Moeda base do site | `currency` | Presente somente em tabelas de preços base; herdado por filhos |

## Preços

O feed `prices` envia dados para o [ponto de extremidade de preços](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Notas |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | exemplo de descontos: preço especial, preço de regra de catálogo, preço de catálogo compartilhado |
| `tierPrices[]` | `tierPrices[]` | |

## Categorias

O feed `categories` envia dados para o [ponto de extremidade de Categorias](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Itens com um `urlPath` vazio (categorias de raiz lógica) são ignorados e nunca enviados.

| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Notas |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | String delimitada por nova linha dividida em matriz |
| `image` | `images[].url` | Matriz de elemento único; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` quando ambos `true`, `[]` caso contrário |

>[!MORELIKETHIS]
>
> - [Assimilar dados de produto e preço com a API de assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — saiba mais sobre o modelo de dados de catálogo de metadados, produtos, categorias, tabelas de preços e preços
> - [Referência da API REST de assimilação de dados do catálogo](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Examine os esquemas de solicitação e resposta para cada ponto de extremidade de feed
> - [Como o [!DNL Commerce Optimizer Connector] funciona com o [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — Saiba como exibições da loja, sites e grupos de clientes são mapeados para fontes de catálogo e catálogos de preços
> - [Catálogos de preços em [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — Gerenciar catálogos de preços criados pela exportação do conector
> - [Integração headless com vitrine](../headless-storefront.md#graphql-commerceoptimizer-query) — Resolva `priceBookId` para sessões com clientes
