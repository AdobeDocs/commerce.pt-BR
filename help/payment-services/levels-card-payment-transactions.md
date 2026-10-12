---
title: Processamento de nível 2 e nível 3
description: Níveis de processamento de pagamento de cartão em [!DNL Payment Services] transações.
role: Admin
feature: Payments, Paas, Saas
exl-id: db8993fe-dd6f-48b5-9e7b-69a0f2e08552
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%
---
# Processamento de nível 2 e nível 3

A [!DNL Payment Services] oferece recursos avançados de processamento de cartão para ajudar os comerciantes a otimizar suas transações de pagamento e reduzir as taxas de intercâmbio. Há três níveis de processamento de cartão disponíveis, cada um com diferentes requisitos de dados de transação.

>[!CAUTION]
>
> Os pedidos do [Fastlane](payments-options.md#fastlane-button) não incluem dados de Nível 2/Nível 3, itens de linha e detalhamento de valor.

## Requisitos em matéria de dados por nível de processamento

![Relatório de transações](assets/level-processing-details.png){width="500" zoomable="yes"}

O [!DNL Payment Services] coleta esses dados e fornece relatórios detalhados das suas transações de pagamento.

## Níveis de processamento disponíveis por rede de cartão

![Detalhes do cartão](assets/cards-details-level-processing.png){width="500" zoomable="yes"}

Consulte [processamento de pagamento](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

### Nível 1

O Nível 1 é o mais comum, requer menos informações e, portanto, geralmente incorre em taxas de intercâmbio mais altas em comparação às transações processadas com dados de Nível 2 ou Nível 3, que geralmente estão relacionados a cartões de crédito corporativos e de compra.

### Nível 2 e nível 3

[!DNL Payment Services] comerciantes no Interchange Plus (IC++) podem se qualificar para o processamento de Nível 2/Nível 3 se fornecerem detalhes de transação adicionais a redes de cartões e atenderem a critérios de qualificação específicos. Esses níveis são particularmente benéficos para os comerciantes que lidam com volumes significativos de compras ou de cartões corporativos, pois podem resultar em economias significativas de custos. O fornecimento de dados detalhados de Nível 2 ou Nível 3 pode:

* Diminua as taxas de processamento e otimize os custos gerais
* Evite fraudes, diminuindo o risco do processador
* Melhorar a segurança da transação

Consulte [O que é IC++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

## Transações de pagamento com cartão de Nível 2 e Nível 3 em [!DNL Payment Services]

Para se qualificarem para o processamento de nível 2 ou nível 3, os comerciantes devem enviar as informações anteriores, embora sejam as redes de cartões que, em última análise, determinam para qual nível uma transação se qualifica durante o processamento.

Consulte as [Perguntas frequentes sobre o processamento de pagamentos](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

O processamento de nível 2 e nível 3 está desabilitado por padrão para [!DNL Payment Services] comerciantes no nível da loja.

O processamento de nível 2 e nível 3 estará disponível se você já estiver usando os preços do IC++. Para habilitar este recurso, você pode fazer isso através da [Interface de Linha de Comando (CLI](configure-cli.md)).

>[!IMPORTANT]
>
>Em caso de dúvidas, entre em contato com o gerente de conta do [!DNL Payment Services].
