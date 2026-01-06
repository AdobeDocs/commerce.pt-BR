---
title: Gerenciamento de usuários
description: Saiba como gerenciar usuários no [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud, Integration
role: Admin
level: Intermediate
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3fe22d47b6fd6cf1077cbd4644ffad08f55826ca
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 0%

---

# Usuário e Identity Management

Para permitir que os usuários acessem o Administrador no [!DNL Adobe Commerce as a Cloud Service], adicione-os como usuários em sua organização e verifique se eles têm acesso ao produto Cloud Service no [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Este processo requer uma organização IMS com acesso a [!DNL Adobe Commerce as a Cloud Service]. Somente um Administrador do sistema ou Administrador de produto da organização pode executar esses processos.

>[!TIP]
>
>Para adicionar vários usuários simultaneamente, você pode fazer um [upload CSV em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
> Você também pode adicionar vários usuários a uma função criando um [grupo de usuários](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Em seguida, você pode adicionar o produto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] ao grupo de usuários.

## Noções básicas sobre funções

As seguintes funções estão disponíveis para [!DNL Adobe Commerce as a Cloud Service]. Para exibir ou editar essas funções, no Administrador do Commerce, navegue até [!UICONTROL **Sistema**] > [!UICONTROL **Permissões**] > [!UICONTROL **Funções de Usuário**].

* **Usuários** - Os usuários têm acesso de Administrador ao Administrador do Commerce, mas não podem gerenciar o acesso no nível do produto no Admin Console. Os usuários também podem usar créditos para [criar instâncias](./getting-started.md#create-an-instance) no [!DNL Commerce Cloud Manager].

  >[!NOTE]
  >
  >Todos os usuários do Commerce, incluindo desenvolvedores e administradores, também devem ter a função Usuário atribuída a eles. É necessário para permissões básicas do Commerce.

* [**Desenvolvedores**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} — Os desenvolvedores têm permissões de usuário e são adicionados à instância do Commerce como um usuário desenvolvedor. Eles podem usar os [[!DNL Admin UI SDK]](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configurar eventos](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} e [criar webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administradores - Há três tipos diferentes de administradores:
   * [Administradores do sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - O administrador do sistema tem acesso a todos os produtos e perfis de produtos na organização por meio da Admin Console.
   * [Administradores de produtos](#add-a-product-admin) - Os administradores de produtos podem [gerenciar usuários, funções e permissões do produto](#add-users) no [!DNL Adobe Admin Console] e [gerenciar usuários no Administrador do Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administradores de perfil de produto](#add-developers-and-product-profile-admins) - Os administradores de perfil de produto não têm acesso ao Administrador do Adobe Commerce, mas podem gerenciar usuários para o produto no [!DNL Adobe Admin Console].

Para obter informações detalhadas sobre as permissões concedidas a cada função dentro do Adobe Commerce, consulte [permissões de usuário](#user-permissions).

## Adicionar um administrador de produto

>[!BEGINTABS]

>[!NOTE]
>
>Atribua a [Função de usuário](#add-users) aos administradores de produtos antes de adicioná-los como administradores de produtos. A função Usuário é necessária para permissões básicas do Commerce.

>[!TAB GA (Provisionado após 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Selecione a guia [!UICONTROL **Usuários**].

1. Selecione a guia [!UICONTROL **Administradores**].

1. Clique em [!UICONTROL **Adicionar administrador**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Avançar**].

1. Selecione a função de [!UICONTROL **Administrador de perfil de produto**].

1. Clique em [!UICONTROL **+**] para adicionar produtos.

1. Selecione a instância existente do Commerce à qual adicionar o administrador. As instâncias do Commerce usam o seguinte formato: `Adobe Commerce - <instance-name> - ACCS - <environment-type> - <tenant-id>`.

1. Selecione o perfil de produto.

1. Clique em [!UICONTROL **Aplicar**].

1. Clique em [!UICONTROL **Salvar**].

>[!TAB Acesso antecipado (provisionado antes de 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![Seleção de produtos no Admin Console mostrando o Adobe Commerce Cloud Manager](./assets/backend.png){width="600" zoomable="yes"}

1. Selecione a guia [!UICONTROL **Administradores**].

1. Clique em [!UICONTROL **Adicionar administrador**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Salvar**].

>[!ENDTABS]

## Adicionar usuários

As instruções a seguir fornecem informações sobre como adicionar usuários ao [!DNL Commerce Cloud Manager] e ao Administrador do Commerce. A interface [!DNL Commerce Cloud Manager] permite criar e gerenciar suas Instâncias do Commerce. Esse processo é necessário para todos os usuários, incluindo desenvolvedores e administradores.

>[!NOTE]
>
>Somente administradores de produtos e administradores de sistemas podem adicionar usuários e desenvolvedores ao produto Adobe Commerce as a Cloud Service.

>[!BEGINTABS]

>[!TAB GA (Provisionado após 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Selecione a guia [!UICONTROL **Produtos**].

1. Selecione o produto [!UICONTROL **Adobe Commerce**].

1. Selecione o produto Commerce Cloud Manager se quiser adicionar o usuário à interface do Cloud Manager, onde ele pode criar e gerenciar instâncias do Commerce, ou selecione a instância do Commerce existente à qual adicionar o usuário. As instâncias do Commerce usam o seguinte formato: `Adobe Commerce - <instance-name> - ACCS - <environment-type> - <tenant-id>`.

1. Selecione a guia [!UICONTROL **Usuários**] e clique em [!UICONTROL **Adicionar usuários**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar e clique em [!UICONTROL **Salvar**].

1. Selecione o perfil de produto desejado.

1. Clique em [!UICONTROL **Aplicar**].

1. Clique em [!UICONTROL **Salvar**].

>[!TAB Acesso antecipado (provisionado antes de 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![Produto do Adobe Commerce Cloud Manager no Admin Console](./assets/backend.png){width="600" zoomable="yes"}

1. Clique no perfil de produto [!UICONTROL **Padrão - Cloud Manager**].

1. Selecione a guia [!UICONTROL **Usuários**] e clique em [!UICONTROL **Adicionar usuários**].

   ![Seleção da guia Usuários no perfil de produto do Admin Console](./assets/tab-select.png){width="600" zoomable="yes"}

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar e clique em [!UICONTROL **Salvar**].

>[!ENDTABS]

### Adicionar desenvolvedores e administradores de perfil de produto

Para adicionar desenvolvedores e administradores de perfil de produto, repita o processo [adicionar usuários](#add-users), mas selecione a guia [!UICONTROL **Desenvolvedores**] ou [!UICONTROL **Administradores**] em vez da guia [!UICONTROL **Usuários**].

>[!NOTE]
>
>Os administradores de perfil de produto não têm acesso ao Administrador do Commerce. Consulte [Noções básicas sobre funções](#understanding-roles) para obter mais informações.
>
>Atribua aos desenvolvedores a função User antes de adicioná-los como desenvolvedores. A função Usuário é necessária para permissões básicas do Commerce.

![Opções da guia Desenvolvedores e Administradores no Admin Console](./assets/tab-select.png){width="600" zoomable="yes"}

## Recursos de função

A lista a seguir descreve os recursos que as funções padrão têm permissão para acessar dentro do Administrador [!DNL Adobe Commerce]. Para editar as permissões padrão para cada função, navegue até [!UICONTROL **Sistema**] > [!UICONTROL **Permissões**] > [!UICONTROL **Funções de usuário**] no Administrador do Commerce.

**Usuários**

* Catálogo
   * Inventário
      * Produtos
         * Ler preço do produto

**Desenvolvedores**

* Catálogo
   * Inventário
      * Produtos
         * Ler preço do produto
* Sistema
   * Transferência de dados
      * Importar histórico
* Configuração de eventos do Adobe IO
   * Verificação de configuração
   * Criar provedor de eventos
   * Atualização da configuração
   * Sincronizar eventos
   * Obter Lista de Provedores de Eventos
* Estrutura de evento
   * Lista de Eventos
   * Testar conexão de evento
   * Inscrever-se em um evento
   * Cancelar inscrição em um evento
   * Status do evento
   * API para obter assinaturas de evento
   * Exibir Interface do administrador de Assinaturas de Eventos
   * Criar interface do administrador de Assinaturas de Eventos
   * Solicitar nova interface do administrador de eventos
* Webhooks
   * Assinatura digital do Webhooks
      * Configurações de assinatura digital do Webhooks
      * Webhooks Assinatura digital Gerar chaves
   * Gerenciamento de Webhooks
      * Grade de Webhooks
      * Edição de Webhooks
      * Webhooks de teste
      * Assinatura da API no webhook
      * Cancelamento de inscrição de API no webhook
      * Lista de webhooks
      * Solicitar novo webhook
      * Logs do Webhooks
      * Obter lista de Webhooks

**Administradores**

Administradores têm acesso a todas as permissões.

## Adicionar um usuário a [!DNL AEM Assets] ou [!DNL Product Visuals]

A seguinte configuração é necessária para [!DNL Adobe Experience Manager Assets] e [!DNL Product Visuals powered by AEM Assets] usuários.

Se sua conta tiver acesso a [[!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service) e você quiser permitir que um usuário acesse os recursos avançados do [[!DNL AEM Assets]](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/overview){target="_blank"} junto com o [!DNL Adobe Commerce as a Cloud Service], conclua o seguinte processo:

>[!NOTE]
>
>Os usuários sem as permissões de ativos apropriadas não poderão acessar os recursos avançados do [!DNL AEM Assets], como a [geração de imagem de IA](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}, as [variações geradas](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"} e muito mais.

>[!TIP]
>
>Para adicionar vários usuários simultaneamente, você pode fazer um [upload CSV em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
>Você também pode adicionar vários usuários a uma função criando um [grupo de usuários](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Em seguida, você pode adicionar o produto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] ao grupo de usuários.

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**].

   ![Seleção de produto do AEM Cloud Manager no Admin Console](./assets/backend-aem.png){width="600" zoomable="yes"}

1. Selecione a guia [!UICONTROL **Usuários**].

1. Clique em [!UICONTROL **Adicionar usuário**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar.

1. Clique em [!UICONTROL **Adicionar produto**].

1. Selecione os seguintes perfis de produto, que são necessários para integrar o [!DNL AEM Assets] ao Commerce:

   * Proprietário da empresa - É necessário criar e gerenciar programas.
   * Gerente de implantação - Obrigatório para implantar o código dos repositórios no AEM.

   Se você estiver adicionando um desenvolvedor que não precisa de acesso às interfaces do Cloud Manager ou do Experience Manager, poderá atribuir a ele a função de desenvolvedor.

   >[!NOTE]
   >
   >Para obter mais informações sobre como essas permissões afetam seu acesso ao [!DNL AEM Assets], consulte [Perfis de Produtos Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}.

1. Clique em [!UICONTROL **Aplicar**].

1. Clique em [!UICONTROL **Salvar**].

Para confirmar se o usuário tem acesso, clique no nome do usuário para abrir a página de perfil. Na seção [!UICONTROL **Produtos**], deve constar [!UICONTROL **Concluído**] em [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]. Pode levar alguns segundos após adicionar o usuário para ver o status atualizado em seu perfil. Atualize a página para ver o status atualizado.

![Perfil de usuário mostrando o status de acesso ao produto concluído](./assets/product-access.png){width="600" zoomable="yes"}

## Acessar a interface do Experience Manager

Depois de adicionar um usuário ao [!DNL AEM Assets], ele pode acessar a interface [!DNL Experience Manager] navegando até [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}.

1. Na seção [!UICONTROL **Acesso Rápido**], clique em [!UICONTROL **Experience Manager**] ou em [!UICONTROL **Exibir Tudo**] se você não vir [!UICONTROL **Experience Manager**]. Em seguida, clique em [!UICONTROL **Cloud Manager**] ou navegue diretamente para [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}.

1. Na página [!UICONTROL **Cloud Manager**], clique em [!UICONTROL **Adicionar programa**] para começar.

1. [Criar um novo programa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [Criar um novo ambiente](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. Depois de criar o ambiente, retorne ao [Admin Console](https://adminconsole.adobe.com){target="_blank"} e selecione [!UICONTROL **Adobe Experience Manager as a Cloud Service**].

1. Agora você deve ver novos perfis de produto. Selecione que contém `- author -`. Por exemplo, `<environment-name> - author - <program-id> - <environment-id>`.

1. [Adicionar usuários ao perfil de produto](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.

* [Configurar [!DNL AEM Assets] para oferecer suporte aos metadados do Commerce](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [Integrar [!DNL AEM Assets] ao Commerce para sincronização de ativos](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization)

## Gerenciamento de identidade e configuração de logon único

{{ims-identity-and-sso-config}}

