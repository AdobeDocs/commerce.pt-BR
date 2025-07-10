---
title: Correspondência automática personalizada
description: Saiba como a correspondência automática personalizada é particularmente útil para comerciantes com lógica de correspondência complexa ou que dependem de um sistema de terceiros que não pode preencher metadados no AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: 7639422b237ad04cada366c541c041bc146ce085
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

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
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**Solicitação**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parâmetro | Tipo de dados | Descrição |
| --- | --- | --- |
| `assetId` | String | Representa a ID de ativo atualizada |

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
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**Solicitação**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parâmetro | Tipo de dados | Descrição |
| --- | --- | --- |
| `productSKU` | String | Representa o SKU do produto atualizado |

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

>[!TIP]
>
> Na chave `asset_roles`, use as [funções de ativos do Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) com suporte, como `thumbnail`, `image`, `small_image` e `swatch_image`.
