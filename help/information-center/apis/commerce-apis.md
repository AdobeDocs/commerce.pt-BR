---
title: APIs do Commerce
description: Compare as famílias de APIs da Adobe Commerce, incluindo Commerce Foundation, Storefront Services, Commerce Optimizer Merchandising Services e Assimilação de dados.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
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
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# APIs

| Família API | Finalidade principal | Usado por |
| --- | --- | --- |
| **APIs do Commerce Foundation GraphQL** | Principais recursos comerciais e transacionais, como operações de catálogo, carrinho, check-out, clientes e pedidos | [!DNL Adobe Commerce] na nuvem, [!DNL Adobe Commerce] no local e [!DNL Adobe Commerce as a Cloud Service] |
| **APIs do GraphQL de Serviços da Loja** | Experiências de catálogo, pesquisa e recomendação orientadas para vitrines por meio de [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations] | [!DNL Adobe Commerce] na nuvem ou no local com serviços configurados e [!DNL Adobe Commerce as a Cloud Service] |
| **APIs da GraphQL de serviços de merchandising da Commerce Optimizer** | Recuperar resultados de catálogo gerenciado pelo Otimizador, exibições de catálogo, contextos de preço, pesquisa, recomendações e merchandising | [!DNL Adobe Commerce] na Nuvem ou no local com o Conector do Otimizador e [!DNL Adobe Commerce Optimizer] autônomo |
| **API REST de Assimilação de Dados Commerce Optimizer** | Adicionar dados de catálogo e preço a uma implementação [!DNL Adobe Commerce Optimizer] independente | Autônomo [!DNL Adobe Commerce Optimizer] conectado a uma fonte de dados externa |

## APIs do Commerce Foundation GraphQL

Principais recursos de comércio, incluindo catálogo, carrinho, check-out, clientes e pedidos. Usado por [!DNL Adobe Commerce] na Nuvem, [!DNL Adobe Commerce] no local e [!DNL Adobe Commerce as a Cloud Service]. Consulte a [API do Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/).

## APIs do GraphQL para serviços de vitrine

Experiências de catálogo, pesquisa e recomendação orientadas à loja até [!DNL Catalog Service], [!DNL Live Search] e [!DNL Product Recommendations]. Usado por [!DNL Adobe Commerce] na nuvem, no local e [!DNL Adobe Commerce as a Cloud Service]. Consulte o [esquema GraphQL do Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## APIs do GraphQL para os serviços de merchandising da Commerce Optimizer

Recupere resultados de catálogo gerenciado pelo Otimizador, exibições de catálogo, contextos de preço, pesquisa, recomendações e merchandising. Usado por [!DNL Adobe Commerce] na Nuvem, no local com [!DNL Adobe Commerce Optimizer Connector] e autônomo [!DNL Adobe Commerce Optimizer]. Consulte [Serviços de merchandising da Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/).

## APIs REST de assimilação de dados do Commerce Optimizer

Adicionar dados de catálogo e preço a uma implementação [!DNL Adobe Commerce Optimizer] independente de uma fonte de dados externa. Consulte [Assimilação de dados Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).

## Integrações do Commerce Optimizer

O [!DNL Adobe Commerce Optimizer] se conecta a outros sistemas por meio de vários caminhos de integração, dependendo se está emparelhado com o [!DNL Adobe Commerce] ou com um back-end de terceiros.

### Adobe Commerce Optimizer Connector

Sincroniza dados de catálogo e preço de [!DNL Adobe Commerce] na Nuvem ou no local para [!DNL Adobe Commerce Optimizer], mantendo [!DNL Adobe Commerce] como o sistema de transação enquanto o Otimizer fornece descoberta e merchandising. Consulte [Integrações do Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md).

### Integrações de comércio de terceiros

Assimila dados de catálogo e preço de uma plataforma de comércio de terceiros, PIM, ERP ou outra origem no [!DNL Adobe Commerce Optimizer] independente por meio da API REST de Assimilação de dados, enquanto a plataforma de terceiros permanece como o sistema transacional de registro.

### API Mesh e App Builder

Use o API Mesh para orquestrar APIs do Adobe Commerce com APIs privadas ou de terceiros. Use o Adobe Developer App Builder para criar aplicativos e integrações personalizados. Para obter orientação sobre extensibilidade relacionada ao Commerce, consulte [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) e [Adobe Commerce extensibility](https://developer.adobe.com/commerce/extensibility/).

Para integrações orientadas por eventos, consulte [Adobe I/O Events for Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events).


### Entrega do carrinho e do check-out

Para o [!DNL Adobe Commerce Optimizer] autônomo com um back-end externo, a loja usa APIs do GraphQL de Serviços de Merchandising para experiências de produtos e, em seguida, entrega o carrinho, check-out, cliente, pedido, pagamento, imposto, envio e preenchimento para o back-end por meio da API Mesh, App Builder ou integração direta.

### AEM Assets

O AEM Assets é uma integração opcional de gerenciamento de ativos digitais que pode ser adicionada a qualquer arquitetura Commerce ou Otimizer, em vez de a um caminho de integração separado. Consulte [Integração do AEM Assets para o Commerce](../aem-assets/aem-assets-integration.md).

## Orientação relacionada

- [Visão geral da arquitetura](../architecture-options/overview.md)
- [Vitrines](../storefronts/overview.md)
- [Integração do AEM Assets para o Commerce](../aem-assets/aem-assets-integration.md)
