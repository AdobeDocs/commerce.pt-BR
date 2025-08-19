---
title: Habilitar [!DNL Payment Services] para produção
description: Conclua o processo de integração habilitando  [!DNL Payment Services]  para produção.
exl-id: 3b1269e8-127b-47f8-9738-9722a5737c63
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Habilitar [!DNL Payment Services] para produção

Você pode colocar o serviço em produção e concluir o [processo de integração](onboard.md), de acordo com as etapas deste tópico, após:

* [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} [Instalar](install.md) a extensão de Serviços de Pagamento
* [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} [Configurar e conectar](connect.md) sua instância
* [Configurar](sandbox.md) e [testar](test-validate.md) sua sandbox

## Definir [!DNL Payment Services] como método de pagamento

Depois de [configurar seus Serviços Commerce](connect.md#configure-commerce-services) e habilitar o [teste de sandbox](sandbox.md#enable-sandbox-testing) ou os [pagamentos ao vivo](#enable-live-payments), você deverá definir [!DNL Payment Services] como seu método de pagamento.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clique em **[!UICONTROL Enable Payment Services]**.

   Esta opção estará visível se você ainda não tiver configurado o [!DNL Payment Services] como o método de pagamento para um ou mais sites.

   Você é direcionado para a área de configurações na exibição Página Inicial com as opções relevantes expandidas (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_), onde é possível habilitar as opções [!DNL Payment Services] como seu [método de pagamento](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}.

1. Em _[!UICONTROL General Configuration]_, defina **[!UICONTROL Enable]**&#x200B;como `Yes`.
1. Defina **[!UICONTROL Payment Action]**, para _[!UICONTROL Credit Card Fields]_&#x200B;e_[!UICONTROL PayPal payment buttons]_, para um dos seguintes:

   | Configuração | Descrição |
   |---|---|
   | `Authorize` | Aprova a compra e suspende os fundos. A quantidade não é retirada até que seja &quot;capturada&quot; pelo comerciante. |
   | `Authorize and Capture` | Aprova a compra e o comerciante &quot;captura&quot; os fundos. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] dá suporte a capturas parciais. Um comerciante pode capturar parcialmente (faturar) partes de um pedido. Por exemplo, você pode capturar cada item individualmente ou um item agora e o restante posteriormente.

1. Clique em **[!UICONTROL Save]**.
1. Clique em **[!UICONTROL Go to Payment Services]** para ser direcionado de volta à Página Inicial de [!DNL Payment Services].
1. [Limpar o cache](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html).

   A limpeza deve ser feita após cada alteração de configuração.

Consulte [Configurar [!DNL Payment Services]](configure-admin.md) para obter mais informações sobre como configurar Campos de Cartão de Crédito e botões de pagamento do PayPal.

## Integração completa do comerciante

A próxima etapa para permitir que suas lojas entrem em operação com os Serviços de pagamento é concluir a integração ao vivo.

Os Serviços de Pagamento fornecem opções de pagamento [**Avançado** (com suporte total) e **Padrão** (Check-out Expresso)](../payment-services/payments-options.md#standard-vs-advanced-payments-experience) e fluxos de integração, dependendo do país em que você opera e da sua experiência de pagamento preferida.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clique em **[!UICONTROL Live onboarding]**.

   Esta opção estará visível se você ainda não tiver concluído a integração ao vivo do [!DNL Payment Services].

1. No modal _Selecione seu país_, selecione o país do qual você está operando.

   Atualmente, os Serviços de Pagamento oferecem suporte total para todas as opções de pagamento em [cinco países](../payment-services/introduction.md#availability). Os Serviços de pagamento fornecem recursos de Finalização expressa (um subconjunto de opções de pagamento) para todos os outros países representados na lista de países.

   O país que você escolher na lista determinará as opções de pagamento, e o fluxo de integração—[Avançado](#advanced-onboarding) (com suporte total) ou [Padrão](#standard-onboarding) (Check-out Expresso) — disponível para você.

>[!TIP]
>
> Depois de escolher e continuar com uma opção de integração — Padrão ou Avançada — você deve concluir novamente a integração para atualizar ou fazer downgrade a partir da sua seleção inicial.

### Integração avançada

Este fluxo de integração está disponível para comerciantes em [países com suporte total](../payment-services/introduction.md#availability).

Depois que o país for selecionado:

1. Na modal exibida, selecione **Avançado**.

   Para a opção **Padrão**, prossiga para o [Fluxo de integração padrão](#standard-onboarding).

1. Clique em **Continuar**.
1. Continue com o fluxo do PayPal para obter a integração avançada totalmente compatível, usando suas credenciais de conta do PayPal (não suas credenciais de conta de sandbox) _ou_ cadastre-se para obter uma nova conta do PayPal.

>[!IMPORTANT]
>
>A **integração avançada** requer que os comerciantes [solicitem o direito aos pagamentos](#request-payments-entitlement-from-adobe) para habilitar a integração ao vivo.

### Integração padrão

Este fluxo de integração Padrão está disponível para comerciantes nos países disponíveis para os quais [somente o suporte para Finalização Expressa](../payment-services/introduction.md#availability) é fornecido.

Depois que o país for selecionado:

1. Na modalidade do _contrato de Serviços de Pagamento_ exibida, clique no link do **contrato de Serviços de Pagamento** para exibir o contrato de Serviços de Pagamento da Adobe Commerce.
1. No modal do _contrato de Serviços de Pagamento_, clique em **Aceito**.
1. Continue com o fluxo do PayPal para a integração do Check-out expresso, usando suas credenciais de conta do PayPal (não suas credenciais de conta de sandbox) ou cadastre-se para obter uma nova conta do PayPal.

>[!IMPORTANT]
>
>[Os campos de pagamento e cartão de crédito do Apple](../payment-services/payments-options.md) não estão disponíveis para a **Integração padrão**.

## Confirmar endereço de email

1. Na barra lateral Admin, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   O botão _[!UICONTROL Live onboarding]_&#x200B;não está mais visível e você vê uma caixa de texto &quot;[!UICONTROL Live payments pending]&quot;.

   Nessa caixa de texto, também pode ser solicitado que você confirme seu endereço de email no PayPal para concluir a integração.

1. Se for solicitado que você confirme seu endereço de email, verifique se o email contém a mensagem de confirmação enviada pelo PayPal e clique em para confirmar seu endereço de email.
1. Na barra lateral Admin, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Atualize a janela do navegador.

   Quando a integração do comerciante do PayPal for aprovada, você deverá ver uma notificação informando que o sistema de pagamento está no modo sandbox e não está processando pagamentos em tempo real.

   >[!IMPORTANT]
   >
   >Se você revogar o consentimento de [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source] para o processamento de seus pagamentos (nas configurações de sua conta do PayPal), os pedidos em seu armazenamento não poderão ser processados por [!DNL Payment Services]. Na Página Inicial dos Serviços de Pagamento, será exibido um alerta sobre o consentimento revogado.

## Solicitar direitos de pagamentos do Adobe

Para permitir que suas lojas sejam ativadas, solicite direitos de pagamentos à Adobe (somente para [Integração avançada](#advanced-onboarding)):

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clique em **[!UICONTROL Get Live Payments]** na sua Página Inicial do [!DNL Payment Services].

   ![Solicitar direitos](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Complete o formulário.
1. Um membro da equipe de vendas entrará em contato com você.

Como alternativa, você pode solicitar direitos de pagamento da Adobe em [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>A **Integração em tempo real** só estará acessível depois que o direito aos pagamentos for aprovado.

## Configurar camada de preços

Obtenha sua [!DNL Payment Services] _ID do Comerciante_:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Na exibição Início, clique em **[!UICONTROL Settings]**. Consulte [Página inicial](payments-home.md) para obter mais informações.
1. Selecione a _ID do Comerciante_ necessária e envie-a para seu Representante de vendas, que configurará a camada de preços correta.

Consulte [Processamento de Nível 2 e Nível 3](levels-card-payment-transactions.md) para obter mais informações sobre transações de pagamento.

## Habilitar pagamentos ao vivo

Uma _ID de comerciante de produção_ é gerada automaticamente e preenchida na [configuração](configure-admin.md). Não altere ou altere esta ID.

Ativar pagamentos em tempo real:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Na Página Inicial, clique em **[!UICONTROL Settings]** na parte superior direita da página. Consulte [Página inicial](payments-home.md) para obter mais informações.
1. Na seção _[!UICONTROL General Configuration]_, defina **[!UICONTROL Payment mode]**&#x200B;como `Production`.
1. Clique em **[!UICONTROL Save]**.
1. [Limpar o cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management){target="_blank"}.

   >[!IMPORTANT]
   >
   >Se você não limpar o cache, os clientes não poderão ver as opções de pagamento do PayPal durante o check-out.

Se você navegar de volta para a Página Inicial do [!DNL Payment Services], a mensagem Modo de pagamento de sandbox não será mais exibida porque você está processando pagamentos em tempo real.

Consulte [Configurar no Admin](configure-admin.md) para ver as opções de configuração herdadas.

>[!IMPORTANT]
>
>Se você revogar o consentimento de [!DNL Payment Services] para o processamento de seus pagamentos (nas configurações de sua conta do PayPal), os pedidos em seu armazenamento não poderão ser processados por [!DNL Payment Services]. Se quiser reativar o processamento do pagamento, conclua a integração novamente. Na Página Inicial dos Serviços de Pagamento, será exibido um alerta sobre o consentimento revogado.

## Teste em produção

É altamente recomendável testar Pagamentos em produção, com cartões de crédito e bancos reais, antes de expor essa funcionalidade aos compradores.

Consulte [Testar e validar](test-validate.md) para obter mais informações.
