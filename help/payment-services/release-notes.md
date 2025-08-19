---
title: Notas de versão do [!DNL Payment Services]
description: Revise as notas de versão para obter informações sobre todas as  [!DNL Payment Services]  versões.
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '4093'
ht-degree: 0%

---


# Notas de versão

Estas notas de versão descrevem a versão inicial do [!DNL Payment Services] e incluem:

![Novos](../assets/new.svg) Novos recursos
![Problema corrigido](../assets/fix.svg) Correções e melhorias
![Problema conhecido](../assets/bug.svg) Problemas conhecidos

Para alterações e correções de recursos lançadas fora da versão normal do recurso, revise as seções _Atualizações do serviço hospedado_.

Saiba mais sobre as próximas versões, o suporte ao produto e quais versões do Adobe Commerce oferecem suporte à extensão [!DNL Payment Services]; consulte os tópicos [Agendamento de versão](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/planning/schedule) e [Disponibilidade do produto](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/product-availability) do Adobe Commerce.

## Atualizações do serviço hospedado

Essas notas de versão descrevem alterações e correções de recursos que ocorreram e foram lançadas fora das versões de recursos regulares do serviço hospedado.

+++Atualizações do serviço hospedado

_25 de abril, 2025_

![Novo problema](../assets/new.svg)<!-- Issue PAY-6051 --> Agora, o painel [!DNL Payment Services] exibe a versão da extensão atual e a versão do painel.

_30 de agosto de 2024_

![Novo problema](../assets/new.svg)<!-- Issue PAY-5658 --> Agora, os comerciantes podem filtrar as transações por Detalhes do Pagamento no [relatório de transações](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=pt-BR), para obter dados mais detalhados e precisos sobre métodos de pagamento.

_15 de julho de 2024_

![Novo problema](../assets/new.svg)<!-- Issue PAY-5571 --> Agora, os comerciantes podem filtrar transações por email de cliente do Commerce no [relatório de transações](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=pt-BR). Insira o email do cliente para filtrar as transações desse email específico.

_9 de julho de 2024_

![Novo problema](../assets/new.svg)<!-- Issue PAY-5488 --> Agora, os comerciantes podem exibir a ID de cliente da Commerce como uma coluna no [relatório de transações](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=pt-BR) para ajudar a identificar as transações colocadas por um cliente específico. Além disso, os comerciantes podem filtrar o relatório de transações por essa ID de cliente da Commerce para pedidos associados.

_5 de março de 2024_

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-5252 --> Agora, os comerciantes podem copiar dados das grades do painel selecionando o conteúdo de uma única célula.

_10 de outubro de 2023_

![Novo problema](../assets/fix.svg)<!-- Issue PAY-4888 --> Agora, os comerciantes podem filtrar as transações de cartão de crédito e débito pelos últimos quatro dígitos do número do cartão no [Relatório de transações](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=pt-BR).

_12 de julho de 2023_

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-4587 --> Um problema introduzido na versão [!DNL Payment Services] 2.1.0 que impedia que as anulações de autorização colocadas por versões anteriores da extensão agora é resolvido. Comerciantes que usam qualquer versão de [!DNL Payment Services] podem anular autorizações.

_9 de junho de 2023_

![Novo](../assets/new.svg)<!-- Issue PAY-4288 --> Agora, os comerciantes podem [configurar _somente_ botões de pagamento do PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=pt-BR#use-only-paypal-payment-buttons)—e _não_ usar a opção de pagamento com cartão de crédito do PayPal. Isso permite que os comerciantes forneçam várias opções de pagamento, incluindo os botões de pagamento Venmo e PayPal, e usem um fornecedor de cartão de crédito existente em vez da opção de pagamento com cartão de crédito PayPal.

![Novo](../assets/new.svg)<!-- Issue PAY-4050 --> Adicionou uma [visualização de dados](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view), que aparece na Página Inicial do Serviço de Pagamento, para o relatório Status do pagamento da ordem.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-4486--> Anteriormente, o botão PayPal PayLater não aparecia no check-out para comerciantes do Reino Unido. Esse problema está resolvido.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-4485--> As exibições de visualização de dados de relatório estão aparecendo na Página Inicial [!DNL Payment Services] quando o [!DNL Payment Services] está desabilitado.

_25 de janeiro de 2023_

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-4102 --> As novas instalações de [!DNL Payment Services] não podem configurar os Serviços Commerce, tornando [!DNL Payment Services] inoperante. Para corrigir esse problema, atualize sua extensão do [!DNL Payment Services] para a versão 1.5.3.

_12 de setembro de 2022_

![Novo](../assets/new.svg)<!-- Issue PAY-3705 --> O `increment_id` agora está disponível para uso na reconciliação de pagamentos em sistemas ERP externos. Ele é propagado para o [`custom_id` _and_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/data.html#reconcile-with-erp-system), visível no webhook do PayPal e nos detalhes da atividade do comerciante para um pagamento.

_31 de agosto de 2022_

![Correção do problema](../assets/fix.svg)<!-- Issue PAY-3629 --> Quando um novo comerciante acessa a Página inicial [!DNL Payment Services] pela primeira vez, a página agora é carregada imediatamente para exibir o conteúdo em vez de exigir uma atualização da página.

_9 de agosto de 2021_

O ![Novo](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay agora está disponível como um Botão Inteligente do PayPal. Esta [opção de pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-options.html?lang=pt-BR#apple-pay-button) permite que os clientes usem o recurso Touch ID em seus dispositivos iOS ou macOS para selecionar o Apple Pay. O Apple Pay processa o pagamento usando as credenciais de pagamento de cartão de crédito e débito armazenadas no dispositivo.

_28 de junho de 2021_

![Novas](../assets/new.svg)<!-- Issue PAY-1720 --> Contestações para ordens de armazenamento agora estão disponíveis no [Relatório de status de pagamento de pedidos](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#view-disputes). Você pode resolver contestações navegando diretamente para o Centro de Resolução do PayPal a partir de [!DNL Payment Services].

As ![Novas](../assets/new.svg)<!-- Issue PAY-2854 --> melhorias na experiência do usuário da Página Inicial [!DNL Payment Services] incluem a capacidade de modificar uma configuração no nível de herança atual e melhorias na exibição do cabeçalho e da navegação.

![Novo](../assets/new.svg)<!-- Issue PAY-2854 --> Agora você pode ver avisos ao alternar do modo de sandbox para o modo de produção e ao tentar sair de um modo de exibição com atualizações que não foram salvas.

![Novo](../assets/new.svg)<!-- Issue PAY-2761 --> Agora é possível personalizar os dados exibidos no [Relatório de status do pagamento da ordem](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html#show-and-hide-columns) e no [Relatório de pagamentos](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/payouts.html#show-and-hide-columns) exibindo ou ocultando colunas usando o controle Configurações de coluna.

+++

>[!NOTE]
>
> As versões ocorrem frequentemente para fornecer novos recursos e correções, conforme necessário. A programação de lançamento não foi corrigida.

## v2.12.0

_20 de agosto de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-6022 --> O [Fastlane](https://experienceleague.adobe.com/pt-br/docs/commerce/payment-services/payments-checkout/payments-options) oferece uma compra mais rápida durante check-outs de convidados.

![Novo](../assets/new.svg)<!-- PAY-6168 --> adicionou a mutação [`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) a [!DNL Payment Services] para permitir transições mais suaves e uma melhor reutilização do carrinho.

![Novo](../assets/new.svg)<!-- PAY-6169 --> adicionou a mutação [`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/) a [!DNL Payment Services] para melhorar o gerenciamento do ciclo de vida da cotação.

![Novo](../assets/new.svg)<!-- PAY-6227 --> Ao fazer check-out com o PayPal, [!DNL Payment Services] ignora a janela pop-up de confirmação de pedido para um processo de compra mais rápido.

![Novo](../assets/new.svg)<!-- PAY-6234 --> Adicionou um novo recurso para a opção de pagamento [Pagar Mais Tarde](https://experienceleague.adobe.com/pt-br/docs/commerce/payment-services/payments-checkout/payments-options). Agora, o configurador de mensagens BNPL oferece mais flexibilidade na exibição de mensagens BNPL de Pagamento Posterior nas páginas de finalização de compra do cliente.

![Problema corrigido](../assets/fix.svg)<!-- PAY-5505 --> Agora, o [!DNL Payment Services] define a cotação como inativa quando um pop-up do Google Pay ou PayPal é fechado na página do produto.

![Problema corrigido](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services] não permite mais que pedidos sejam criados com cotações vazias.

## v2.11.1

_14 de março de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção de um problema](../assets/fix.svg)<!-- PAY-5849 --> que afetou [Itens de linha](line-items.md) durante o check-out. Agora, o [!DNL Payment Services] melhorou a confiabilidade do processo de finalização para **Itens de Linha**. Se você encontrar um problema semelhante, entre em contato com o representante de vendas do [!DNL Payment Services] para obter assistência.

## v2.11.0

_13 de março de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes


![Novo](../assets/new.svg)<!-- PAY-5938 --> Agora, o [!DNL Payment Services] permite que os comerciantes gerenciem configurações de pagamento para maximizar a flexibilidade em seus negócios. Esta versão melhora a capacidade de anexar [várias contas do PayPal](https://experienceleague.adobe.com/pt-br/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts) para as regiões e marcas que um comerciante aceita. Nossa equipe de vendas pode fornecer um link de integração para configurar os escopos de visualização do site e da loja.

![Novo](../assets/new.svg)<!-- PAY-5968 --> Agora, o [!DNL Payment Services] atualiza a configuração de Administrador com os valores de **ID do Comerciante do PayPal** e **Status do Comerciante do PayPal**. Esses valores fornecem aos comerciantes maior visibilidade sobre o status da conta do PayPal.

![Corrigido o problema](../assets/fix.svg)<!-- PAY-5816 --> Restaurou a funcionalidade de ordem normal em [!DNL Payment Services] ao resolver um problema que estava causando erros em todos os posicionamentos de pedidos com a versão v2.9.0.

![Correção de um problema](../assets/fix.svg)<!-- PAY-5825 --> em que o minicarrinho Apple Pay usava uma URL de totais estimados incorreta para clientes conectados. Agora, [!DNL Payment Services] garante cálculos totais precisos.

![Correção de um problema](../assets/fix.svg)<!-- PAY-5826 --> Melhoria na confiabilidade do gerenciamento de pedidos ao resolver um problema que causava um erro HTTP 500 ao alterar o status da cotação para `inactive`.

![Problema corrigido](../assets/fix.svg)<!-- PAY-5849 --> Corrigido um problema no qual `LineItemProvider` gerava exceções para quantidades decimais abaixo de 1. Agora, o [!DNL Payment Services] oferece melhor suporte para quantidades fracionárias.

![Correção de um problema](../assets/fix.svg)<!-- PAY-5868 --> Correção de um erro de valor de cartão-presente durante o check-out. [!DNL Payment Services] agora garante valores precisos durante o processo de finalização.

![Correção de um problema](../assets/fix.svg)<!-- PAY-5911 --> Resolução de erros durante a criação de remessas para pedidos feitos com métodos de pagamento online que não[!DNL Payment Services], aumentando a confiabilidade geral.

![Problema corrigido](../assets/fix.svg)<!-- PAY-5954 --> O [!DNL Payment Services] agora oferece uma experiência de finalização mais suave ao resolver um problema em que o Apple Pay não conseguiu fazer um pedido quando um cartão de crédito diferente foi selecionado na carteira.

![Problema corrigido](../assets/fix.svg)<!-- PAY-5971 --> O [!DNL Payment Services] não redireciona mais os clientes para a página de revisão do pedido quando o Apple Pay falha, evitando interrupções desnecessárias do check-out.

## v2.10.3

_24 de fevereiro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção do problema](../assets/fix.svg)<!-- PAY-xxxx --> Melhoria geral na estabilidade e no desempenho.

![Correção de um problema](../assets/fix.svg)<!-- PAY-xxxx -->: melhorias e otimizações gerais. Correção de bugs críticos da v2.10.2.

## v2.10.2

_21 de fevereiro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Problema conhecido](../assets/bug.svg)<!-- PAY-xxxx --> contém erros críticos que podem afetar a estabilidade e o desempenho. A Adobe recomenda atualizar para a v2.10.3 em vez de usar essa versão (v2.10.2).

## v2.10.1

_5 de fevereiro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5813 --> Suporte adicionado para Adobe Commerce 2.4.8 e PHP 8.4.

## v2.10.0

_13 de dezembro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5702 --> O [!DNL Payment Services] agora oferece suporte aos endpoints do GraphQL para compartimentação sem compra, permitindo que os clientes salvem seus métodos de pagamento sem concluir uma transação.

![Novo](../assets/fix.svg)<!-- PAY-5789 --> O [!DNL Payment Services] agora oferece suporte à [autenticação Segura 3D com o Google Pay](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/payment-services/security-compliance/security#3ds), aprimorando a segurança para comerciantes e clientes durante transações de pagamento.

![Correção](../assets/fix.svg)<!-- PAY-5703 --> A [!DNL Payment Services] adiciona a capacidade de [clientes salvarem cartões diretamente em sua **Minha Conta**](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting), melhorando a conveniência e simplificando check-outs futuros. `Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/).

![Correção](../assets/fix.svg)<!-- PAY-5762 --> corrigiu um problema onde os códigos de cupom não eram aplicados na página de revisão do pedido quando o pedido era iniciado a partir da página de detalhes do produto (PDP).

![Correção](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services] agora exibe descrições e endereços de cobrança para [cartões com cofre na página de check-out](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting), dando aos clientes mais visibilidade sobre seus métodos de pagamento salvos.

![Correção](../assets/fix.svg)<!-- PAY-5793 --> O [!DNL Payment Services] permite que os comerciantes armazenem o endereço de cobrança de cartões com cofre diretamente da página de check-out, garantindo informações de pagamento precisas e completas.

## v2.9.0

_7 de novembro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services] agora oferece suporte a uma **URL atualizada do SDK para Apple Pay**, melhorando a integração para comerciantes que usam o Apple Pay. Esse recurso é compatível com o macOS 14 e versões posteriores, os dispositivos que executam versões anteriores do macOS não exibirão essa funcionalidade.

![Novo](../assets/new.svg)<!-- PAY-5630 --> Atualizou as páginas **Check-out**, **Produto**, **Carrinho** e **Minicarrinho** para oferecer suporte à **URL atualizada do SDK para Apple Pay**, aprimorando a experiência do usuário para comerciantes que oferecem o Apple Pay como uma opção de pagamento.

![Novo](../assets/new.svg)<!-- PAY-5635 --> Estimativas de envio aprimoradas **com base no endereço de pagamento do Apple**, permitindo que os clientes vejam os custos de envio precisos durante o check-out.

![Correção](../assets/fix.svg)<!-- PAY-5661 --> Correção de vários **[!DNL Payment Services]problemas no check-out**, melhorando a confiabilidade do processo de pagamento para comerciantes e compradores.

![Correção](../assets/fix.svg)<!-- PAY-5692 --> Corrigido um problema no qual o **nome e sobrenome do cliente** não foram adicionados ao pedido ao usar os **botões inteligentes para check-out expresso**.

![Correção](../assets/fix.svg)<!-- PAY-5712 --> Resolveu um problema em que os comerciantes **não conseguiam concluir o check-out usando a opção de pagamento Check-out Subtotal Zero** quando o valor total estava livre.

## v2.8.1

_13 de setembro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg)<!-- PAY-5644 --> Corrigiu um problema com o cache de parâmetros SDK ao usar vários escopos em [!DNL Payment Services]. A configuração do SDK agora é armazenada em cache separadamente para cada escopo, em vez de ser armazenada em uma única chave. Isso garante que o cache de cada escopo seja invalidado independentemente, melhorando a confiabilidade ao gerenciar vários escopos.

## v2.8.0

_13 de setembro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services] agora oferece suporte ao envio de informações de número de rastreamento para o PayPal quando um [número de rastreamento é inserido](track-shipment.md) no Adobe Commerce.

![Correção](../assets/fix.svg)<!-- PAY-5626 --> O [!DNL Payment Services] otimizou o processo de solicitação para o registro do comerciante quando os clientes visitam a página de check-out do Commerce. Anteriormente, solicitações separadas eram feitas para cada Método de pagamento (Campos hospedados, Google Pay, Apple Pay e Botões inteligentes). Essa melhoria reduz o número de chamadas, melhorando o desempenho e a eficiência durante o processo de finalização.

![Correção](../assets/fix.svg)<!-- PAY-5645 --> [!DNL Payment Services] agora impede que o pop-up PayPal/Google Pay seja aberto se o comprador não concordar com os termos e condições personalizados criados pelo comerciante na página de check-out.

![Correção](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services] solucionou um problema relacionado ao detalhamento de item de linha do imposto no portal PayPal. Se o custo de envio de um pedido tiver imposto associado a ele, o imposto será incluído como parte do custo de envio, e será visível dessa maneira nos detalhes do item de linha mostrados no portal PayPal.

## v2.7.0

_2 de agosto de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services] agora dá suporte a [dados de item de linha no nível de pedido](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/payment-services/payments-checkout/manage/line-items). Esse recurso permite que os comerciantes vejam informações detalhadas sobre os itens de um pedido, como detalhes do produto, quantidade e preço (incluindo imposto, descontos e outras informações relevantes).

![Novo](../assets/new.svg)<!-- PAY-5380 --> O [!DNL Payment Services] aprimora a [Configuração na experiência de Administrador](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/payment-services/configure/configure-admin#general-configuration) para comerciantes, para um processo de integração mais fácil e intuitivo. Este recurso permite que os comerciantes redefinam suas [!DNL Payment Services] IDs.

![Novo](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services] inclui uma [notificação de falha de pagamento](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails). Esse recurso fornece notificações quase em tempo real de falhas de pagamento aos comerciantes, para que os pedidos possam ser salvos, entrando em contato com o comprador e melhorando potencialmente a resolução do problema.

![Correção](../assets/fix.svg)<!-- PAY-5469 --> Corrigido um problema no qual o **pop-up Pagamento do Google foi bloqueado pelo Safari**. Os compradores agora podem concluir suas transações de pagamento de Google Pay no Safari.

![Correção](../assets/fix.svg)<!-- PAY-5492 --> corrigiu um problema quando um comerciante adicionava termos e condições personalizados à página de check-out. Durante um [check-out expresso](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience), um comprador agora pode aceitar esses termos e condições para concluir o check-out sem problemas.

![Correção](../assets/fix.svg)<!-- PAY-5532 --> funcionalidades aprimoradas de ISPU (Seleção na Loja) com **InstantPurchase**. **Os Métodos de Entrega ISPU** não são mais exibidos quando um comprador faz um pedido com **InstantPurchase**.

![Correção](../assets/fix.svg)<!-- PAY-5606 --> Corrigido um problema no seletor de país **Página de Configuração** que ocorria quando o país do comerciante estava definido como **Alemanha**.

## v2.6.0

_4 de junho de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-4877 --> Agora, o [!DNL Payment Services] oferece suporte aos [recursos de preços L2/L3](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/levels-card-payment-transactions.html). Este recurso só está disponível para [!DNL Payment Services] clientes com preço do IC++ habilitado. Se quiser usar os dados de processamento L2/L3 para [!DNL Payment Services], entre em contato com o gerente de conta do [!DNL Payment Services].

![Correção](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] permite habilitar o Apple Pay diretamente da extensão, sem baixar e hospedar o [arquivo de associação de domínio](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain).

## v2.5.0

_23 de abril de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services] agora oferece suporte às [diretrizes do Adobe Commerce para o `--db-prefix` parâmetro](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) para o Adobe Commerce versões 2.4.7 e mais recentes.

## v2.4.3

_16 de abril de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg)<!-- Issue PAY-5106 --> Corrigido um problema que preenchia incorretamente os totais do valor do pedido durante o check-out entre o PayPal e a Adobe Commerce. Agora, os comerciantes podem garantir que os totais do valor do pedido estejam corretos ao fazer um pedido.

## v2.4.2

_11 de abril, 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- Issue xxx --> Suporte adicionado para o Adobe Commerce 2.4.7.

## v2.4.1

_4 de abril, 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg)<!-- PAY-5322 --> Corrigiu um problema de compatibilidade de PCI com versões mais recentes da Adobe Commerce. Agora, o [!DNL Payment Services] está adaptado aos requisitos de check-out no Adobe Commerce como a opção de pagamento.

![Correção](../assets/fix.svg)<!-- PAY-5323 --> PayLater e Venmo são exibidos corretamente no Adobe Commerce. Correção de um erro que impedia o Administrador de mostrar as opções de alternância PayLater e Venmo.

## v2.4.0

_20 de março de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Os novos](../assets/new.svg)<!-- PAY-4868 --> comerciantes podem [configurar o Google Pay com êxito durante toda a experiência de compra](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=pt-BR), de modo semelhante a outros botões de pagamento em [!DNL Payment Services] por meio do Administrador.

![Novo](../assets/new.svg)<!-- PAY-4381 --> [Os Serviços de Pagamento oferecem suporte ao Google Pay por meio do GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/), permitindo que os comerciantes tenham uma experiência headless Commerce com o método de pagamento Google Pay.

![Novo](../assets/new.svg)<!-- PAY-4878 --> Agora, o recurso de check-out básico do [!DNL Payment Services] é fornecido para comerciantes do Adobe Commerce e do Magento Open Source.O [!DNL Payment Services] agora oferece suporte a comerciantes com empresas em qualquer uma das 200 regiões geográficas do mundo.O check-out básico do [!DNL Payment Services] fornece opções de débito/crédito, PayPal, Venmo (quando disponível) e PayLater (quando disponíveis) em uma integração de autoatendimento.

![Correção](../assets/fix.svg)<!-- PAY-5291 --> O recebimento da confirmação de pagamento para algumas transações pode estar atrasado. Nesse caso, agora os comerciantes podem obter um status de pagamento atualizado para um pedido. [Os serviços de pagamento detectam o status pendente de uma transação de pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/order-payment-status.html) em um pedido, detectando transações pendentes, monitorando proativamente essas transações e atualizando quando o status pendente foi capturado.

## v2.3.4

_1º de março de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5244 --> Corrigido a compatibilidade de check-out assíncrono.

![Correção](../assets/fix.svg)<!-- PAY-5253 --> Corrigido um erro no qual um token de cofre não pertencente a [!DNL Payment Services] não podia ser excluído.

## v2.3.3

_14 de fevereiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5048 --> suporte adicionado para PHP 8.3

![Correção](../assets/fix.svg)<!-- PAY-5048 --> Corrigiu um erro com o sinalizador `is_deleted`. Agora, os pedidos não falham devido ao status `Rejected` enviado da extensão.

## v2.3.2

_26 de janeiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg)<!-- PAY-5183 --> de problemas de desempenho REST/GraphQL corrigidos. Agora, o botão de cartão de crédito é renderizado quando buscado pela API.

## v2.3.1

_7 de dezembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-5047 --> A marca do cartão de crédito/débito ou o tipo de método de pagamento agora está disponível nos seguintes locais:
- a página de pedido do cliente na loja
- o email de confirmação do pedido enviado ao comprador
- na [exibição de detalhes do pedido](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html?lang=pt-BR#view-an-order) no Administrador do Commerce.

## v2.3.0

_1 de dezembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-4381 --> [Os Serviços de Pagamento agora oferecem suporte à integração com o GraphQL](https://developer.adobe.com/commerce/webapi/graphql/payment-services/). Com suporte da GraphQL para botões de pagamento do PayPal, campos hospedados e Apple Pay, o [!DNL Payment Services] agora oferece suporte a uma configuração headless Commerce.

## v2.2.1

_27 de setembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-4870 --> que preenche incorretamente o novo atributo de cabeçalho na loja ao enviar a versão da extensão com a versão mais recente. Anteriormente, com a versão `1.3.0` do Conector de serviços da Commerce, não era possível estender `User-Agent header` da extensão [!DNL Payment Services].

## v2.2.0

_30 de agosto de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- PAY-4638 --> Adição de uma [integração com Signifyd](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security-compliance/fraud-protection.html?lang=pt-BR), que fornece serviços automatizados de proteção contra fraude.

![Novo](../assets/new.svg)<!-- PAY-3981 --> [Promoveu o Apple Pay a uma opção de pagamento separada](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=pt-BR#apple-pay-button), fora dos botões de pagamento do PayPal, para aumentar a visibilidade do comprador da opção de pagamento e permitir que os comerciantes controlem a disposição e o estilo do Apple Pay.

![Novo](../assets/new.svg)<!-- PAY-4002 --> Melhoria na experiência do usuário de check-out de campos de cartão de crédito, incluindo aprimoramentos de estilo, como a adição de ícones de pagamento, para reduzir a carga cognitiva do comprador e aumentar as conversões.

![Nova](../assets/new.svg)<!-- PAY-4002 --> Adicionada funcionalidade para permitir que os comerciantes [classifiquem a ordem de suas opções de pagamento](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=pt-BR#payment-buttons) para priorizar determinadas opções de pagamento. Essa funcionalidade incentiva uma taxa de conversa de check-out mais alta.

![Novos](../assets/new.svg)<!-- PAY-4035 --> Comerciantes agora podem monitorar com eficiência a integridade de suas lojas e identificar problemas de transação usando o novo [Relatório de transações](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/reporting/transactions.html?lang=pt-BR) disponível na home page de Administrador[!DNL Payment Services]. O relatório também apresenta dados sobre taxas de autorização de transações e tendências de transações negativas.

## v2.1.0

_9 de junho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- Issue xxx --> Suporte adicionado para o Adobe Commerce 2.4.7-beta1.

![Novo](../assets/new.svg)<!-- Issue xxx --> Adicionado [disponibilidade nos seguintes países e moedas associadas](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=pt-BR#availability): Austrália, França, Reino Unido.

![Novo](../assets/new.svg)<!-- Issue PAY-4296 --> Adicionado [recursos expandidos para funções de Administrador](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=pt-BR#configure-roles) para garantir que os usuários Administradores possam criar e gerenciar pedidos para clientes e possam visualizar[!DNL Payment Services] no menu Vendas.

![Novo](../assets/new.svg)<!-- Issue PAY-4236 --> Adicionado [anulação automática para pedidos com erros durante o check-out](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/checkout.html?lang=pt-BR#order-auto-voided-if-error).

![Novo](../assets/new.svg)<!-- Issue PAY-4183 --> criou a funcionalidade de [mostrar o botão de opção de pagamento de cartão de crédito/débito](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=pt-BR#debit-or-credit-card-button) na página de check-out.

## v2.0.0

_10 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg)<!-- Issue PAY-4152 --> Suporte adicionado para PHP 8.2 e Adobe Commerce 2.4.6. Não compatível com PHP 7.x.

## v1.6.1

_10 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg)<!-- Issue PAY-4226 --> Corrigido um problema que impedia que novos [!DNL Payment Services] comerciantes usassem o check-out no Administrador.[!DNL Payment Services] estava usando a ID de cliente do Commerce, que não existe para novos clientes.

![Correção](../assets/fix.svg)<!-- Issue PAY-4205 --> Corrigido um problema que fazia com que o estado do endereço de remessa especificado fosse substituído pelo estado nas configurações de imposto padrão durante o check-out usando a [opção PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/payments-options.html?lang=pt-BR#paypal-smart-buttons). Agora, os clientes podem ter seus pedidos entregues em um estado diferente daquele configurado como padrão nas configurações de imposto do comerciante.

![Correção](../assets/fix.svg)<!-- Issue PAY-4202 --> Corrigido um problema que impedia que os clientes usassem o cofre de cartões para concluir uma compra ou excluir um método de pagamento com cofre para uma loja [usando a ação de pagamento `Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html?lang=pt-BR#set-payment-services-as-payment-method). Anteriormente, um erro &quot;ID do Provider Vault não encontrada&quot; aparecia quando o cliente tentava usar ou modificar seus cartões de crédito com cofre.

## v1.6.0

_17 de fevereiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Novo](../assets/new.svg)<!-- Issue PAY-3540 --> Adição do [recurso de conformidade PCI 3DS para comerciantes que fazem transações na União Europeia (UE) e na Grã-Bretanha](security.md#3ds). Esse nível adicional de segurança, que exige que os compradores se autentiquem junto ao emissor do cartão de crédito, ajuda a evitar fraudes on-line e é exigido como parte das regulamentações de conformidade da União Europeia (UE).

![Novo](../assets/new.svg)<!-- Issue PAY-3609 --> Adicionou a capacidade de [habilitar a compartimentação de cartão no Administrador](vaulting.md#use-vaulting-in-the-admin). Isso permite que os comerciantes criem um pedido para clientes no Administrador usando seus métodos de pagamento com cofre.

## v1.5.4

_29 de janeiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-4110 --> que impedia os compradores de fazer um pedido usando botões de pagamento na página do produto, minicarrinho e carrinho. Os compradores agora podem concluir os pedidos com sucesso.

## v1.5.3

_25 de janeiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-4102 --> Liberou uma correção para um problema conhecido incompatível com versões anteriores. Esta versão bloqueia a versão da extensão de ID de serviço para a versão estável mais recente, o que habilita novamente as novas instalações do [!DNL Payment Services] para configurar os Serviços Commerce.

## v1.5.2

_22 de dezembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3992 --> Faturamento aprimorado em [!DNL Payment Services] quando um método de pagamento é recusado.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] agora exibe corretamente os botões de pagamento do PayPal para comerciantes que usam o modelo personalizado [Acionar Check-out](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} para a página de check-out. Anteriormente, a minicart exibia intermitentemente os botões.

## v1.5.1

_23 de novembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Novo](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] agora inclui o número da versão no cabeçalho do agente do usuário para que as solicitações possam rastrear, filtrar ou descontinuar pontos de extremidade não utilizados.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] agora exibe corretamente os dados do pedido quando um pedido é feito a partir da página do produto usando botões de pagamento.

## v1.5.0

_18 de novembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Novo](../assets/new.svg)<!-- Issue PAY-3880 --> Agora um comprador pode [guardar (salvar) suas informações de cartão de crédito durante o check-out](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html?lang=pt-BR) para usar em uma compra posterior para a mesma loja ou outra na mesma conta de comerciante.

Os ![Novos](../assets/new.svg)<!-- Issue PAY-3950 --> Comerciantes agora podem habilitar o [recurso Commerce de Compra Instantânea](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html?lang=pt-BR) para suas lojas para que os compradores possam (usar [informações de cartão de crédito com cofre](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/payments-checkout/vaulting.html?lang=pt-BR)) agilizar o check-out.

## v1.4.1

_14 de outubro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Correção](../assets/fix.svg)<!-- Issue PAY-3766 --> Quando o método de pagamento de um cliente é recusado, a mensagem de erro visível é mais descritiva. Ele aconselha o cliente a inserir novamente as informações de pagamento e tentar novamente, tentar outro método de pagamento ou entrar em contato com o banco sobre a transação recusada.

## v1.4.0

_30 de setembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Novo](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] agora inclui a capacidade de configurar uma conta comercial para [usar várias contas comerciais do PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=pt-BR#use-multiple-paypal-accounts). Isso permite que o comerciante opere suas lojas em vários países usando moedas diferentes ou use o Adobe Commerce para uma parte da sua empresa.

![Os novos](../assets/new.svg)<!-- Issue PAY-3231 --> comerciantes podem [adicionar um [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=pt-BR#add-soft-descriptor) à configuração de sites ou exibições de loja individuais que são mostradas nos extratos bancários de transações do cliente para definir marcas, lojas ou linhas de produtos.

![Novo](../assets/new.svg)<!-- Issue PAY-3707 --> [Habilite ou desabilite campos de cartão de crédito e botões de pagamento do PayPal](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/configure/settings.html?lang=pt-BR#configure-payment-options) para check-out nas configurações[!DNL Payment Services].

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3546 --> Quando um cliente clica em **[!UICONTROL Edit cart]**, a página redireciona para a página do carrinho e mostra os itens atualizados em vez de mostrar um carrinho vazio.

## v1.3.1

_6 de setembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3663 --> Agora, quando o armazenamento de um comerciante está capturando uma ordem autorizada com uma moeda não global, o processo de captura é concluído e nenhum erro é exibido.

## v1.3.0

_9 de agosto de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Nova](../assets/new.svg)<!-- Issue PAY-XX --> A versão de disponibilidade geral—[!DNL Payment Services] agora é [compatível com [!DNL Adobe Commerce] e [!DNL Magento Open Source] versões 2.4.0 a 2.4.5](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/product-availability).

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-x --> O Apple Pay agora é compatível com o navegador Safari v15.5 em dispositivos móveis e desktop.

## v1.2.0

_29 de junho de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-x --> O Apple Pay é incompatível com o navegador Safari v15.5 no dispositivo móvel e no desktop. Ao usar o Safari versão 15.5, não é possível concluir o check-out com o Apple Pay.

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-3264 --> anteriormente, quando um usuário conectado selecionava um endereço de cobrança/remessa diferente do endereço padrão para sua conta, o check-out falhava. Agora, o endereço de cobrança/entrega selecionado é enviado (em vez do endereço salvo padrão) e o check-out é concluído com êxito.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3314 --> Se você desativar os botões de pagamento do PayPal para check-out, nenhum erro será exibido.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-3330 --> Os pagamentos não falham mais durante o check-out quando um usuário convidado insere um número de telefone que inclui traços.

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> Quando as credenciais do Commerce Services são inválidas,[!DNL Payment Services] agora o alerta exibindo um erro de credenciais na Página Inicial do [!DNL Payment Services] no Administrador.

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] é incompatível com `commerce-data-export` v101.20 e superior, o que o torna incompatível com a [[!DNL Channel manager] extensão](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html?lang=pt-BR).

## v1.1.0

_31 de março de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Nova](../assets/new.svg)<!-- Issue PAY-2127 --> A versão de disponibilidade geral—[!DNL Payment Services] agora é [compatível com [!DNL Adobe Commerce] e [!DNL Magento Open Source] versões 2.4.0 a 2.4.4](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/product-availability).

![Novo](../assets/new.svg)<!-- Issue PAY-2682 --> A extensão [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source] agora está disponível para comerciantes canadenses. Os comerciantes podem exibir a configuração de pagamentos em [francês](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) ou [inglês](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/overview.html?lang=pt-BR#accepted-credit-cards-and-currencies).

![Novo](../assets/new.svg)<!-- Issue PAY-2681 --> O [!DNL Payment Services] oferece suporte a [Dólares canadenses (CAD)](introduction.md#accepted-credit-cards-and-currencies) para cartões de crédito e transações no PayPal.

![Os novos](../assets/new.svg)<!-- Issue PAY-2680 --> comerciantes podem [integrar [!DNL Payment Services]](onboard.md) a extensão em inglês ou francês.

![Novos](../assets/new.svg)<!-- Issue PAY-2678 --> Comerciantes agora podem exibir relatórios financeiros, tanto o [Status do pagamento do pedido](order-payment-status.md) quanto os [Relatórios de pagamentos](payouts.md), em dólares canadenses (CAD).

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] agora é compatível com o [PHP 8.1](https://www.php.net/releases/8.1/en.php).

![Correção de um problema](../assets/fix.svg)<!-- Issue PAY-3017 --> Alerta de modo de sandbox aprimorado para exibir alertas adequados com vários armazenamentos.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-2742 --> Agora é possível habilitar e desabilitar os métodos de pagamento disponíveis, como Venmo, no nível de exibição da loja. Anteriormente, só era possível configurar métodos de pagamento por site.

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-2277 --> Agora é possível [habilitar ou desabilitar botões de pagamento individuais do PayPal](configure-admin.md#payment-buttons).

![Problema corrigido](../assets/fix.svg)<!-- Issue PAY-2561 --> Os produtos removidos anteriormente não aparecem no carrinho na página _Pedido de revisão_.

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-2842 --> Transações de cartão de crédito de teste [podem falhar com PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=pt-BR) ao processar pagamentos em um ambiente de sandbox.

## v1.0.0

_29 de novembro de 2021_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.0 e mais recentes

![Nova](../assets/new.svg)<!-- Issue PAY-2127 --> A versão de disponibilidade geral—[[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) agora é compatível com [!DNL Adobe Commerce] e [!DNL Magento Open Source] versões 2.4.0 a 2.4.3-p1.

![Novo](../assets/new.svg)<!-- Issue PAY-124 --> A extensão [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source] pode ser instalada para [[!DNL Adobe Commerce] instâncias da infraestrutura de nuvem](install.md#adobe-commerce-on-cloud-infrastructure) ou [Locais](install.md#on-premises). Esses métodos exigem o uso de uma interface de linha de comando.

![Novo](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] dá suporte a uma [conta de sandbox](sandbox.md) que permite aos comerciantes avaliar a extensão no modo de teste.

![Os novos](../assets/new.svg)<!-- Issue PAY-666 --> comerciantes podem [configurar a extensão Serviços de Pagamento](configure-admin.md) com comportamentos de pagamento básicos, como a utilização da [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) alternando entre ambientes de sandbox ou de produção.

![Novo](../assets/new.svg)<!-- Issue PAY-780 --> seus compradores podem fazer check-out com [!DNL Payment Services] ou através de [criação manual de pedido](create-order.md).

![Novos](../assets/new.svg)<!-- Issue PAY-1856 --> Relatórios abrangentes, via [Status do pagamento da ordem](order-payment-status.md) e [Relatórios de pagamentos](payouts.md), estão disponíveis para [!DNL Payment Services] para fornecer uma visão clara dos pedidos da sua loja e pagamentos relacionados.

![Novo](../assets/new.svg)<!-- Issue PAY-311 --> O [!DNL Payment Services] oferece suporte para preços hierárquicos flexíveis, com base no volume total de processamento, adaptado a qualquer comerciante.

![Novo](../assets/new.svg)<!-- Issue PAY-1443 --> Você pode [personalizar facilmente a aparência](payments-options.md) dos botões de pagamento e campos de cartão de crédito do PayPal para a extensão [!DNL Payment Services].

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-2473 --> O uso de [chaves do Composer incorretas](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=pt-BR) durante a instalação da extensão impede que o usuário [autentique](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) com o `MAGEID` correto.

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] relatórios [podem não sincronizar imediatamente](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html?lang=pt-BR).

![Problema conhecido](../assets/bug.svg)<!-- Issue PAY-2475 --> Sua [conta de sandbox do PayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html?lang=pt-BR) para [!DNL Payment Services] não pode ser verificada se você criar essa conta durante a integração.
