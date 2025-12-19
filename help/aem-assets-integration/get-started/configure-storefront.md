---
title: Configurar a vitrine eletrônica
description: Saiba como conectar a loja do Edge Delivery Services à integração do AEM Assets.
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Configurar a vitrine eletrônica

A integração do AEM Assets exibe imagens de produtos gerenciadas no AEM Assets, em vez de usar imagens hospedadas no Adobe Commerce. A integração permite recursos aprimorados de gerenciamento de imagens, incluindo otimização, recorte e entrega avançados por meio da Rede de entrega de conteúdo (CDN) da Adobe.

Para habilitar a integração em vitrines do Commerce viabilizadas pelo Edge Delivery Services, atualize o arquivo de configuração de vitrines (`config.json`) para adicionar o parâmetro `"commerce-assets-enabled": true`.

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

Para obter mais informações sobre como usar o AEM Assets com a Loja Commerce da Edge Delivery Services, conclua a configuração da loja descrita no tópico [integração com o AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) na documentação da *Loja Adobe Commerce*.
