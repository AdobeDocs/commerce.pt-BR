---
title: Conector do Adobe Commerce Optimizer para Commerce
description: Saiba como conectar seus dados da nuvem do Commerce ou do projeto local à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
hidefromtoc: true
hide: true
source-git-commit: 5d0cfb2c389bf11f89815e7d1fbc2861a6b48962
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---


# Visão geral

O Adobe Commerce Connector é a ponte de integração que sincroniza os dados de catálogo e preço entre uma Adobe Commerce Cloud existente na nuvem ou implantação local e um modelo de dados de catálogo combinável do Adobe Commerce Optimizer. Isso habilita recursos como pesquisa de IA dinâmica, recomendações, headless de carregamento rápido, incluindo vitrines do Adobe Commerce no Edge Delivery Services e análise de desempenho em tempo real.

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

## Arquitetura e experiência

O Adobe Commerce Connector opera mapeando a hierarquia de catálogo `website/store/storeview` do Commerce para o modelo de dados `channel/policy/source` do Adobe Commerce Optimizer.

Em vez de configurar e gerenciar os Serviços da Commerce (Live Search e Recomendações de Produtos) com o Administrador da Commerce, você usa as [ferramentas de Merchandising da Adobe Commerce Optimizer](../optimizer/merchandising/overview.md) para gerenciar a descoberta de produtos (Live Search) e a configuração de regras de recomendações (Recomendações de Produtos).  A instância do Adobe Commerce se torna a origem de dados para dados de catálogo e preço. Quando os dados são atualizados no Commerce, as atualizações são sincronizadas com a instância do Adobe Commerce Optimizer.

## Fluxos de trabalhos

O Conector permite vários workflows principais:

* **Exportar dados do catálogo do Commerce para o Adobe Commerce Optimizer**—os dados do catálogo de preços e preços são exportados no nível `website`. Os dados de atributos do produto e do produto são exportados no nível `store view`. Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites e exibições de loja).

  Para habilitar este fluxo de trabalho, use o Composer para instalar a extensão PHP `adobe-commerce/commerce-data-export-aco-adapter` e forneça as credenciais IMS para autenticar a conexão entre o projeto Commerce.

* **Mapear os dados do Commerce `website/store/storeview` para exportar para o Adobe Commerce Optimizer**

  Você tem a opção de personalizar as configurações do exportador do Adobe Commerce Optimizer para exportar dados apenas para escopos específicos, atualizando a configuração do exportador a partir da grade de Armazenamento em Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* **Configuração e gerenciamento da regra de merchandising**

  Quando o Conector está habilitado, as regras de merchandising para descoberta de produtos e recomendações são definidas e gerenciadas na interface do usuário do Adobe Commerce Optimizer, não nas páginas [!UICONTROL Live Search] e [!UICONTROL Product Recommendations] do Administrador do Commerce.

* **Implantar a Commerce Storefront no Edge Delivery Services**

  Depois de configurar a integração com o Adobe Commerce Optimizer, você pode configurar e implantar uma Commerce Storefront nos serviços da Edge Delivery para fornecer desempenho ultrarrápido, escalabilidade, criação contínua de conteúdo, personalização integrada e custos operacionais reduzidos usando a arquitetura combinável, orientada por API e os componentes modulares disponíveis com o Adobe Commerce Optimizer.

## Requisitos para usar a integração

* Adobe Commerce 2.4.5+

   * PHP 8.1, 8.2, 8.3 ou 8.4
   * Composer 2.x

* Licença do Adobe Commerce Optimizer com uma instância de sandbox provisionada.

* Acesse o [repo.magento.com](https://repo.magento.com) para baixar o metapackage do Conector Commerce usando o Composer.

* Acesso de administrador a uma [instância da sandbox do Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

O usuário do Adobe Commerce que configura a integração deve ter:

* Acesso de administrador ao Administrador do Adobe Commerce.

* [Acesso de linha de comando ao servidor de aplicativos do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Acesso de desenvolvedor à [Organização IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) onde o projeto do Adobe Commerce Optimizer é provisionado.

## Introdução

1. **Configurar a integração**

   1. [Instalar o pacote Commerce Connector](#install-the-commerce-connector-package).

   1. [Obtenha os valores necessários para configurar a conexão com o Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Habilitar a integração com o Adobe Commerce Optimizer](#enable-the-adobe-commerce-optimizer-integration).

   1. [Verifique se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working).

   1. [Personalizar a configuração de exportação de dados](#customize-commerce-data-export-configuration) (opcional).

1. **[Configurar lojas Adobe Commerce Optimizer](#configure-adobe-commerce-optimizer-stores)**

1. **[Configurar uma Commerce Storefront no Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Instale o pacote Commerce Connector

O metapackage do Adobe Commerce Connector Composer está disponível para todos os comerciantes do Commerce com uma licença ativa para o Adobe Commerce Optimizer.

### Etapas de instalação

1. Adicionar o módulo `adobe-commerce/commerce-data-export-aco-adapter` usando o Composer:

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. Implante as alterações no ambiente de preparo do Adobe Commerce.

Depois que as alterações são implantadas, a opção Commerce Optimizer Otimizer fica disponível no menu Admin do Commerce.

>[!NOTE]
>
>Para obter instruções detalhadas sobre a instalação de extensões, consulte os guias a seguir:
>
>[Instalar extensão no Adobe Commerce na Infraestrutura em Nuvem](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Instalar Adobe Commerce de extensão no local](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Obter os valores necessários para configurar a conexão do Commerce Optimizer

### Obter credenciais de API

>[!NOTE]
>
>Se você já tiver um projeto do App Builder Developer na organização IMS em que a instância do Commerce Optimizer está implantada, poderá obter as credenciais da API e a ID da organização necessárias das credenciais de servidor para servidor OAUTH nesse projeto.

Crie um novo projeto de desenvolvedor no console do Adobe Developer para obter credenciais de API e configurar a integração entre instâncias do Commerce e do Commerce Optimizer. Para obter instruções, consulte [Criar um projeto do App Builder](https://developer.adobe.com/commerce/extensibility/events/project-setup/) na documentação do desenvolvedor.

Depois de criar o projeto, salve os seguintes valores da página de credenciais de servidor para servidor do OAUTH:

* **ID da Organização** (`org_id`)

* **IMS `client_id` e`client_secret`**

### Obter detalhes da instância do Adobe Commerce Optimizer

Salve os seguintes valores dos detalhes da instância do Adobe Commerce Optimizer.

* **ID da instância—**&#x200B;O identificador exclusivo da instância do Adobe Commerce Optimizer. Também conhecida como ID do locatário.

  Obtenha a ID da instância do URL para acessar sua instância do Adobe Commerce Optimizer. Por exemplo, na URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, a ID da instância é `1234567890abcdef`.

* **Região —**&#x200B;A região em que sua instância da sandbox da Adobe Commerce Optimizer está hospedada.

  Obtenha a região no URL do Adobe Commerce Optimizer. Por exemplo, na URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, a região é `na1`.

## Habilitar a integração do Adobe Commerce Optimizer

>[!IMPORTANT]
>
>O processamento da sincronização de dados é iniciado conforme você executa o comando de configuração. Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites e exibições de loja). Dependendo do tamanho do catálogo, o processo de sincronização de dados pode levar muitas horas.

Usando as credenciais da API e os detalhes da instância coletados nas etapas anteriores, agora é possível configurar a integração entre as instâncias do Commerce e do Adobe Commerce Optimizer.

1. No Administrador do Commerce, selecione **[!UICONTROL Adobe Commerce Optimizer]** para exibir a página de configuração com instruções.

   ![Página de configuração do Adobe Commerce Optimizer](../assets/aco-connector-config-page.png)

1. Na linha de comando, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para se conectar ao ambiente de preparo do Commerce.

1. Execute o seguinte comando da CLI do Commerce para configurar a integração, substituindo os valores de espaço reservado pelos valores do seu projeto do Commerce Optimizer:

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Verifique a conexão retornando ao Administrador do Commerce e selecionando a opção [!UICONTROL Adobe Commerce Optimizer].

   Ao clicar na opção, ela abre a interface do usuário do Adobe Commerce Optimizer em uma nova guia.

## Verifique se a sincronização de dados está funcionando

Você pode verificar a sincronização de dados do Commerce Admin e do Commerce Optimizer.

* A **[página Status de sincronização do feed de dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** mostra o progresso da sincronização dos dados de catálogo do Commerce com o Adobe Commerce Optimizer.

* A página **[[!UICONTROL Data Sync]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)** no Adobe Commerce Optimizer mostra os dados de catálogo transferidos da sua instância do Commerce.

1. Verifique se os dados do catálogo estão fluindo do Commerce para o Commerce Optimizer:

   No Administrador do Commerce, abra a página [!UICONTROL Data Feed Sync Status] selecionando [!UICONTROL System] **&#x200B; > [!UICONTROL Data Transfer] > &#x200B;** [!UICONTROL Data Feed Sync Status]**.

   ![Página Status da sincronização do feed de dados com relatórios de status do item de feed](./assets/data-feed-sync-status.png)

   Se a sincronização de dados tiver sido iniciada, os dados do feed mostrarão os registros enviados com êxito. Você também pode visualizar e solucionar problemas de sincronização visualizando os detalhes de cada feed.

1. Verifique se o Adobe Commerce Optimizer está recebendo os dados do catálogo:

   No menu Commerce Optimizer, selecione **[!UICONTROL Data Sync]** para abrir a página Sincronização de Dados.

   ![Sincronização de Dados](./assets/data-sync.png)

### Solução de problemas

Se a sincronização de dados não tiver sido iniciada, verifique se os índices do catálogo são válidos. Se os índices forem inválidos, execute o seguinte comando na Commerce CLI para reindexar os dados do catálogo:

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Personalizar a configuração da exportação de dados do Commerce

Você tem a opção de personalizar as configurações do exportador do Adobe Commerce Optimizer para exportar dados apenas para escopos específicos, atualizando a configuração do exportador a partir da grade de Armazenamento em Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* No nível `website`, desabilitar a configuração do exportador interrompe a exportação de preços e dados do catálogo de preços para o Adobe Commerce Optimizer.

* No nível `storeview`, desabilitar a configuração do exportador interrompe a exportação de produtos e atributos do produto para o Adobe Commerce Optimizer.

Quando a configuração é alterada, os índices correspondentes são invalidados para acionar a reexportação das entidades afetadas.

## Configurar lojas Adobe Commerce Optimizer

Configure lojas Adobe Commerce Optimizer criando visualizações e políticas de catálogo&#x200B; Consulte [Criação de Exibições de Catálogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) no Guia do Adobe Commerce Optimizer.

Observe que os catálogos de preços são criados automaticamente a partir dos grupos de clientes do Adobe Commerce.

## Configurar uma vitrine eletrônica do Commerce no Edge Delivery Services

Esta seção fornece uma visão geral de alto nível das etapas necessárias para configurar sua loja do Commerce. Informações detalhadas estão disponíveis no site de documentação da [Adobe Commerce Storefront] (https://experienceleague.adobe.com/developer/commerce/storefront/).

1. Clone e implante o modelo padrão da Adobe Commerce Storefront no EDS usando a [ferramenta do Site Creator](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. [Configurar um ambiente de desenvolvimento local](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment).

1. [Instalar pacote de Compatibilidade da GraphQL Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).&#x200B;

1. [Configurar cabeçalhos CORS para a instância do Commerce no ambiente de nuvem](#configure-cors-headers-for-commerce-instance).

1. [Conecte a vitrine às fontes de dados do Commerce](#connect-the-storefront-to-commerce-data-sources).

### Configurar cabeçalhos do CORS para a instância do Commerce

Para permitir que as solicitações do GraphQL venham de uma loja do Edge Delivery Services (EDS) para o Adobe Commerce em um ambiente de nuvem ou local, use uma das seguintes opções para adicionar cabeçalhos específicos do Compartilhamento de recursos entre origens (CORS) aos endpoints do Adobe Commerce GraphQL.&#x200B;

1. Adicione cabeçalhos CORS (Cross-Origin Resource Sharing, Compartilhamento de recursos entre origens) aos endpoints do Adobe Commerce GraphQL.&#x200B;

   **Opção 1: implemente um módulo personalizado PHP para que o Adobe Commerce Foundation possa adicionar cabeçalhos CORS.&#x200B;**

   **Opção 2: instalar um módulo de comunidade de terceiros graycore/magento2-cors&#x200B;** - Consulte a [configuração do CORS](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/) na documentação da *Adobe Commerce Storefront*.

1. Adicione as seguintes variáveis do CORS ao arquivo de configuração de ambiente do Commerce na instância da nuvem `app.yaml`:

   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_HEADERS: *`
   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_ORIGINS: *`

### Conectar a loja a fontes de dados do Commerce

No repositório GitHub do código de modelo padrão da Loja, atualize o arquivo de configuração da vitrine eletrônica, `config.json` com os seguintes parâmetros:

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"` - Obtenha este valor na [página de detalhes da instância do Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/get-started#get-instance-details)&#x200B;

* `"AC-Environment-Id": "Customer organization ID"` - Obter este valor do [projeto de nuvem do Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/overview#project-overview)

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` - Obtenha esse valor do Administrador do Adobe Commerce Optimizer.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` — Obtenha esse valor do administrador do Adobe Commerce Optimizer.&#x200B;

* `"AC-Source-Locale": "Catalog source – Store View code from Commerce cloud instance"`

Para obter mais informações, consulte [Configuração da vitrine eletrônica](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) na documentação da *Vitrine da Adobe Commerce*.


