---
title: Compatibilidade para  [!DNL Payment Services]
description: Saiba se o  [!DNL Payment Services]  está disponível em seu país e sua compatibilidade com a versão do Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
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

>[!VIDEO](https://video.tv.adobe.com/v/3447923?captions=por_br)

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

[!DNL Payment Services] aceita as moedas dos países [nos quais está disponível](#availability). Consulte [Configuração de moeda](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=pt-BR) para obter mais informações sobre a configuração de taxas de moeda.

Para obter mais informações sobre as moedas e os métodos de pagamento disponíveis com os produtos e serviços do PayPal, consulte as seguintes páginas:

* [Documentação de moedas com suporte](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Documentação de métodos de pagamento](https://developer.paypal.com/docs/checkout/payment-methods/).
