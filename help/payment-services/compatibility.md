---
title: Compatibilidade para  [!DNL Payment Services]
description: Saiba se o  [!DNL Payment Services]  está disponível em seu país e sua compatibilidade com a versão do Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
exl-id: 4bef8429-5053-424d-806a-9e8b96295b1b
TQID: https://experienceleague.adobe.com/UUD0IiEiwh0sZKMkclOJtoC2bKYcmDN3WAWD16mfad4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 454
ht-degree: 0%

---

# Compatibilidade para [!DNL Payment Services]

O [!DNL Payment Services] está disponível para o Adobe Commerce e o Magento Open Source. [!DNL Payment Services] agora é compatível com o Adobe Commerce versões 2.4.x.

## Pré-requisitos

Para usar o [!DNL Payment Services], primeiro você precisará conectar sua instância do Commerce. **Você configurou esta conexão apenas uma vez**.

1. Se você não tiver certeza se sua instância está conectada, navegue até **Sistema** > Serviços > **Commerce Services Connector** e exiba os valores de chave de API pública e privada nas seções Chaves de sandbox e Chaves de produção, e os campos Projeto e Espaço de dados na seção Identificador SaaS. Se esses valores estiverem presentes, sua instância será conectada.

1. Se ainda precisar conectar sua instância, exiba as instruções na página [Commerce Services Connector](../landing/saas.md).

   >[!TIP]
   >
   > Consulte nosso vídeo tutorial do [Adobe Commerce Services Connector](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) para obter mais informações.

1. Se você já tiver conectado sua instância, navegue até a página [integração](onboard.md) para obter as próximas etapas.

>[!IMPORTANT]
>
> Todos os comerciantes qualificados para [!DNL Payment Services] podem usar **um espaço de dados de produção** e **dois espaços de dados de teste**.

## Experiência [!DNL Payment Services] padrão vs. avançada

O [!DNL Payment Services] fornece opções de pagamento **Padrão** (Check-out Expresso) e **Avançado** (com suporte total) e fluxos de integração, dependendo do país em que você opera.

>[!NOTE]
>
> [!DNL Payment Services] fornece [recursos de Check-out Expresso](../payment-services/payments-options.md) (subconjunto de opções de pagamentos) para outros [países disponíveis durante a integração](../payment-services/production.md#complete-merchant-onboarding).

### Qual é a opção [!DNL Payment Services] certa para você?

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

Consulte [Conectar](connect.md) para obter mais informações sobre como configurar sua extensão do [!DNL Payment Services].

>[!BEGINTABS]

>[!TAB Padrão (Check-out Expresso)]

![check-out](assets/icon-check.png) do PayPal Check-out

Botão ![verificar](assets/icon-check.png) Cartão de crédito ou débito do PayPal

![verificar](assets/icon-check.png) configurações de check-out personalizado

![verificar](assets/icon-check.png) Preços padrão

![Verificação](assets/icon-check.png) **Disponível em XX países**

[![saiba mais](assets/learn-more-button.svg)](onboard.md)

>[!TAB Avançado (Totalmente suportado)]

![verificar](assets/icon-check.png) Cartão de débito

![verificar](assets/icon-check.png) crédito do PayPal

![verificar](assets/icon-check.png) campos de cartão de crédito

![botão Verificar](assets/icon-check.png) do Apple Pay

![botão Verificar](assets/icon-check.png) do Google Pay

![verificar](assets/icon-check.png) botões de Pagamento do PayPal

Botão ![verificar](assets/icon-check.png) Venmo

Botão ![verificar](assets/icon-check.png) Cartão de crédito ou débito do PayPal

Botão ![verificar](assets/icon-check.png) pagar mais tarde

![verificar](assets/icon-check.png) configurações de check-out personalizado

![verificar](assets/icon-check.png) Preços personalizados

![verificação](assets/icon-check.png) (recursos de preços N2/N3 - Somente EUA)

![check](assets/icon-check.png) **Disponível somente nos Estados Unidos (EUA), Canadá (CA) e Austrália (AUS). França (FR), Reino Unido (UK)**

[![saiba mais](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Consulte as páginas da [política de ciclo de vida](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=pt-BR) e das [[!DNL Payment Services] notas de versão](release-notes.md) para obter mais informações sobre versões e lançamentos específicos.

Para obter as instruções completas e iniciar o processo de integração, consulte [Introdução ao [!DNL Payment Services]](onboard.md).

### Cartões de crédito e moedas aceitos

[!DNL Payment Services] aceita as moedas dos países em que está disponível. Consulte [Configuração de moeda](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=pt-BR) para obter mais informações sobre a configuração de taxas de moeda.

Para obter mais informações sobre as moedas e os métodos de pagamento disponíveis com os produtos e serviços do PayPal, consulte as seguintes páginas:

* [Documentação de moedas com suporte](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Documentação de métodos de pagamento](https://developer.paypal.com/docs/checkout/payment-methods/).
