---
title: Opções de arquitetura de implementação
description: Compare arquiteturas da Adobe Commerce, incluindo Commerce Foundation, Adobe Commerce as a Cloud Service, Conector do Otimizer e Otimizer independente.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%
---

# Opções de arquitetura de implementação

As arquiteturas de implementação do Adobe Commerce combinam três camadas: um back-end de comércio ([!DNL Adobe Commerce] ou [!DNL Adobe Commerce Optimizer]), uma vitrine e um conjunto de serviços e integrações conectados. Compare as seguintes opções para identificar qual sistema possui catálogo, preço, carrinho, check-out, pedidos e transações do cliente em cada arquitetura.

## Resumo das opções de arquitetura

Compare as opções por propriedade de transação e por experiência da loja.

### Plataforma e transações do Commerce

| Opção | Sistema de registro | Caminho da transação | Melhor ajuste |
| --- | --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]com o Commerce Foundation** | Commerce Foundation gerenciado pela Adobe | Serviços Commerce Foundation e Commerce conectados gerenciados | Clientes que desejam uma Commerce de software as a service (SaaS) gerenciada pela Adobe com propriedade reduzida de infraestrutura |
| **[!DNL Adobe Commerce]na nuvem ou no local com o[!DNL Adobe Commerce Optimizer Connector]** | Commerce Foundation existente, para dados e transações do Commerce | APIs existentes do Commerce Foundation e serviços de transação conectados | Clientes que desejam adicionar os recursos de descoberta e merchandising do Otimizer a uma implantação existente do [!DNL Adobe Commerce] |
| **Independente [!DNL Adobe Commerce Optimizer] com uma infraestrutura de comércio externo** | Plataforma de comércio existente ou de terceiros. Dados de catálogo e preço são adicionados ao Otimizer a partir de uma origem externa | API Mesh, App Builder ou integrações diretas conectam a loja a serviços de carrinho, checkout, cliente, pedido, pagamento, imposto, envio e atendimento de terceiros | Clientes que desejam recursos do Otimizer enquanto mantêm uma plataforma de comércio transacional existente ou de terceiros |
| **[!DNL Adobe Commerce]na nuvem ou no local com o Commerce Foundation** | Commerce Foundation | APIs do Commerce Foundation e integrações configuradas de pagamento, imposto, envio, inventário e preenchimento | Clientes que precisam da plataforma [!DNL Adobe Commerce] completa com controle de implantação na nuvem ou infraestrutura local |

### Experiência da vitrine

As vitrines se conectam a APIs do Commerce Foundation, Serviços de Vitrines ([!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations]) ou Serviços de Merchandising do [!DNL Adobe Commerce Optimizer].

| Opção | Experiência da vitrine | Caminho de dados da vitrine |
| --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]com o Commerce Foundation** | A Commerce Storefront é alimentada pela Edge Delivery Services ou por outra experiência headless compatível | Storefront Services, mais APIs do Commerce Foundation para dados principais da plataforma |
| **[!DNL Adobe Commerce]na nuvem ou no local com o[!DNL Adobe Commerce Optimizer Connector]** | Loja headless Edge Delivery Services ou personalizada usando experiências do Otimizer | Serviços de merchandising da Commerce Optimizer APIs da GraphQL para dados de catálogo e merchandising gerenciados pelo Otimizador |
| **Independente [!DNL Adobe Commerce Optimizer] com uma infraestrutura de comércio externo** | Commerce Storefront habilitada pela Edge Delivery Services ou uma loja headless personalizada | APIs GraphQL de Serviços de merchandising da Commerce Optimizer para dados de catálogo e merchandising |
| **[!DNL Adobe Commerce]na nuvem ou no local com o Commerce Foundation** | Edge Delivery Services, Luma, PWA ou loja headless personalizada | APIs do Commerce Foundation, mais Serviços da Storefront quando configurado |

## Adobe Commerce as a Cloud Service

![Diagrama de arquitetura do Adobe Commerce as a Cloud Service com Commerce Foundation gerenciado e Storefront Services alimentando uma Commerce Storefront](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Limite da chave**—O Adobe gerencia a plataforma Commerce Foundation. A arquitetura usa os Serviços da Loja, incluindo [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations], para experiências da loja. [!DNL Product Visuals] desenvolvido pela AEM Assets é uma integração SaaS opcional. Consulte [Integração do AEM Assets para o Commerce](../aem-assets/aem-assets-integration.md).

**Referências:**

- [Visão geral das [!DNL Adobe Commerce as a Cloud Service]](/help/cloud-service/overview.md)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Esquema do GraphQL de Serviços da Storefront](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce com Commerce Foundation

![Diagrama de arquitetura do Adobe Commerce na nuvem ou no local com as APIs do Storefront Services e do Commerce Foundation, alimentando uma loja da Commerce](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Limite de chave** — o Commerce Foundation é proprietário da plataforma Commerce e dos fluxos de transação. [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations] fornecem acesso otimizado à loja para catálogo, pesquisa e recomendações quando configuradas. A integração do AEM Assets é opcional. Consulte [Integração do AEM Assets para o Commerce](../aem-assets/aem-assets-integration.md).

**Referências:**

- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [API do Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/)
- [Esquema do GraphQL de Serviços da Storefront](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Adobe Commerce com o conector do Otimizer

![Diagrama de arquitetura do Conector do Adobe Commerce Optimizer sincronizando dados de catálogo e preço do Adobe Commerce com a Adobe Commerce Optimizer, alimentando uma Commerce Storefront por meio de APIs de serviços de merchandising](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**Limite de chave** — o Conector sincroniza dados de catálogo e preço de [!DNL Adobe Commerce] para [!DNL Adobe Commerce Optimizer]. [!DNL Adobe Commerce] permanece como o sistema de transações, enquanto o Otimizer fornece experiências de descoberta e comercialização por meio de suas APIs de Serviços de Merchandising.

**Referências:**

- [Integrações do Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md)
- [Serviços de merchandising da Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [API do Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Commerce Optimizer independente com back-end de terceiros

![Diagrama de arquitetura de sistemas de origem de propriedade do cliente enviando dados de catálogo e preço por meio da Assimilação de dados para uma Adobe Commerce Optimizer autônoma, alimentando uma Commerce Storefront conectada a uma infraestrutura comercial de terceiros](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**Limite de chave**—O [!DNL Adobe Commerce Optimizer] independente possui experiências de merchandising e descoberta de catálogos, mas não o back-end transacional do Commerce. Os dados de catálogo e preço são inseridos por meio da API REST de assimilação de dados. A loja da Edge Delivery Services usa APIs do GraphQL de serviços de merchandising para experiências de produtos e se conecta ao back-end de terceiros para carrinho e check-out.

**Referências:**

- [O que é o Adobe Commerce Optimizer?](/help/optimizer/overview.md)
- [Assimilação de dados Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Serviços de merchandising da Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Referência rápida de terminologia

| Termo preferencial | Significado | Evite usar como um rótulo de arquitetura atual |
| --- | --- | --- |
| **Commerce Foundation** | Recursos básicos de comércio e transacionais | Núcleo Commerce, Camada de base PHP |
| **Serviços de vitrine** | APIs orientadas à loja para o Serviço de catálogo, o Live Search e as Recomendações de produto | Um rótulo limitado a apenas uma plataforma Commerce |
| **Serviços de merchandising da Commerce Optimizer** | APIs do Otimizer para descoberta de catálogos e experiências de comercialização | APIs do Commerce Foundation |
| **Commerce Storefront habilitada pela Edge Delivery Services** | Implementação de vitrine para o cliente | Uma família de API |

## Orientação relacionada

- [Arquiteturas de referência](reference-architectures.md)
- [Escolha uma opção do Commerce](../portfolio/choose-commerce-option.md)
- [Vitrines](../storefronts/overview.md)
- [APIs](../apis/commerce-apis.md)
