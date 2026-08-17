---
title: Notas de versão do Adobe Commerce Optimizer
description: Informações de versão mensais do  [!DNL Adobe Commerce Optimizer], incluindo atualizações da API REST de assimilação de dados e da API GraphQL para recuperação de dados de catálogo da loja.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 413d0932d402615c9e155e1650a7c8aba2c082a1
workflow-type: tm+mt
source-wordcount: 1522
ht-degree: 0%

---

# Notas de versão

As notas de versão a seguir contêm atualizações para [!DNL Adobe Commerce Optimizer], incluindo:

* Novos recursos e melhorias no [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour).
* Atualizações da [API REST de assimilação de dados](https://developer.adobe.com/commerce/services/reference/rest/) e da [API GraphQL para recuperação de dados de catálogo da loja](https://developer.adobe.com/commerce/services/reference/graphql/).

  {{aco-api-updates-and-dropins}}

## Agosto de 2026

>[!BEGINSHADEBOX]

_7 de agosto de 2026_

![Novo](../assets/new.svg) **Novo campo `externalIds`**—Adicionado `externalIds` ao GraphQL do Serviço de Catálogo, expondo a fonte de dados externa associada a um produto para que os consumidores de vitrine e integração possam identificar a fonte de dados de origem. Consulte [Retornar externalIds para um produto](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases#return-external-ids-for-a-product){target="_blank"}
<!--DATA-7307-->

![Correção](../assets/fix.svg) **Correção da resposta `refineProduct` para produtos configuráveis**—Correção de um problema em que a consulta `refineProduct` retornava `priceRange: null` e `roles: ["hidden"]` para produtos configuráveis específicos, garantindo informações precisas de visibilidade e preços para os consumidores de vitrine.
<!--COMOPT-2367-->

{{aco-release}}

>[!ENDSHADEBOX]

## Julho de 2026

>[!BEGINSHADEBOX]

_20 de julho de 2026_

![Correção](../assets/fix.svg) **Desempenho de navegação de categoria**—Otimizações de desempenho aplicadas ao serviço de categoria, resultando em maior taxa de transferência e menor latência P99 para a consulta `CategoryNavigation`, melhorando a capacidade de resposta do serviço e a experiência geral do usuário sob carga alta.
<!--DATA-7131 DATA-7250-->

{{aco-release}}

>[!ENDSHADEBOX]

## Junho de 2026

>[!BEGINSHADEBOX]

_24 de junho de 2026_

<!-- v1.3 -->

![Novo](../assets/new.svg) **Novo campo `canEditQuantity`** — Adicionado `canEditQuantity` a `ProductViewOptionValueProduct` no GraphQL de Serviço de Catálogo. Ele expõe a configuração de quantidade **Definida pelo Usuário** opcional para seleções de pacotes do Administrador do Commerce, para que os consumidores da loja possam determinar se a quantidade de uma seleção de pacote é editável.
<!--COMOPT-2050-->

### Pesquisa semântica

[!DNL Adobe Commerce Optimizer] agora oferece suporte à **[pesquisa semântica]** na guia [**Pesquisa avançada**](./settings.md#advanced-search) em **[!UICONTROL Settings]**. A pesquisa semântica usa a IA para corresponder produtos por significado e contexto ao lado da pesquisa por palavra-chave, reduzindo as páginas de pesquisa vazias para consultas em linguagem natural. Ela é ativada por padrão para catálogos em inglês qualificados. Opcionalmente, você pode ajustar **[!UICONTROL Semantic boost]**, **[!UICONTROL Similarity threshold]** e **[!UICONTROL Fuzzy search]** na mesma guia. Nenhuma configuração de atributo ou alteração de vitrine eletrônica é necessária. [Saiba mais](./setup/semantic-search.md).

### Filtros de preço de recomendação (beta)

As unidades de recomendação do produto agora oferecem suporte a [**filtros de preço**](./merchandising/recommendations/filters.md#price) na etapa **[!UICONTROL Filter products]**. Inclua ou exclua candidatos usando intervalos mínimos e máximos de **estáticos** ou regras de **dinâmicas** na página de detalhes do produto que comparam os produtos recomendados com o **preço calculado final** do produto exibido atualmente na tabela de preços ativa da loja. As regras de preço filtram o conjunto de candidatos. Eles não reclassificam os produtos. [Saiba mais](./merchandising/recommendations/filters.md#price).

{{aco-release}}

>[!ENDSHADEBOX]

## Maio de 2026

>[!BEGINSHADEBOX]

### Aumento inteligente de classificação

As [Regras de merchandising](./merchandising/rules/add.md#intelligent-ranking-boost) para pesquisa, listas de produtos padrão e [páginas de categoria](./merchandising/rules/add.md#rule-types) agora incluem **[!UICONTROL Intelligent Ranking Boost]**. Você pode ajustar a intensidade com que estratégias como **Mais visualizados** ou **Tendências** influenciam a ordem do produto em relação à relevância textual nos sinais de pesquisa e comportamento em listagens de categorias. A visualização da regra reflete sua configuração. O aumento é aplicado no momento da consulta, de modo que não é necessário sincronizar novamente o catálogo ao alterá-lo.

### Atualizações da API

_28 de maio de 2026_

<!-- v1.2 -->

![Correção](../assets/fix.svg) **Árvores de navegação completas**—As categorias descendentes marcadas agora são incluídas corretamente nas árvores `navigation` filtradas por família quando existe um nó intermediário não marcado no caminho. Essa correção garante que os compradores vejam todas as categorias relevantes na navegação, facilitando a navegação e a descoberta de itens.
<!--DATA-7183-->

![Correção](../assets/fix.svg) **Tratamento de espaçador vazio em `categoryTree` solicitações**—Correção de um problema em que a consulta [`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) retornava um erro de servidor interno quando o argumento `slugs` incluía uma cadeia de caracteres vazia. Valores de espaçador vazios agora são ignorados, de modo que as frentes de loja e as integrações continuam a resolver dados de categoria sem solicitações com falha.
<!--DATA-7184-->

![Corrigir](../assets/fix.svg) **`searchCategory`solicitações retornam resultados em ordem alfabética, que não diferenciam maiúsculas de minúsculas**—A consulta `searchCategory` agora classifica os resultados de pesquisa em ordem alfabética, sem diferenciação entre maiúsculas e minúsculas, garantindo uma ordem consistente e previsível. As categorias com prefixos mais curtos aparecem primeiro quando os nomes são idênticos.
<!--COMOPT-2142-->

_4 de maio de 2026_

<!--v1.53-->

**Exibição de moeda correta**—Os preços de produtos da vitrine agora exibem o código monetário correto (por exemplo, USD) para todos os tipos de produtos. Anteriormente, alguns produtos exibiam `NONE` em vez da moeda esperada, resultando em preços ausentes.

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## Abril de 2026

**Data de lançamento**: 7 de abril de 2026

>[!BEGINSHADEBOX]

### Regras de catálogo

[Regras de categoria](./merchandising/rules/add.md) estendem as regras de merchandising para que você possa direcionar categorias e controlar a ordem dos produtos nas páginas de categoria com a mesma classificação e as mesmas ações (fixar, aumentar, enterrar) da pesquisa.

### Filtro de preço (beta)

Os filtros de recomendação agora incluem um [filtro de intervalo de preços](./merchandising/recommendations/filters.md#price) (mínimo e máximo).

### Atualizações da API

_29 de abril de 2026_

<!--v1.52 release-->

**Solicitação em lote necessária** — a API do GraphQL agora impõe um máximo de 100 SKUs por solicitação ao recuperar dados de catálogo. Consulte [limites documentados](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery).

<!--DATA-7156-->

_17 de abril de 2026_

<!--v1.51 release-->

**Localizar categorias por nome com o GraphQL** — A nova consulta [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) retorna categorias correspondentes com paginação para vitrines e integrações. Consulte a referência da API para obter parâmetros e campos de resposta. <!--COMOPT-1819-->

_7 de abril, 2026_

<!--v1.50 release-->

**Pesquisas de categoria mais simples** — A consulta [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) trata `family` como opcional, para que você possa resolver categorias por slug sem fornecer uma família.

{{aco-release}}

>[!ENDSHADEBOX]

## Março de 2026

Não houve nenhuma versão [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) este mês. Consulte Atualizações de API abaixo.

>[!BEGINSHADEBOX]

### Atualizações da API

_24 de março de 2026_

Os pacotes dinâmicos agora retornam uma faixa de preço calculada. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## Fevereiro de 2026

**Data de lançamento**: 19 de fevereiro de 2026

>[!BEGINSHADEBOX]

### Exibição de catálogo para regras e recomendações de merchandising

Agora você pode especificar uma exibição de catálogo ao [criar unidades de recomendação](./merchandising/recommendations/create.md) ou [regras de merchandising](./merchandising/rules/add.md).

### Atualizações da API

_19 de fevereiro de 2026_

<!--v1.48-->

**Conteúdo de categoria mais avançada para vitrines** — A consulta [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) agora retorna descrições, imagens e metatags de SEO, para que vitrines possam renderizar páginas de categoria mais avançadas.<!--DATA-6933-->

_12 de fevereiro de 2026_

<!--v1.49-->

**Dados aprimorados do produto por categoria** — a API do GraphQL adiciona o tipo [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} para que você possa consultar e filtrar produtos por categoria com menos viagens de ida e volta.

{{aco-release}}

>[!ENDSHADEBOX]

## Janeiro de 2026

Não houve nenhuma versão [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) este mês. Consulte Atualizações de API abaixo.

>[!BEGINSHADEBOX]

### Atualizações da API

_19 de janeiro de 2026_

* **As categorias mais avançadas são compatíveis com a REST API** — as operações [API de Categorias](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) agora aceitam valores `metaTags`, `images` e `description` opcionais, além de `families`, para que você possa oferecer um merchandising mais elaborado e detalhes de SEO para as categorias.

{{aco-release}}

>[!ENDSHADEBOX]

## Dezembro de 2025

**Data de lançamento**: 10 de dezembro de 2025

>[!BEGINSHADEBOX]

### Oportunidades

Os merchandisers agora podem obter recomendações alimentadas por IA por meio do [Adobe Sites Optimizer](./manage-results/opportunities.md) para detectar problemas no site e sugerir correções de desempenho.

### Camadas do catálogo

Agora os comerciantes podem usar [Camadas do catálogo](./setup/catalog-layer.md) para sobrepor dados do produto sem editar o catálogo de origem, gerenciar a prioridade da camada e usar a correção automática do Adobe Sites Optimizer.

{{aco-release}}

>[!ENDSHADEBOX]

## Novembro de 2025

Não houve nenhuma versão [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) este mês. Consulte Atualizações de API abaixo.

>[!BEGINSHADEBOX]

### Atualizações da API

_21 de novembro de 2025_

**Instruções de autenticação atualizadas para a API REST de assimilação de dados** — agora as instruções fazem referência aos tokens de acesso OAuth e aos escopos corretos das credenciais do Developer Console para o serviço de assimilação de dados. Se os escopos de credencial estiverem desatualizados, gere-os novamente para manter o acesso.

_3 de novembro de 2025_

<!-- v1.43 -->

**Conteúdo de produto localizado em camadas no GraphQL** — Agora você pode fornecer conteúdo de produto com reconhecimento de localidade e específico de canal do [!DNL Adobe Commerce Optimizer].

* Personalizar conteúdo do produto por segmento do cliente
* Aplicar substituições específicas de localidade sem duplicar dados do catálogo base
* Controlar substituições em nível de campo com máscaras de camada
* Usar camadas de conteúdo premium, sazonais e otimizadas para dispositivos móveis

Nenhuma alteração no esquema da API do GraphQL: as camadas se aplicam por meio da consulta `products` existente e dos cabeçalhos de solicitação. Consulte [Camada do catálogo](./setup/catalog-layer.md).

{{aco-release}}

>[!ENDSHADEBOX]

## Outubro de 2025

**Data de lançamento**: 14 de outubro de 2025

>[!BEGINSHADEBOX]

### Commerce Optimizer Salesforce Commerce Connector

O [!DNL Commerce Optimizer Salesforce Commerce Connector] é um novo kit inicial do App Builder que sincroniza os dados de catálogo do Salesforce B2C Commerce em [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Para Administradores:**

* As alterações no catálogo do Salesforce (produtos, preços, metadados, catálogos de preços) são sincronizadas com [!DNL Commerce Optimizer] automaticamente.
* É executado fora de [!DNL Adobe Commerce] para menos pontos de contato de integração.
* As atualizações agendadas mantêm os dados de [!DNL Commerce Optimizer] atualizados para merchandising e recomendações.

**Para Desenvolvedores:**

* Estrutura extensível para assimilação do catálogo Salesforce nos serviços de merchandising SaaS.
* Implementações de referência, documentos de design e amostras de código para obter compilações e soluções de problemas mais rápidas.

### Pesquisa em camadas

* **Pesquisa em camadas (GA)** — A pesquisa de produtos agora oferece suporte à correspondência de `startsWith` e `contains`. Consulte [Pesquisa em camadas e tipos de pesquisa expandidos](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### Atualizações da API

* _17 de outubro de 2025_

  **Adicionar suporte à API REST para assimilar camadas de produto** — Use a [API de camadas de catálogo](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) para personalizar e substituir dados de produto base para contextos, localidades ou requisitos comerciais específicos. Depois de criar camadas, você pode aplicá-las e gerenciá-las no [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->

* _14 de outubro de 2025_

  **Árvores de categoria programáticas** — Crie, atualize e gerencie árvores de categoria para navegação e agrupamento via REST (global ou específico de canal), em escala — até 10.000 árvores e 500 categorias por árvore. Consulte [Categorias](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} na _Referência da API REST de assimilação de dados do catálogo_.<!--DCAT-2649-->

* _8 de outubro de 2025_

  **Mapeamento de categoria mais claro para assimilação de dados** — Novas diretrizes explicam o formato de descrição da categoria e as regras de hierarquia e esclarecem que os valores de produto `routes.path` devem corresponder a uma descrição da categoria existente (por exemplo, `men/clothing`).

{{aco-release}}

>[!ENDSHADEBOX]

## Setembro de 2025

Não houve nenhuma versão [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) este mês. Consulte Atualizações de API abaixo.

>[!BEGINSHADEBOX]

### Atualizações da API

_23 de setembro de 2025_

* **Gerenciar categorias usando a API REST** — Use a [API de Categorias](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) para criar e gerenciar categorias. As categorias organizam os produtos em grupos lógicos e oferecem suporte a hierarquias aninhadas por meio de caminhos baseados em slug. Depois de atribuir categorias a produtos, recupere-as com as consultas do GraphQL `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)` e do `[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` para renderizar menus de vitrine e árvores de categoria.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## Agosto de 2025

**Data de lançamento**: 28 de agosto de 2025

>[!BEGINSHADEBOX]

### Região da UE já disponível

A região de produção da UE (**eu1**) está disponível para organizações IMS. Quando você [adicionar uma [!DNL Commerce Optimizer] instância](./get-started.md#step-1-create-an-instance) no Cloud Manager, escolha **[!UICONTROL European Union]** como **[!UICONTROL Region]** (somente produção).

Os URLs de produção de base da região da União Europeia são:

* Administrador: `https://eu1.admin.commerce.adobe.com`
* REST e GraphQL: `https://eu1.api.commerce.adobe.com`

![Caixa de diálogo de criação de instância do Cloud Manager com o campo Região](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]

