---
title: Acompanhando suas remessas em [!DNL Payment Services]
description: Personalizar as informações de rastreamento e remessas de [!DNL Payment Services] exibidas no Painel do Comerciante do Paypal.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%
---
# Acompanhando suas remessas em [!DNL Payment Services]

O [!DNL Payment Services] permite que os comerciantes vejam as informações de rastreamento de uma remessa no Painel do Comerciante do PayPal.

Consulte o tópico [remessas](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank} para obter mais informações sobre a grade remessas do Adobe Commerce.

## Como funciona o rastreamento da sua remessa

Essa funcionalidade depende de o pedido ter sido faturado, já que o PayPal deve receber um `capture_id` para processar as informações de rastreamento. Se um comerciante enviar seus produtos antes da captura, as informações de rastreamento não serão enviadas para o PayPal.

>[!NOTE]
>
> É recomendável criar uma remessa por número de rastreamento, associando os itens corretos com a remessa.

## Adição do número de rastreamento

As instruções a seguir irão orientá-lo pelo processo de criação de uma remessa no Adobe Commerce com [!DNL Payment Services]:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.

1. Na coluna **[!UICONTROL Action]** da ordem selecionada, clique em **[!UICONTROL View]**.

1. Clique em **[!UICONTROL Ship]**.

1. Role para baixo até o bloco **[!UICONTROL Payment & Shipping Method]** e clique em **[!UICONTROL Add Tracking Number]** em **[!UICONTROL Shipping Information]**.

1. Defina o **[!UICONTROL Carrier]**.

1. Para acompanhar a remessa, insira o **[!UICONTROL Title]** e **[!UICONTROL Number]**.

1. Clique em **[!UICONTROL Submit Shipment]**.

>[!NOTE]
>
> Como alternativa, você pode estar usando um módulo de entrega para inserir as informações do número de rastreamento. Verifique se o módulo de remessa está salvando as informações do número de rastreamento no campo `tracking_number`.

### Compatibilidade com terceiros

Qualquer extensão de terceiros é compatível com a funcionalidade quando uma entidade de remessa é criada por meio da [API do Commerce](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
