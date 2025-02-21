---
title: Processamento de nível 2 e nível 3
description: Níveis de processamento de pagamento de cartão em  [!DNL Payment Services]  transações.
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Processamento de nível 2 e nível 3

Há três níveis de processamento de cartão disponíveis no [!DNL Payment Services]:

* O Nível 1 é o mais comum, requer menos informações e, portanto, geralmente incorre em taxas de intercâmbio mais altas em comparação às transações processadas com dados de Nível 2 ou Nível 3, que geralmente estão relacionados a cartões de crédito corporativos e de compra.

* Com os níveis 2 e 3, os clientes do [!DNL Payment Services] com preços do Interchange Plus (IC++) que aceitam muitas transações de cartão de compra ou de cartão corporativo podem receber uma taxa de processamento mais baixa ao permitir que o [!DNL Payment Services] envie mais informações sobre uma transação. Se a transação se qualificar, de acordo com os requisitos da rede de cartões, o comerciante poderá receber uma taxa de processamento mais baixa para uma determinada transação.

>[!NOTE]
>
>Os preços de Nível 2 e Nível 3 só se aplicam às transações Visa e MasterCard. A American Express oferece somente preços de nível 2. A Discover não oferece preços de nível 2 nem de nível 3. Consulte [processamento de pagamento](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

Consulte [O que é IC++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

Os dados de processamento de nível 2 e nível 3 permitem que os comerciantes reduzam os preços do IC++ se fornecerem alguns detalhes adicionais sobre a compra que reduzam o risco do processador e forneçam aspectos benéficos:

* Os grandes clientes pagarão menos ao fornecer esses dados de processamento.

* Os clientes têm menos probabilidade de encontrar situações fraudulentas, pois os pedidos têm mais informações.

No entanto, as redes de cartões, como Visa e Mastercard, determinam, em última análise, se uma transação se qualifica para o processamento de nível 2 ou de nível 3:

* Os dados de Nível 2 contêm informações adicionais, como o valor do imposto do pedido, o código do cliente ou o número da OC.

* Os dados de nível 3 são informações mais detalhadas sobre a venda, o que ajuda a se qualificar para taxas de intercâmbio ainda mais baixas em comparação ao nível 2. Os dados de Nível 3 contêm informações como uma descrição do item comprado, a quantidade de unidades compradas, a unidade de medida dos itens solicitados e outros detalhes específicos.

O [!DNL Payment Services] coleta esses dados e fornece relatórios detalhados das suas transações de pagamento.

## Transações de pagamento com cartão de Nível 2 e Nível 3 em [!DNL Payment Services]

Para se qualificarem para o processamento de nível 2 ou nível 3, os comerciantes devem enviar as informações anteriores, embora sejam as redes de cartões que, em última análise, determinam para qual nível uma transação se qualifica durante o processamento.

Consulte as [Perguntas frequentes sobre o processamento de pagamentos](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

O processamento de nível 2 e nível 3 está desabilitado por padrão para [!DNL Payment Services] comerciantes no nível da loja.

O processamento de nível 2 e nível 3 estará disponível se você já estiver usando os preços do IC++. Para habilitar este recurso, você pode fazer isso através da [Interface de Linha de Comando (CLI](configure-cli.md)).

>[!IMPORTANT]
>
>Em caso de dúvidas, entre em contato com o gerente de conta do [!DNL Payment Services].
