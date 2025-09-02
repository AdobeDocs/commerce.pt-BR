---
title: Criar eventos personalizados
description: Saiba como criar eventos personalizados para conectar seus dados do Adobe Commerce a outros produtos Adobe DX.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

As substituições de atributo para eventos padrão são compatíveis somente com o Experience Platform. Os dados personalizados não são encaminhados para painéis e rastreadores de métricas do Commerce.

Para qualquer evento com `customContext`, o coletor substitui campos de junções definidos em contextos relevantes por campos em `customContext`. O caso de uso para substituições é quando um desenvolvedor deseja reutilizar e estender contextos definidos por outras partes da página em eventos já compatíveis.

### Exemplos

Exibição de produto com substituições publicadas pelo Adobe Commerce Events SDK:

```javascript
mse.publish.productPageView({
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

No Experience Platform Edge:

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Lojas baseadas em Luma:

Em lojas baseadas em Luma, a publicação de eventos é implementada nativamente. Portanto, você pode definir dados personalizados estendendo o `customContext`.

Por exemplo:

```javascript
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
```

Consulte [substituição de evento personalizado](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md) para saber mais sobre como lidar com dados personalizados.

>[!NOTE]
>
> Substituir eventos por atributos personalizados pode afetar os relatórios padrão do Adobe Analytics.
