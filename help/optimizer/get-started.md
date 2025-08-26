---
title: Introdução
description: Saiba como começar a usar o  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 7a77cc79be9b6f835668b394909ea2325b642b03
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# Introdução

Este guia orienta você na configuração do [!DNL Adobe Commerce Optimizer] do início ao fim. Embora este guia cubra todas as funções, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/) para obter o conteúdo detalhado específico do desenvolvedor.

## Pré-requisitos

Antes de começar, verifique se você tem:

- **Conta da Adobe Experience Cloud** com [!DNL Adobe Commerce Optimizer] direitos
- **Acesso de administrador da organização** para criar instâncias e gerenciar usuários
- **Conta do GitHub** para carregar dados de amostra e desenvolvimento de vitrine
- **Noções básicas** sobre conceitos de comércio eletrônico

## Guia de início rápido

Siga estas etapas essenciais para executar o ambiente [!DNL Adobe Commerce Optimizer]:

### Etapa 1. Criar uma instância

1. Faça logon no [Adobe Experience Cloud](https://experience.adobe.com/).
1. Navegue até **Commerce** > **Commerce Cloud Manager**.
1. Clique em **Adicionar Instância** > **Commerce Optimizer**.

   ![Criar Instância](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Definir configurações de instância:
   - **Nome**: nome descritivo (por exemplo, &quot;Sandbox da minha empresa&quot;)
   - **Descrição**: breve descrição da finalidade
   - **Região**: selecione sua região preferencial
   - **Tipo de ambiente**: começar com um ambiente **Sandbox** para testes

1. Clique em **Adicionar instância**.

   A Cloud Manager é atualizada para incluir sua nova instância. Para obter detalhes sobre como acessá-lo e gerenciá-lo, consulte [Gerenciar uma instância](#manage-an-instance).

>[!NOTE]
>
>As instâncias de sandbox estão limitadas à região da América do Norte. Não é possível alterar a região após a criação.

### Etapa 2. Configurar o ambiente

Depois de criar sua instância:

1. [Gerencie sua instância](#manage-an-instance) pelo Commerce Cloud Manager.
1. Configure o acesso do usuário usando o [Guia de Gerenciamento de Usuários](./user-management.md).

### Etapa 3. Adicionar dados de amostra (opcional)

Para testes e aprendizado, siga as instruções em [Carregar Dados de Amostra](#add-sample-data).

## Fluxos de trabalho baseados em função

A configuração e o gerenciamento do [!DNL Adobe Commerce Optimizer] dependem de três funções principais. Cada função tem tarefas e responsabilidades específicas:

![Fluxo de Trabalho de Alto Nível](./assets/high-level-workflow.png){zoomable="yes"}

### Tarefas do administrador

Os administradores gerenciam instâncias, usuários e configurações organizacionais.

| Tarefa | Descrição | Link |
|---|---|---|
| **Gerenciar usuários** | Adicionar usuários, desenvolvedores e administradores | [Gerenciamento de usuários](./user-management.md) |
| **Criar instâncias** | Configurar ambientes de sandbox e produção | [Criar Instância](#create-an-instance) |
| **Gerenciar instâncias** | Verifique o status, atualize o nome e a descrição da instância e obtenha os URLs principais para acesso do aplicativo e da API | [Gerenciar instâncias](#manage-instances) |
| **Configurar Acesso** | Configurar exibições e políticas do catálogo | [Exibições do catálogo](./setup/catalog-view.md) |

### Tarefas do desenvolvedor

Os desenvolvedores lidam com a implementação técnica e a integração de dados, incluindo tarefas de arquitetura de plataforma.

| Tarefa | Descrição | Link |
|---|---|---|
| **Acessar o Developer Console** | Criar projetos e gerar credenciais | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Assimilar Dados do Catálogo** | Importar dados do produto de sistemas existentes | [API de assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) |
| **Configurar a vitrine eletrônica** | Configurar vitrine do Edge Delivery Services | [Instalação da Storefront](./storefront.md) |

### Tarefas do merchandiser

Os merchandisers otimizam e personalizam a experiência de compra por meio da descoberta de produtos e de recomendações. Eles também usam dados e análises do comprador para tomar decisões estratégicas sobre posicionamento de produtos, preços e promoções na loja.

| Tarefa | Descrição | Link |
|---|---|---|
| **Descoberta de Produto** | Configurar pesquisa e filtragem | [Visão geral do merchandising](./merchandising/overview.md) |
| **Recomendações** | Configurar recomendações de produtos alimentados por IA | [Recomendações de produto](./merchandising/recommendations/overview.md) |
| **Acompanhamento de Desempenho** | Monitorar métricas de sucesso | [Métricas de sucesso](./manage-results/success-metrics.md) |

## Gerenciar instâncias

Gerenciar instâncias no Commerce Cloud Manager.

>[!NOTE]
>
>Nem todos os usuários do Adobe Commerce Optimizer têm acesso ao Cloud Manager. O acesso depende da função e das permissões atribuídas à conta de usuário.

1. Faça logon no [Adobe Experience Cloud](https://experience.adobe.com/).

1. Abra o Commerce Cloud Manager:

   - Em **Acesso rápido**, clique em **Commerce**.
   - Visualize suas instâncias disponíveis.

### Pesquisar e filtrar instâncias

Depois de fazer logon, o painel mostra todas as instâncias de produtos do Commerce disponíveis na organização.
A coluna Product indica para qual aplicativo do Commerce a instância está provisionada.

![Pesquisa e filtro de instância](./assets/search-filter-instances.png){zoomable="yes"}

Use as ferramentas Filtro e Pesquisa para localizar rapidamente instâncias específicas por data de criação, região, criador, tipo de produto, ambiente ou status.

### Acessar o aplicativo [!DNL Adobe Commerce Optimizer]

Quando o aplicativo estiver aberto, alterne facilmente entre ambientes como sandbox e produção para visualizar dados e configurações para cada um sem retornar ao Commerce Cloud Manager.

1. No Commerce Cloud Manager, clique no nome da instância para abrir o aplicativo [!DNL Adobe Commerce Optimizer].

1. Alternar entre [!DNL Adobe Commerce Optimizer] instâncias sem sair do aplicativo.

   A lista suspensa de instâncias lista todas as instâncias do Otimizer disponíveis na organização. Selecione a instância a ser exibida.

   ![Alternador de Instância](./assets/context-switcher.png){zoomable="yes"}

### Obter detalhes da instância

Exiba os detalhes da instância clicando no ícone de informações ao lado do nome da instância.

![Detalhes da instância](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

Observe as seguintes informações principais:

- **Ponto de extremidade do GraphQL** para recuperar dados de catálogo do Commerce usando a API de merchandising
- **Ponto de extremidade do Serviço de Catálogo** para assimilação de dados usando a API REST
- **URL do Commerce Optimizer** para acessar o aplicativo [!DNL Adobe Commerce Optimizer]
- **ID da Instância** a ID de locatário exclusiva que identifica a instância

Se você for um desenvolvedor, precisará desses detalhes para configurar seu ambiente de desenvolvimento e se conectar às APIs do [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Para acessar os detalhes da instância, você deve ter as permissões necessárias em sua organização do Adobe IMS. Se você não vir os detalhes da instância ou não puder acessar o aplicativo, entre em contato com o administrador da organização.

### Editar nome e descrição da instância

Atualize o nome e a descrição da instância, conforme necessário.

1. Clique no ícone **Editar** ao lado do nome de uma instância.
1. Atualize o **Nome da instância** e a **Descrição** conforme necessário.
1. Clique em **Salvar**.

## Adicionar dados de amostra

A Adobe fornece um repositório GitHub com dados e ferramentas de exemplo para ajudá-lo a aprender e testar os recursos do [!DNL Adobe Commerce Optimizer].
Os dados de amostra são baseados no [cenário comercial do Carvelo](./use-case/admin-use-case.md) e incluem:

- Catálogo de produtos com peças automotivas
- Vários catálogos de preços e cenários de preços
- Exibições de catálogo e políticas para diferentes negociantes
- Exemplos completos de fluxos de trabalho

**Carregar os dados de exemplo:**

1. Acesse o [repositório GitHub da Assimilação de dados do catálogo de amostra](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion).

1. Siga as instruções de configuração no arquivo README do repositório para concluir as seguintes tarefas:

   - Configurar o ambiente
   - Concluir o processo de assimilação de dados
   - Criar exibições e políticas de catálogo usando os dados de amostra
   - Verifique a assimilação de dados verificando os dados do Serviço de Catálogo na página [Sincronização de Dados](./setup/data-sync.md)

## Próximas etapas

Após concluir a instalação:

1. Configurar a loja:
   - Configurar [vitrine do Edge Delivery Services](./storefront.md)
   - Conectar-se aos dados do catálogo

1. Conheça o caso de uso Carvelo:
   - Siga o [fluxo de trabalho completo](./use-case/admin-use-case.md)
   - Praticar com cenários reais

1. Configurar merchandising:
   - Configurar a [descoberta de produto](./merchandising/overview.md)
   - Criar [recomendações](./merchandising/recommendations/overview.md)

1. Monitorar desempenho:
   - Rastrear [métricas de sucesso](./manage-results/success-metrics.md)
   - Analisar [desempenho da pesquisa](./manage-results/search-performance.md)

## Solução de problemas

### Problemas comuns

| Problema | Solução |
|---|---|
| **Não é possível criar uma instância** | Verifique se você tem [!DNL Adobe Commerce Optimizer] direitos e permissões de administrador. |
| **Instância não aparecendo** | Verifique sua organização do Adobe IMS e atualize a página. |
| **Não é possível acessar a instância** | Verifique se você foi adicionado como usuário no Admin Console. |
| **Dados de exemplo não carregam** | Verifique as credenciais da instância e os endpoints da API. |

### Obter ajuda

- **Recursos do desenvolvedor**: [Documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/)
- **Recursos da vitrine**: [documentação da vitrine da Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR)
- **Tutoriais**: [Tutoriais do Commerce Optimizer](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)
- **Suporte**: [recursos de Suporte da Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/overview)
