---
title: Reembolsos
description: Criar reembolsos para [!DNL Payment Services] pedidos no Administrador como parte do processo de memorando de crédito.
exl-id: 2b3721a1-9c9d-4e3f-ab7d-5bd61573dcb4
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
source-wordcount: '305'
ht-degree: 0%
---
# Reembolsos

Os reembolsos de [!DNL Payment Services] pedidos são criados no Administrador como parte do processo de aviso de crédito. Um aviso de crédito é um documento que mostra a quantia devida ao cliente, para uma restituição total ou parcial, que pode ser aplicada a uma compra ou reembolsada diretamente ao cliente. Os avisos de crédito só podem ser emitidos para ordens [faturadas](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Consulte [Avisos de Crédito](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} em nosso guia do usuário principal para obter mais informações e saber como emitir e imprimir avisos de crédito.

Para pedidos processados com PayPal ou um cartão de crédito, você pode:

* Reembolsar o valor total da ordem
* Reembolsar uma quantia parcial de uma ordem (ou várias quantias parciais)
* Reembolsar um valor inferior ao valor de um item de pedido específico

Consulte [Emitir um memorando de crédito](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} em nosso guia do usuário principal para obter mais informações.

>[!NOTE]
>
>Ocorre um erro para pedidos processados por cartão de crédito ou PayPal se você tentar reembolsar parcialmente um pedido por mais do que o valor restante do pedido (valor original menos o total de reembolsos existentes) ou se você emitir um reembolso por um valor maior do que o valor total do pedido.

A configuração [!UICONTROL Payment Action] na sua configuração [!UICONTROL Payment Settings]—`Authorize` ou `Authorize and Capture`—determina o [fluxo de trabalho básico de reembolso](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} para pedidos.

Consulte a [seção de configuração da ação de pagamento](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} de _Emitindo um Aviso de Crédito_ para obter mais informações.
