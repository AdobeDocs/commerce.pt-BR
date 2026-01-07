---
title: Testar e validar
description: O teste e a validação ajudam a garantir que as  [!DNL Payment Services]  funções funcionem conforme o esperado e forneçam as melhores opções de pagamento para seus clientes
exl-id: 95b4615e-73b0-41e8-83e2-e65a0b22f10f
feature: Payments, Checkout, Paas, Saas
source-git-commit: b75cad4fd71b5ab9c0199ca47800c36cbd1ae76c
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Testar e validar

Antes de expor o [!DNL Payment Services] for [!DNL Adobe Commerce] e o [!DNL Magento Open Source] aos seus compradores, é uma boa ideia testar em seu ambiente de sandbox as _and_ em produção. O teste e a validação ajudam a garantir que as funções do [!DNL Payment Services] funcionem conforme o esperado e forneçam as melhores opções de pagamento para sua loja e seus clientes.

## Teste em ambiente de sandbox

Testar o [!DNL Payment Services] em um ambiente de sandbox é uma etapa de validação importante, embora seja um ambiente simulado conectado somente à sandbox do PayPal, não aos bancos e comerciantes reais.

1. Conclua um check-out bem-sucedido de sua loja, com [Campos de Cartão de Crédito](payments-options.md#credit-card-fields) ou com qualquer um dos [botões de pagamento do PayPal](payments-options.md#paypal-smart-buttons). Consulte [Testando credenciais](#testing-credentials) para obter mais informações sobre como usar cartões de crédito falsos para testes.
1. Capture (quando sua ação de pagamento for [definida como `Authorize and Capture`](onboard.md#set-payment-services-as-payment-method)), [restitua](refunds.md) ou [anule](voids.md) a ordem recém-concluída. Você também pode simplesmente [criar uma fatura](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"} para um pedido, se sua ação de pagamento estiver definida como `Authorize` em vez de `Authorize and Capture`.
1. Em 24-48 horas, exiba a transação e outras informações no [Relatório de pagamentos](payouts.md).
1. Veja detalhes do pedido no [Relatório de status do pagamento do pedido](order-payment-status.md).

### Testar em ambientes de desenvolvimento locais

Testar métodos de pagamento PayPal, PayLater e Venmo em ambientes de desenvolvimento locais requer que seu ambiente seja acessível pela Internet. Estes métodos de pagamento usam um [retorno de chamada de envio do lado do servidor](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/) que requer que o PayPal se comunique com sua instância do Commerce para recuperar as opções de envio e calcular os totais.

>[!INFO]
>
>Sem um URL acessível pela Internet, o retorno de chamada do delivery não pode funcionar, o que resulta em um fluxo de check-out diferente da produção. Sempre teste com um URL acessível para garantir resultados precisos.

Para expor seu ambiente local:

1. Use um serviço de túnel como o [ngrok](https://ngrok.com/) para criar uma URL acessível publicamente para o seu ambiente local.

1. Atualize sua configuração de URL base do Commerce para corresponder ao URL do Grok:

   ```bash
   bin/magento config:set web/unsecure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento config:set web/secure/base_url https://your-ngrok-url.ngrok.io/
   bin/magento cache:flush
   ```

1. Conclua seus testes com os métodos de pagamento PayPal, PayLater ou Venmo.

1. Restaure a configuração original do URL básico quando o teste estiver concluído.

Se o tempo de resposta do endpoint for inferior a 5 segundos, o PayPal exibe uma mensagem de erro na janela pop-up.

### Testando credenciais

Ao testar e validar sua sandbox, você deve usar números de cartão de crédito falsos para não criar encargos reais para uma conta de cartão de crédito existente.

Use o Gerador de Cartão de Crédito do PayPal para [gerar informações de cartão de crédito aleatórias](https://www.paypal.com/us/smarthelp/article/where-can-i-find-test-credit-card-numbers-ts2157) para testes.

Para testar o Apple Pay no modo de sandbox:

* Crie uma [conta de testador de sandbox da Apple](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account), completa com informações falsas sobre cartão de crédito e cobrança.
* [Registre seus domínios de sandbox](https://developer.paypal.com/docs/checkout/apm/apple-pay/#link-registeryoursandboxdomains).

>[!NOTE]
>
>O processamento de pagamento de sandbox do PayPal às vezes é lento e o serviço pode ocasionalmente falhar. Essa situação não é uma indicação da velocidade e da eficiência do processamento de pagamento de produtos em tempo real.

## Teste em produção

É altamente recomendável que você teste o [!DNL Payment Services] na produção, com cartões de crédito e bancos reais, antes de expor essa funcionalidade aos compradores. Embora o teste de [!DNL Payment Services] na sandbox seja importante, o teste na produção é o método mais à prova de falhas para garantir que [!DNL Payment Services] funcione conforme o esperado.

Você pode testar [!DNL Payment Services] na produção de uma das duas formas a seguir:

* Escolha um horário em que você saiba que nenhum pedido será feito pelos compradores.
* Use uma loja na web que esteja temporariamente inacessível aos compradores, mas que esteja acessível a você para testes.

Conclua seus testes de produção com cartões de crédito reais e contas do PayPal, testando todo o ciclo de vida de um pagamento, incluindo captura e reembolso. Concluir todo o fluxo de pagamento e check-out durante os testes fornece a imagem mais clara de como a funcionalidade do [!DNL Payment Services] funcionará quando os compradores ao vivo estiverem usando-a.

Você também deve verificar se as informações exibidas nos extratos bancários dos métodos de pagamento usados no teste de produção estão corretas e esperadas (incluindo a descrição da sua empresa).

Para testar o Apple Pay no modo de produção, você deve [registrar os domínios de produção](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).
