---
title: Mapeamento de campos para Feeds [!DNL Adobe Commerce Optimizer Connector]
description: Saiba mais sobre o mapeamento de campos [!DNL Adobe Commerce Optimizer Connector] dos dados do catálogo [!DNL Adobe Commerce] para os formatos de API de assimilação [!DNL Adobe Commerce Optimizer] para todos os feeds.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 1e34df4f07f9043675104fce55c58e0617463b33
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# Mapeamento de campos para feeds de conector

Esta página documenta como o [!DNL Adobe Commerce Optimizer Connector] transforma campos de catálogo [!DNL Adobe Commerce] no formato exigido pelo [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. Consulte a [referência do conector](connector-reference.md#supported-feeds) para obter a lista de feeds com suporte e seus pontos de extremidade de API.

## Produtos

O feed `products` envia dados para o [ponto de extremidade de produtos](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Detalhes do mapeamento |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | Define `origin` para `"AdobeCommerce"` |
| `status` | `status` | Converte o status em maiúsculas. Usa `DISABLED` se o status estiver ausente ou se um produto configurável ou agrupado não tiver valores de opção. |
| `description` | `description` | Usa uma string vazia se a descrição estiver ausente. |
| `shortDescription` | `shortDescription` | Usa uma string vazia se a descrição curta estiver ausente. |
| `visibility` | `visibleIn` | Divide o valor separado por vírgulas e mapeia `Catalog` a `CATALOG` e `Search` a `SEARCH`. Descarta outros valores. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Divide palavras-chave separadas por nova linha em uma matriz e elimina espaços em branco. |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Sempre adiciona uma entrada `aco_ac_attributes` como o primeiro atributo. Seu valor JSON inclui `inStock` e `lowStock` como cadeias de caracteres. Inclui `weight` e `weightType` quando esses valores estão disponíveis. |
| `attributes[]` | `attributes[]` | Mapeia cada entrada para seu código de atributo, valores de sequência de caracteres e ID de referência de variante correspondente, quando disponível. Ignora `inStock`, `lowStock`, `categories`, `weight` e `weightType`. Os valores relacionados ao estoque estão incluídos em `aco_ac_attributes`. As categorias são exportadas como rotas. |
| `images[]` | `images[]` | Ignora imagens sem uma URL.<br>Exporta `url`, `label` (vazio se ausente) e `sortOrder` (número inteiro, o padrão é `0`).<br>Classifica imagens por `sortOrder` em ordem crescente.<br>Mapeia funções padrão: `image` para `BASE`, `small_image` para `SMALL`, `thumbnail` para `THUMBNAIL` e `swatch_image` para `SWATCH`. Exporta outras funções como `customRoles[]`. |
| `categoryData[].categoryPath` | `routes[].path` | Ignora entradas com um caminho de categoria vazio. |
| `categoryData[].productPosition` | `routes[].position` | Usa `0` se a posição do produto estiver ausente. |
| `links[].type` + `links[].sku` | `links[]` | `type` em maiúsculas; entradas sem `sku` descartadas |
| `parents[].productType` + `parents[].sku` | `links[]` | Mapeia `configurable` para `VARIANT_OF` e `bundle` ou `bundle_fixed` para `IN_BUNDLE`. Converte outros tipos de produto em maiúsculas. Ignora os pais sem um SKU. |
| `configurable options` | `configurations[]` | Exporta opções que têm uma ID e pelo menos um valor.<br>Mapeia `id` a `attributeCode`. Define `type` como `SWATCH` quando `swatchType` está presente, caso contrário, como `CONFIGURABLE`.<br>Usa a ID do valor padrão como `defaultVariantReferenceId`.<br>Mapeia cada valor para `variantReferenceId`, `label`, `colorHex` e `imageUrl`. |
| `bundle options` | `bundles[]` | Exporta opções que contêm pelo menos um item.<br>Usa o rótulo de opção como `group` ou `Bundle group` se o rótulo estiver vazio. Copia `required` para a saída.<br>Define `multiSelect` como `true` para os tipos de renderização `checkbox` e `multi`.<br>Lista as SKUs padrão em `defaultItemSkus`. Cada item inclui `sku`, `qty` (o padrão é `0`) e `userDefinedQty` (de `qtyMutability`, o padrão é `false`). |

## Metadados de atributos do produto

O feed `productAttributes` envia dados para o [ponto de extremidade de metadados](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.

| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Detalhes do mapeamento |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Consulte a tabela de conversão abaixo |
| `dataType` e `frontendInput` | `dataType` | Usa as regras de conversão abaixo. |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | Quando um sinalizador é `true`, adiciona seu valor correspondente:<br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversão do tipo de dados

Quando `dataType` for `int`, o conector verificará `frontendInput`. Para outros tipos de dados, `frontendInput` não afeta a conversão.

| Entrada `dataType` | Entrada `frontendInput` | Saída `dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` ou `select` | `TEXT` |
| `int` | Qualquer outro valor, incluindo um valor ausente | `INTEGER` |
| `decimal` | Não usado | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | Não usado | `TEXT` |
| `OBJECT` | Não usado | `OBJECT` |
| Qualquer outro valor | Não usado | `TEXT` |

>[!NOTE]
>
>Quando um atributo usa o tipo de dados `OBJECT`, a [API de produtos](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} tenta analisar seu valor armazenado como JSON. Se a análise for bem-sucedida, a API retornará o valor como um objeto aninhado. Use `OBJECT` para dados de atributo estruturado que não podem ser representados como um valor único. Para obter instruções, consulte [Adicionar atributos de produto dinamicamente](../../data-export/add-attribute-dynamically.md).

## Catálogos de preços

O feed `priceBooks` envia dados para o [ponto de extremidade de catálogos de preços](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

Ao contrário dos outros feeds de conector, o feed `priceBooks` não é coletado por um indexador [!DNL SaaS Data Export] em [!DNL Adobe Commerce]. O conector gera esse feed a partir do site e da configuração do grupo de clientes no Administrador.

Para cada site, o conector cria um catálogo de preços base e um catálogo de preços filho para cada grupo de clientes.

Usar estas fórmulas para `priceBookId`:

- Catálogos de preços base para preços regulares: `priceBookId = websiteCode`.
- Catálogos de preços filhos para grupos de clientes: `priceBookId = websiteCode::sha1(customerGroupId)`, onde `sha1(customerGroupId)` é o resumo hexadecimal SHA-1 da ID do número inteiro do grupo de clientes.

O feed de preços usa a mesma fórmula para atribuir cada entrada de preço a um catálogo de preços. Para obter informações sobre como uma vitrine resolve `priceBookId` para uma sessão de cliente, consulte [Integração de vitrine headless](../headless-storefront.md#graphql-commerceoptimizer-query).


| Campo ou valor do Source | Campo de API [!DNL Commerce Optimizer] | Detalhes do mapeamento |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | Adiciona este campo aos catálogos de preços filhos. Seu valor identifica o catálogo de preços base. |
| Nome do site | `name` | Usa o nome do site para catálogos de preços base. Usa `Customer group name (Website name)` para catálogos de preços filho. |
| `websiteCode` | `parentId` | Presente somente em catálogos de preços filhos; aponta para o catálogo de preços base |
| Moeda base do site | `currency` | Inclui este campo somente nos catálogos de preços base. Os livros de preços infantis o omitem. |

## Preços

O feed `prices` envia dados de [!DNL Adobe Commerce] para o [ponto de extremidade de preços](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Campo de entrada do feed | Campo de API [!DNL Commerce Optimizer] | Detalhes do mapeamento |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | Passa o SKU inalterado. |
| `websiteCode`, `customerGroupCode` | `priceBookId` | Combina `websiteCode` com o hash SHA-1 da ID de grupo de clientes em `customerGroupCode`. Se `customerGroupCode` for `0`, usa `websiteCode` sozinho. |
| `regular` | `regular` | Transmite o preço normal inalterado. |
| `discounts[]` | `discounts[]` | Se o valor de origem for `null`, exporta uma matriz vazia.<br>Para entradas com `code` definido como `special_price` e um `percentage`, define `percentage` como `100 - percentage` quando o valor está entre `0` e `100`. Define como `0` nesse intervalo ou fora dele.<br>Passa outras entradas, incluindo preços especiais com base em preços, sem alterações. |
| `tierPrices[]` | `tierPrices[]` | Usa uma matriz vazia se o valor de origem estiver ausente ou for `null`. |

## Categorias

O feed `categories` envia dados de [!DNL Adobe Commerce] para o ponto de extremidade [Categorias](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Itens com um `urlPath` vazio (categorias de raiz lógica) são ignorados e nunca enviados.

| Campo [!DNL Adobe Commerce] | Campo de API [!DNL Commerce Optimizer] | Detalhes do mapeamento |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | Exporta a posição da categoria quando presente. Omite o campo quando ele estiver ausente. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | String delimitada por nova linha dividida em matriz |
| `image` | `images[].url` | Matriz de elemento único; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` quando ambos `true`, `[]` caso contrário |

|0&rbrace; | `metaTags/keywords` | Divide as palavras-chave delimitadas por nova linha em uma matriz e elimina os espaços em branco. `metaKeywords`|
|0&rbrace; | `images[].url` | Quando `image` está presente, exporta uma imagem com a função `BASE`. `image`Exporta uma matriz vazia quando a imagem está vazia ou ausente. |
| `isActive` + `includeInMenu` | `families` | Adiciona `top_menu` somente quando ambos os valores são `true`. Caso contrário, exporta uma matriz vazia. |
|0&rbrace; | `attributes[]` | Exporta entradas com um `attributeCode` não vazio como `{code, values[]}`. `attributes[]`Converte valores em cadeias de caracteres. Omite `attributes` quando não existem entradas qualificadas. |

>[!MORELIKETHIS]
>
> - [Assimilar dados de produto e preço com a API de assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — saiba mais sobre o modelo de dados de catálogo de metadados, produtos, categorias, tabelas de preços e preços
> - [Referência da API REST de assimilação de dados do catálogo](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Examine os esquemas de solicitação e resposta para cada ponto de extremidade de feed
> - [Como o [!DNL Commerce Optimizer Connector] funciona com o [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — Saiba como exibições da loja, sites e grupos de clientes são mapeados para fontes de catálogo e catálogos de preços
> - [Catálogos de preços em [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — Gerenciar catálogos de preços criados pela exportação do conector
> - [Integração headless com vitrine](../headless-storefront.md#graphql-commerceoptimizer-query) — Resolva `priceBookId` para sessões com clientes
