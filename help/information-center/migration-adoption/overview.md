---
title: Migração e adoção
description: Saiba mais sobre as rotas de adoção do Adobe Commerce Optimizer, modernização de uma loja existente ou migração completa para o Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
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
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# Migração e adoção

A adoção não precisa ser uma mudança única e completa da plataforma. Selecione uma rota com base no fato de sua meta imediata ser a modernização da loja, a melhoria de merchandising, a modernização do back-end ou uma mudança completa para o software gerenciado como um serviço (SaaS).

## Rotas de adoção

### Modernizar a implantação existente do Adobe Commerce

- Mantenha a Commerce Foundation existente como back-end transacional.
- Adote a Commerce Storefront viabilizada por [!DNL Edge Delivery Services].
- Use o Storefront Services, o App Builder, a API Mesh e uma integração opcional do AEM Assets.

### Usar o Commerce Optimizer como uma ponte

- Conecte a nuvem [!DNL Adobe Commerce] ou no local usando o [!DNL Adobe Commerce Optimizer Connector].
- Adote serviços de merchandising, detecção, recomendações e uma vitrine da Edge Delivery Services.
- Mantenha [!DNL Adobe Commerce] como o sistema principal de registro de produtos, preços, estrutura de catálogo, carrinho, check-out, clientes e pedidos.
- Use esta arquitetura como uma possível transição para [!DNL Adobe Commerce as a Cloud Service].

### Migrar totalmente para o Adobe Commerce as a Cloud Service

- Avalie o aplicativo atual, as personalizações, as integrações, a loja e os dados.
- Modernizar personalizações usando padrões de extensibilidade compatíveis com SaaS.
- Reconstrua ou adapte a loja e as integrações.
- Migrar e validar o catálogo, os clientes, os pedidos, a configuração e os dados personalizados compatíveis.
- Teste, corte e opere o novo ambiente SaaS.

### Adotar o Adobe Commerce Optimizer independente

- Assimilar dados de catálogo e preço de uma plataforma Commerce de terceiros, PIM, ERP ou outra fonte.
- Use os Serviços de merchandising do [!DNL Adobe Commerce Optimizer] para recuperação de catálogo, descoberta, recomendações e merchandising.
- Use a Commerce Storefront habilitada por [!DNL Edge Delivery Services].
- Mantenha o carrinho, o checkout, os clientes, os pedidos, os pagamentos, os impostos, a remessa e o atendimento nos sistemas de terceiros conectados.

## Sequência recomendada

1. Avalie o estado atual e defina a propriedade do sistema.
1. Estabeleça limites de integração de API primeiro.
1. Modernize a vitrine e a camada de experiência.
1. Adote serviços de merchandising e AEM Assets em paralelo.
1. Migre o Commerce Foundation quando necessário.
1. Validar, cortar, monitorar e otimizar.

## Orientação relacionada

- [Escolha uma opção do Commerce](../portfolio/choose-commerce-option.md)
- [Opções de arquitetura](../architecture-options/overview.md)
- [Modernizar uma vitrine existente](../implementation-guides/modernize-storefront.md)
- [Ativar o Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
