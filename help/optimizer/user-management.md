---
title: Gerenciamento de usuários
description: Saiba como gerenciar usuários no [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 02758aa5cc14af6d46bfc4bb7865fa37a787d4cb
workflow-type: tm+mt
source-wordcount: '458'
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

1. Navegue até o [Admin Console](https://adminconsole.adobe.com) e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce as a Cloud Service - Back-end**].

   ![selecionar produto](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Selecione a guia [!UICONTROL **Administradores**].

1. Clique em [!UICONTROL **Adicionar administrador**].

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Salvar**].

## Adicionar usuários, desenvolvedores e administradores de perfil de produto

>[!BEGINSHADEBOX &quot;Pré-requisitos&quot;]
>
O provisionamento a seguir é necessário para o gerenciamento de usuários:

- Organização IMS provisionada para [!DNL Adobe Commerce Optimizer]
- Uma conta do Adobe Experience Cloud na mesma organização IMS com a função de administrador do sistema ou do produto

>[!ENDSHADEBOX]

Use as instruções a seguir para adicionar usuários e desenvolvedores ao [!DNL Commerce Cloud Manager], onde você gerencia suas instâncias do Commerce.

1. Navegue até [Adobe Admin Console](https://adminconsole.adobe.com) e entre com sua Adobe ID.

1. Selecione sua organização.

1. Na guia [!UICONTROL **Produtos**], em [!UICONTROL **Produtos e Serviços**], selecione o produto [!UICONTROL **Adobe Commerce as a Cloud Service - Back-end**].

   ![selecionar produto](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Clique no perfil de produto [!UICONTROL **Padrão - Cloud Manager**].

1. Selecione a guia [!UICONTROL **Usuários**], [!UICONTROL **Desenvolvedores**] ou [!UICONTROL **Administradores**] e clique em [!UICONTROL **Adicionar Usuários**] ou [!UICONTROL **Adicionar Desenvolvedores**] ou [!UICONTROL **Adicionar Administradores**].

   Os administradores adicionados desta tela são atribuídos ao grupo [administradores do perfil de produto](#understanding-roles).

   ![seleção de guia](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Insira o nome de usuário ou endereço de email dos usuários que deseja adicionar como administradores e clique em [!UICONTROL **Salvar**].

## Gerenciamento de usuários em massa

É possível adicionar vários usuários com mais eficiência usando um dos seguintes métodos:

- Use o recurso **Adicionar usuários por CSV** na Adobe Admin Console para executar um [upload CSV em massa](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Adicione vários usuários a uma função criando um [grupo de usuários](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Em seguida, adicione o produto [!UICONTROL **Adobe Commerce as a Cloud Service - Back-end**] ao grupo de usuários.

