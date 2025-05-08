---
title: Reembolsos
description: Criar reembolsos para  [!DNL Payment Services] pedidos no Administrador como parte do processo de memorando de crédito.
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Reembolsos

Os reembolsos de [!DNL Payment Services] pedidos são criados no Administrador como parte do processo de aviso de crédito. Um aviso de crédito é um documento que mostra a quantia devida ao cliente, para uma restituição total ou parcial, que pode ser aplicada a uma compra ou reembolsada diretamente ao cliente. Os avisos de crédito só podem ser emitidos para ordens [faturadas](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Consulte [Avisos de Crédito](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} em nosso guia do usuário principal para obter mais informações e saber como emitir e imprimir avisos de crédito.

Para pedidos processados com PayPal ou um cartão de crédito, você pode:

* Reembolsar o valor total da ordem
* Reembolsar uma quantia parcial de uma ordem (ou várias quantias parciais)
* Reembolsar um valor inferior ao valor de um item de pedido específico

Consulte [Emitir um memorando de crédito](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} em nosso guia do usuário principal para obter mais informações.

>[!NOTE]
>
>Ocorre um erro para pedidos processados por cartão de crédito ou PayPal se você tentar reembolsar parcialmente um pedido por mais do que o valor restante do pedido (valor original menos o total de reembolsos existentes) ou se você emitir um reembolso por um valor maior do que o valor total do pedido.

A configuração [!UICONTROL Payment Action] na sua configuração [!UICONTROL Payment Settings]—`Authorize` ou `Authorize and Capture`—determina o [fluxo de trabalho básico de reembolso](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} para pedidos.

Consulte a [seção de configuração da ação de pagamento](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} de _Emitindo um Aviso de Crédito_ para obter mais informações.
