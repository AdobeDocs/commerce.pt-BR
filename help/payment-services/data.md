---
title: Dados disponíveis
description: Use dados de relatórios financeiros para reconciliar relatórios com sistemas não-Commerce.
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Dados disponíveis

Alguns dados de pedidos e pagamentos estão disponíveis para que você possa coordenar os relatórios financeiros do Adobe Commerce em sistemas externos.

## Reconciliar com o sistema ERP

Você pode reconciliar o Adobe Commerce financial reporting com seu sistema não-Adobe Enterprise Resource Planning (ERP) usando a ID de incremento associada a uma ordem específica.

Quando os Serviços de Pagamento enviam a ordem do Commerce para o PayPal, a ID do incremento é incluída como `custom_id` _e_ no `invoice_id` (que também contém uma sequência de caracteres aleatória após `increment_id`).

As IDs são facilmente acessíveis nos detalhes de atividade do comerciante para um pagamento e no webhook do PayPal.

O `invoice_id` e `custom_id` são exibidos perto da parte inferior dos detalhes de atividade do comerciante para um pagamento:

![`custom_id` no detalhe de atividade de comerciante](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

`custom_id` e `invoice_id` nos detalhes no webhook do PayPal:

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

Consulte a documentação das REST APIs do PayPal para obter mais informações:

* [`purchase_unit`, no qual `custom_id` e `invoice_id` residem](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [Mostrar detalhes do pedido](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
