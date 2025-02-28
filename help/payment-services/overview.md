---
title: Introdução a  [!DNL Payment Services]
description: Saiba como instalar e usar o [!DNL Payment Services] como uma solução de processamento de pagamento pronta para uso, robusta e segura para seus [!DNL Adobe Commerce] e [!DNL Magento Open Source] sites.
role: User
level: Intermediate
feature: Payments, Checkout
exl-id: 1d41f86a-f874-48df-9173-9cf9f07e6d79
source-git-commit: 62b708f79ac011ef33b37f67384df7c94571ced2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Introdução ao [!DNL Payment Services]

O [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source] é a sua solução de autoatendimento completa, incluindo testes de sandbox e uma configuração simples, para fornecer um processamento de pagamento robusto e seguro para os sites da Commerce.

Seja você uma pequena empresa, uma empresa de médio porte ou uma grande empresa, essa solução de pagamentos ajuda a reduzir a sobrecarga operacional, aumentar a receita e fornecer ferramentas úteis para melhorar toda a experiência do comprador.

[!DNL Payment Services] é:

* Fácil de configurar e manter
* Projetado para maximizar seu lucro
* Seguro
* Projetado para atender a todas as suas necessidades de pagamento
* Autocontido no Administrador

## Recursos

[!DNL Payment Services] é o seu balcão central para check-out online (desde acordos e reembolsos até o pagamento). Ele fornece ferramentas poderosas para fornecer a você o insight e o controle necessários para criar a melhor experiência para seus compradores.

* [**Integração**](onboard.md) — o processo orienta você pela inscrição comercial, configuração técnica, direitos, configuração do ambiente de sandbox e habilitação de pagamento ao vivo.
* [**Opções de pagamento**](payments-options.md)—Defina as opções de pagamento para personalizar os métodos disponíveis para seus clientes de loja (ou de várias lojas).
* **Relatórios financeiros de gerenciamento de fluxo de caixa**—Sincronize [detalhes de pagamento](order-payment-status.md) com ordens para obter total transparência ao volume processado, saldo de pagamento, [pagamentos](payouts.md) e [relatórios de nível de transação](transactions.md) detalhados para reconciliação financeira e o máximo em visibilidade de transação.
* **Preços transparentes**—Os preços são claros e antecipados; o que você vê é o que você ganha.
* **Experiência eficiente de check-out**—Remova todas as barreiras para um check-out rápido e simples e crie clientes fiéis, com os recursos de [cofre de cartão](vaulting.md) e [Compra Instantânea](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) (habilitada por padrão para o Adobe Commerce).

## Disponibilidade

[!DNL Payment Services] está disponível para [!DNL Adobe Commerce] e [!DNL Magento Open Source]. A extensão [!DNL Payment Services] é compatível com [!DNL Adobe Commerce] versões 2.4.4 - 2.4.7-p3.

Atualmente, o [!DNL Payment Services] oferece suporte total (via [Integração avançada](../payment-services/production.md#advanced-onboarding)) para todas as opções de pagamento nestes países:

* Estados Unidos (US)
* Canadá (CA)
* Austrália (AUS)
* França (FR)
* Reino Unido (UK)

Os Serviços de Pagamento fornecem [recursos de Finalização Expressa](../payment-services/payments-options.md) (subconjunto de opções de pagamento) para outros [países disponíveis durante a integração](../payment-services/production.md#complete-merchant-onboarding).

Consulte as páginas [Política de ciclo de vida](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html) e [[!DNL Payment Services] notas de versão](release-notes.md) para obter mais informações sobre versões e lançamentos específicos.

### Qual é a opção [!DNL Payment Services] certa para você?

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

Consulte [Conectar](connect.md) para obter mais informações sobre como configurar sua extensão do [!DNL Payment Services].

### Cartões de crédito e moedas aceitos

[!DNL Payment Services] aceita as moedas dos países [nos quais está disponível](#availability). Consulte [Configuração de moeda](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html) para obter mais informações.

Para ver quais moedas o PayPal oferece suporte, consulte a [Documentação de moedas compatíveis](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

Para ver quais métodos de pagamento o PayPal aceita, consulte sua [documentação sobre métodos de pagamento](https://developer.paypal.com/docs/checkout/payment-methods/).

## Introdução

A integração e a configuração do [!DNL Payment Services] foram concluídas em apenas algumas etapas:

1. Obter a [[!DNL Payment Services] extensão](install.md).
1. Conecte sua instância do Commerce aos Serviços da Commerce.
1. Integrar e configurar o serviço de sandbox.
1. Habilite [!DNL Payment Services] como método de pagamento e comece a processar pagamentos de teste.
1. Conclua a integração do comerciante para habilitar os pagamentos ao vivo para seus sites.
1. Ative [!DNL Payment Services] no modo Online para iniciar o processamento de pagamentos online.

Para obter as instruções completas e iniciar o processo de integração, consulte [Integração [!DNL Payment Services]](onboard.md).
