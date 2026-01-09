---
title: Usuário e Identity Management
description: Saiba como criar e gerenciar usuários e atribuir funções de usuário para  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 423d6f3fb544fb33b8e4e689fdfbbb3cf5b700f3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Gerenciamento de usuários

Para habilitar o acesso a [!DNL Adobe Commerce Optimizer], adicione usuários do [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} e verifique se eles têm acesso ao produto Commerce.

É possível atribuir usuários a qualquer uma das seguintes funções:

- **Usuário**— Os usuários têm acesso à interface do usuário [!DNL Adobe Commerce Optimizer] para exibir e gerenciar exibições de catálogo e regras de merchandising, além de acompanhar métricas de desempenho.

- [**Desenvolvedor**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}— Os desenvolvedores têm permissões de usuário e acesso à Adobe Developer Console. Isso significa que eles podem criar projetos e configurar credenciais para usar ferramentas de desenvolvedor, como as APIs e SDKs do [!DNL Adobe Commerce Optimizer], juntamente com ferramentas de extensibilidade do Adobe, como o App Builder e a API Mesh.

- **Administrador** - Há três tipos diferentes de funções administrativas:
   - [Administradores do sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - O administrador do sistema tem acesso a todos os produtos e perfis de produtos na organização por meio da Adobe Admin Console.
   - [Administradores de produtos](#add-a-product-admin) - Os administradores de produtos podem [gerenciar usuários, funções e permissões do produto](#add-users-and-admins) no [!DNL Adobe Admin Console].
   - [Administradores de perfil de produto](#add-users-developers-and-product-profile-admins) - Os administradores de perfil de produto podem gerenciar usuários para o produto no [!DNL Adobe Admin Console].

## Adicionar um administrador de produto

>[!BEGINTABS]

>[!NOTE]
>
>Atribua a [Função de usuário](#add-users) aos administradores de produtos antes de adicioná-los como administradores de produtos. A função Usuário é necessária para permissões básicas do Commerce.

Há duas maneiras diferentes de adicionar usuários administradores de produtos ao Adobe Commerce Optimizer com base em quando sua organização foi provisionada. Em organizações de acesso antecipado, cada usuário com a função de administrador de produto recebe permissão para gerenciar todas as instâncias na organização. Em organizações de Disponibilidade geral (GA) provisionadas após 13 de outubro de 2025, você pode atribuir um usuário como administrador de produto para instâncias específicas. Quando o usuário administrador do produto faz logon, ele pode ver apenas as instâncias que tem permissão para gerenciar.

>[!TAB GA (Provisionado após 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Selecione a guia [!UICONTROL **Usuários**].

1. Selecione a guia [!UICONTROL **Administradores**].

1. Clique em [!UICONTROL **Adicionar administrador**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Avançar**].

1. Selecione a função de [!UICONTROL **Administrador de perfil de produto**].

1. Clique em **+** para adicionar produtos.

1. Selecione a instância existente do Commerce Optimizer à qual adicionar o administrador. As instâncias do Commerce Optimizer usam o seguinte formato: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Selecione o perfil de produto.

1. Clique em [!UICONTROL **Aplicar**].

1. Clique em [!UICONTROL **Salvar**].

>[!TAB Acesso antecipado (provisionado antes de 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![selecionar produto](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Selecione a guia [!UICONTROL **Administradores**].

1. Clique em [!UICONTROL **Adicionar administrador**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Salvar**].

>[!ENDTABS]

## Adicionar usuários

As instruções a seguir fornecem informações sobre como adicionar usuários ao [!DNL Commerce Cloud Manager] e ao Commerce Optimizer. A interface [!DNL Commerce Cloud Manager] permite criar e gerenciar suas instâncias do Commerce Optimizer. Esse processo é necessário para todos os usuários, incluindo desenvolvedores e administradores.

>[!NOTE]
>
>Somente administradores de produtos e administradores de sistemas podem adicionar usuários e desenvolvedores ao produto do Adobe Commerce Optimizer.

>[!BEGINTABS]

>[!TAB GA (Provisionado após 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Selecione a guia [!UICONTROL **Produtos**].

1. Selecione o produto [!UICONTROL **Adobe Commerce**].

1. Selecione o produto Commerce Cloud Manager se quiser adicionar o usuário à interface do Cloud Manager, onde ele pode criar e gerenciar instâncias do Commerce Optimizer, ou selecione a instância do Commerce Optimizer existente à qual adicionar o usuário. As instâncias do Commerce Optimizer usam o seguinte formato: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Selecione a guia [!UICONTROL **Usuários**] e clique em [!UICONTROL **Adicionar usuários**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar e clique em [!UICONTROL **Salvar**].

1. Selecione o perfil de produto desejado.

1. Clique em [!UICONTROL **Aplicar**].

1. Clique em [!UICONTROL **Salvar**].

>[!TAB Acesso antecipado (provisionado antes de 13 de outubro de 2025)]

1. Navegue até <https://adminconsole.adobe.com> e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![selecionar produto](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. Clique no perfil de produto [!UICONTROL **Padrão - Cloud Manager**].

1. Selecione a guia [!UICONTROL **Usuários**] e clique em [!UICONTROL **Adicionar usuários**].

   ![seleção de guia](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar e clique em [!UICONTROL **Salvar**].

>[!ENDTABS]

### Adicionar desenvolvedores e administradores de perfil de produto

Para adicionar desenvolvedores e administradores de perfil de produto, repita o processo [adicionar usuários](#add-users), mas selecione a guia [!UICONTROL **Desenvolvedores**] ou [!UICONTROL **Administradores**] em vez da guia [!UICONTROL **Usuários**].

>[!NOTE]
>
>Atribua aos desenvolvedores a função User antes de adicioná-los como desenvolvedores. A função Usuário é necessária para permissões básicas do Commerce.

![seleção de guia](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## Gerenciamento de usuários em massa

É possível adicionar vários usuários com mais eficiência usando um dos seguintes métodos:

- Use o recurso **Adicionar usuários por CSV** na Adobe Admin Console para executar um [upload CSV em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Adicione vários usuários a uma função criando um [grupo de usuários](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Em seguida, adicione os produtos apropriados ao grupo de usuários.

## Gerenciamento de identidade e configuração de logon único

{{ims-identity-and-sso-config}}
