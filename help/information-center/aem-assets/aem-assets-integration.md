---
title: Integração do AEM Assets para o Commerce
description: Saiba como integrar o AEM Assets ao Adobe Commerce, Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer para gerenciar imagens e mídias de produtos de forma central.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
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
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Integração do AEM Assets para o Commerce

A integração do AEM Assets habilita os recursos de Visuais de produto no Adobe Commerce para que você possa gerenciar imagens, vídeos e outras mídias do produto centralmente no AEM Assets. É um complemento opcional que funciona com qualquer opção de arquitetura do Commerce, não com uma plataforma Commerce separada.

## Caminhos de integração por arquitetura

Há dois caminhos de integração. O caminho depende da arquitetura do Commerce.

| Arquitetura do Commerce | Caminho de integração do AEM Assets | Saiba mais |
| --- | --- | --- |
| [!DNL Adobe Commerce] na nuvem ou no local | Integração do [!DNL AEM Assets] para o Commerce. Usa o pacote de integração do Commerce para sincronizar e gerenciar imagens, vídeos e outras mídias do produto entre [!DNL Adobe Commerce] e [!DNL AEM Assets]. | [Integração do AEM Assets para o Commerce](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] ativado por [!DNL AEM Assets] | [configuração de integração do AEM Assets](/help/aem-assets-integration/overview.md#next-steps) |
| Autônomo [!DNL Adobe Commerce Optimizer] | [!DNL Product Visuals] ativado por [!DNL AEM Assets]. Os dados de catálogo base e preço são recebidos por meio da [API de assimilação de dados do otimizador](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/). | [Visualizações de produto com o AEM Assets](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce] com o [!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals] ativado por [!DNL AEM Assets]. Os dados de catálogo e preço são sincronizados de [!DNL Adobe Commerce] pelo Conector. | [Integrações do Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals] é o caminho de integração para o Adobe Commerce as a Cloud Service e o Adobe Commerce Optimizer. Ele sincroniza imagens de produtos gerenciados pela AEM com a camada de catálogo do Commerce e as entrega para experiências da loja por meio de APIs da loja.

## Antes de escolher

- Os requisitos de instalação e licenciamento diferem entre o caminho do Commerce na nuvem ou no local e o caminho do Commerce as a Cloud Service ou do Adobe Otimizer [!DNL Product Visuals]. Analise primeiro os requisitos específicos da implantação.
- [!DNL AEM Assets] gerencia ativos digitais. Ele não substitui o catálogo, os preços, o carrinho, o checkout ou o sistema de pedidos da Commerce.
- Os ativos do produto são correspondidos aos produtos da Commerce usando o SKU ou outros metadados correspondentes documentados.
- Se as equipes de marketing e merchandising precisarem de imagens de produtos e fluxos de trabalho de ativos centralizados, escolha o caminho que corresponda à arquitetura do Commerce.

## Informações relacionadas

- [Documentação do Adobe Experience Manager Assets](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/overview)
- [Visão geral da arquitetura](../architecture-options/overview.md)
- [APIs](../apis/commerce-apis.md)
