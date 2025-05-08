---
title: Fluxo [!DNL Payment Services] de integração
description: Conecte sua instância com a funcionalidade  [!DNL Payment Services]  ao concluir algumas etapas de integração.
role: User
level: Intermediate
exl-id: 1ee8c660-0941-4378-a1d7-ae45de3de211
feature: Payments, Checkout, Integration, Paas, Saas
source-git-commit: 9f7690ae325853b9b4a590b3d1cd538909a26462
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Fluxo de integração do [!DNL Payment Services]

Para começar a usar o [!DNL Payment Services], você deve concluir algumas etapas de integração. Para obter uma orientação precisa, selecione a opção Adobe Commerce abaixo que melhor se alinha à instância e à versão da sua organização.

Este diagrama de fluxo mostra o processo geral de integração do [!DNL Payment Services] em todas as versões:

![Fluxo de integração](assets/flow-payment-services.png){width="700" zoomable="yes"}

Veja abaixo a sua versão específica do Adobe Commerce para integrar com o [!DNL Payment Services].

## Ajude-me a encontrar minha instância e versão

### Adobe Commerce ou Magento Open Source | v2.4.7+

Estes diagramas de fluxo mostram o processo geral de integração do [!DNL Payment Services] com um Adobe Commerce ou Magento Open Source mais recente do que a v2.4.7.

>[!BEGINTABS]

>[!TAB Sandbox]

Este diagrama de fluxo mostra o processo de integração da sandbox com uma Adobe Commerce ou Magento Open Source mais recente que a v2.4.7, em que o [!DNL Payment Services] já está pronto para uso com o Adobe Commerce.

![Fluxo de integração](assets/flow-sandbox-configuration-onboarding-2.4.7.png){width="700" zoomable="yes"}

**Etapas de integração para versões v2.4.7+ Parte 1: Sandbox**

1. [Conecte sua instância](connect.md#configure-commerce-services) aos Serviços Commerce. Essa conexão deve ser concluída apenas uma vez por instância do Commerce. [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."}
1. [Configure o serviço de sandbox](sandbox.md#enable-sandbox-testing) (ou, como alternativa, prossiga para [habilitar pagamentos ao vivo](sandbox.md#enable-live-payments) se você testou a funcionalidade em outro ambiente) com uma conta de processamento de pagamento do PayPal de teste.
1. Testar Pagamentos em um ambiente [sandbox](sandbox.md#test-in-sandbox-environment).

[![saiba mais](assets/learn-more-button.svg)](https://helpx.adobe.com/br/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB Produção]

Este diagrama de fluxo mostra as etapas de produção necessárias para habilitar o [!DNL Payment Services].

![Fluxo de integração](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**Etapas de integração para versões v2.4.7+ Parte 2: Produção**

1. [Defina [!DNL Payment Services] como seu método de pagamento](production.md#set-payment-services-as-payment-method), no modo sandbox, para iniciar o processamento de pagamentos de teste.
1. [Solicitar direitos de pagamentos](production.md#request-payments-entitlement-from-adobe) para habilitar a integração ao vivo.
1. [Conclua a integração do comerciante](production.md#complete-merchant-onboarding) para habilitar os pagamentos ao vivo para seus sites da Commerce.
1. [Obtenha sua [!DNL Payment Services] ID do Comerciante](production.md#configure-pricing-tier) e entregue-a ao setor de Vendas para configurar o tipo de preço correto.
1. [Habilite [!DNL Payment Services] no modo ativo](production.md#enable-live-payments) para iniciar o processamento de pagamentos ao vivo.
1. Testar Pagamentos, nos ambientes [sandbox](sandbox.md#test-in-sandbox-environment) e [produção](production.md#test-in-production).

[![saiba mais](assets/learn-more-button.svg)](production.md)

>[!ENDTABS]

### Adobe Commerce ou Magento Open Source | v2.4.0-2.4.6 [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."}

Estes diagramas de fluxo mostram o processo geral de integração do [!DNL Payment Services] com o Adobe Commerce ou o Magento Open Source versões 2.4.0 a 2.4.6. É necessário baixar e instalar o [!DNL Payment Services] para iniciar a integração.

>[!BEGINTABS]

>[!TAB Sandbox]

Este diagrama de fluxo mostra as etapas da sandbox necessárias para a integração do [!DNL Payment Services] com o Adobe Commerce ou o Magento Open Source versões 2.4.0 a 2.4.6.

![Fluxo de integração](assets/flow-sandbox-installation-configuration-onboarding-2.4.0.png){width="700" zoomable="yes"}

**Etapas de integração para versões v2.4.0-2.4.6 Parte 1: Sandbox**

1. [Instale a [!DNL Payment Services] extensão](install.md#get-payment-services), se necessário.
1. [Obter credenciais de API](connect.md#obtain-api-credentials).
1. [Conecte sua instância](connect.md#configure-commerce-services) aos Serviços Commerce. Essa conexão deve ser concluída apenas uma vez por instância do Commerce.
1. [Configure o serviço de sandbox](sandbox.md#enable-sandbox-testing) (ou, como alternativa, prossiga para [habilitar pagamentos ao vivo](sandbox.md#enable-live-payments) se você testou a funcionalidade em outro ambiente) com uma conta de processamento de pagamento do PayPal de teste.
1. Testar Pagamentos em um ambiente [sandbox](sandbox.md#test-in-sandbox-environment).

[![saiba mais](assets/learn-more-button.svg)](https://helpx.adobe.com/br/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB Produção]

Este diagrama de fluxo mostra o processo geral de habilitação do [!DNL Payment Services] em um ambiente de produção com o Adobe Commerce ou Magento Open Source versões 2.4.0 a 2.4.6.

![Fluxo de integração](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**Etapas de integração para versões v2.4.0-2.4.6 Parte 2: Produção**

1. [Defina [!DNL Payment Services] como seu método de pagamento](production.md#set-payment-services-as-payment-method), no modo sandbox, para iniciar o processamento de pagamentos de teste.
1. [Solicitar direitos de pagamentos](production.md#request-payments-entitlement-from-adobe) para habilitar a integração ao vivo.
1. [Conclua a integração do comerciante](production.md#complete-merchant-onboarding) para habilitar os pagamentos ao vivo para seus sites da Commerce.
1. [Obtenha sua [!DNL Payment Services] ID do Comerciante](production.md#configure-pricing-tier) e entregue-a ao setor de Vendas para configurar o tipo de preço correto.
1. [Habilite [!DNL Payment Services] no modo ativo](production.md#enable-live-payments) para iniciar o processamento de pagamentos ao vivo.
1. Testar Pagamentos, nos ambientes [sandbox](sandbox.md#test-in-sandbox-environment) e [produção](production.md#test-in-production).

[![saiba mais](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

>[!NOTE]
>
>Se você não configurar os Serviços da Commerce no Administrador (Parte 1), não poderá configurar sandbox ou pagamentos em tempo real.

>[!MORELIKETHIS]
>
> * [Solução de problemas [!DNL Payment Services] instalação](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=pt-BR)
> * [Conta de sandbox do PayPal não verificada](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html?lang=pt-BR)
> * [Dados do relatório [!DNL Payment Services] atrasados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html?lang=pt-BR)
> * [Falha no cartão de crédito de teste com PayPal ao processar pagamentos em um ambiente de Sandbox](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=pt-BR)