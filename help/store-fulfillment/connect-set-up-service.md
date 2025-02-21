---
title: Conectar a Solução de Abastecimento da Loja
description: Estabeleça as conexões entre o Adobe Commerce e a solução Store Fulfillment. Crie e autorize uma integração do Adobe Commerce e adicione as credenciais da conta Store Fulfillment à configuração do serviço do Adobe Commerce.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Conectar a Solução de Abastecimento da Loja

Conecte os Serviços de Abastecimento de Loja com o Adobe Commerce adicionando as credenciais de autenticação e os dados de conexão necessários ao Administrador do Adobe Commerce.

- **[Configurar [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)**-Crie uma integração do Adobe Commerce para os serviços de Atendimento da Loja e gere os tokens de acesso para autenticar solicitações recebidas dos servidores de Atendimento da Loja.

- **[Configurar credenciais de conta para os Serviços de Atendimento da Loja](#configure-store-fulfillment-account-credentials)**-Adicione suas credenciais para conectar o Adobe Commerce à sua conta de Atendimento da Loja.

>[!NOTE]
>
>Conclua a configuração da conexão e valide a conexão com êxito antes de começar o teste.

## Criar uma integração do Adobe Commerce

Para integrar o Adobe Commerce aos serviços de Atendimento da loja, crie uma integração do Commerce e gere tokens de acesso que possam ser usados para autenticar solicitações dos servidores de Atendimento da loja. Você também deve atualizar as opções [!UICONTROL Consumer Settings] do Adobe Commerce para evitar `The consumer isn't authorized to access %resources.` erros de resposta nas solicitações do Adobe Commerce para os serviços [!DNL Store Fulfillment].

1. No Administrador, crie a Integration for Store Fulfillment.

   - Nomear a extensão
   - Insira seu endereço de email
   - Digite a senha da sua conta de administrador

1. Configure permissões de Acesso a recursos da API para a integração com o seguinte:

   - Vendas > Atualização de ordem BOPIS
   - Sistema > Armazenar Permissões de Aplicativo de Atendimento

1. Gere os tokens de acesso para autenticação salvando e ativando a integração.

1. Copie e salve os tokens de acesso em um local seguro e criptografado.

1. Trabalhe com seu Gerente de conta para concluir a configuração no lado de Atendimento da loja e autorizar a integração.

1. Habilite a opção [!UICONTROL Consumer Settings] do Adobe Commerce para [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens].

   - No Administrador, vá para **[!UICONTROL Stores]** > [!UICONTROL Configuration] > **[!UICONTROL Services]** > **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]**

   - Defina a opção [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] como **[!UICONTROL Yes]**.

>[!IMPORTANT]
>
> O token de integração é específico do ambiente. Se você restaurar o banco de dados para um ambiente com os dados de origem de um ambiente diferente, por exemplo, restaurando os dados de produção de um ambiente de preparo, exclua a tabela `oauth_token` da exportação do banco de dados para que os detalhes do token de integração não sejam substituídos durante a operação de restauração.


## Configurar credenciais da conta de Abastecimento do Repositório

Depois de preencher o formulário de entrada, uma conta de Atendimento de Loja Walmart é criada para você. Você receberá as seguintes credenciais quando elas estiverem disponíveis:

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] (geralmente o mesmo da configuração acima)

Essas credenciais são necessárias para configurar e usar o Atendimento da Loja.

>[!NOTE]
>
>O processo de criação de conta pode levar algum tempo para ser concluído. Enquanto você aguarda as credenciais, [revise e defina outras configurações para a solução de Atendimento de Loja](service-config-settings-overview.md).

### Adicionar credenciais para se conectar ao Atendimento da Loja

1. Configure as [credenciais da conta](enable-general.md) para os ambientes de Produção e Sandbox.

1. No Administrador, vá para **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**

1. Insira as credenciais de conta fornecidas para o **[!UICONTROL Production environment]**. Todos os campos são obrigatórios.

1. Selecione **[!UICONTROL Save Config]**.

1. Teste a conexão selecionando **[!UICONTROL Validate Credentials]**.

>[!NOTE]
>
>Se as credenciais forem inválidas, verifique se você inseriu os valores corretos para cada ambiente e revalide. Entre em contato com o representante de conta se ainda tiver problemas de conexão.
