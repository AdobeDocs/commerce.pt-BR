---
title: Opções de pagamento
description: Defina as opções de pagamento para personalizar os métodos disponíveis para seus clientes de loja.
exl-id: 95e648e6-6cb8-4226-b5ea-e1857212f20a
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 0d00ce6e5291b3753cb7e2ee9e8af262b2c8894f
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%

---

# Opções de pagamento

Com [!DNL Adobe Commerce] e [!DNL Magento Open Source] [!DNL Payment Services], você tem várias opções de pagamento disponíveis.

Você pode definir essas opções de pagamento em [Configurações da página inicial](payments-home.md) ou [Configuração da loja](configure-admin.md) (recomendado para opções de pagamento herdadas ou para uma configuração de várias lojas).

Há comportamentos diferentes para cada método de pagamento, dependendo de onde você está no processo de finalização:

* Página do produto — A página de produto de um item
* Minicarrinho — Disponível após clicar no ícone do carrinho quando um produto foi adicionado aos carrinhos
* Carrinho de compras — Disponível ao clicar em _Exibir e editar carrinho_ no minicarrinho
* Exibição de check-out — Disponível ao clicar em _Prosseguir para o check-out_ do minicarrinho ou carrinho de compras

>[!IMPORTANT]
>
>A integração do [!DNL Payment Services] deve ser concluída para que os pagamentos possam ser processados.

## Experiência de Pagamentos Padrão vs. Avançados

A [!DNL Payment Services] fornece opções de pagamento e fluxos de integração **Avançado** (com suporte total) e **Padrão** (Check-out Expresso), dependendo do país em que você opera.

* **Avançado** - Todas as [opções de pagamentos](../payment-services/payments-options.md) disponíveis estão disponíveis para os [países com suporte total](../payment-services/introduction.md#availability) atuais. Durante a integração para habilitar pagamentos ao vivo, selecione a [opção de integração avançada](../payment-services/production.md#advanced-onboarding).

* **Padrão** - Um subconjunto de opções de pagamento (Check-out Expresso)—cartões de crédito e débito do PayPal—está disponível para outros países com suporte. [Os campos de cartão de crédito](#credit-card-fields) e [Pagamento Apple](#apple-pay-button) não estão disponíveis para esta opção de integração. Durante a integração para habilitar pagamentos ao vivo, selecione a [Opção de integração padrão](../payment-services/production.md#standard-onboarding).

Consulte [Habilitar [!DNL Payment Services] para produção](../payment-services/production.md#complete-merchant-onboarding) para obter informações sobre como concluir a integração avançada e padrão.

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] fornece um check-out simples e seguro para métodos de pagamento com cartão de crédito ou débito. Quando um comprador faz o check-out usando campos de cartão de crédito, ele insere seu nome, endereço de cobrança e informações de cartão de crédito ou débito para fazer seu pedido. As informações de seus clientes são usadas com segurança durante a sessão de compra para orientá-los perfeitamente pelo fluxo de finalização.

![Campos de cartão de crédito no check-out](assets/credit-card-fields.png){width="500" zoomable="yes"}

## [!UICONTROL Digital Wallets]

### Botão [!DNL Apple Pay]

Com o [!DNL Apple Pay], os comerciantes podem fornecer uma experiência de check-out segura e simplificada no Safari (para até 99 domínios por conta de comerciante), o que pode aumentar as conversões. Os detalhes armazenados de pagamento, contato e envio do botão [!DNL Apple Pay] são preenchidos automaticamente com base nos dispositivos iOS ou macOS dos clientes, permitindo uma experiência de finalização rápida com apenas um toque.

![Botão Pagar do Apple no minicart](assets/applepay-button.png){width="500" zoomable="yes"}

Quando ativado, o botão [!DNL Apple Pay] fica visível na página do produto, no minicarrinho, no carrinho de compras e nas exibições de check-out. Você pode configurar [!DNL Apple Pay] na configuração de armazenamento ou na Página Inicial da extensão.

>[!NOTE]
>
>  O certificado de verificação de domínio Apple Pay já está incluído no código de Serviços de pagamento. Verifique se o caminho `/.well-known/apple-developer-merchantid-domain-association` retorna um código de resposta 200. Consulte a [documentação do desenvolvedor do PayPal sobre integração com o Apple Pay](https://developer.paypal.com/docs/checkout/apm/apple-pay/#download-and-host-sandbox-domain-association-file) para obter mais informações sobre o certificado **verificação de Domínio do PayPal do Apple**.

Consulte [Configurações](settings.md#apple-pay) para obter mais informações.

### Botão [!DNL Google Pay]

Ao integrar o [!DNL Google Pay] à sua experiência de finalização de compra, os comerciantes podem coletar informações sobre pagamentos salvos, contatos e remessa na Conta da Google do comprador, oferecendo uma finalização de compra conveniente e simplificada em navegadores e aplicativos compatíveis.

O [!DNL Google Pay] está disponível somente em determinados países ou regiões e em determinados dispositivos. Consulte a [[!DNL Google Pay] documentação](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration) para obter mais informações.

![Botão Pagar do Google no check-out](assets/google-pay-button.png){width="500" zoomable="yes"}

Quando ativado, o botão [!DNL Google Pay] fica visível na página do produto, no minicarrinho, no carrinho de compras e nas exibições de check-out. Consulte [Configurações](configure-admin.md) para obter mais informações.

>[!NOTE]
>
> A API [!DNL Google Pay] só pode ser usada em sites em um contexto seguro. Consulte a documentação de [Solução de problemas](https://developers.google.com/pay/api/web/support/troubleshooting) para obter mais informações.

### [!DNL PayPal Payment Buttons]

O [!DNL PayPal payment buttons], que usa o PayPal para concluir uma compra, armazena o endereço de entrega, os endereços de cobrança e os detalhes de pagamento do comprador para uso posterior. Os compradores podem usar qualquer método de pagamento armazenado ou oferecido anteriormente pelo PayPal.

![Botão PayPal](assets/paypal-button.png){width="350" zoomable="yes"}

Você pode configurar [!UICONTROL PayPal payment buttons] na configuração do armazenamento ou na Página Inicial [!DNL Payment Services]. Consulte [Configurações](settings.md#payment-buttons) para obter mais informações.

Saiba mais sobre a disponibilidade de métodos de pagamento por país na [Documentação de métodos de pagamento](https://developer.paypal.com/docs/checkout/payment-methods/) do PayPal.

#### Botão [!DNL PayPal]

Os clientes podem fazer check-out com facilidade e confiança usando o botão PayPal.

O botão [!DNL PayPal] é visível na página do produto, no minicarrinho, no carrinho de compras e nas exibições de check-out.

#### Botão [!DNL Venmo]

Os clientes podem fazer check-out usando o botão [Venmo](https://venmo.com/).

O botão [!DNL Venmo] é visível na página do produto, no minicarrinho, no carrinho de compras e nas exibições de check-out.

#### Botão Cartão de crédito ou débito do PayPal

Os clientes podem fazer check-out usando o botão PayPal Débito ou Cartão de crédito.

O botão PayPal Debit or Credit card (Cartão de crédito ou débito do PayPal) está visível na página de check-out.

Esta opção pode ser usada para apresentar uma opção de pagamento com cartão de crédito ou débito aos seus compradores com um botão hospedado no PayPal, como alternativa à integração com cartão de crédito.

#### Botão [!DNL Pay Later]

Ofereça aos clientes pagamentos a curto prazo, sem juros e outras opções de financiamento para que eles possam comprar agora e pagar depois com o botão [!DNL Pay Later].

O botão [!DNL Pay Later] é visível na página do produto, no minicarrinho, no carrinho de compras e nas exibições de check-out.

Consulte informações sobre as ofertas do Pay Later na [documentação de ofertas do PayPal do PayPal](https://developer.paypal.com/docs/checkout/pay-later/us/). Use a lista suspensa **País ou região** para selecionar uma região de interesse.

Saiba como desabilitar ou habilitar as mensagens de [!DNL Pay Later] atualizando a configuração [Configurações](settings.md#payment-buttons).

### Usar somente botões de pagamento do PayPal

Para colocar rapidamente sua loja em modo de produção, você pode configurar _somente_ botões de pagamento do PayPal (Venmo, PayPal e assim por diante).—em vez de também usar a opção de pagamento com cartão de crédito PayPal.

Isso permite:

* Forneça várias opções de pagamento para seus clientes, incluindo os botões de pagamento Venmo e PayPal, com a opção de desativar os campos de cartão hospedado no PayPal e usar um provedor de cartão de crédito existente.
* Use seu fornecedor de cartão de crédito existente para pagamentos com cartão de crédito, ao mesmo tempo que usa outras opções de pagamento do PayPal.
* Use os botões de pagamento do PayPal em regiões onde o PayPal não oferece suporte a cartões de crédito como uma opção de pagamento.

Para **capturar pagamentos com _somente_ botões de pagamento do PayPal (_não_ a opção de pagamento com cartão de crédito do PayPal)**:

1. Certifique-se de que seu repositório esteja [no modo de produção](settings.md#enable-payment-services).
1. [Configure os botões de pagamento do PayPal desejados](settings.md#payment-buttons) em Configurações.
1. Desative _a opção **[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;na seção&#x200B;_[!UICONTROL Payment buttons]_._

Para **capturar pagamentos com seu provedor de cartão de crédito existente _e_ botões de pagamento do PayPal**:

1. Certifique-se de que seu repositório esteja [no modo de produção](settings.md#enable-payment-services).
1. [Configure os botões de pagamento do PayPal desejados](settings.md#payment-buttons).
1. Desative _a opção **[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)**&#x200B;na seção&#x200B;_[!UICONTROL Payment buttons]_._
1. Desative _a opção **[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)**&#x200B;na seção&#x200B;_[!UICONTROL Credit card fields]_ e use sua [conta de provedor de cartão de crédito existente](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html?lang=pt-BR#payments)._

## Opções de check-out

Com o [!DNL Payment Services], você pode configurar a experiência de check-out para que o Adobe Commerce se ajuste melhor às preferências e aos comportamentos dos compradores. Recursos como a [compartimentalização](vaulting.md) do cartão de crédito e a anulação automática de pedidos garantem uma transação simples e sem complicações para seus clientes.

Com o Adobe Commerce e o Magento Open Source [!DNL Payment Services], você tem várias experiências de check-out disponíveis. Há comportamentos diferentes para cada método de pagamento, dependendo de onde você está no processo de finalização:

* Página do produto — A página do produto de um item

* Minicarrinho — Disponível ao clicar no ícone do carrinho quando um produto foi adicionado aos carrinhos

* Carrinho de compras — Disponível ao clicar em Exibir e editar carrinho pelo minicarrinho

* Exibição de check-out — — Disponível após clicar em Prosseguir para check-out do minicarrinho ou carrinho de compras

### Recálculo de pedido

Quando um cliente entra no fluxo de finalização do minicarrinho, carrinho de compras ou página do produto, ele é direcionado a uma página de revisão do pedido, onde pode ver o endereço de envio selecionado em uma janela pop-up do PayPal. Depois que o cliente selecionar o método de entrega, a quantia da ordem será recalculada apropriadamente e o cliente poderá ver os custos e impostos de entrega.

Quando um cliente entra no fluxo de finalização da página de finalização da compra, o sistema já sabe o endereço de entrega e o valor final calculado, e os totais são devidamente representados.

Feriados fiscais, custos de envio e imposto sobre vendas podem variar amplamente de local para local. Depois que [!DNL Payment Services] receber o endereço e a taxa de remessa, ele recalcula rapidamente todos os custos aplicáveis e os exibe adequadamente durante os últimos estágios da finalização.

Saiba mais sobre a disponibilidade de métodos de pagamento por país na documentação [Métodos de pagamento do PayPal](https://developer.paypal.com/docs/checkout/payment-methods/){target=_blank}.
