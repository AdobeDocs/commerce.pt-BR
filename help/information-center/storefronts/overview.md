---
title: Vitrines
description: Saiba mais sobre as opções da loja da Adobe Commerce, incluindo a Loja Commerce habilitada pela Edge Delivery Services e implementações headless personalizadas.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
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
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# Vitrines

A loja é separada das camadas de backend e API do Commerce. Dependendo da arquitetura selecionada, uma vitrine pode recuperar dados das APIs do Commerce Foundation, das APIs de Serviços da Vitrine, das APIs de Serviços de Merchandising do [!DNL Adobe Commerce Optimizer] ou de sistemas conectados por meio da API Mesh, App Builder ou outros mecanismos de integração. Consulte [Opções de arquitetura](../architecture-options/overview.md) para saber como cada vitrine se compara com uma infraestrutura do Commerce.

## Commerce Storefront ativado por Edge Delivery Services

A Commerce Storefront viabilizada pelo [!DNL Edge Delivery Services] é uma opção de vitrine para o cliente criada na placa do Adobe Commerce, usando componentes internos e blocos de conteúdo. É compatível com qualquer uma das [visões gerais de arquitetura](../architecture-options/overview.md), conectando-se ao Commerce Foundation, Storefront Services ou [!DNL Adobe Commerce Optimizer] Merchandising Services, dependendo do back-end. Consulte a [visão geral da Adobe Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Serviços de vitrine

[!DNL Storefront Services] são serviços orientados à loja usados com [!DNL Adobe Commerce]. As APIs de serviço fornecem acesso otimizado a recursos como:

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

O [!DNL Adobe Commerce] na Nuvem ou no local (quando configurado) e o [!DNL Adobe Commerce as a Cloud Service] usam os Serviços da Storefront. Eles não são exclusivos de [!DNL Adobe Commerce as a Cloud Service] e não devem ser usados como o rótulo distintivo entre as duas opções de plataforma [!DNL Adobe Commerce]. Consulte o [esquema GraphQL do Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Loja headless personalizada

As opções de vitrine além da Commerce Storefront viabilizadas pelo [!DNL Edge Delivery Services] incluem [!DNL Luma], [!DNL PWA Studio], ou uma vitrine headless personalizada, dependendo dos requisitos de suporte e implementação da plataforma. Uma loja headless personalizada se conecta às mesmas famílias de API que qualquer outra opção de loja — Commerce Foundation, Storefront Services ou Commerce Optimizer Merchandising Services — com base na [opção de arquitetura](../architecture-options/overview.md) selecionada.

## Integração de carrinho e check-out

As transações de carrinho e check-out são manipuladas depende do back-end do Commerce, não da tecnologia de vitrine:

- Quando o Commerce Foundation [!DNL Adobe Commerce] é o back-end, a loja usa as APIs do Commerce Foundation para operações de carrinho, check-out, cliente e pedido, juntamente com integrações configuradas de pagamento, imposto, envio e preenchimento.
- Quando uma plataforma de comércio de terceiros é o back-end (como no [!DNL Adobe Commerce Optimizer] independente), a loja se conecta aos serviços de carrinho, finalização, cliente, pedido, pagamento, imposto, envio e preenchimento da plataforma por meio da API Mesh, App Builder ou de uma integração direta.

## Orientação relacionada

- [Visão geral da arquitetura](../architecture-options/overview.md)
- [APIs](../apis/commerce-apis.md)
