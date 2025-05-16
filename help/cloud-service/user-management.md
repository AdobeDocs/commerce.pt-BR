---
title: Gerenciamento de usuários
description: Saiba como gerenciar usuários no [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Gerenciamento de usuários

{{accs-early-access}}

Se você quiser que os usuários acessem o Administrador em [!DNL Adobe Commerce as a Cloud Service], é necessário adicioná-los como usuários em sua organização e garantir que eles tenham acesso ao produto Cloud Service no [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Este processo requer uma organização IMS com acesso a [!DNL Adobe Commerce as a Cloud Service]. Somente um Administrador do sistema ou Administrador de produto da organização pode executar esses processos.

>[!TIP]
>
>Para adicionar vários usuários simultaneamente, você pode fazer um [upload CSV em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> Você também pode adicionar vários usuários a uma função criando um [grupo de usuários](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Em seguida, você pode adicionar o produto [!UICONTROL **Adobe Commerce as a Cloud Service - Back-end**] ao grupo de usuários.

## Noções básicas sobre funções

As seguintes funções estão disponíveis para [!DNL Adobe Commerce as a Cloud Service]. Para exibir ou editar essas funções, no Administrador do Commerce, navegue até **Sistema** > **Permissões** > **Funções de Usuário**.

* **Usuários** - Os usuários têm acesso de Administrador ao Administrador do Commerce, mas não podem gerenciar acesso no nível do produto no Admin Console. Os usuários também podem usar créditos para [criar instâncias](./getting-started.md#create-an-instance) no [!DNL Commerce Cloud Manager].

* [**Desenvolvedores**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Os desenvolvedores têm permissões de usuário e são adicionados à instância do Commerce como um usuário desenvolvedor. Isso significa que eles podem usar o [SDK da Interface do Administrador](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configurar eventos](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} e [criar webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administradores - Há três tipos diferentes de administradores:
   * [Administradores do sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - O administrador do sistema tem acesso a todos os produtos e perfis de produtos na organização por meio da Admin Console.
   * [Administradores de produtos](#add-a-product-admin) - Os administradores de produtos podem [gerenciar usuários, funções e permissões do produto](#add-users-and-admins) no [!DNL Adobe Admin Console] e [gerenciar usuários no Administrador do Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administradores de perfil de produto](#add-users-developers-and-product-profile-admins) - Os administradores de perfil de produto não têm acesso ao Administrador do Adobe Commerce, mas podem gerenciar usuários para o produto no [!DNL Adobe Admin Console].

Para obter informações detalhadas sobre as permissões concedidas a cada função dentro do Adobe Commerce, consulte [permissões de usuário](#user-permissions).

## Adicionar um administrador de produto

1. Navegue até https://adminconsole.adobe.com e faça logon com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce as a Cloud Service - Back-end**].

   ![selecionar produto](./assets/backend.png){width="600" zoomable="yes"}

1. Selecione a guia [!UICONTROL **Administradores**].

1. Clique em [!UICONTROL **Adicionar administrador**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Salvar**].

## Adicionar usuários, desenvolvedores e administradores de perfil de produto

As instruções a seguir fornecem informações sobre como adicionar usuários e desenvolvedores ao [!DNL Commerce Cloud Manager] e ao Administrador do Commerce. A interface [!DNL Commerce Cloud Manager] permite criar e gerenciar suas Instâncias do Commerce.

>[!NOTE]
>
>Somente administradores de produtos e administradores de sistemas podem adicionar usuários e desenvolvedores ao produto Adobe Commerce as a Cloud Service.

1. Navegue até https://adminconsole.adobe.com e faça logon com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce as a Cloud Service - Back-end**].

   ![selecionar produto](./assets/backend.png){width="600" zoomable="yes"}

1. Clique no perfil de produto [!UICONTROL **Padrão - Cloud Manager**].

1. Selecione a guia [!UICONTROL **Usuários**], [!UICONTROL **Desenvolvedores**] ou [!UICONTROL **Administradores**] e clique em [!UICONTROL **Adicionar Usuários**] ou [!UICONTROL **Adicionar Desenvolvedores**] ou [!UICONTROL **Adicionar Administradores**].

   >[!NOTE]
   >
   >Os administradores adicionados desta tela são [administradores de perfil de produto](#understanding-roles) e não têm acesso ao Administrador do Commerce.

   ![seleção de guia](./assets/tab-select.png){width=600 zoomable="yes"}

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Salvar**].

## Recursos de função

A lista a seguir descreve os recursos que as funções padrão têm permissão para acessar dentro do Administrador do Adobe Commerce. Para editar as permissões padrão para cada função, navegue até **Sistema** > **Permissões** > **Funções de usuário** no Administrador do Commerce.

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
