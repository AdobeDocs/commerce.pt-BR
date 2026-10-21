---
title: Visão geral da arquitetura do Commerce
description: Saiba mais sobre o modelo de produto do Adobe Commerce e onde encontrar opções de arquitetura detalhadas, vitrine e orientação sobre a API.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Visão geral da arquitetura do Commerce

As arquiteturas Adobe Commerce geralmente combinam três camadas: um back-end de comércio ([!DNL Adobe Commerce] ou [!DNL Adobe Commerce Optimizer]), uma vitrine e um conjunto de serviços e integrações conectados. Esta seção orienta você sobre o modelo do produto e o aponta para as comparações detalhadas, diagramas e referências de API mantidos em cada página dedicada.

## Introdução

| Seção | Use-o para |
| ------- | --------- |
| [Plataformas e serviços](../portfolio/platform-and-services.md) | Entenda o que é cada produto da Commerce: Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer e Adobe Commerce as a Cloud Service. |
| [Escolha uma opção do Commerce](../portfolio/choose-commerce-option.md) | Compare as opções do Commerce com base na propriedade da transação, no modelo de implantação e nas necessidades de comercialização. |
| [Opções de arquitetura](../architecture-options/implementation-architectures.md) | Compare detalhadamente todas as quatro arquiteturas compatíveis, incluindo diagramas de sistema e links de referência. |
| [Vitrines](../storefronts/overview.md) | Entenda as opções de vitrine e como elas se conectam a cada arquitetura. |
| [APIs](../apis/commerce-apis.md) | Compare as famílias de APIs usadas no Commerce Foundation, Storefront Services e Commerce Optimizer. |
| [Integração do AEM Assets para o Commerce](../aem-assets/aem-assets-integration.md) | Adicione gerenciamento de ativos digitais centralizado a qualquer arquitetura Commerce ou Otimizer. |
| [Migração e adoção](../migration-adoption/overview.md) | Planeje uma mudança entre arquiteturas ou uma adoção em fases do Adobe Commerce Optimizer. |

## Referência rápida de terminologia

| Termo preferencial | Significado | Evite usar como um rótulo de arquitetura atual |
| --- | --- | --- |
| **Commerce Foundation** | Recursos básicos de comércio e transacionais | Camada básica do Commerce e do PHP |
| **Serviços de vitrine** | APIs orientadas à loja para o Serviço de catálogo, o Live Search e as Recomendações de produto | Um rótulo limitado a apenas uma plataforma Commerce |
| **Serviços de merchandising da Commerce Optimizer** | APIs do Otimizer para descoberta de catálogos e experiências de comercialização | APIs do Commerce Foundation |
| **Commerce Storefront habilitada pela Edge Delivery Services** | Implementação de vitrine para o cliente | Uma família de API |

## Orientação relacionada

- [Arquiteturas de implementação](implementation-architectures.md)
- [Arquiteturas de referência](reference-architectures.md)
- [Criar uma nova loja](../implementation-guides/build-new-storefront.md)
