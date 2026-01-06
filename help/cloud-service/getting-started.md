---
title: Introdução ao  [!DNL Adobe Commerce as a Cloud Service]
description: Saiba como começar a usar o  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud, Integration
role: Admin, Developer, User
level: Beginner
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3fe22d47b6fd6cf1077cbd4644ffad08f55826ca
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Introdução

[!DNL Adobe Commerce as a Cloud Service] fornece a maioria das configurações prontas para uso. Depois de concluir alguns processos de configuração básica, seu armazenamento não pára de funcionar. Este guia orienta você na criação e no trabalho com uma instância e ajuda a configurar sua organização para ter sucesso. Ele garante que suas equipes tenham acesso adequado ao [!DNL Adobe Commerce as a Cloud Service] e às ferramentas necessárias para começar.

O [!DNL Adobe Commerce as a Cloud Service] é uma plataforma comercial nativa em nuvem que oferece flexibilidade, escalabilidade e eficiência para proporcionar experiências de comércio digital. Essa oferta SaaS é uma plataforma totalmente gerenciada e sem versão que fornece uma experiência de atualização contínua sem intervenção manual.

## Componentes principais

[!DNL Adobe Commerce as a Cloud Service] consiste nos seguintes componentes:

* **[[!DNL Adobe Experience Cloud]](https://experience.adobe.com/)** - Seu ponto de entrada central para todos os produtos do [!DNL Adobe Commerce] em [experience.adobe.com](https://experience.adobe.com/)
   * Clique em [!UICONTROL **Commerce**] em [!UICONTROL **Acesso rápido**] para abrir o Commerce Cloud Manager
* **[[!DNL Commerce Cloud Manager]](https://experience.adobe.com/#/commerce/cloud-service)** - Crie e gerencie instâncias, acesse URLs de API e o Administrador do Commerce
* **[[!DNL Adobe Admin Console]](https://adminconsole.adobe.com/)** - Gerenciar usuários e funções
* **Administrador do Commerce** - Gerencie configurações de produtos, pedidos, clientes e loja
* **[Loja equipada com [!DNL Edge Delivery Services]](./storefront.md)** - Crie e personalize uma loja voltada para o cliente usando um sistema combinável de alto desempenho que ofereça velocidade, SEO e experiência do usuário excepcionais para comerciantes e desenvolvedores
* **[[!DNL Adobe Developer App Builder]](https://developer.adobe.com/app-builder/)** - Crie integrações personalizadas usando o [!DNL App Builder], juntamente com outras ferramentas de extensibilidade, como o [kit inicial de integração](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) e [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/)

## Configuração e gerenciamento

Como parte do processo de configuração do [!DNL Adobe Commerce as a Cloud Service], o administrador do sistema, os comerciantes e os desenvolvedores configuram o acesso e os recursos para a sua organização, incluindo o provisionamento de recursos em nuvem e a atribuição de usuários às funções apropriadas com base em suas responsabilidades.

### Fluxo de trabalho de configuração e gerenciamento

Como um grupo combinado, o administrador do sistema, o comerciante e o desenvolvedor precisam seguir estas etapas essenciais para colocar sua instância do Commerce em funcionamento:

1. **Todos os usuários**: [Criar uma instância](#create-an-instance)
1. **Administrador do Sistema**: [Adicionar usuários e atribuir funções](user-management.md#add-users-and-admins)
1. **Comerciantes**: [Acesse o Administrador do Commerce](#access-an-instance) e [importe seu catálogo](#import-your-catalog)
1. **Desenvolvedores**: [Configure sua loja](storefront.md) e explore a [plataforma de desenvolvedor](overview.md#developer-platform)

#### Fluxo de trabalho do AEM Assets e Visuais de produto

As etapas a seguir são necessárias para integrar [!DNL Adobe Experience Manager Assets] ou [!DNL Product Visuals powered by AEM Assets] a [!DNL Adobe Commerce as a Cloud Service]:

1. **Administrador do Sistema**: [Adicionar usuários ao [!DNL AEM Assets] perfil de produto [!DNL Product Visuals] 5&rbrace;](user-management.md#add-a-user-to-aem-assets-or-product-visuals)
1. **Desenvolvedores**: [Integrar [!DNL AEM Assets] e [!DNL Product Visuals]](../aem-assets-integration/overview.md)
1. **Comerciantes**: [Acesse seus [!DNL AEM Assets] e [!DNL Product Visuals]](./user-management.md#access-the-experience-manager-interface)

### Tarefas de configuração e gerenciamento baseadas em função

Selecione uma guia abaixo para ver gráficos de fluxo de trabalho de alto nível para a função correspondente:

>[!BEGINTABS]

>[!TAB Fluxo de trabalho de comerciante e administrador do sistema]

Este diagrama fornece uma visão geral de alto nível de como os administradores do sistema e comerciantes acessam e gerenciam as instâncias do [!DNL Adobe Commerce as a Cloud Service]. Consulte o [Guia do Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html) para obter mais informações sobre fluxos de trabalho de administrador.

![Diagrama do administrador do sistema e do fluxo de trabalho do comerciante para o Adobe Commerce as a Cloud Service](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Fluxo de trabalho do desenvolvedor]

Este diagrama fornece uma visão geral de alto nível de como os desenvolvedores criam integrações com o [!DNL Adobe Commerce as a Cloud Service] usando o App Builder. Consulte a [documentação da API](https://developer.adobe.com/commerce/webapi/rest/) para obter mais informações.

![Diagrama do fluxo de trabalho do desenvolvedor para criar integrações com o Adobe Commerce as a Cloud Service](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

Selecione sua função para encontrar recursos para começar a usar o processo de configuração:

>[!BEGINTABS]

>[!TAB Administrador do sistema]

Como administrador do sistema, você é responsável por configurar a organização e gerenciar o acesso do usuário.

| Tarefa | Descrição | Recurso |
|------|-------------|----------|
| Compreender a plataforma | Saiba mais sobre a arquitetura e os benefícios do Adobe Commerce as a Cloud Service | [Visão geral](overview.md) |
| Comparar recursos | Entender as diferenças entre o Cloud Service e outras ofertas da Adobe Commerce | [Comparação de recursos](feature-comparison.md) |
| Criar uma instância | Provisionamento de ambientes de sandbox e produção | [Criar uma instância](#create-an-instance) |
| Configurar gerenciamento de usuários | Adicionar usuários, atribuir funções e gerenciar permissões | [Gerenciamento de usuários](user-management.md) |
| Configurar [!DNL AEM Assets] e [!DNL Product Visuals] (opcional) | Adicionar usuários, atribuir funções e gerenciar permissões | [Gerenciamento de usuários](user-management.md#add-a-user-to-aem-assets-or-product-visuals) |

>[!TAB Comerciante]

Como comerciante, você se concentra no gerenciamento de produtos, pedidos e conteúdo de vitrine.

| Tarefa | Descrição | Recurso |
|------|-------------|----------|
| Acessar sua instância | Faça logon no Administrador do Commerce para gerenciar sua loja | [Acessar uma instância](#access-an-instance) |
| Explorar casos de uso | Conheça os cenários e workflows práticos de negócios | [Casos de uso](./use-cases.md) |
| Importar catálogo | Saiba como importar os dados do produto para a plataforma | [Importar seu catálogo](#import-your-catalog) |
| Acessar [!DNL AEM Assets] e [!DNL Product Visuals] (opcional) | Acesse o experience manager para começar a usar o [!DNL AEM Assets] e o [!DNL Product Visuals] | [Acessar a interface do Experience Manager](./user-management.md#access-the-experience-manager-interface) |

>[!TAB Desenvolvedor]

Como desenvolvedor, você precisa saber como criar integrações personalizadas e estender a funcionalidade da plataforma.

| Tarefa | Descrição | Recurso |
|------|-------------|----------|
| Entender a arquitetura | Saiba mais sobre a extensibilidade e as APIs da plataforma | [Visão geral - Plataforma do desenvolvedor](overview.md#developer-platform) |
| Configurar um ambiente de desenvolvimento | Criar uma instância de sandbox para desenvolvimento e teste | [Criar uma instância](#create-an-instance) |
| Criar loja | Saiba como configurar e personalizar a Commerce Storefront | [Configuração de vitrine](./storefront.md) |
| Configurar a loja | Saiba como configurar sua loja | [Configuração de vitrine](./storefront.md) |
| Explorar opções de integração | Saiba mais sobre o App Builder, a API Mesh e outras ferramentas de extensibilidade às quais você tem acesso | [Visão geral - Plataforma do desenvolvedor](overview.md#developer-platform) |
| Integrar [!DNL AEM Assets] e [!DNL Product Visuals] (opcional) | Saiba como integrar [!DNL AEM Assets] e [!DNL Product Visuals] a [!DNL Adobe Commerce] | [integração com o AEM Assets](../aem-assets-integration/overview.md) |

>[!ENDTABS]

### Próximas etapas

Depois de concluir suas tarefas de configuração específicas por função:

* **Administradores do sistema**: revise as [responsabilidades compartilhadas](shared-responsibility.md) diretrizes
* **Comerciantes**: Explore [casos de uso](use-cases.md) para ver cenários de negócios comuns
* **Desenvolvedores**: confira a [documentação do desenvolvedor do Adobe Commerce](https://developer.adobe.com/commerce/docs)

## Noções básicas do Adobe Commerce as a Cloud Service

As seções a seguir descrevem os processos básicos que você precisa concluir para colocar sua instância do Commerce em funcionamento.

### Criar uma instância

>[!NOTE]
>
>Antes de criar uma instância, o administrador de produto ou administrador de sistema da sua organização deve adicioná-lo como usuário do produto [!DNL Adobe Commerce as a Cloud Service]. Consulte [Adicionar usuários e administradores](./user-management.md#add-users-and-admins) para obter mais informações.

[!DNL Adobe Commerce as a Cloud Service] instâncias usam um sistema baseado em crédito. Você pode criar várias instâncias, mas cada instância requer créditos disponíveis. O número de créditos que você tem inicialmente depende da sua assinatura.

1. Faça logon em sua conta do [[!DNL Adobe Experience Cloud]](https://experience.adobe.com/).

1. Em [!UICONTROL Quick access], clique em [!UICONTROL **Commerce**] para abrir o [!UICONTROL Commerce Cloud Manager].

   O [!UICONTROL Commerce Cloud Manager] exibe uma lista de [!DNL Adobe Commerce as a Cloud Service] instâncias que estão disponíveis em sua organização do Adobe IMS.

1. Clique em [!UICONTROL **Adicionar instância**] no canto superior direito da tela.

   ![Botão Criar instância e campo de nome de instância no Commerce Cloud Manager](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Selecione [!UICONTROL **Commerce as a Cloud Service**].

1. Insira um **Nome** e uma **Descrição** para sua instância.

1. Escolha o [!UICONTROL **Tipo de Ambiente**] para sua instância. Você pode escolher entre as seguintes opções:

   * [!UICONTROL **Sandbox**] - Somente para fins de design e teste. Você deve iniciar a jornada [!DNL Adobe Commerce as a Cloud Service] usando o ambiente de sandbox.

   >[!NOTE]
   >
   > As instâncias de sandbox são somente para fins de design e teste. Você não deve usar dados de produção em um ambiente de sandbox.
   >
   >As instâncias de sandbox estão limitadas à região da América do Norte.

   * [!UICONTROL **Produção**] - Para lojas online e sites voltados para o cliente.

   >[!NOTE]
   >
   >A infraestrutura do Adobe Commerce as a Cloud Service está disponível globalmente. Para obter informações sobre ambientes de produção em sua região, entre em contato com o representante de atendimento ao cliente.

1. Selecione a região onde deseja que sua instância seja hospedada.

   >[!NOTE]
   >
   >Depois de criar a instância, você não poderá modificar a região.

1. Clique em [!UICONTROL **Adicionar instância**].

### Acessar uma instância

Após criar uma instância, você pode acessá-la pelo [!UICONTROL Commerce Cloud Manager].

1. Faça logon em sua conta do [Adobe Experience Cloud](https://experience.adobe.com/).

1. Em [!UICONTROL Quick access], clique em [!UICONTROL **Commerce**] para abrir o [!UICONTROL Commerce Cloud Manager].

   O [!UICONTROL Commerce Cloud Manager] exibe uma lista de instâncias que estão disponíveis em sua organização do Adobe IMS.

1. Para abrir o [!UICONTROL Commerce Admin] para uma instância, clique no nome da instância.

>[!TIP]
>
>Para ver informações sobre sua instância, incluindo os endpoints REST e GraphQL e o URL Admin, clique no ícone de informações ao lado do nome da instância.

Os URLs base do seu Administrador e pontos de extremidade diferem com base na região e no ambiente, usando o seguinte padrão:

* Admin
   * Administrador de produção da América do Norte: `https://na1.admin.commerce.adobe.com`
   * Administrador de sandbox da América do Norte: `https://na1-sandbox.admin.commerce.adobe.com`
   * Administrador de produção na Europa: `https://eu1.admin.commerce.adobe.com`
* REST e GRAPHQL
   * GraphQL de produção da América do Norte: `https://na1.api.commerce.adobe.com`
   * GraphQL de sandbox da América do Norte: `https://na1-sandbox.api.commerce.adobe.com`
   * GraphQL de produção na Europa: `https://eu1.api.commerce.adobe.com`

### Importar seu catálogo

Por padrão, [!DNL Adobe Commerce as a Cloud Service] instâncias não incluem dados de produtos. Você tem a opção de incluir dados de amostra do produto ao criar uma instância para fins de teste e aprendizado antes de importar seu próprio catálogo.

Há duas maneiras de importar seu catálogo para o [!DNL Adobe Commerce as a Cloud Service]:

* [**Administrador do Commerce**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Uma interface amigável que permite importar os dados do catálogo com apenas alguns cliques.
* [**Importar API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - Uma API REST que permite importar os dados do catálogo de forma programática.

### Configurar a loja

Agora que você criou uma instância, você está pronto para [configurar sua vitrine eletrônica](storefront.md) com a tecnologia do [!DNL Edge Delivery Services].

## Recursos adicionais

* [Notas de versão](release-notes.md)
* [Guia de migração](migration/overview.md)
* [Documentação da Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
