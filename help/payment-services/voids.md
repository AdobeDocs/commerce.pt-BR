---
title: Nulos
description: Anulações permitem que você libere os fundos em uma conta de cartão de crédito ou débito que estão bloqueados ou retidos por uma autorização para a quantia de uma compra.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Nulos

Com [!DNL Payment Services], você pode usar a funcionalidade existente do Commerce para anular transações. Anulações permitem que você libere os fundos em uma conta de cartão de crédito ou débito que estão bloqueados ou retidos por uma autorização para a quantia de uma compra.

>[!NOTE]
>
>Você só poderá anular uma transação se o pagamento ainda não tiver sido capturado.

Se sua loja está [configurada](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para autorizar (não capturar) fundos apenas no ponto de venda, uma compra em sua loja resulta em um pedido com status `Processing` no Administrador do Commerce.

Você também pode [cancelar um pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} que não esteja faturado. Quaisquer autorizações não capturadas também são anuladas como parte desse processo de cancelamento.

>[!NOTE]
>
>Cancelar uma ordem também produz um cancelamento, mas a anulação de uma ordem não aciona um cancelamento.

Para saber mais sobre as etapas básicas pelas quais uma ordem é encaminhada, consulte o tópico do [Fluxo de trabalho de ordem](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} no guia do usuário principal.

Para saber mais sobre a funcionalidade void e como anular uma transação de pedido, consulte [Processando um Pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} no guia do usuário principal.
