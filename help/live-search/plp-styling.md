---
title: Widget da página de listagem de produtos
description: Habilitando e estilizando o  [!DNL Live Search Product Listing Page Widget]
exl-id: 50ba8046-869a-4071-b3a3-a6392544c07b
source-git-commit: c0a6f038d2528a67da6f1bb4f5e5bb140afc7dfc
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---

# Widget da página de listagem de produtos

O [!DNL Live Search Product Listing Page Widget] (PLP) usa a plataforma Commerce Services para fornecer uma página de listagem de produtos com desempenho, pesquisável e compatível com facetas. Este tópico descreve como ativar e estilizar o widget PLP.

## Ativar o dispositivo PLP

Quando o serviço [!DNL Live Search] é instalado, a funcionalidade de pesquisa padrão é convertida para [!DNL Live Search] automaticamente.

O widget PLP [!DNL Live Search] é habilitado por padrão para novas instalações.

Se você estiver atualizando o [!DNL Live Search] e o widget PLP já tiver sido desativado, ele permanecerá assim.

>[!NOTE]
>
>Se você estiver migrando do Adaptador de Pesquisa obsoleto, consulte o [guia de migração](migrate-to-plp.md) para obter orientações detalhadas sobre cenários, pré-requisitos e instruções passo a passo.

Para ativar o dispositivo PLP:

1. No Administrador do Adobe Commerce, acesse Lojas → Configurações → Configuração.
1. Na navegação à esquerda, clique em **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**.
1. Clique na seção [!UICONTROL Storefront Features].
1. Definir [!UICONTROL Enable Product Listing Widget] = Sim
1. Salvar configuração
1. Se solicitado, limpe o cache ( vá para Sistema > Ferramentas > Gerenciamento de cache > [!UICONTROL Flush Magento Cache]).

>[!IMPORTANT]
>
>Quando o [!DNL Live Search Product Listing Page Widget] está habilitado, a direção da ordem de classificação em uma página de listagem de produtos não pode ser alterada.

## Recursos do widget

O widget PLP fornece os seguintes recursos prontos para uso:

- Botões Adicionar ao carrinho - Disponível somente para produtos simples.
- Várias imagens por produto — a imagem pode mudar quando uma cor diferente é escolhida para um produto configurável.
- Suporte para amostras de cores - Observe que o atributo de cor deve ser escrito `color` para que o código seja validado corretamente.

### Personalização do widget

Além dos recursos prontos do widget PLP, você pode personalizar ainda mais o widget para incluir os seguintes recursos:

- Filtrar por atributos
- Suporte a vários idiomas
- Controles deslizantes de preço

Para obter informações sobre como personalizar o widget PLP para lidar com os recursos acima, consulte o arquivo readme do `storefront-product-listing-page` no seguinte [repositório](https://github.com/adobe/storefront-product-listing-page/). O arquivo readme neste repositório fornece um exemplo de como personalizar o dispositivo PLP e implantar essas personalizações no seu site.

>[!WARNING]
>
>Se você personalizar o widget PLP usando o código disponível no repositório, será responsável pela manutenção e pelas atualizações necessárias. Quaisquer novos recursos de widget PLP lançados pelo Adobe podem ser incompatíveis com sua implementação personalizada.

## Exemplo de estilo

Você pode personalizar a aparência do widget PLP para corresponder ao seu site usando o [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/).

>[!NOTE]
>
>Elementos com classes personalizadas em um tema do Adobe Commerce não são herdados. Esses elementos devem ser direcionados por sua classe específica para corresponder às classes personalizadas; as classes de ação principais não funcionarão em um botão de widget. Os elementos genéricos de destino dentro do CSS são herdados; `button` aplica-se aos botões do widget.

Os divs realçados contêm a classe de destino `ds-sdk-product-item__product-name`.

![Paginação](assets/plp-css-example.png)

Personalize o nome do produto adicionando uma regra para torná-lo em letras maiúsculas.

```css
.ds-sdk-product-item__product-name {
 text-transform: uppercase;
}
```

![Paginação](assets/plp-css-example-after.png)

## Classes CSS

### Lista de produtos

- `.ds-sdk-product-list`: div externa
- `.ds-sdk-product-list__grid`: div interna

![Paginação](assets/plp-css-product-list.png)

#### Paginação de lista de produtos

- `.ds-plp-pagination`

![Paginação](assets/plp-css-pagination.png)

- `.ds-plp-pagination_item`

![Item de paginação](assets/plp-css-pagination-item.png)

- `.ds-plp-pagination_item--current`

![Item atual de paginação](assets/plp-css-pagination-item-current.png)

### Widgets

- `.ds-widgets`: div externa
- `.ds-widgets__actions`: div interna do lado esquerdo
- `.ds-widgets__results`: div interna do lado direito

![Resultados do widget](assets/plp-css-widgets.png)

### Lista suspensa Classificar

- `.ds-sdk-sort-dropdown`

![Classificar lista suspensa](assets/plp-css-dropdown.png)

- `.ds-sdk-sort-dropdown__button`

![Botão suspenso](assets/plp-css-dropdown-button.png)

- `.ds-sdk-sort-dropdown__items`

![Itens suspensos](assets/plp-css-dropdown-items.png)

- `.ds-sdk-sort-dropdown__items--item`

![Item suspenso](assets/plp-css-dropdown-item.png)

- `.ds-sdk-sort-dropdown__items--item-selected`

![Item selecionado na lista suspensa](assets/plp-css-dropdown-selected.png)

- `.ds-sdk-sort-dropdown__items--item-active`

![Seleção ativa suspensa](assets/plp-css-dropdown-active.png)

### Facetas

- `.ds-plp-facets`
- `.ds-plp-facets__header`
- `.ds-plp-facets__header_title`
- `.ds-plp-facets__header__clear-all`

![Título do cabeçalho do Facets](assets/plp-css-facets-title-clear.png){width="350"}

- `.ds-plp-facets__pills`
- `.ds-sdk-pill`

![pílulas facetadas](assets/plp-css-facets-pill.png){width="350"}

- `.ds-sdk-pill__label`
- `.ds-sdk-pill__cta`

![Rótulo de facetas](assets/plp-css-pill-label-cta.png){width="350"}

- `.ds-plp-facets__list`

![Lista de aspectos](assets/plp-css-facets-list.png){width="350"}

- `.ds-sdk-input`
- `.ds-sdk-input__label`
- `.ds-sdk-product-item__product-swatch-group`
- `ds-sdk-product-item__product-swatch-item`
- `.ds-sdk-input_fieldset_show-more`

![Entrada](assets/plp-css-sdk-input.png)

- `.ds-sdk-labelled-input`

![Entrada rotulada](assets/plp-css-labelled-input.png)

- `.ds-sdk-labelled-input__input`
- `.ds-sdk-labelled-input__label`

![Rótulo de entrada](assets/plp-css-labelled-input-label.png)

### Item do produto

- `.ds-sdk-product-item`
- `.ds-sdk-product-item__image`
- `.ds-sdk-product-item__product-name`
- `.ds-sdk-product-item__product-options`
- `.ds-sdk-product-price`
   - `.ds-sdk-product-price--no-discount`
   - `.ds-sdk-product-price--grouped`
   - `.ds-sdk-product-price--bundle`
   - `.ds-sdk-product-price--discount`

![Produto](assets/plp-css-product.png)

### Carregando

- `.ds-sdk-loading`
- `.ds-sdk-loading__spinner`
- `.ds-sdk-loading__spinner-label`

![Carregando indicador](assets/plp-css-loading.png)

## Desabilitar o dispositivo PLP

Para desativar o dispositivo PLP:

1. Vá para **Lojas** > Configurações > **Configuração** > **[!DNL Live Search]** > **Recursos de Vitrine** e defina **Habilitar Widgets de Listagem de Produtos** como &quot;Não&quot;.
1. Selecione **Salvar configuração** para salvar a configuração.
