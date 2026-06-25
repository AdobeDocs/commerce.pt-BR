---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: As informações da versão mais recente do  [!DNL Catalog Service] para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: c87bcff49f3c17379331e18fb9a0e890a5b9717c
workflow-type: tm+mt
source-wordcount: 2682
ht-degree: 0%

---

# Notas de versão do [!DNL Commerce Storefront Catalog Service]

Essas notas de versão abordam as atualizações mais recentes do serviço de catálogo da Commerce, incluindo:

- **[Versões do Serviço de Catálogo da Loja](#storefront-catalog-service)**

   - Aprimoramentos do esquema da API do Serviço de catálogo para recuperação aprimorada de dados
   - Melhorias de segurança, desempenho e confiabilidade para a API do serviço de catálogo e infraestrutura subjacente.

  Consulte [Esquema dos Serviços de vitrine](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) na documentação do Desenvolvedor do Commerce para obter mais informações sobre essas APIs.

- **[Versões do metapackage do Serviço de Catálogo](#catalog-service-metapackage)**

   - Dependências atualizadas para melhorar o desempenho, a estabilidade e a compatibilidade com outros componentes do Adobe Commerce.

- **[Versões do Instalador do Serviço de Catálogo](#catalog-service-installer)**

   - Dependências atualizadas para manter a compatibilidade entre o Serviço de catálogo e sua pilha do Commerce.

>[!NOTE]
>
>Se o seu projeto do Commerce usa o Adobe Commerce Optimizer para fornecer dados de catálogo ao Commerce Edge Delivery Service ou a lojas headless, consulte as [notas de versão do Adobe Commerce Optimizer](../optimizer/release-notes.md) para obter as atualizações de API mais recentes.

As atualizações são categorizadas por tipo:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) Correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos

O suporte é fornecido para a versão mais recente. As notas de versão para versões mais antigas estão incluídas para referência.

## Serviço de Catálogo da Loja

### Maio de 2026

**Data de lançamento**: 20 de maio de 2026
<!-- v1.55 -->

![Novo](../assets/new.svg) Limite imposto de no máximo 100 SKUs por solicitação para clientes Adobe Commerce e Adobe Commerce as a Cloud Service de acordo com [limites e limites documentados](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits).
<!--DATA-7163-->

**Data de lançamento**: 13 de maio de 2026
<!--v1.54-->

![Nova](../assets/new.svg) **Ordem de classificação de categoria no GraphQL** — O tipo de GraphQL `CategoryView` agora inclui um campo de posição, portanto, as vitrines podem exibir categorias na ordem em que os comerciantes configuram na hierarquia do catálogo.
<!--DATA-7166-->

**Data de lançamento**: 4 de maio de 2026
<!-- v1.53 -->

![Correção](../assets/fix.svg) Os preços dos produtos da vitrine agora exibem o código monetário correto (por exemplo, USD) para todos os tipos de produtos. Anteriormente, alguns produtos exibiam `NONE` em vez da moeda esperada, resultando em preços ausentes. Esta atualização garante uma renderização de preço consistente e precisa em toda a loja.<!--DATA-7115-->

### Abril de 2026

**Data de lançamento**: 29 de abril de 2026
<!--v1.52-->

![Novo](../assets/new.svg) Limite imposto de no máximo 100 SKUs por solicitação para Adobe Commerce Optimizer e Adobe Commerce as a Cloud Service
clientes de acordo com [limites e limites documentados](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

**Data de lançamento**: 17 de abril de 2026
<!--v1.51-->

![Novo](../assets/new.svg) Adicionada uma nova consulta do GraphQL `searchCategory` que permite aos clientes pesquisar categorias por nome com resultados paginados. A consulta aceita um `searchTerm` necessário (mínimo de 3 caracteres) e parâmetros `family`, `pageSize` e `currentPage` opcionais. Os resultados incluem objetos `CategoryTreeView` correspondentes com metadados de categoria completa, `totalCount` e `pageInfo` para paginação. <!--COMOPT-1819-->

Esta consulta está disponível somente para clientes que usam os Serviços de merchandising da Adobe Commerce Optimizer. Consulte [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/).

### Março de 2026

**Data de lançamento**: 24 de março de 2026
<!--v1.49-->

![Novo](../assets/new.svg) Suporte adicionado para computar e retornar o intervalo de preços para pacotes dinâmicos.
<!--DATA-7115-->

### Dezembro de 2025

**Data de lançamento**: 11 de dezembro de 2025
<!-- v1.46 -->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade.
<!--DATA-6852, DATA-6864-->

### Novembro de 2025

**Data de lançamento**: 17 de novembro de 2025
<!-- v1.45 -->

![Novo](../assets/new.svg) **Filtragem de Atributo por Nome**-A consulta do GraphQL `productSearch` agora oferece suporte à filtragem de atributos de produto com o campo `names`. <!--DATA-6831--> Com esse filtro, é possível:

- Reduzir o tamanho do payload de resposta solicitando apenas atributos específicos
- Combine com o filtro `roles` existente para restringir por função de visibilidade e nome de atributo
- Exemplos:

  **Filtrar somente por nomes de atributo**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **Filtrar por funções e nomes:**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>Para recuperar todos os atributos sem filtragem, omita o argumento `names` ou forneça uma matriz vazia.

**Data de lançamento**: 6 de novembro de 2025
<!-- v1.44 -->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade. <!--DATA-6852, DATA-6864-->

![Correção](../assets/fix.svg) Os produtos agrupados agora podem ser consultados quando o pai não tem preços; os produtos filho retornam suas próprias funções de visibilidade.<!--DATA-6779-->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade. <!--DATA-6721, DATA-6864-->

### Setembro de 2025

**Data de lançamento**: 8 de setembro de 2025
<!-- v1.42 -->

![Novo](../assets/new.svg) **Suporte a preços de camada adicionado** para consultar preços de volume:<!--DATA-6643-->

Para recuperar preços de camada:

1. Use a consulta `products` com suas SKUs desejadas
2. Para **SimpleProductView**, acesse `price.tiers`
3. Para **ComplexProductView**, acesse `priceRange.minimum.tiers` e `priceRange.maximum.tiers`
4. Cada camada contém o preço com desconto de `tier` e `quantity` condições
5. Definir limites de quantidade com `gte` (maior que ou igual a) e `lt` (menor que)

**Exemplo:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![Correção](../assets/fix.svg) **Preços de camada filtrados pelo preço final mínimo** <!--DATA-6643-->

A API agora retorna somente camadas cujo preço com desconto é **menor que** o preço final mínimo do produto. As camadas mais altas são omitidas porque o preço final mínimo seria aplicado na loja.

Aplicável a:

- **Produtos simples**: `price.tiers` inclui somente camadas com `tier.amount.value` &lt; `price.final.amount.value` (mínimo final).
- **Produtos complexos**: `priceRange.minimum.tiers` e `priceRange.maximum.tiers` usam a mesma regra ao criar o intervalo de preços.

**Data de lançamento**: 2 de setembro de 2025
<!-- v1.41 -->

![Correção](../assets/fix.svg) **Tratamento de erros aprimorado para informações de preços ausentes**—Quando os dados de preços ainda não são recebidos, a API retorna `null` para o campo de preços em vez de gerar um erro, permitindo que os clientes lidem com os dados ausentes normalmente.<!--DATA-6612-->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade.<!--DATA-6671-->

### Julho de 2025

**Data de lançamento**: 30 de julho de 2025
<!-- v1.40 -->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6619-->

**Data de lançamento**: 24 de julho de 2025
<!-- v1.39 -->

![Novo](../assets/new.svg) **Recuperar unidades de recomendação por ID de unidade**-O novo ponto de extremidade do GraphQL `recommendationsByUnitIds` recupera unidades de recomendação por ID exclusiva para obter acesso mais flexível e direcionado.

- `unitIds` é necessário (lista de recIds para busca).
- Parâmetros de contexto (`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`) se comportam da mesma forma que na consulta de recomendações existente.

- **Exemplo**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6316-->

**Data de lançamento**: 15 de julho de 2025
<!-- v1.38 -->

![Novos](../assets/new.svg) **Tipos de produto de cartão-presente**. O Serviço de vitrine do catálogo agora oferece suporte a atributos de produto como objetos JSON ou matrizes, permitindo o gerenciamento flexível de tipos complexos, como cartões-presente.<!--DATA-6573-->

+++Versões anteriores

### Junho de 2025

**Data de lançamento**: 20 de junho de 2025
<!-- v1.37 -->

![Nova](../assets/new.svg) **Configuração do catálogo de preços hierárquico** — Intervalos de preços precisos para o catálogo de preços pai-filho. Os cálculos respeitam a hierarquia e as regras herdadas; reduz os erros de precificação quando vários catálogos de preços são vinculados. Somente Adobe Commerce Optimizer. Consulte [Catálogos de Preços](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![Novo](../assets/new.svg) **Chaves que não diferenciam maiúsculas de minúsculas** — As pesquisas de chave em consultas agora não diferenciam maiúsculas de minúsculas, reduzindo os erros de maiúsculas e minúsculas. <!--DATA-6494, DCAT-2495-->

**Data de lançamento**: 20 de junho de 2025
<!-- v1.36 -->

![Novo](../assets/new.svg) **Eventos de E/S Públicos para a Loja de Catálogos**—Foram adicionados eventos de E/S públicos para integração e observação em tempo real (CSS e EDS).<!--DATA-6329-->

![Novo](../assets/new.svg) **Renderização no Servidor (SSR)**—Melhorias de arquitetura para oferecer suporte ao SSR para melhor desempenho, SEO e UX em catálogos grandes.<!--DATA-6278, DATA-6280-->

![Novo](../assets/new.svg) **Infraestrutura e Segurança**—Novas funções do AWS, integração do ServiceNow e pipelines de CI/CD para o serviço de eventos.

![Novo](../assets/new.svg) **Formatos de evento e capacidade de observação** — cargas simplificadas, monitoramento aprimorado, dados aprimorados de eventos de variantes.<!--DATA-6332, DATA-6402, -->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6404, DATA-6410, -->

**Data de lançamento**: 13 de junho de 2025
<!-- v1.35 -->

![Novo](../assets/new.svg) **Recuperar dados não armazenados em cache**-Habilite o cabeçalho `Magento-Is-Preview` para passar dados não armazenados em cache do ponto de extremidade do catálogo para o Serviço de Pesquisa.<!--DATA-6345-->

![Novo](../assets/new.svg) **Opções de produtos de seleção múltipla**. A API do GraphQL agora expõe se as opções de produtos permitem várias seleções (por exemplo, agrupar &quot;escolher vários itens&quot;).<!--DATA-6487-->

![Novo](../assets/new.svg) Atualização da validação de preço na assimilação de dados para oferecer suporte a produtos sem preços.<!--DATA-6098-->

![Correção](../assets/fix.svg) Tratamento de erros aprimorado para preço de pacote simples no Adobe Commerce Optimizer.<!--DATA-6541-->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6273, DATA-6485, -->

### Abril de 2025

**Data de lançamento**: 8 de abril de 2025
<!-- v1.34 -->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-5732-->

<!-- v1.33 -->
![Correção](../assets/fix.svg) A infraestrutura agora oferece suporte a catálogos extremamente grandes (até ~440 milhões de SKUs) sem afetar as cargas de trabalho existentes.

### Março de 2025

**Data de lançamento**: 28 de março de 2025
<!-- v1.32 -->

![Corrigir](../assets/fix.svg) Atributos sem funções não são mais indexados por padrão para o catálogo combinável, melhorando o tempo de indexação e reduzindo o armazenamento. O comportamento herdado pode ser reativado por meio de um sinalizador de recurso.

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### Fevereiro de 2025

**Data de lançamento**: 18 de fevereiro de 2025
<!-- v1.31 -->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6389, DATA-6367, DATA-6373-->

### Dezembro de 2024

**Data de lançamento**: 9 de dezembro de 2024
<!-- v1.30 -->

Versão principal: [modelo de dados de catálogo combinável](https://developer.adobe.com/commerce/services/optimizer/) para frentes de loja headless, gerenciamento de cabeçalho e manipulação de dados de produto.

![Novo](../assets/new.svg) **Modelo de Dados de Catálogo de Composição (CCDM)** — Oferece suporte a clientes que usam o catálogo de composição para frentes de loja headless. Os novos endpoints aceitam a Exibição de catálogo e as IDs de política (compatíveis com versões anteriores). Detalhes e preços do produto configuráveis com paginação interna.<!--DATA-6018, DATA-6288-->

![Novo](../assets/new.svg) **Gerenciamento de Cabeçalho**-`AC-Locale` renomeado para `AC-Scope-Locale` para operações de API de catálogo combinável; mapeamento de cabeçalho e valores padrão especificados.<!--DATA-6303, DATA-6078-->

![Novos](../assets/new.svg) **Dados e preços do produto**-Suporte para modelo de dados de catálogo combinável e manipulação de preços aprimorada para produtos configuráveis.<!--DATA-6279-->

`CurrencyEnum` atualizado para oferecer suporte a `NONE` para consultas de pesquisa de produtos, alinhado à lógica de federação.<!--DATA-6285-->

![Correção](../assets/fix.svg) **Infraestrutura e atualizações**—Melhorias no nível do sistema para segurança, desempenho e estabilidade.

![Correção](../assets/fix.svg) As opções de pacote de produtos agora exibem apenas os produtos habilitados.<!--DATA-6347-->

**Data de lançamento**: 9 de dezembro de 2024
<!-- v1.29 -->

![Novo](../assets/new.svg) **Ordenação de imagens em consultas de produtos**—As imagens de produtos no campo `images` do GraphQL agora seguem a exportação de catálogo `sortOrder` para comportamento consistente da loja e da API.<!--DATA-6258-->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6619-->

**Data de lançamento**: dezembro de 2024
<!-- v1.28 -->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### Outubro de 2024

**Data de lançamento**: 22 de outubro de 2024
<!-- v1.26 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![novo](../assets/new.svg) esquema do GraphQL agora inclui `lastModifiedAt` nas informações do produto para mapas de site precisos e reindexação do mecanismo de pesquisa (por exemplo, Google).
<!--DATA-6209-->

### Setembro de 2024

**Data de lançamento**: 26 de setembro de 2024
<!-- v1.27 -->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.
<!--DATA-6243-->

### Agosto de 2024

**Data de lançamento**: 22 de agosto de 2024
<!-- v1.23 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) As informações do produto agora podem ser recuperadas sem os dados de substituição de produto (preços). Anteriormente, essas consultas retornavam: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**Data de lançamento**: 13 de agosto de 2024
<!-- v1.22 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para recuperar todas as variantes por SKU de produto. Consulte a [Referência da API do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).
<!--DATA-6067-->

### Maio de 2024

**Data de lançamento**: 23 de maio de 2024
<!-- v1.19 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes


![Correção](../assets/fix.svg) O sinalizador `InStock` para valores de opção agora respeita o status `enabled` de escopo da variante de produto.

<!--DATA-5033-->

![Correção](../assets/fix.svg) Suporte adicionado para preços de produtos com até 16 dígitos e 4 casas decimais. Ressincronize a partir do [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) ou da [CLI](../data-export/data-export-cli-commands.md) para aplicar as atualizações.
<!--DATA-5033-->

#### Limitações conhecidas

Os seguintes recursos ainda não são compatíveis:

- O tamanho máximo da carga dos atributos dinâmicos é de 9 MB.
- O preço do produto do Grupo pode ser calculado com preços simples do produto.
- Em uma matriz de imagens, somente a primeira imagem contém funções.

Use a API Mesh e a API principal do GraphQL para:

- Preço Mínimo Anunciado
- Nível de preços
- Pacote de produtos com preços fixos

Para obter detalhes e exemplos, consulte [Serviço de Catálogo e API Mesh](mesh.md).

### Abril de 2024

**Data de lançamento**: 11 de abril de 2024
<!-- v1.18 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para o PHP 8.3.

![Novas](../assets/new.svg) As consultas de [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) e [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) agora retornam dados de opções personalizáveis para produtos simples e complexos.<!--DATA-5538-->

### Fevereiro de 2024

**Data de lançamento**: 22 de fevereiro de 2024
<!-- v1.17 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) O [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) agora está disponível para fluxos de dados (Product Recommendations, Live Search, Catalog Service). Requer `catalog-service` metapackage v3.1.0+.

**Data de lançamento**: 13 de fevereiro de 2024
<!-- v1.16 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

Os vídeos de produtos ![Novos](../assets/new.svg) agora têm suporte da API de Serviço de Catálogo.
![Correção](../assets/fix.svg) As opções indisponíveis agora são mostradas no widget PDP.

#### Limitações conhecidas

Estes recursos ainda não são compatíveis:

- O tamanho máximo da carga dos atributos dinâmicos é de 9 MB.
- Preço de produto de grupo. Esse valor pode ser calculado com preços simples do produto.
- Em uma matriz de imagens, somente a primeira imagem contém funções.

Use a API Mesh e a API principal do GraphQL para:

- Preço Mínimo Anunciado
- [Nível de preços](mesh.md)

### Outubro de 2023

**Data de lançamento**: 12 de outubro de 2023
<!-- v1.13 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo oferece suporte ao sinalizador `inStock` para variantes de produtos.
![Novo](../assets/new.svg) Os campos `urlKey` e `externalId` foram adicionados ao esquema do GraphQL.
Há suporte para ![Novos](../assets/new.svg) produtos e cartões-presente baixáveis.

### Setembro de 2023

**Data de lançamento**: 19 de setembro de 2023
<!-- v1.12 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de catálogo agora usa a [indexação de preços SaaS](../price-index/price-indexing.md).
![Correção](../assets/fix.svg) Esta versão contém correções de erros e melhorias no lado do serviço.

### Julho de 2023

**Data de lançamento**: 18 de julho de 2023
<!-- v1.11 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora dá suporte à consulta do GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para Recomendações de Produto.

### Junho de 2023

**Data de lançamento**: 27 de junho de 2023
<!-- v1.10 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) A API de Serviço de Catálogo agora dá suporte a `related products`.

### Abril de 2023

**Data de lançamento**: 12 de abril de 2023
<!-- v1.7 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora limpa as variantes de produtos excluídas.
![Corrigir](../assets/fix.svg) melhorias na escalabilidade e no desempenho da infraestrutura.

### Março de 2023

**Data de lançamento**: 28 de março de 2023
<!-- v1.6 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Amostras adicionadas à consulta [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Novo](../assets/new.svg) Adicionou a capacidade de obter `entityId` usando a [API Mesh](mesh.md).

**Data de lançamento**: 6 de março de 2023
<!-- v1.5 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adicionado [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) funcionalidade GraphQL.
![Correção](../assets/fix.svg) Desempenho e escalabilidade da API aprimorados.

### Fevereiro de 2023

**Data de lançamento**: 7 de fevereiro de 2023
<!-- v1.4 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) metapackage de serviço de catálogo publicado para simplificar as etapas de instalação.
![Corrigir](../assets/fix.svg) melhorias na escalabilidade e no desempenho da API.

### Janeiro de 2023

**Data de lançamento**: 17 de janeiro de 2023
<!-- v1.3 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Simplificou e melhorou a experiência de integração.
![Novos](../assets/new.svg) Novos pontos de extremidade de sandbox do cliente estão disponíveis para teste de pré-produção.
![Novo](../assets/new.svg) suporte adicionado para produtos virtuais.
![Corrigir](../assets/fix.svg) melhorias na escalabilidade e no desempenho da API.

### Novembro de 2022

**Data de lançamento**: 18 de novembro de 2022
<!-- v1.1 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora oferece suporte à [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) da Adobe.
![Correção](../assets/fix.svg) Aprimoramento da escalabilidade da API e desempenho geral.

### Outubro de 2022

**Data de lançamento**: 4 de outubro de 2022
<!-- v1.0 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Suporte para produtos agrupados e agrupados.
![Novo](../assets/new.svg) substituições de visibilidade B2B adicionadas. Agora os produtos podem ser pesquisados e adicionados ao carrinho para grupos específicos de clientes.
O serviço ![Fix](../assets/fix.svg) agora está mais estável e melhorou o desempenho.

### Setembro de 2022

**Data de lançamento**: 12 de setembro de 2022
<!-- v0.3 -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novas](../assets/new.svg) imagens de variantes: imagens de produtos retornadas com base nas opções selecionadas.
![Novo](../assets/new.svg) Funções de preço: somente membros de grupos de clientes específicos podem ver os preços do produto.
![Correção](../assets/fix.svg) Estabilidade e desempenho do serviço aprimorados.
![Novas](../assets/new.svg) atualizações são recebidas quando produtos são excluídos do catálogo.

### Agosto de 2022

**Data de lançamento**: 9 de agosto de 2022
<!-- Beta -->

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) As consultas `products` e `refineProduct` retornam os seguintes dados:

- Atributos de produto predefinidos (sistema).
- Atributos dinâmicos do produto e filtrá-los por função (página de exibição do produto/página da lista de produtos).
- Opções de produto.
- Imagens de produto e filtrá-las por função (PDP/PLP).
- Um preço específico para produtos simples e faixas de preço para produtos configuráveis.
- Preços de grupo e faixas de preços do cliente. Eles retornam um preço padrão de fallback para os compradores sem um grupo de clientes.
- Tipos de produto que usam preços específicos do cliente B2B.

+++

## Metappackage do Serviço de Catálogo

Atualizações no metapackage PHP do Serviço de Catálogo (`magento/catalog-service`).

- Para clientes do Adobe Commerce as a Cloud Service, a versão mais recente é instalada em seu ambiente.

- Para o Adobe Commerce na nuvem ou no local, a Adobe recomenda usar o Composer para atualizar o metapackage do Serviço de catálogo nos seus ambientes de nuvem na versão mais recente.

### Versão v3.4.0

**Data de lançamento**: 8 de junho de 2026

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) **Suporte para monitoramento do status de sincronização do feed de dados**—Atualizou as dependências do metapackage do Serviço de Catálogo para incluir a extensão Status do Exportador de Dados (`magento/module-data-exporter-status`). Isso habilita o [monitoramento do status de sincronização do feed de dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) pelo Administrador do Commerce sem exigir nenhuma etapa adicional de instalação ou configuração

![Novo](../assets/new.svg) Atualizou as dependências para manter a compatibilidade entre o Serviço de Catálogo e a pilha do Commerce.

### Versão v3.3.0

**Data de lançamento**: 14 de outubro de 2025

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Nova](../assets/new.svg) **Atualização de serviços de dados**—`magento/data-services` dependência atualizada para ^8.0.0. Verifique o ambiente e o uso personalizado da API dos serviços de dados para obter compatibilidade com a versão 8.x antes de atualizar.

![Novo](../assets/new.svg) Versão e metadados atualizados para a versão 3.3.0.

### Versão v3.2.0

**Data de lançamento**: 12 de abril de 2024

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Nova](../assets/new.svg) Versão e metadados atualizados para 3.2.0. Nenhuma outra alteração de dependência.

### Versão v3.1.0

**Data de lançamento**: 26 de janeiro de 2024

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adição de novas dependências de pacote:

- **Exportador de dados de permissão de categoria** (`magento/module-category-permission-data-exporter`) para exportar dados de permissão de categoria usados pelo serviço de catálogo.
- **Administrador de Sincronização de Catálogo** `magento/module-catalog-sync-admin` para interface do usuário do Administrador e configuração relacionada à sincronização de catálogo.

![Novo](../assets/new.svg) Versão e metadados atualizados para a versão 3.1.0.

## Instalador do Serviço de Catálogo

O instalador é fornecido com a extensão do Serviço de catálogo e lida com verificações de instalação e ambiente para que o Serviço de catálogo corresponda à sua pilha do Commerce.

- Para clientes do **Adobe Commerce as a Cloud Service**, a versão mais recente do instalador está instalada em seu ambiente.

- Para **Adobe Commerce na infraestrutura de nuvem** ou **no local**, mantenha o instalador alinhado ao [metapackage do Serviço de Catálogo](#catalog-service-metapackage).

Sempre que você usa o Composer para atualizar o `magento/catalog-service`, o pacote do instalador é atualizado automaticamente para a versão mais recente. Você também pode usar o Composer para atualizar o `magento/catalog-service-installer` separadamente quando essas notas de versão descreverem uma alteração necessária, por exemplo, suporte para uma nova versão do PHP. Dessa forma, sua ferramenta de instalação permanece compatível com a versão do Serviço de catálogo executada.

### versão v1.0.6

**Data de lançamento**: 25 de março de 2026

![Novo](../assets/new.svg) **PHP 8.5**—Garante a compatibilidade quando o Serviço de Catálogo opera no PHP 8.5.

## Documentação relacionada

- Para projetos implantados no **Adobe Commerce na nuvem, no local ou Adobe Commerce as a Cloud Service, consulte a seguinte documentação:

   - [Guia do Serviço de catálogo](overview.md)
   - [Referência da API do GraphQL do Serviço de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Guia de administração do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Guia do Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Guia do Adobe Commerce na nuvem](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- Para projetos que usam o **Adobe Commerce Optimizer** ou o **Adobe Commerce Optimizer Connector**, consulte a seguinte documentação:

   - [Guia do desenvolvedor de serviços de merchandising](https://developer.adobe.com/commerce/services/optimizer/)
   - [Referência da API do GraphQL de merchandising](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Guia do Adobe Commerce Optimizer](../optimizer/overview.md)
