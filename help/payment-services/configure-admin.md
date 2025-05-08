---
title: Configuração de serviços de pagamento herdados
description: Após a instalação, você pode configurar [!DNL Payment Services] no Administrador na configuração da loja.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 51b3f5fffda1402d25bb57402eae82afc8515a14
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# Configuração [!DNL Payment Services] herdada

Você pode personalizar o [!DNL Payment Services] de acordo com suas necessidades com opções de configuração úteis no Administrador.

Ao configurar [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source] no Administrador, essas configurações se aplicam apenas ao ambiente definido no campo _[!UICONTROL Method]_&#x200B;de&#x200B;_[!UICONTROL General Configuration]_. Quaisquer alterações feitas nos campos de configuração são independentes da alternância da seleção _[!UICONTROL Method]_. Se você alternar o método, suas seleções não serão redefinidas.

## Configuração geral

Você pode habilitar [!DNL Payment Services] para sua loja e _[!UICONTROL Merchant Location]_&#x200B;e habilitar testes de sandbox ou pagamentos ao vivo na seção&#x200B;_[!UICONTROL General Configuration]_.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Defina o campo _[!UICONTROL Merchant Country]_&#x200B;no&#x200B;_[!UICONTROL Merchant Location]_. Se um _[!UICONTROL Merchant Country]_&#x200B;não for especificado, o&#x200B;_[!UICONTROL Default Country]_ da configuração geral será usado.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;para acessar a seção&#x200B;_[!UICONTROL [!DNL Payment Services]]_.
1. Na seção _[!UICONTROL [!DNL Payment Services]]_, expanda a seção&#x200B;_[!UICONTROL General Configuration]_.
1. Para **Habilitar**, defina-o como `Yes` para habilitar [!DNL Payment Services] para seu armazenamento.
1. Para o **Método**, defina-o como `Sandbox` se você ainda estiver testando o [!DNL Payment Services] para sua loja ou `Production` se você estiver pronto para habilitar pagamentos ao vivo.
1. Os valores **[!UICONTROL Payment Services Sandbox ID]** e **[!UICONTROL Payment Services Production ID]** são preenchidos automaticamente depois que você configura o [Commerce Services Connector](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} e visita o painel [!DNL Payment Services] pela primeira vez. Faça isso para concluir a integração dos ambientes de sandbox e/ou produção. Esses valores associam sua SaaS ID a [!DNL Payment Services].

   >[!WARNING]
   >
   > Se precisar alterar a ID do espaço de dados no Commerce Services Connector, redefina a ID do [!DNL Payment Services]. Clique em **Redefinir ID de Serviços de Pagamento** para redefinir suas IDs de Sandbox ou Produção. Se você redefinir suas [!DNL Payment Services] IDs, será necessário integrar novamente.

1. Seus valores de **[!UICONTROL PayPal Merchant ID]** e **[!UICONTROL PayPal Merchant Status]** são fornecidos automaticamente pelo PayPal assim que você visita o painel [!DNL Payment Services] pela primeira vez.
1. Para o **Descritor Flexível** (valores personalizados que são exibidos em demonstrativos bancários de transações do cliente para definir entre lojas/marcas/catálogos), adicione seu texto personalizado (até 22 caracteres) ao campo de texto, substituindo `Soft descriptor` ou o valor existente.
1. Clique em **[!UICONTROL Save Config]** para salvar suas alterações.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

![Exibição da Solução Adobe em Destaque](assets/config-view-all.png){width="700" zoomable="yes"}

### Opções de configuração

| Campo | Escopo | Descrição |
|---|---|---|
| [!UICONTROL Enable] | site | Habilite ou desabilite o [!DNL Payment Services] para o seu site. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | exibição de loja | Defina o método ou ambiente para sua loja. Opções: [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | exibição de loja | Sua ID de comerciante de sandbox, que é gerada automaticamente durante a integração da sandbox. |
| [!UICONTROL Payment Services Production ID] | exibição de loja | Sua ID de comerciante de produção, que é gerada automaticamente durante a integração da produção (ao vivo). |
| [!UICONTROL PayPal Merchant ID] | exibição de loja | Sua ID exclusiva de conta de comerciante do PayPal, gerada ao criar sua conta do PayPal. |
| [!UICONTROL PayPal Merchant Status] | exibição de loja | Status da ID de Comerciante do PayPal. |
| [!UICONTROL Soft Descriptor] | exibição de site ou loja | Adicione um descritor simples ao(s) site(s) e às visualizações da loja para adicionar informações às transações do cliente que definem marcas, lojas ou linhas de produtos. |

## [!UICONTROL Credit Card Fields]

As opções de pagamento do [!UICONTROL Credit Card Fields] oferecem check-out simples e seguro para métodos de pagamento com cartão de crédito ou débito.

Consulte [Opções de pagamentos](payments-options.md#paypal-smart-buttons) para obter mais informações.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Na seção _[!UICONTROL Payment Services]_, expanda a seção&#x200B;_[!UICONTROL Credit Card Fields]_.
1. Para **[!UICONTROL Title]**, insira texto (se necessário) para alterar o nome do método de pagamento conforme mostrado durante o check-out.
1. Para [definir a ação de pagamento](production.md#set-payment-services-as-payment-method), selecione **[!UICONTROL Authorize]** ou **Autorizar e Capturar**.
1. Para priorizar um método de pagamento na página de check-out, forneça um valor `Numeric Only` no campo **[!UICONTROL Sort order]**.
1. Para **[!UICONTROL Show on checkout page]**, escolha `Yes` para habilitar campos de cartão de crédito na página de check-out.
1. Para **[!UICONTROL Vault Enabled]**, escolha `Yes` para habilitar a compartimentalização de cartão de crédito para check-out.
1. Para **[!UICONTROL Vault Enabled in Admin]**, escolha `Yes` para permitir que o comerciante crie pedidos para clientes usando seu cartão de crédito com cofre.
1. Para habilitar **[!UICONTROL 3D Secure authentication]** (`Off` por padrão), escolha `Always` ou `When required`.
1. Para **[!UICONTROL Debug Mode]**, escolha `Yes` para habilitar o modo de depuração ou `No` para desabilitá-lo.
1. Clique em **[!UICONTROL Save Config]** para salvar suas alterações.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

### Opções de configuração

| Campo | Escopo | Descrição |
|---|---|---|
| [!UICONTROL Title] | exibição de loja | Adicione o texto a ser exibido como o título para esta opção de pagamento na exibição de Método de Pagamento durante a finalização da compra. Opções: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site | A [ação de pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=pt-BR) para o método de pagamento especificado. Opções: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | exibição de loja | A ordem de classificação do método de pagamento especificado na página de check-out. Valor `Numeric Only` |
| [!UICONTROL Show on checkout page] | site | Ative ou desative os campos de cartão de crédito na página de check-out. Opções: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | exibição de loja | Habilite ou desabilite o [cofre de cartão de crédito](vaulting.md). Opções: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | exibição de loja | Habilite ou desabilite o recurso para [comerciante concluir pedidos de clientes no Administrador](vaulting.md) usando um método de pagamento com cofre. Opções: [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | site | Habilite ou desabilite a [autenticação Segura do 3DS](security.md#3ds). Opções: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | site | Ative ou desative o Modo de depuração. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Apple Pay]

A opção de pagamento [!UICONTROL Apple Pay] permite que o comerciante ofereça o Apple Pay aos seus compradores, que podem usar o Touch ID em seus dispositivos para fazer compras no navegador Safari. Os comerciantes podem adicionar até 99 domínios por conta de comerciante.

Consulte [Opções de pagamentos](payments-options.md#apple-pay-button) para obter mais informações.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Na seção _[!UICONTROL Payment Services]_, expanda a seção&#x200B;_[!UICONTROL Apple Pay]_.
1. Para **[!UICONTROL Title]**, insira texto (se necessário) para alterar o nome do método de pagamento conforme mostrado durante o check-out.
1. Para [definir a ação de pagamento](production.md#set-payment-services-as-payment-method), selecione **[!UICONTROL Authorize]** ou **[!UICONTROL Authorize and Capture]**.
1. Especifique onde a opção [!DNL Apple Pay] está habilitada no Adobe Commerce selecionando `Yes` nas seguintes opções, conforme necessário:
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. Para habilitar o modo de depuração, selecione `Yes` para **[!UICONTROL Debug Mode]** (`No` o desabilita).
1. Para salvar as alterações, clique em **[!UICONTROL Save Config]**.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

### Opções de configuração

| Campo | Escopo | Descrição |
|---|---|---|
| [!UICONTROL Title] | exibição de loja | Adicione o texto a ser exibido como o título para esta opção de pagamento na exibição de Método de Pagamento durante a finalização da compra. Opções: [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site | A [ação de pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=pt-BR) para o método de pagamento especificado. Opções: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | site | Habilite ou desabilite [!DNL Apple Pay] na página de check-out. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | exibição de loja | A ordem de classificação do método de pagamento especificado na página de finalização da compra. Valor `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | exibição de loja | Habilite ou desabilite [!DNL Apple Pay] na página de detalhes do produto. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | exibição de loja | Habilite ou desabilite [!DNL Apple Pay] na visualização do minicarrinho. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | exibição de loja | Habilite ou desabilite o [!DNL Apple Pay] na página do carrinho. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | site | Ative ou desative o Modo de depuração. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

A opção de pagamento [!UICONTROL Google Pay] permite que o comerciante ofereça o Google Pay aos seus compradores, que podem usar a Carteira do Google em seus dispositivos para fazer compras.

Consulte [Opções de pagamentos](payments-options.md#google-pay-button) para obter mais informações.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Na seção _[!UICONTROL Payment Services]_, expanda a seção&#x200B;_[!UICONTROL Google Pay]_.
1. (Opcional) Altere o nome do método de pagamento mostrado durante o check-out inserindo o novo nome no campo **[!UICONTROL Title]**.
1. [Defina a ação de pagamento](production.md#set-payment-services-as-payment-method) selecionando **[!UICONTROL Authorize]** ou **[!UICONTROL Authorize and Capture]**.
1. Especifique onde a opção [!DNL Google Pay] está habilitada no Adobe Commerce selecionando `Yes` nas seguintes opções, conforme necessário:
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. Para habilitar **[!UICONTROL 3D Secure authentication]** (`Off` por padrão), escolha `Always` ou `When required`.
1. Para habilitar o modo de depuração, selecione `Yes` para **[!UICONTROL Debug Mode]** (`No` o desabilita).
1. Configure a aparência do botão _[!UICONTROL Google Pay]_&#x200B;selecionando **[!UICONTROL Button Color]**,**[!UICONTROL Button Type]**&#x200B;e **[!UICONTROL Button Style]**&#x200B;conforme necessário.
1. Para definir a altura, usa o valor padrão para a altura definida em **[!UICONTROL Button Style]**.
1. Para salvar as alterações, clique em **[!UICONTROL Save Config]**.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

### Opções de configuração

| Campo | Escopo | Descrição |
|---|---|---|
| [!UICONTROL Title] | exibição de loja | Especifica o rótulo de texto que é exibido para esta opção de pagamento na exibição de Método de Pagamento durante o check-out. Opções: `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | site | A [ação de pagamento](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=pt-BR) para o método de pagamento especificado. Opções: `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | site | Habilite ou desabilite [!DNL Google Pay] na página de check-out. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | exibição de loja | A ordem de classificação do método de pagamento especificado na página de finalização da compra. Valor `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | exibição de loja | Habilite ou desabilite [!DNL Google Pay] na página de detalhes do produto. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | exibição de loja | Habilite ou desabilite [!DNL Google Pay] na visualização do minicarrinho. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | exibição de loja | Habilite ou desabilite [!DNL Google Pay] na página do carrinho. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | exibição de loja | Habilite ou desabilite a [autenticação Segura 3D](security.md#3ds). Opções: [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | site | Ative ou desative o Modo de depuração. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | Exibição da loja | Defina a cor do botão [!DNL Google Pay]. Opções: `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | Exibição da loja | Defina o tipo do botão [!DNL Google Pay]. Opções: `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

Consulte a documentação das [opções de objeto da solicitação de API de Pagamento do Google](https://developers.google.com/pay/api/web/reference/request-objects) para obter mais informações.

## [!DNL PayPal Payment Buttons]

As opções de pagamento do [!DNL PayPal payment buttons] oferecem ao seu cliente um processo de finalização simples, rápido e seguro.

Consulte [Opções de pagamentos](payments-options.md#paypal-smart-buttons) para obter mais informações.

Configurar [!DNL PayPal payment buttons]

Você pode ativar e configurar as opções de pagamento dos botões de pagamento do PayPal em Admin:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Na seção _[!UICONTROL Payment Services]_, expanda a seção&#x200B;_[!UICONTROL PayPal payment buttons]_.
1. Para alterar o nome do método de pagamento conforme mostrado durante o check-out, edite o campo _[!UICONTROL Title]_.
1. Para [definir a ação de pagamento](production.md#set-payment-services-as-payment-method), selecione **[!UICONTROL Authorize]** ou **[!UICONTROL Authorize and Capture]**.
1. Para priorizar um método de pagamento na página de check-out, forneça um valor `Numeric Only` no campo **[!UICONTROL Sort order]**.
1. Para habilitar/desabilitar as [mensagens de Pagamento Posterior](payments-options.md#pay-later-button), selecione `Yes`/`No` para **[!UICONTROL Display Pay Later Message]**.
1. Especifique onde os botões de pagamento do PayPal são habilitados no Adobe Commerce selecionando `Yes` nas seguintes opções, conforme necessário:
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Para habilitar Venmo como uma opção de pagamento, selecione `Yes` para **[!UICONTROL Venmo Enabled]**.
1. Para habilitar cartões de crédito e débito como opção de pagamento (botão Inteligente do PayPal), selecione `Yes` para **[!UICONTROL Credit and Debit Card Enabled]**.
1. Para habilitar/desabilitar a opção de pagamento [Pagar Mais Tarde](payments-options.md#pay-later-button) do PayPal, selecione `Yes`/`No` para **[!UICONTROL PayPal Pay Later Enabled]**.
1. Para habilitar o modo de depuração, selecione `Yes` para **[!UICONTROL Debug Mode]** (`No` o desabilita).
1. Para salvar as alterações, clique em **[!UICONTROL Save Config]**.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

### Opções de configuração

| Campo | Escopo | Descrição |
|---|---|---|
| [!UICONTROL Title] | exibição de loja | Adicione o texto a ser exibido como o título para esta opção de pagamento na exibição de Método de Pagamento durante a finalização da compra. Opções: campo de texto |
| [!UICONTROL Payment Action] | site | A [ação de pagamento](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} para o método de pagamento especificado. Opções: [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | site | Ative ou desative a mensagem Pagar mais tarde no carrinho de compras, página do produto, minicarrinho e durante o fluxo de finalização. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on checkout page] | exibição de loja | Habilite ou desabilite [!DNL PayPal payment buttons] na página de check-out. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | exibição de loja | Habilite ou desabilite [!DNL PayPal payment buttons] na página de detalhes do produto. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | exibição de loja | Habilite ou desabilite [!DNL PayPal payment buttons] na visualização do minicarrinho. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | exibição de loja | Habilite ou desabilite o [!DNL PayPal payment buttons] na página do carrinho. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | exibição de loja | Habilite ou desabilite a opção de pagamento Venmo onde os botões de pagamento são exibidos. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | exibição de loja | Ative ou desative as opções de cartão de Crédito e Débito onde os botões de pagamento são exibidos. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | exibição de loja | Ativar ou desativar a aparência da opção de pagamento PayPal Pay Posteriormente, onde os botões de pagamento são exibidos. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | site | Ative ou desative o Modo de depuração. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Estilo do botão

Você também pode configurar as opções _[!UICONTROL Button style]_&#x200B;dos botões de pagamento:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. No painel esquerdo, expanda **[!UICONTROL Sales]** e escolha **[!UICONTROL Payment Methods]**.
1. Expanda a seção _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Na seção _[!UICONTROL [!DNL Payment Services]]_, expanda a seção&#x200B;_[!UICONTROL PayPal Smart Button Styling]_.
1. Para definir o layout, selecione `Vertical` ou `Horizontal` para **[!UICONTROL Layout]**
1. Para definir a cor, selecione uma das cores disponíveis em **[!UICONTROL Color]**.
1. Para definir a forma, selecione `Rectangular` ou `Pill` para **[!UICONTROL Shape]**.
1. Para usar a altura padrão, selecione `Yes` ou `No` para **[!UICONTROL Use Default Height]**.
1. Para definir a altura personalizada, adicione a altura de pixel desejada para **[!UICONTROL Height]**.
1. Para definir o slogan, selecione `Yes` ou `No` para **[!UICONTROL Tagline]**.
1. Para salvar as alterações, clique em **[!UICONTROL Save Config]**.
1. Navegue até **[!UICONTROL System]** > **[!UICONTROL Cache Management]** e clique em **[!UICONTROL Flush Cache]** para atualizar todos os caches inválidos.

Você também pode configurar o estilo do botão de pagamento [em Configurações](settings.md#button-style) da Página Inicial dos Serviços de Pagamento.

### Opções de configuração

| Campo | Escopo | Descrição |
|--- |--- |--- |
| [!UICONTROL Layout] | Exibição da loja | Definir estilo de layout para botões de pagamento Paypal. Opções: `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | Exibição da loja | Defina a cor dos botões de pagamento do Paypal. Opções: [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | Exibição da loja | Defina a forma dos botões de pagamento Paypal. Opções: `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | Exibição da loja | Define se os botões de pagamento do PayPal usam uma altura padrão. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | Exibição da loja | Defina a altura dos botões de pagamento do PayPal. Valor padrão: nenhum |
| [!UICONTROL Label] | Exibição da loja | Defina o rótulo que aparece nos botões de pagamento do PayPal. Opções: `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | Exibição da loja | Ativa o slogan. Opções: `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Liberar o cache

Se você alterar a configuração, [limpe manualmente o cache](/help/payment-services/settings.md#flush-the-cache) para que o armazenamento mostre as definições de configuração mais recentes.
