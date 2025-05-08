---
title: Configurar o teste de sandbox
description: Use uma conta de sandbox do PayPal para usar  [!DNL Payment Services]  no modo de teste.
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Configurar o teste de sandbox

Antes de iniciar a integração da sandbox, você deve se inscrever para obter uma conta gratuita do desenvolvedor do PayPal e criar contas de comerciante (para usar na integração) e de comprador (para usar para testar o check-out). Você pode criar várias contas de desenvolvedor, se desejar.

Uma conta de sandbox do PayPal permite usar [!DNL Payment Services] no modo de teste. O PayPal exige que você use uma conta de teste, email e senha de sandbox de negócios gerada pelo Portal do desenvolvedor do PayPal para integração com a sandbox. *Não crie outra conta durante o processo de integração da sandbox.*

## Integração com sandbox

Para concluir a integração da sandbox:

1. Navegue até a [página Conta de Desenvolvedor do PayPal](https://developer.paypal.com/developer/accounts/).
1. Clique em **[!UICONTROL Log in to Dashboard]** e faça logon com sua conta de teste de sandbox Comercial gerada pelo Portal do Desenvolvedor do PayPal ou clique em **Inscrever-se** para criar uma conta.
1. Criar uma conta de sandbox do PayPal:
   1. Vá para _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**.
   1. Clique em **[!UICONTROL Create account]**.

      Se você criou uma conta de sandbox do PayPal durante o processo de integração do PayPal com sandbox, deverá [redefinir sua sandbox de integração](#reset-your-sandbox-account), pois, ou não poderá verificar seu email.

   1. Selecione **[!UICONTROL Business]** como o Tipo de Conta e clique em **[!UICONTROL Create]**.
   1. Na seção _[!UICONTROL Sandbox Accounts]_, clique nos três pontos na coluna&#x200B;_[!UICONTROL Manage accounts]_ para a conta de sandbox que você criou.
   1. Clique em **[!UICONTROL View/edit account]**.

      ![PayPal - Exibir/editar conta de sandbox](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Copie e salve a ID de email e a senha gerada pelo sistema para uso futuro.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Clique em **[!UICONTROL Sandbox onboarding]**.

   Essa opção estará visível se você ainda não tiver concluído a integração da sandbox para [!DNL Payment Services].

   Uma ID de comerciante de sandbox é gerada automaticamente e preenchida em [configurações](settings.md). Não altere ou altere esta ID.

   Você tem uma janela do PayPal para conectar uma conta do PayPal para começar a aceitar pagamentos.

1. Digite o email e a senha da conta de sandbox do PayPal gerada na etapa 3 (não as informações da conta comercial do PayPal) e seu país ou região.
1. Clique em **[!UICONTROL Next]**.

   ![PayPal - Conectar conta do PayPal para pagamentos](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Continue a seguir o fluxo do PayPal, usando suas credenciais de conta de sandbox salvas anteriormente.
1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

   O botão **[!UICONTROL Sandbox onboarding]** não está mais visível e você vê o texto &quot;Pagamentos de sandbox pendentes&quot;.

Quando a integração da sandbox do PayPal for aprovada, você deverá ver uma notificação informando que o sistema de pagamento está no modo de sandbox e não está processando pagamentos em tempo real.

>[!IMPORTANT]
>
>Se você revogar o consentimento de [!DNL Payment Services] para [!DNL Adobe Commerce] e [!DNL Magento Open Source] para o processamento de seus pagamentos (nas configurações de sua conta do PayPal), os pedidos em seu armazenamento não poderão ser processados por [!DNL Payment Services]. Na página inicial dos Serviços de pagamento, é exibido um alerta sobre o consentimento revogado. Para ignorar o alerta, clique em **[!UICONTROL Do not show again]**.

### Redefinir sua conta de sandbox

Se você criou uma conta de sandbox do PayPal durante o processo de integração do PayPal com sandbox, deve redefinir sua sandbox de integração porque, ou não, pode verificar seu email.

Para redefinir sua conta de sandbox:

1. Clique em **[!UICONTROL Reset sandbox]**. [Criar uma conta de sandbox comercial do PayPal](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Clique em **[!UICONTROL Sandbox onboarding]** e conclua o próximo conjunto de etapas.

## Habilitar número de telefone de contato

O número de telefone de contato permite obter os números de telefone de contato que o PayPal coleta de seus clientes. O PayPal sempre coleta números de telefone de contato dos titulares de contas do PayPal para ajudar a confirmar suas identidades e contatá-los para resolver problemas em suas contas ou para concluir seus processos de atendimento. No entanto, o PayPal desencoraja o uso de números de telefone de contato diretamente do comerciante, pois pode afetar negativamente as vendas. Consulte a documentação do [PayPal obter números de telefone de contato](https://www.sandbox.paypal.com/businessmanage/preferences/website) para obter mais informações.

Este recurso é `off` por padrão. Ao ativá-lo, os administradores de loja podem ver números de telefone quando um cliente conclui um fluxo de Check-out de marca fora da página de check-out.

>[!IMPORTANT]
>
>Essa configuração não se aplica a outros fluxos de check-out.

## Teste em ambiente de sandbox

É altamente recomendável usar testes de espaços de dados para ambientes de integração e preparo, e testar Pagamentos em produção, com cartões de crédito e bancos reais, antes de expor essa funcionalidade para os compradores.

Consulte [Testar e validar](test-validate.md) para obter mais informações.
