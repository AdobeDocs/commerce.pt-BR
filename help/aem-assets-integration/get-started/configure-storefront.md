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
source-git-commit: null
workflow-type: tm+mt
source-wordcount: 137
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

Para obter mais informações sobre como usar o AEM Assets com a Loja Commerce da Edge Delivery Services, conclua a configuração da loja descrita no tópico [integração com o AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=pt-BR) na documentação da *Loja Adobe Commerce*.
