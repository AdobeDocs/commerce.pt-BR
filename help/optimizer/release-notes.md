---
title: Notas de versão
description: As informações da versão mais recente de  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
source-git-commit: a42f6b3348eed476095c6d9777ac9486579fe6ea
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# Notas de versão

As notas de versão a seguir contêm atualizações para [!DNL Adobe Commerce Optimizer].

## Abril de 2026

**Data de lançamento**: 7 de abril de 2026

>[!BEGINSHADEBOX]

### Regras de catálogo (beta)

As regras de merchandising agora incluem [regras de categoria](./merchandising/rules/add.md), para que você possa direcionar uma ou mais categorias e controlar a ordem do produto nas páginas de categoria usando a mesma classificação inteligente e as mesmas ações manuais (fixar, impulsionar, enterrar) da pesquisa.

### Filtro de preço (beta)

Os filtros de recomendação agora oferecem suporte a um [filtro de preço](./merchandising/recommendations/filters.md#price) que você pode usar para definir um intervalo de preço mínimo e máximo para produtos.

{{aco-release}}

>[!ENDSHADEBOX]

## Fevereiro de 2026

**Data de lançamento**: 19 de fevereiro de 2026

>[!BEGINSHADEBOX]

### Exibição de catálogo de regras e recomendações de merchandising (beta)

Adição da capacidade de especificar uma exibição de catálogo ao [criar unidades de recomendação](./merchandising/recommendations/create.md) ou [regras de merchandising](./merchandising/rules/add.md).

{{aco-release}}

>[!ENDSHADEBOX]

## Dezembro de 2025

**Data de lançamento**: 10 de dezembro de 2025

>[!BEGINSHADEBOX]

### Oportunidades

As recomendações de otimização de site baseadas em IA agora estão disponíveis por meio da [integração com o Adobe Sites Optimizer](./manage-results/opportunities.md). Esse recurso ajuda os comerciantes a identificar e solucionar problemas que afetam o desempenho do site de comércio por meio da detecção automatizada e de recomendações inteligentes.

### Camadas do catálogo

Adicionadas [camadas de catálogo](./setup/catalog-layer.md) para que você possa modificar os dados do produto sem alterar os dados de origem, incluindo o gerenciamento de prioridade de camada e a integração com os recursos de correção automática do Adobe Sites Optimizer.

{{aco-release}}

>[!ENDSHADEBOX]

## Outubro de 2025

**Data de lançamento**: 14 de outubro de 2025

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

O [!DNL Commerce Optimizer Salesforce Commerce Connector] é um novo kit inicial de integração do App Builder que permite aos administradores e desenvolvedores do Commerce conectar facilmente os dados de catálogo do Salesforce B2C Commerce com o [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Para Administradores:**

* As atualizações de catálogo no Salesforce (produtos, preços, metadados, catálogos de preços) são sincronizadas automaticamente com o Commerce Optimizer — não é necessária nenhuma intervenção manual.
* A integração funciona independentemente do Adobe Commerce, reduzindo a complexidade e os possíveis pontos de falha.
* Os administradores podem confiar em atualizações programadas regularmente para garantir dados precisos do catálogo no Commerce Optimizer, melhorando o merchandising e as recomendações de produtos.

**Para Desenvolvedores:**

* O kit inicial fornece uma estrutura simplificada e extensível para assimilar dados de catálogo do Salesforce nos serviços de merchandising do SaaS.
* Implementações de referência, documentação de design e exemplos de código estão disponíveis para acelerar integrações personalizadas ou solução de problemas.<!--COMOPT-536-->

### Pesquisa em camadas

* Versão do GA para os seguintes recursos de pesquisa avançada: pesquisa em camadas usando `startsWith` e `contains`. [Saiba mais](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### APIs de categorias

Uma nova API REST de categorias agora está disponível, permitindo que administradores e desenvolvedores criem, atualizem e gerenciem programaticamente várias árvores de categorias para navegação e agrupamento de produtos. A API é compatível com configurações globais e específicas de canal e foi projetada para alta escalabilidade, suportando até 10.000 árvores de categoria e 500 categorias por árvore. Para obter detalhes, consulte [Categorias](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#categories) no _Guia do Desenvolvedor de Serviços de Merchandising_.<!--DCAT-2649-->

{{aco-release}}

>[!ENDSHADEBOX]

## Agosto de 2025

**Data de lançamento**: 28 de agosto de 2025

>[!BEGINSHADEBOX]

### Região da UE já disponível

O suporte da região da União Europeia (eu1) para organizações de IMS do cliente já está disponível. Agora você pode selecionar **União Europeia** como **Região** ao [adicionar uma instância do Commerce Optimizer](./get-started.md#step-1-create-an-instance) na Cloud Manager. A região da União Europeia só está disponível para ambientes de produção.

Os URLs de produção de base da região da União Europeia são:

* Administrador: `https://eu1.admin.commerce.adobe.com`
* REST e GraphQL: `https://eu1.api.commerce.adobe.com`

![criar instância](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]
