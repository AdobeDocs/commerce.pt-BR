---
title: Acompanhando suas remessas em [!DNL Payment Services]
description: Personalizar [!DNL Payment Services] informações de remessa e rastreamento exibidas no Painel do Comerciante do Paypal.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '211'
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
