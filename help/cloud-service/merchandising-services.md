---
title: Modelo de dados de catálogo combinável e serviços de merchandising
description: Saiba como o Modelo de Dados do Catálogo de Composição altera a entrega do catálogo no [!DNL Adobe Commerce as a Cloud Service] e o que os comerciantes e as equipes de vitrine precisam saber.
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: c67e36c5a607fa1112a3a34b71c89de1b0162b10
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%
---

# Serviços de merchandising

O Adobe Commerce as a Cloud Service agora é compatível com o modelo de dados de catálogo combinável (CCDM) por meio dos Serviços de merchandising. A Adobe Commerce Optimizer apresentou esse modelo de dados, e a CCDM fornece aos dois produtos uma base comum para atender aos recursos de comercialização e navegação do catálogo de vitrines, enquanto a Commerce Foundation continua gerenciando produtos, preços e transações.

Este tópico explica quais alterações ocorrem com o CCDM, quais recursos continuam e o que a alteração significa para comerciantes, parceiros e desenvolvedores de vitrine.

## Quais alterações o CCDM apresenta?

O modelo do catálogo original usa o Serviço de catálogo para fornecer dados de produtos para vitrines, com o Live Search e o Product Recommendations fornecendo recursos de pesquisa, merchandising e recomendação. Neste modelo, o Commerce sincroniza usando a [exportação de dados SaaS](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview).

Com a CCDM, esses recursos operam na mesma base de catálogo que capacita o Adobe Commerce Optimizer. [Exibições de catálogo](../optimizer/setup/catalog-view.md) e [políticas](../optimizer/setup/policies.md) definem o contexto do catálogo disponível para uma vitrine. As políticas determinam a variedade de produtos e as regras de merchandising podem ser aplicadas em todas as exibições de catálogo ou ser personalizadas para uma exibição específica.

Isso altera a forma como o catálogo é configurado, acessado e comercializado. O CCDM se baseia nos recursos de pesquisa, recomendações e merchandising do catálogo original do Commerce e, ao mesmo tempo, introduz controles no nível de visualização do catálogo. Os recursos adicionais de gerenciamento e geração de relatórios são descritos abaixo.

A Commerce Foundation continua sendo a fonte canônica de produtos e preços. Os dados de produto e preço sincronizam de uma maneira para o CCDM por meio de uma integração nativa do Adobe Commerce as a Cloud Service. A configuração do site, da loja e da visualização de loja permanece no Commerce, juntamente com o carrinho existente, o checkout e os fluxos de trabalho de gerenciamento de pedidos.

## Licenciamento e provisionamento

Os Serviços de merchandising estão incluídos na SKU atual do Adobe Commerce as a Cloud Service. Não é um segundo produto ou assinatura e não requer uma compra, um direito ou um locatário separados da Adobe Commerce Optimizer.

## Visão geral da arquitetura

O [!DNL Commerce Foundation] continua sendo o registro principal de produtos e preços e gerencia transações. A integração nativa sincroniza dados de produto e preço de uma maneira de [!DNL Commerce] para CCDM. Você não instala um conector separado ou um aplicativo [!DNL App Builder] para esta sincronização.

As vitrines usam os Serviços de merchandising com suporte do CDM para recuperar dados de catálogo e contexto para navegação, pesquisa, recomendações e merchandising. As solicitações usam o contexto do catálogo para recuperar produtos e preços para o público-alvo desejado. Você continua a gerenciar as configurações de site, armazenamento e exibição de loja no [!DNL Commerce].

O diagrama a seguir mostra a posição dos Serviços de merchandising na arquitetura mais ampla do Adobe Commerce as a Cloud Service.

![Arquitetura do Commerce mostrando o fluxo de dados do catálogo para os Serviços de Merchandising](./assets/data-flow-ccdm.png){zoomable="yes"}

## O que há de novo para comerciantes?

O novo modelo permite determinar o escopo das regras de merchandising existentes para todas as exibições de catálogo ou para uma exibição específica. Isso permite aplicar merchandising a cada público-alvo da loja. Saiba como [determinar o escopo de uma regra de merchandising para exibições de catálogo](../optimizer/merchandising/rules/add.md#create-a-rule).

No Administrador, você pode configurar o contexto do catálogo com [!UICONTROL Catalog Views] e [!UICONTROL Policies]. Você também pode usar [!UICONTROL Success Metrics] para revisar receita, conversão, envolvimento, aquisição e taxa de rejeição. Consulte [Métricas de sucesso](../optimizer/manage-results/success-metrics.md) para obter mais detalhes.

## Considerações antes da adoção

Analise como o modelo CCDM afeta seus fluxos de trabalho de licenciamento, integrações de catálogo, vitrine e administrador antes de adotar os Serviços de merchandising.

### Gerenciamento e integrações de catálogo

Continue gerenciando produtos e preços em [!DNL Commerce Foundation]. A integração nativa os sincroniza com o CCDM. Não crie um segundo catálogo de produtos para Serviços de merchandising.

### Implementação da loja

A forma como a loja recupera dados de catálogo depende da implementação:

- **[!DNL Adobe Commerce Storefront]** menus — Os menus suspensos controlam a transição. Nenhuma alteração de código é necessária. Consulte a [documentação de configuração da loja](https://experienceleague.adobe.com/en/tools/commerce-storefront/).
- **Personalizar ou outras lojas**—Atualize seus cabeçalhos de solicitação de catálogo conforme descrito na [referência de configuração de cabeçalho](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

Revise suas consultas de catálogo e solicite cabeçalhos para o modelo baseado em CCDM. Não presuma que as consultas ou os cabeçalhos existentes permaneçam inalterados. As consultas do GraphQL de merchandising diferem das consultas usadas no modelo original de serviços de catálogo. Consultas adicionais são compatíveis com o CCDM. Use a [Referência da API do GraphQL de merchandising](https://developer.adobe.com/commerce/services/reference/graphql/) e verifique o contexto do catálogo necessário com base na [referência do cabeçalho da loja](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

### Aplicativos e extensões de terceiros

Revise aplicativos e extensões de terceiros que leem dados de catálogo ou consomem eventos de catálogo com seu provedor. A compatibilidade depende de como cada aplicativo ou extensão usa essas interfaces.

### Experiência do administrador

O Adobe Commerce as a Cloud Service com CCDM usa [[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/admin-unified-experience) (Unified Shell). A Adobe lançou o Unified Shell separadamente do CCDM. As instâncias existentes no modelo original de serviços de catálogo retêm acesso ao Classic e ao Unified Shell.

### Limites

O modelo CCDM não altera os limites do Adobe Commerce as a Cloud Service. Compartilhar uma base de catálogo com o Otimizer não significa que o Commerce herda a capacidade ou os limites do Otimizer.

## Disponibilidade e migração

As organizações que começam com o Adobe Commerce as a Cloud Service após esta versão recebem Serviços de merchandising por padrão. Se sua organização exigir o modelo original de dados do catálogo, entre em contato com a equipe de conta da Adobe para discutir se uma exceção está disponível.

As organizações que tinham o Adobe Commerce as a Cloud Service antes desta versão podem escolher qualquer modelo de catálogo ao [provisionar uma nova instância](./getting-started.md#create-an-instance). Por padrão, o alternador [!UICONTROL Enable CCDM] está desabilitado. Depois que o CCDM é ativado, não é possível desativá-lo.

As instâncias existentes não são alteradas automaticamente. Na disponibilidade geral (GA), não é possível migrar uma instância existente dos serviços de catálogo originais para os Serviços de merchandising.
