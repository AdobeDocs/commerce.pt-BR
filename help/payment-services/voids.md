---
title: Nulos
description: Anulações permitem que você libere os fundos em uma conta de cartão de crédito ou débito que estão bloqueados ou retidos por uma autorização para a quantia de uma compra.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
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
source-wordcount: '244'
ht-degree: 0%
---
# Nulos

[!DNL Payment Services] dá suporte à funcionalidade existente do Commerce para anular transações. Uma anulação libera fundos em uma conta de cartão de crédito ou débito que estão sendo mantidos por uma autorização para a quantia de compra. As transações só poderão ser anuladas se o pagamento ainda não tiver sido capturado.

* Se sua loja está [configurada](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para autorizar (não capturar) fundos apenas no ponto de venda, uma compra em sua loja resulta em um pedido com o status `Processing` no Administrador do Commerce.

* Você também pode [cancelar um pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} que não esteja faturado. Quaisquer autorizações não capturadas também são anuladas como parte desse processo de cancelamento.

>[!NOTE]
>
>Cancelar uma ordem também produz um cancelamento, mas a anulação de uma ordem não aciona um cancelamento.

Para saber mais sobre as etapas básicas pelas quais uma ordem é encaminhada, consulte o tópico do [Fluxo de trabalho de ordem](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} no guia do usuário principal.

Para saber mais sobre a funcionalidade void e como anular uma transação de pedido, consulte [Processamento de um Pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} no guia do usuário principal.
