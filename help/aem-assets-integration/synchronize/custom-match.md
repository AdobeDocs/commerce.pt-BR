---
title: Correspondência automática personalizada
description: Saiba como a correspondência automática personalizada é particularmente útil para comerciantes com lógica de correspondência complexa ou que dependem de um sistema de terceiros que não pode preencher metadados no AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Correspondência automática personalizada

Se a estratégia de correspondência automática padrão (**correspondência automática OOTB**) não estiver alinhada aos seus requisitos de negócios específicos, selecione a opção de correspondência personalizada. Esta opção oferece suporte ao uso do [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) para desenvolver um aplicativo de correspondência personalizado que lida com lógica de correspondência complexa ou com ativos provenientes de um sistema de terceiros que não pode preencher metadados no AEM Assets.

## Configurar correspondência automática personalizada

1. No Administrador do Commerce, navegue até **[!UICONTROL Store]** > Configuração > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Selecione **[!UICONTROL Custom Matcher]** como regra de correspondência.

1. Ao selecionar esta regra de correspondência, o Administrador exibe campos adicionais para configurar os **pontos de extremidade** e os **parâmetros de autenticação** necessários para a lógica de correspondência personalizada.

## Pontos de extremidade da API do correspondedor personalizado

Ao criar um aplicativo de correspondência personalizado usando o [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, o aplicativo deve expor os seguintes pontos de extremidade:

* Ponto de extremidade **Ativo App Builder para URL do produto**
* Ponto de extremidade **Produto App Builder para URL do ativo**

### Ativo App Builder para endpoint do URL do produto

Esse endpoint recupera a lista de SKUs associadas a um determinado ativo:

#### Exemplo de uso

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Solicitação**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parâmetro | Tipo de dados | Descrição |
| --- | --- | --- |
| `assetId` | String | Representa a ID de ativo atualizada |
| `eventData` | String | Retorna a carga de dados associada ao `assetId` |

**Resposta**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### Produto App Builder para endpoint do URL do ativo

Esse endpoint recupera a lista de ativos associados a determinada SKU:

#### Exemplo de uso

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Solicitação**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parâmetro | Tipo de dados | Descrição |
| --- | --- | --- |
| `productSKU` | String | Representa o SKU do produto atualizado. |
| `asset_matches` | String | Retorna todos os ativos associados a um `productSku` específico. |

O parâmetro `asset_matches` contém os seguintes atributos:

| Atributo | Tipo de dados | Descrição |
| --- | --- | --- |
| `asset_id` | String | Representa a ID de ativo atualizada. |
| `asset_roles` | String | Retorna todas as funções de ativo disponíveis. Usa [funções de ativos do Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) com suporte, como `thumbnail`, `image`, `small_image` e `swatch_image`. |
| `asset_format` | String | Fornece os formatos disponíveis para o ativo. Os valores possíveis são `image` e `video`. |
| `asset_position` | String | Mostra a posição do ativo. |

**Resposta**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```
