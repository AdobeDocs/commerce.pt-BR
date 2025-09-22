---
title: Facetas
description: '[!DNL Live Search] facetas usam várias dimensões de valores de atributo como critérios de pesquisa.'
exl-id: d036265e-1868-461d-ab4c-7f469b1c6f5b
source-git-commit: 31223f4196187e4960c5bec0e90aa55cc4e0ac9a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Facetas

Faceting é um método de filtragem de alto desempenho que usa várias dimensões de valores de atributo como critérios de pesquisa. A pesquisa facetada é semelhante, mas consideravelmente &quot;mais inteligente&quot; do que a [navegação em camadas](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=pt-BR) padrão. A lista de filtros disponíveis é determinada pelos [atributos filtráveis](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/navigation/navigation-layered.html?lang=pt-BR#filterable-attributes) de produtos retornados nos resultados da pesquisa.

[!DNL Live Search] usa a consulta `productSearch`, que retorna facetas e outros dados específicos de [!DNL Live Search]. Consulte [`productSearch` query](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) na documentação do desenvolvedor para ver exemplos de código.

![Resultados de pesquisa filtrados](assets/storefront-search-results-run.png)

Em uma faceta, os compradores podem selecionar várias opções, como &quot;Básico&quot; e &quot;Consolado&quot; em &quot;Estilo&quot; e os resultados da pesquisa são atualizados para exibir apenas esses estilos. Da mesma forma, se um comprador selecionar opções em várias facetas, como &quot;Básico&quot; em &quot;Estilo&quot; e &quot;Interno&quot; em &quot;Clima&quot;, os resultados da pesquisa serão atualizados para exibir o estilo selecionado e o clima selecionado.

Qualquer faceta definida pode ser usada como um parâmetro de URL e os resultados serão filtrados com base nos valores de parâmetro: `http://yourstore.com?brand=acme&color=red`.

## Requisitos de facetagem

Os requisitos do atributo de categoria e produto para facetas são semelhantes aos atributos filtráveis usados para navegação em camadas. Cada propriedade da loja de um atributo deve ter o valor &quot;Usar na navegação em camadas dos resultados da pesquisa&quot; definido como &quot;Sim&quot;. Você pode revisar e atualizar a configuração do atributo no menu [!DNL Stores] > [!DNL Attribute] no Administrador.

>[!NOTE]
>
>Se você definir uma categoria de produto como uma faceta, a faceta exibirá a categoria e a subcategoria.
>
>![Faceta de categorias](assets/facet-category.png)

Consulte [limites e limites](./boundaries-limits.md#facets) para saber mais sobre os requisitos de facetas em [!DNL Live Search].

Se você tiver um grande número de atributos com os quais lidar, considere combinar atributos em um único &quot;metatributo&quot;. Por exemplo, sapatos geralmente têm tamanhos numéricos, enquanto camisas são comumente dimensionadas &quot;S/M/L/XL&quot;. Esses dois tipos de tamanhos podem ser combinados em um único atributo pesquisável.

| Configuração | Descrição |
|--- |--- |
| [Configurações de exibição de categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/create/categories-display-settings.html?lang=pt-BR) | Âncora - `Yes` |
| [Propriedades do atributo](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=pt-BR) | [Tipo de Entrada de Catálogo](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/attributes-input-types.html?lang=pt-BR) - `Yes/No`, `Dropdown`, `Multiple Select`, `Price`, `Visual swatch` (somente widget), `Text swatch` (somente widget) |
| Propriedades da vitrine do atributo | Usar na Navegação em Camadas de Resultados da Pesquisa - `Yes` |

## Agregação de facetas

A agregação de facetas é executada da seguinte maneira: se a loja tiver três facetas (categorias, cor e preço) e os filtros do comprador em todos os três (cor = azul, preço é de $10,00 a 50,00, categorias = `promotions`).

* Agregação `categories` - Agrega `categories`, e aplica os filtros `color` e `price`, mas não o filtro `categories`.
* Agregação `color` - Agrega `color`, e aplica os filtros `price` e `categories`, mas não o filtro `color`.
* Agregação `price` - Agrega `price`, e aplica os filtros `color` e `categories`, mas não o filtro `price`.

## Valores de atributo padrão

Os seguintes atributos de produto têm [propriedades de vitrine](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=pt-BR) que são usadas por [!DNL Live Search] e habilitadas por padrão.

| Propriedade | Propriedade da vitrine | Atributo |
|---|---|---|
| Classificável | Usado para Classificação na Lista de Produtos | `price` |
| Pesquisável | Usar na pesquisa | `price` <br />`sku`<br />`name` |
| FiltrávelNaPesquisa | Uso na navegação em camadas - Filtrável (com resultados) | `price`<br />`visibility`<br />`category_name` |

## Propriedades de atributo não-sistema padrão

A tabela a seguir mostra a pesquisa padrão e as propriedades filtráveis de atributos não pertencentes ao sistema, incluindo aqueles específicos aos dados de amostra do Luma. Definir a propriedade de atributo *Usar na Pesquisa* como `Yes` torna o atributo pesquisável tanto no [!DNL Live Search] quanto no Adobe Commerce nativo.

| Código do atributo | Pesquisável | Usar na navegação em camadas |
|--- |--- |--- |
| atividade | Sim | Filtrável (com resultados) |
| attributes_brand | Sim | Não |
| marca | Sim | Não |
| clima | Sim | Filtrável (com resultados) |
| colar | Sim | Filtrável (com resultados) |
| cor | Sim | Filtrável (com resultados) |
| custo | Sim | Não |
| eco_collection | Sim | Filtrável (com resultados) |
| gênero | Sim | Filtrável (com resultados) |
| fabricante | Sim | Filtrável (com resultados) |
| material | Sim | Filtrável (com resultados) |
| finalidade | Sim | Filtrável (com resultados) |
| strap_bags | Sim | Filtrável (com resultados) |
| style_general | Sim | Filtrável (com resultados) |

## Propriedades padrão do atributo do sistema

A tabela a seguir mostra a pesquisa padrão e as propriedades filtráveis dos atributos do sistema.

| Código do atributo | Pesquisável | Usar na navegação em camadas |
|--- |--- |--- |
| allow_open_amount | Sim | Filtrável (com resultados) |
| descrição | Sim | Não |
| name | Sim | Não |
| preço | Sim | Filtrável (com resultados) |
| descrição_curta | Sim | Não |
| sku | Sim | Não |
| status | Sim | Não |
| tax_class_id | Sim | Não |
| url_key | Sim | Não |
| peso | Sim | Não |
