---
title: Supercaptura
description: Saiba mais sobre os requisitos de captura excessiva e a configuração da extensão Serviços de pagamento.
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# Supercaptura

A captura em excesso permite que comerciantes qualificados com um contrato de captura em excesso do PayPal capturem mais do que o valor originalmente autorizado ao faturar um pedido. Por exemplo, a quantia final pode aumentar devido a ajustes baseados no peso ou alterações nos custos de material entre a autorização e o preenchimento.

O PayPal determina o limite de captura excessiva para cada conta de comerciante. Habilitar a captura excessiva em [!DNL Payment Services] não estabelece um contrato nem aumenta o limite aprovado pelo PayPal.

>[!NOTE]
>
>Este tópico descreve a captura excessiva na extensão [!DNL Payment Services]. Para [!DNL Adobe Commerce as a Cloud Service], consulte [Valores de captura personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) para os requisitos separados de disponibilidade e habilitação.

## Pré-requisitos

Antes de ativar a captura excessiva:

* A captura excessiva está disponível somente no [!DNL Payment Services] 2.17.0 ou posterior.
* A captura excessiva está disponível somente para empresas com sede nos EUA. Os [requisitos de captura excessiva (PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954) do PayPal também se aplicam aos comerciantes com sede nos EUA que vendem para compradores do PayPal no Espaço Econômico Europeu (EEA).
* A captura excessiva não está disponível para métodos de pagamento alternativos (APMs).
* Obtenha um contrato de captura excessiva com o PayPal e confirme o limite aprovado para sua conta de comerciante com seu gerente de conta do PayPal.
* Defina o método de pagamento **[!UICONTROL Payment Action]** como `Authorize`. A captura excessiva se aplica a pedidos autorizados capturados posteriormente durante o faturamento, não a pedidos capturados automaticamente com `Authorize and Capture`. Consulte [Definir [!DNL Payment Services] como método de pagamento](production.md#set-payment-services-as-payment-method).

## Ativar captura excessiva

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Selecione o site a ser configurado usando o seletor de escopo de loja.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Na seção _[!UICONTROL Payment Services]_, expanda a seção&#x200B;_[!UICONTROL General Configuration]_.
1. Defina **[!UICONTROL Over Capture Enabled]** como `Yes`.
1. Clique em **[!UICONTROL Save Config]** para salvar suas alterações.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

## Capturar um pagamento autorizado

A captura excessiva ocorre durante o faturamento no Admin. O valor de captura solicitado deve estar dentro do limite aprovado pelo PayPal para sua conta de comerciante. Consulte [Criar uma fatura](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) para o fluxo de trabalho de faturamento padrão.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. Abrir um pedido com um pagamento autorizado que ainda não foi capturado.
1. Clique em **[!UICONTROL Invoice]**.
1. No campo custom capture amount, insira o valor total a ser capturado. Por exemplo, se o valor autorizado for USD 100 e o encargo final acordado for USD 110, digite `110`, não `10`. O valor solicitado deve estar dentro do limite aprovado pelo PayPal.
1. Selecione a captura online da fatura para solicitar o pagamento através do provedor de pagamento.
1. Revise a fatura e clique em **[!UICONTROL Submit Invoice]**.

### Capturar usando a API de fatura

Usar o ponto de extremidade padrão [Criar uma fatura](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice):

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

Use o código de armazenamento para o pedido e a ID interna do pedido. Autentique com um Administrador autorizado ou token de integração e defina `Content-Type: application/json`.

O exemplo de carga a seguir solicita uma fatura completa com captura online do USD 110 para um pedido autorizado para o USD 100, desde que o contrato PayPal do comerciante permita esse valor:

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

Neste exemplo:

1. `capture` solicita captura online.
1. `notify` controla se o Commerce envia o email de notificação de fatura.
1. `custom_capture_amount` é o valor final a ser capturado, não o aumento sobre o valor autorizado.

## Solução de problemas de uma captura rejeitada

Se o PayPal rejeitar uma solicitação de captura excessiva:

* Confirme se um contrato de captura em excesso está ativo para a conta de comerciante do PayPal usada para o pagamento.
* Verifique se o valor solicitado está dentro do limite aprovado. Se exceder o limite, solicite um valor menor ou entre em contato com o gerente de conta do PayPal para discutir um aumento.
