---
title: Headless
description: Saiba como integrar o [!DNL Product Recommendations] em uma loja headless.
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Headless

Você pode integrar o [!DNL Product Recommendations] em uma loja headless usando o [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) ou uma tecnologia de front-end personalizada, como o React ou o Vue JS.

Os integradores personalizados e headless devem consultar essas instruções do Luma e do PWA como uma implementação sugerida. Há muitas maneiras de implementar as Recomendações de produto em soluções headless e esta documentação não aborda todos os cenários. Os integradores devem cobrir o evento, o design e o teste de suas implementações.

[!DNL Product Recommendations] requer [dados comportamentais e de catálogo](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html) para operar. O processo de sincronização de dados de catálogo permanece inalterado em uma implementação headless, mas são necessárias alterações para a coleta de dados comportamentais.

>[!NOTE]
>
>As instâncias headless devem implementar eventos para acionar o painel Recomendações de produto.

Para integrar o [!DNL Product Recommendations] em uma loja headless, você deve:

1. Envie dados comportamentais ao Adobe Sensei para analisar e calcular os resultados das Recomendações de produto. Você também pode enviar dados adicionais para habilitar a recomendação do produto [relatórios de métricas](workspace.md).

1. Buscar resultados de recomendações de produtos e renderizar esses resultados na página.

Você pode executar essas duas ações usando os SDKs disponíveis, conforme descrito no fluxo de trabalho a seguir.

1. [Instalar](install-configure.md) o módulo [!DNL Product Recommendations].

1. Instale e use o [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) para acionar os [eventos comportamentais](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

   O mínimo de eventos necessário para retornar [!DNL Product Recommendations] resultados:

   | Evento | Categoria |
   |--- | ---|
   | `view` | produto |
   | `add-to-cart` | produto |
   | `place-order` | check-out |

   Para habilitar [relatórios de métricas](workspace.md), os seguintes eventos adicionais são necessários:

   | Evento | Categoria |
   |--- | ---|
   | `impression-render` | unidade de recomendação |
   | `view` | unidade de recomendação |
   | `rec-click` | unidade de recomendação |
   | `rec-add-to-cart-click` | unidade de recomendação (se um botão &quot;Adicionar ao carrinho&quot; estiver presente no template de recomendações) |

1. Quando os eventos forem acionados, use o [Coletor de Eventos da Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) para manipular os eventos e enviá-los para a Adobe Sensei.

1. Depois que os dados comportamentais forem coletados, você poderá [criar](create.md) [!DNL Product Recommendations] no Administrador.

1. Use o [SDK de Recomendações](https://developer.adobe.com/commerce/services/product-recommendations/) para buscar as unidades de recomendação na vitrine. O SDK retorna os dados do produto necessários para renderizar as unidades de recomendação em uma página.

1. Saiba como usar a [`recommendations` consulta do GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para retornar informações sobre blocos de recomendações de produtos para uma determinada SKU e muito mais.
