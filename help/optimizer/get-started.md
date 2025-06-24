---
title: Introdução
description: Saiba como começar a usar o  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Introdução

Este artigo mostra como se atualizar com o [!DNL Adobe Commerce Optimizer]. Embora este guia se concentre nas funções de merchandiser e administrador, ele inclui tarefas breves de alto nível que um desenvolvedor executaria. Consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog/) para obter o conteúdo detalhado específico do desenvolvedor.

## Qual é a sua função?

A configuração bem-sucedida do [!DNL Adobe Commerce Optimizer] geralmente envolve os seguintes membros da equipe:

- Administrador
- Desenvolvedor
- Merchandiser

Cada membro da equipe tem seu próprio conjunto de funções e responsabilidades, conforme descrito na tabela a seguir:

| Função(ões) | Tarefa |
|---|---|
| Administrador | Use o Admin Console para criar administradores, grupos de usuários, usuários e desenvolvedores&#x200B;. |
|  | Crie uma nova instância [!DNL Adobe Commerce Optimizer] no Commerce Cloud Manager.&#x200B; |
|  | Configure suas políticas e visualizações do catálogo. |
| Desenvolvedor | Use o Developer Console para criar um projeto, conceder acesso à API dos desenvolvedores e instalar os aplicativos e as personalizações necessários. |
|  | Conecte-se ao sistema de back office (carrinho, check-out) usando a API Mesh e o App Builder&#x200B;. |
|  | Assimile os dados do catálogo de suas soluções comerciais existentes usando a API de assimilação de dados dos serviços de merchandising&#x200B; |
|  | Configurar a loja |
| Merchandiser | Configurar a descoberta de produtos&#x200B;. |
|  | Configurar recomendações de produto. |

Cada função desempenha uma parte integral na integração e inicialização bem-sucedidas do ambiente do [!DNL Adobe Commerce Optimizer]. O diagrama a seguir mostra um fluxo de trabalho de alto nível do início ao fim para cada função na organização:

![Fluxo de Trabalho de Alto Nível](./assets/high-level-workflow.png){zoomable="yes"}

### Administrador

Os administradores são responsáveis por configurar instâncias, gerenciar usuários, grupos e direitos para sua organização.

- **[Acesse o Adobe Admin Console](https://helpx.adobe.com/br/enterprise/admin-guide.html)** - Gerenciar Direitos do Adobe em toda a organização. Consulte [gerenciamento de usuários](./user-management.md) para saber como você, o administrador de produtos ou o administrador de sistemas de sua organização pode adicionar usuários ao produto [!DNL Adobe Commerce Optimizer].

- **Criar uma instância** - [!DNL Adobe Commerce Optimizer] instâncias usam um sistema baseado em crédito. É possível criar várias instâncias de Sandbox e Produção, com cada instância exigindo um crédito correspondente. A quantidade de créditos que você tem inicialmente depende de sua assinatura. [Saiba mais](#create-an-instance).

- **Acessar uma instância** - Depois de criar uma instância, você pode acessá-la pelo [!UICONTROL Commerce Cloud Manager]. [Saiba mais](#access-an-instance).

- **Configurar políticas e exibições de catálogo** - Saiba como [definir suas políticas e exibições de catálogo](./setup/catalog-view.md). O catálogo não só contém os dados do produto, como também ajuda a definir a estrutura de negócios.

### Desenvolvedor

Os desenvolvedores criam projetos e credenciais, instalam extensões, assimilam dados de catálogo e executam tarefas gerais de arquitetura da plataforma. Consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog/) para obter o conteúdo detalhado específico do desenvolvedor.

- **Acessar o Developer Console** - Acesse o [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) para criar um projeto para o [!DNL Adobe Commerce Optimizer], gerar tokens de acesso e instalar os aplicativos e as personalizações necessários.

- **Assimilar dados de catálogo** - Consulte a documentação da [API de assimilação de dados](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) para saber como importar dados de catálogo para o [!DNL Adobe Commerce Optimizer].

  Os dados do catálogo assimilados estão visíveis na página [sincronização de dados](./setup/data-sync.md).

- **Configurar a loja** - Antes de configurar a loja, primeiro crie uma instância, que é uma tarefa normalmente executada pelo [administrador](#administrator) da sua organização. Com sua instância criada, você está pronto para continuar com a [configuração](./storefront.md) da sua Commerce Storefront habilitada pela Edge Delivery Services.

### Merchandiser

O merchandiser usa dados e análises do comprador para tomar decisões estratégicas sobre posicionamento de produtos, preços e promoções na loja, além de otimizar as experiências de compra por meio da descoberta de produtos e de recomendações.

- **Configurar a descoberta e as recomendações de produtos** - Saiba como [criar experiências personalizadas](./merchandising/overview.md) para seus compradores por meio de recomendações e descobertas de produtos.

## Criar uma instância

1. Faça logon em sua conta do [Adobe Experience Cloud](https://experience.adobe.com/).

1. Em [!UICONTROL Quick access], clique em [!UICONTROL **Commerce**] para abrir o [!UICONTROL Commerce Cloud Manager].

   O [!UICONTROL Commerce Cloud Manager] exibe uma lista de [!DNL Adobe Commerce] instâncias que estão disponíveis em sua organização do Adobe IMS, incluindo ambas as instâncias provisionadas para [!DNL Adobe Commerce Optimizer] e [!DNL Adobe Commerce as a Cloud Service].

1. Clique em [!UICONTROL **Adicionar instância**] no canto superior direito da tela.

   ![Criar Instância](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. Selecione [!UICONTROL **Commerce Optimizer**].

1. Insira um **Nome** e uma **Descrição** para sua instância.

1. Selecione a região onde deseja que sua instância seja hospedada.

   >[!NOTE]
   >
   >Após criar uma instância, não é possível alterar a região.

1. Escolha um dos [!UICONTROL **Tipos de Ambiente**] a seguir para sua instância:

   - [!UICONTROL **Sandbox**] - Ideal para fins de design e teste. Você deve iniciar a jornada [!DNL Adobe Commerce Optimizer] usando o ambiente de sandbox.
   - [!UICONTROL **Produção**] - Para lojas online e sites voltados para o cliente.

   >[!NOTE]
   >
   >Atualmente, as instâncias de sandbox estão limitadas à região da América do Norte.

1. Clique em [!UICONTROL **Adicionar instância**].

   A nova instância agora está disponível no Cloud Manager.

1. Para exibir detalhes da instância, incluindo os endpoints do GraphQL e do Serviço de Catálogo, o URL para acessar o aplicativo do Adobe Commerce Optimizer e o ID da Instância (ID do locatário), clique no ícone de informações ao lado do nome da instância.

   ![Criar Instância](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## Acessar uma instância

1. Faça logon em sua conta do [Adobe Experience Cloud](https://experience.adobe.com/).

1. Em [!UICONTROL Quick access], clique em [!UICONTROL **Commerce**] para abrir o [!UICONTROL Commerce Cloud Manager].

   O [!UICONTROL Commerce Cloud Manager] exibe uma lista de instâncias que estão disponíveis em sua organização do Adobe IMS.

1. Para abrir o aplicativo [!UICONTROL Commerce Optimizer] associado a uma instância, clique no nome da instância.


