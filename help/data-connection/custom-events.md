---
title: Criar eventos personalizados
description: Saiba como criar eventos personalizados para conectar seus dados do Adobe Commerce a outros produtos Adobe DX.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 25d796da49406216f26d12e3b1be01902dfe9302
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Criar eventos personalizados

Você pode estender a [plataforma de eventos](events.md) criando seus próprios eventos de vitrine eletrônica para coletar dados exclusivos de seu setor. Quando você cria e configura um evento personalizado, ele é enviado para o [Coletor de Eventos da Adobe Commerce](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector).

## Lidar com eventos personalizados

Eventos personalizados são compatíveis somente com o Adobe Experience Platform. Os dados personalizados não são encaminhados para painéis e rastreadores de métricas do Adobe Commerce.

Para qualquer evento `custom`, o coletor:

- Adiciona `identityMap` com `ECID` como identidade primária
- Inclui `email` em `identityMap` como uma identidade secundária _se_ `personalEmail.address` estiver definido no evento
- Envolve o evento completo dentro de um objeto `xdm` antes de encaminhar para a Edge

Exemplo:

Evento personalizado publicado pelo Adobe Commerce Events SDK:

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

No Experience Platform Edge:

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> O uso de eventos personalizados pode afetar os relatórios padrão do Adobe Analytics.

## Lidar com substituições de eventos (atributos personalizados)

Para qualquer conjunto de eventos com um `customContext`, o coletor substitui ou estende os campos na carga do evento dos campos no `custom context`. O caso de uso para substituições é quando um desenvolvedor deseja reutilizar e estender contextos definidos por outras partes da página em eventos já compatíveis.

As substituições de evento são aplicáveis somente ao encaminhar para o Experience Platform. Elas não são aplicadas aos eventos de análise do Adobe Commerce e do Sensei. O Coletor de Eventos da Adobe Commerce [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) fornece informações adicionais.

>[!NOTE]
>
>Ao aumentar o `productListItems` com atributos personalizados em cargas de evento do Experience Platform, associe produtos usando o SKU. Este requisito não se aplica a `product-page-view` eventos.

### Uso

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### Exemplo 1 - adicionar `productCategories`

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### Exemplo 2 - adicionar contexto personalizado antes de publicar o evento

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### Exemplo 3 - o contexto personalizado definido no editor substitui o contexto personalizado definido anteriormente na Camada de dados de clientes Adobe.

Neste exemplo, o evento `pageView` terá **Nome de Página Personalizado 2** no campo `web.webPageDetails.name`.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### Exemplo 4 - adicionar contexto personalizado a `productListItems` com eventos com vários produtos

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

>[!NOTE]
>
> Substituir eventos por atributos personalizados pode afetar os relatórios padrão do Adobe Analytics.
