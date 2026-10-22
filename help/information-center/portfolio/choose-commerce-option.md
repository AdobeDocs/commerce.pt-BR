---
title: Escolha uma opção do Commerce
description: Compare as arquiteturas do Adobe Commerce com base na propriedade de transações, no modelo de implantação e nas necessidades de comercialização.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
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
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# Escolha uma opção do Commerce

Comece identificando qual sistema possui o carrinho, o checkout, os pedidos e outras transações. Em seguida, escolha o caminho de merchandising que se adapta a esse back-end.

## Perguntas para orientar sua decisão

Use as seguintes perguntas para identificar quais opções serão avaliadas. Considere seu back-end de comércio existente, quanta responsabilidade de infraestrutura você deseja manter e se é necessário melhorar a descoberta de produtos e o merchandising. A Adobe Commerce Optimizer fornece recursos de detecção e comercialização. Ele não substitui o back-end que lida com transações.

1. **Deseja que a Adobe gerencie a plataforma Commerce como software as a service (SaaS)?**
   - Sim: avalie o Adobe Commerce as a Cloud Service.
   - Não: se você precisar do Adobe Commerce e quiser manter o controle sobre sua infraestrutura em nuvem ou local, avalie o Adobe Commerce na nuvem ou no local.
1. **Você precisa do Adobe Commerce para manipular carrinhos, check-out, pedidos e outras transações?**
   - Sim: avaliar o Adobe Commerce na nuvem ou no local, ou o Adobe Commerce as a Cloud Service. Essas opções usam o Commerce Foundation como back-end transacional.
   - Não: mantenha seu back-end transacional existente ou de terceiros. Se você também precisar de recursos de detecção e comercialização do Adobe, avalie o Adobe Commerce Optimizer independente.
1. **Deseja usar o Adobe Commerce Optimizer para melhorar a descoberta de produtos e o merchandising com seu back-end comercial de terceiros existente?**
   - Sim: avalie o Adobe Commerce Optimizer independente e, ao mesmo tempo, retenha o back-end de terceiros para transações.
1. **Você já opera o Adobe Commerce na Nuvem ou no local e deseja uma descoberta e um merchandising mais sólidos?**
   - Sim: avalie o Adobe Commerce Optimizer Connector para sincronizar dados de catálogo e preço enquanto o Adobe Commerce continua a manipular transações.

Use a tabela de comparação abaixo para corresponder suas respostas a um ponto de partida. Para obter diagramas detalhados do sistema, consulte [Opções de arquitetura](../architecture-options/overview.md).

## Comparar opções do Commerce

| Sua exigência | Ponto de partida recomendado | Sistema proprietário de transações | Merchandising e descoberta |
| --- | --- | --- | --- |
| O Adobe gerencia a plataforma Commerce como SaaS. | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service Foundation | Use os serviços da Commerce fornecidos para o Adobe Commerce as a Cloud Service. Para obter a disponibilidade da integração do Adobe Commerce Optimizer, consulte a nota abaixo nesta tabela. |
| Precisa do Adobe Commerce e deseja manter o controle sobre sua infraestrutura em nuvem ou local. | [Adobe Commerce na nuvem ou no local](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | Use os serviços compatíveis da Commerce conforme necessário. |
| No Adobe Commerce na nuvem ou no local, e deseja adotar o Adobe Commerce Optimizer para descoberta e merchandising. | Adobe Commerce com o [Adobe Commerce Optimizer Connector](/help/aco-connector/overview.md) | O Adobe Commerce continua sendo o sistema de registro de transações. | O conector sincroniza dados de catálogo e preço com a Adobe Commerce Optimizer, que fornece experiências de descoberta e merchandising. |
| Ter um back-end comercial de terceiros e desejar detecção e merchandising do Adobe Commerce Optimizer sem substituir esse back-end. | [Adobe Commerce Optimizer](/help/optimizer/overview.md) autônomo | Sua infraestrutura de comércio de terceiros | Enviar dados de catálogo e preço para o Adobe Commerce Optimizer. Integre o carrinho, o check-out e outras operações transacionais com o back-end por meio da API Mesh, do App Builder ou de uma integração direta. |

>[!NOTE]
>
>Uma integração entre o Adobe Commerce as a Cloud Service e o Adobe Commerce Optimizer está no roteiro do Commerce. Se você precisar de ambas as plataformas, planeje usá-las como opções de arquitetura separadas por enquanto. Entre em contato com o gerente de conta da Adobe para saber mais sobre a linha do tempo da integração.

## Orientação relacionada

- [Plataformas e serviços](platform-and-services.md)
- [Opções de arquitetura](../architecture-options/overview.md)
- [Introdução](../get-started/get-started-by-role.md)
