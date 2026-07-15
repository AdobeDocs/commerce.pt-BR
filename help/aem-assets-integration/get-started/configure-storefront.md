---
title: Configurar a vitrine eletrônica
description: Saiba como conectar a loja do Edge Delivery Services à integração do AEM Assets.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# Configurar a vitrine eletrônica

## Ativar exibição de imagem do produto no AEM Assets {#enable-product-images}

A integração do AEM Assets exibe imagens de produtos do AEM Assets, em vez do Adobe Commerce, permitindo otimização avançada, recorte e entrega de CDN.

Para habilitar a integração em vitrines do Commerce viabilizadas pelo Edge Delivery Services, adicione o parâmetro `"commerce-assets-enabled": true` ao arquivo de configuração de vitrines (`config.json`).

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Os menus suspensos do Commerce detectam automaticamente a configuração `commerce-assets-enabled` e ajustam o tratamento da imagem de acordo.

Para obter mais informações sobre como usar o AEM Assets com a Commerce Storefront habilitada pela Edge Delivery Services, consulte o tópico [integração com o AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) na documentação da *Adobe Commerce Storefront*.

>[!TIP]
>
>Para permitir que os autores naveguem e insiram o AEM Assets em páginas de conteúdo estático, consulte [Conectar o AEM Assets ao Da.live para criação de conteúdo estático](#connect-aem-assets-authoring).

## Conectar o AEM Assets ao Da.live para criação de conteúdo estático {#connect-aem-assets-authoring}

>[!NOTE]
>
>Essa configuração é separada da extensão Integração do AEM Assets. Fornecido pelo [Da.live](https://da.live){target="_blank"}, permite que os autores naveguem e insiram AEM Assets em páginas de conteúdo estático (por exemplo, páginas de aterrissagem ou blocos de conteúdo) por meio do painel [!UICONTROL Library] e do [!UICONTROL Content Advisor]. Imagens de produtos sincronizadas por meio da Integração do AEM Assets são configuradas separadamente usando a configuração `commerce-assets-enabled`.

Use as etapas a seguir para conectar o AEM Assets a uma loja de Criação de documentos (Da.live) para que os autores possam navegar e inserir o AEM Assets a partir do **[!UICONTROL Content Advisor]** ao editar conteúdo estático.

>[!NOTE]
>
>Para obter instruções detalhadas de configuração, consulte [Configurar o AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} na documentação da Da.live e [Integrar o AEM Assets durante a criação de conteúdo para o Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} na documentação do AEM Assets.

### Etapa 1: abrir a configuração do site no Da.live

1. No [Da.live](https://da.live){target=_blank}, localize e abra sua loja.

1. Na navegação estrutural, selecione o ícone **[!UICONTROL Settings]** ao lado do nome do site para abrir a planilha de configuração do site.

### Etapa 2: Copiar o URL do repositório do AEM

1. Em uma nova guia, vá para [experience.adobe.com](https://experience.adobe.com){target=_blank} e navegue até **[!UICONTROL Experience Manager]**.

1. Abra o Adobe Experience Manager Assets: role até a seção **[!UICONTROL My Authoring]** e selecione **[!UICONTROL Assets]** ao lado do ambiente **[!UICONTROL Production]**.

1. Na barra de endereços do navegador, copie o segmento que começa com `author` até `.com` (inclusive), por exemplo, `author-p107634-e1009805.adobeaemcloud.com`.

### Etapa 3: adicionar a ID do repositório à sua configuração

1. Para configurar o site, volte para Da.live e selecione **[!UICONTROL data]** na configuração do site.

1. Preencha a planilha da seguinte maneira:

   | Célula | Valor |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | O URL copiado na Etapa 2 |

1. Selecione **[!UICONTROL Save]** e depois selecione a seta para trás ao lado do nome do site para retornar à raiz do site.

   >[!NOTE]
   >
   > O host `author-` com prefixo procura ativos na camada do autor. Para entregar ativos por meio do Dynamic Media, use um host com prefixo `delivery-`. Para todas as opções de `aem.repositoryId`, consulte [Configurar AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}.

### Etapa 4: conectar o AEM Assets por meio da biblioteca

1. Na raiz do site, selecione a pasta **[!UICONTROL index]** para abri-la.

1. No editor, abra o painel **[!UICONTROL Library]** e selecione **[!UICONTROL AEM Assets]**.

   O popover **[!UICONTROL Content Advisor]** é aberto e mostra suas pastas e arquivos do AEM Assets.

Sua loja agora está conectada ao AEM Assets. Você pode procurar e inserir ativos diretamente do **[!UICONTROL Content Advisor]**.

## Documentação relacionada

* [Integração do AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/){target=_blank} na documentação da *Adobe Commerce Storefront*—configuração da loja e comportamento de manipulação de imagens.

* [Integre o AEM Assets ao criar conteúdo para o Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} na documentação do *AEM Assets*.

* [Configurar AEM Assets](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} e [Trabalhando com mídia](https://docs.da.live/authors/guides/adding-media){target=_blank} na documentação Do.live.
