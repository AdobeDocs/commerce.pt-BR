---
title: Integrar [!DNL Payment Services]
description: Conecte sua instância com a funcionalidade  [!DNL Payment Services]  ao concluir algumas etapas de integração.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Integrar [!DNL Payment Services]

Para começar a usar o [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source], você deve concluir algumas etapas de integração para conectar sua instância à funcionalidade de pagamentos.

## Fluxo de integração

Este diagrama de fluxo mostra o processo geral de integração do [!DNL Payment Services].

![Fluxo de integração](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> Para as versões 2.4.7 ou mais recentes do Adobe Commerce, você pode ignorar a etapa de extensão do Marketplace, pois o [!DNL Payment Services] está disponível e pronto para uso.

Após concluir a integração para sandbox ou pagamentos ao vivo, os relatórios financeiros podem ser acessados de [!DNL Payment Services] no Administrador.

Se a sandbox e os pagamentos ao vivo forem integrados e ativados, você poderá alternar facilmente entre esses modos na Página Inicial do [!DNL Payment Services].

## Pré-requisitos

Para usar o [!DNL Payment Services], você deve ter todos os módulos dependentes habilitados e os seguintes módulos disponíveis para a sua instância:

* Módulo do Conector de Serviços
* Módulo de ID de serviços
* Chaves de API

Os módulos Services Connector e Services ID são instalados automaticamente durante a [instalação do [!DNL Payment Services]](install.md).

Quando a instalação for concluída, você poderá ver uma nova seção nas definições de configuração (**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**) se expandir **[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**.

Para saber como criar ou acessar suas chaves de API, consulte [Credenciais de API](#obtain-api-credentials).

## Etapas de integração

1. [Instalar a [!DNL Payment Services] extensão](install.md#get-payment-services).
1. [Obter credenciais de API](connect.md#obtain-api-credentials).
1. [Conecte sua instância](connect.md#configure-commerce-services) aos Serviços Commerce. Essa conexão deve ser concluída apenas uma vez por instância do Commerce.
1. [Configure o serviço de sandbox](sandbox.md#enable-sandbox-testing) (ou, como alternativa, prossiga para [habilitar pagamentos ao vivo](sandbox.md#enable-live-payments) se você testou a funcionalidade em outro ambiente) com uma conta de processamento de pagamento do PayPal de teste.
1. [Defina [!DNL Payment Services] como seu método de pagamento](production.md#set-payment-services-as-payment-method), no modo sandbox, para iniciar o processamento de pagamentos de teste.
1. [Solicitar direitos de pagamentos](production.md#request-payments-entitlement-from-adobe) para habilitar a integração ao vivo.
1. [Conclua a integração do comerciante](production.md#complete-merchant-onboarding) para habilitar os pagamentos ao vivo para seus sites da Commerce.
1. [Obtenha sua [!DNL Payment Services] ID do Comerciante](production.md#configure-pricing-tier) e entregue-a ao setor de Vendas para configurar o tipo de preço correto.
1. [Habilite [!DNL Payment Services] no modo ativo](production.md#enable-live-payments) para iniciar o processamento de pagamentos ao vivo.
1. Testar Pagamentos, nos ambientes [sandbox](sandbox.md#test-in-sandbox-environment) e [produção](production.md#test-in-production).

>[!NOTE]
>
>Se você não configurar os Serviços da Commerce no Administrador (etapa 3), não poderá configurar sandbox ou pagamentos em tempo real.

## Solução de problemas

* [Solução de problemas [!DNL Payment Services] instalação](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [Conta de sandbox do PayPal não verificada](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [Dados do relatório [!DNL Payment Services] atrasados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* [Falha no cartão de crédito de teste com PayPal ao processar pagamentos em um ambiente de Sandbox](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
