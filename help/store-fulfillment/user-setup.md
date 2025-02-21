---
title: Configuração de usuário
description: Configure fontes aprimoradas do Inventory management como lojas de comerciantes para dar suporte à solução Store Fulfillment para Adobe Commerce.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Configuração de usuário

Os usuários do aplicativo Store Assist são gerenciados no Adobe Commerce. No entanto, esses usuários não interagem diretamente com o Adobe Commerce. O gerenciamento de usuários é configurado no Adobe Commerce para habilitar conexões seguras entre o Adobe Commerce e o aplicativo.

O modelo de Usuário do Aplicativo de Abastecimento da Loja é separado de outros modelos de usuário do Adobe Commerce. O aplicativo mantém seu próprio modelo de permissão por meio de funções de usuário e usuários que podem ser atribuídos a todos os locais ou a locais específicos. As seguintes permissões são suportadas: Ordem de separação, Ordem de Dispensa e Redução de quantidade de itens (e cancelamento).

>[!TIP]
>
>Para obter melhores resultados, [configure sua conexão](connect-set-up-service.md) antes de adicionar usuários e permissões aos associados da loja que usam o aplicativo Store Assist.

## Aplicativo de Assistência da Loja - Funções de Usuário

Durante a configuração inicial do usuário para o aplicativo Store Assist, crie funções de usuário para personalizar permissões de usuário para o aplicativo Store Assist. Por exemplo, você pode criar diferentes funções para gerentes de loja e associados de loja e atribuir diferentes recursos de função para gerenciar permissões para cada tipo de usuário.

Configurar Funções de Usuário de **[!UICONTROL System > Store Fulfillment App Permissions > All Store Fulfillment App Users]**.

### Informações da função

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|----------------------------|-------------------------|-----------|--------------|
| **[!UICONTROL Role Name]** | Ative ou desative o usuário. | Global | Sim |

### Recursos da função

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Resource Access]** | Liste os grupos de permissões disponíveis que podem ser atribuídos a uma função de usuário. No momento, a Store Fulfillment Solution não tem diferentes níveis de permissão definidos para funções de recurso. Todas as funções de usuário têm o mesmo acesso a recursos. | Global | Sim |

## Store Assist - Informações do usuário

Gerenciar perfis de usuário do aplicativo de Assistência da Loja nas configurações do Sistema de Administração: **[!UICONTROL System > Store Fulfillment App Permissions > All Store Fulfillment App Users]**.

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL is Active]** | Ative ou desative o usuário. | Global | Sim |
| **[!UICONTROL User Name]** | Nome de usuário associado ao usuário | Global | Sim |
| **[!UICONTROL First Name]** | Nome associado ao usuário | Global | Não |
| **[!UICONTROL Last Name]** | Sobrenome associado ao usuário | Global | Não |
| **[!UICONTROL Role]** | Função associada ao usuário | Global | Não |
| **[!UICONTROL Access to all locations]** | Atribua aos usuários acesso a todas as lojas ou selecione lojas individualmente. | Global | Não |
| **Localidade da Interface** | Se sua loja tiver vários idiomas, defina o Local da interface para o idioma a ser usado para a interface de administrador. | Global | Não |
| **Ativo desde** | Para definir uma data de início, selecione o ícone de calendário. | Global | Não |
| **Ativo para** | Defina a Data de expiração selecionando o ícone do calendário. Definir uma data de expiração é útil para configurar atribuições temporárias de usuários ou funções. Após a data de expiração, o status da conta do usuário muda para `Inactive`, mas a conta ainda pode ser atualizada, se necessário. | Global | Não |
