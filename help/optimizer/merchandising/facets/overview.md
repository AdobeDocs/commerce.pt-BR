---
title: Visão geral dos aspectos
description: Saiba mais sobre os aspectos em [!DNL Adobe Commerce Optimizer] e como eles melhoram os resultados da pesquisa.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Facetas

Facetas é um método de filtragem de alto desempenho que usa várias dimensões de valores de atributo como critérios de pesquisa.

![Resultados de pesquisa filtrados](../../assets/storefront-search-results-run.png)

Em uma faceta, os compradores podem selecionar várias opções, como &quot;Básico&quot; e &quot;Consolado&quot; em &quot;Estilo&quot; e os resultados da pesquisa são atualizados para exibir apenas esses estilos. Da mesma forma, se um comprador selecionar opções em várias facetas, como &quot;Básico&quot; em &quot;Estilo&quot; e &quot;Interno&quot; em &quot;Clima&quot;, os resultados da pesquisa serão atualizados para exibir o estilo selecionado e o clima selecionado.

Qualquer faceta definida pode ser usada como um parâmetro de URL e os resultados serão filtrados com base nos valores de parâmetro: `http://yourstore.com?brand=acme&color=red`.

## Agregação de facetas

A agregação de facetas é executada da seguinte maneira: se a loja tiver três facetas (categorias, cor e preço) e os filtros do comprador em todos os três (cor = azul, preço é de $10,00 a 50,00, categorias = `promotions`).

- Agregação `categories` - Agrega `categories`, e aplica os filtros `color` e `price`, mas não o filtro `categories`.
- Agregação `color` - Agrega `color`, e aplica os filtros `price` e `categories`, mas não o filtro `color`.
- Agregação `price` - Agrega `price`, e aplica os filtros `color` e `categories`, mas não o filtro `price`.

## Valores de atributo padrão

Os [atributos do produto](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#operation/createProductMetadata) a seguir são usados por [!DNL Adobe Commerce Optimizer] e habilitados por padrão.

| Propriedade | Descrição | Atributo |
|---|---|---|
| Classificável | Usado para Classificação na Lista de Produtos | `price` |
| Pesquisável | Usar na pesquisa | `price` <br />`sku`<br />`name` |

## Propriedades de atributo não-sistema padrão

A tabela a seguir mostra a pesquisa padrão e as propriedades filtráveis de atributos que não são do sistema. Definir a propriedade de atributo *Usar na Pesquisa* como `Yes` torna o atributo pesquisável em [!DNL Adobe Commerce Optimizer].

| Código do atributo | Pesquisável |
|--- |--- |
| atividade | Sim |
| attributes_brand | Sim |
| marca | Sim |
| clima | Sim |
| colar | Sim |
| cor | Sim |
| custo | Sim |
| eco_collection |
| gênero | Sim |
| fabricante | Sim |
| material | Sim |
| finalidade | Sim |
| strap_bags | Sim |
| style_general | Sim |

## Propriedades padrão do atributo do sistema

A tabela a seguir mostra a pesquisa padrão e as propriedades filtráveis dos atributos do sistema.

| Código do atributo | Pesquisável |
|--- |--- |
| allow_open_amount | Sim |
| descrição | Sim |
| name | Sim |
| preço | Sim |
| descrição_curta | Sim |
| sku | Sim |
| status | Sim |
| tax_class_id | Sim |
| url_key | Sim |
| peso | Sim |
