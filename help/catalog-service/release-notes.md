---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: As informações da versão mais recente do  [!DNL Catalog Service] para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 7e7ffa0684d0135baf362f94d286d80de89a6bd6
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 0%

---

# Notas de versão do [!DNL Commerce Storefront Catalog Service]

Essas notas de versão abordam as atualizações mais recentes do serviço de catálogo da Commerce, incluindo:

- **Versões do Serviço de Catálogo da Loja**

   - Aprimoramentos do esquema da API do Serviço de catálogo para recuperação de dados aprimorada.
   - Melhorias de segurança, desempenho e confiabilidade para a API do serviço de catálogo e infraestrutura subjacente.

- **Versões do metapackage do Serviço de Catálogo**

   - Dependências atualizadas para melhorar o desempenho, a estabilidade e a compatibilidade com outros componentes do Adobe Commerce.

As atualizações são categorizadas por tipo:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos

O suporte é fornecido para a versão mais recente. As notas de versão para versões mais antigas estão incluídas para referência.

## Serviço de Catálogo da Loja

### versão v1.46

_11 de dezembro de 2025_

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade. <!--DATA-6852, DATA-6864-->

### versão v1.45

_17 de novembro de 2025_

![Novo](../assets/new.svg) **Filtragem de Atributo por Nome**-A consulta do GraphQL `productSearch` agora oferece suporte à filtragem de atributos de produto com o campo `names`. <!--DATA-6831--> Com este filtro, você pode:

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

### versão v1.44

_6 de novembro de 2025_

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade. <!--DATA-6852, DATA-6864-->

### versão v1.43

_3 de novembro de 2025_

![Novo](../assets/new.svg) **Camadas de Produto para personalização de produto multidimensional**—Adicionou suporte para entrega de conteúdo específico de canal e com reconhecimento de localidade para implementações do Adobe Commerce Optimizer.<!--DATA-6632-->

- Atender conteúdo de produto diferente a segmentos de clientes diferentes
- Aplicar personalizações específicas de localidade sem duplicar dados básicos
- Controlar substituições em nível de campo com máscaras de camada
- Suporte a camadas de conteúdo premium, sazonais e otimizadas para dispositivos móveis

  As camadas são recuperadas usando a consulta `products` existente, são aplicadas no lado do servidor a partir de cabeçalhos de solicitação e não exigem alterações de esquema. Consulte [Camada do catálogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-layer) no _Guia do Adobe Commerce Optimizer_.

![Correção](../assets/fix.svg) Os produtos agrupados agora podem ser consultados quando o pai não tem preços; os produtos filho retornam suas próprias funções de visibilidade.<!--DATA-6779-->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade. <!--DATA-6721, DATA-6864-->

### versão v1.42

_8 de setembro de 2025_

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

### versão v1.41

_2 de setembro de 2025_

![Correção](../assets/fix.svg) **Tratamento de erros aprimorado para informações de preços ausentes**—Quando os dados de preços ainda não são recebidos, a API retorna `null` para o campo de preços em vez de gerar um erro, permitindo que os clientes lidem com os dados ausentes normalmente.<!--DATA-6612-->

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar o desempenho e a estabilidade.<!--DATA-6671-->

### Versão v1.40

_30 de julho de 2025_

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6619-->

### versão v1.39

_24 de julho de 2025_

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

### versão v1.38

_15 de julho de 2025_

![Novos](../assets/new.svg) **Tipos de produto de cartão-presente**. O Serviço de vitrine do catálogo agora oferece suporte a atributos de produto como objetos JSON ou matrizes, permitindo o gerenciamento flexível de tipos complexos, como cartões-presente.<!--DATA-6573-->


### versão v1.37

_20 de junho de 2025_

![Nova](../assets/new.svg) **Configuração do catálogo de preços hierárquico** — Intervalos de preços precisos para o catálogo de preços pai-filho. Os cálculos respeitam a hierarquia e as regras herdadas; reduz os erros de precificação quando vários catálogos de preços são vinculados. Somente Adobe Commerce Optimizer. Consulte [Catálogos de Preços](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![Novo](../assets/new.svg) **Chaves que não diferenciam maiúsculas de minúsculas** — As pesquisas de chave em consultas agora não diferenciam maiúsculas de minúsculas, reduzindo os erros de maiúsculas e minúsculas. <!--DATA-6494, DCAT-2495-->

### versão v1.36

_20 de junho de 2025_

![Novo](../assets/new.svg) **Eventos de E/S Públicos para a Loja de Catálogos**—Foram adicionados eventos de E/S públicos para integração e observação em tempo real (CSS e EDS).<!--DATA-6329-->

![Novo](../assets/new.svg) **Renderização no Servidor (SSR)**—Melhorias de arquitetura para oferecer suporte ao SSR para melhor desempenho, SEO e UX em catálogos grandes.<!--DATA-6278, DATA-6280-->

![Novo](../assets/new.svg) **Infraestrutura e Segurança**—Novas funções do AWS, integração do ServiceNow e pipelines de CI/CD para o serviço de eventos.

![Novo](../assets/new.svg) **Formatos de evento e capacidade de observação** — cargas simplificadas, monitoramento aprimorado, dados aprimorados de eventos de variantes.<!--DATA-6332, DATA-6402, -->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6404, DATA-6410, -->

+++ Versões anteriores

## versão v1.35

_13 de junho de 2025_

![Novo](../assets/new.svg) **Recuperar dados não armazenados em cache**-Habilite o cabeçalho `Magento-Is-Preview` para passar dados não armazenados em cache do ponto de extremidade do catálogo para o Serviço de Pesquisa.<!--DATA-6345-->

![Novo](../assets/new.svg) **Opções de produtos de seleção múltipla**. A API do GraphQL agora expõe se as opções de produtos permitem várias seleções (por exemplo, agrupar &quot;escolher vários itens&quot;).<!--DATA-6487-->

![Novo](../assets/new.svg) Atualização da validação de preço na assimilação de dados para oferecer suporte a produtos sem preços.<!--DATA-6098-->

![Correção](../assets/fix.svg) Tratamento de erros aprimorado para preços de pacotes simples no Adobe Commerce Optimizer, garantindo a conformidade com a documentação da API.<!--DATA-6541-->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6273, DATA-6485, -->

## versão v1.34

_23 de março de 2025_

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-5732-->

## versão v1.33

_29 de abril de 2025_

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura. A infraestrutura agora é compatível com catálogos extremamente grandes (até ~440 milhões de SKUs) sem afetar as cargas de trabalho existentes.

### versão v1.32

_28 de março de 2025_

![Corrigir](../assets/fix.svg) Atributos sem funções não são mais indexados por padrão para o catálogo combinável, melhorando o tempo de indexação e reduzindo o armazenamento. O comportamento herdado pode ser reativado por meio de um sinalizador de recurso.

![Corrigir](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade. <!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### versão v1.31

_18 de fevereiro de 2025_

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6389, DATA-6367, DATA-6373-->

### versão v1.30

_9 de dezembro de 2024_

Versão principal: [modelo de dados de catálogo combinável](https://developer.adobe.com/commerce/services/optimizer/) para frentes de loja headless, gerenciamento de cabeçalho e manipulação de dados de produto.

![Novo](../assets/new.svg) **Modelo de Dados de Catálogo de Composição (CCDM)** — Oferece suporte a clientes que usam o catálogo de composição para frentes de loja headless. Os novos endpoints aceitam a Exibição de catálogo e as IDs de política (compatíveis com versões anteriores). Detalhes e preços do produto configuráveis com paginação interna.<!--DATA-6018, DATA-6288-->

![Novo](../assets/new.svg) **Gerenciamento de Cabeçalho**-`AC-Locale` renomeado para `AC-Scope-Locale` para operações de API de catálogo combinável; mapeamento de cabeçalho e valores padrão especificados.<!--DATA-6303, DATA-6078-->

![Novos](../assets/new.svg) **Dados e preços do produto**-Suporte para modelo de dados de catálogo combinável e manipulação de preços aprimorada para produtos configuráveis.<!--DATA-6279-->

`CurrencyEnum` atualizado para oferecer suporte a `NONE` para consultas de pesquisa de produtos, alinhado à lógica de federação.<!--DATA-6285-->

![Correção](../assets/fix.svg) **Infraestrutura e atualizações**—Melhorias no nível do sistema para segurança, desempenho e estabilidade.

![Correção](../assets/fix.svg) As opções de pacote de produtos agora exibem apenas os produtos habilitados.<!--DATA-6347-->

### versão v1.29

_9 de dezembro de 2024_

![Novo](../assets/new.svg) **Ordenação de imagens em consultas de produtos**—As imagens de produtos no campo `images` do GraphQL agora seguem a exportação de catálogo `sortOrder` para comportamento consistente da loja e da API.<!--DATA-6258-->

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6619-->

### versão v1.28

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### versão v1.27

_26 de setembro de 2024_

![Correção](../assets/fix.svg) melhorias no nível do sistema e na infraestrutura para aprimorar a segurança, o desempenho e a estabilidade.<!--DATA-6243-->

### versão v1.26

_22 de outubro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![novo](../assets/new.svg) esquema do GraphQL agora inclui `lastModifiedAt` nas informações do produto para mapas de site precisos e reindexação do mecanismo de pesquisa (por exemplo, Google). <!--DATA-6209-->

### versão v1.23

_22 de agosto de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) As informações do produto agora podem ser recuperadas sem os dados de substituição de produto (preços). Anteriormente, estas consultas retornavam: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### versão v1.22

_13 de agosto de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para recuperar todas as variantes por SKU de produto. Consulte a [Referência da API do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### versão v1.19

_23 de maio de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes


![Correção](../assets/fix.svg) <!--DATA-5033-->O sinalizador `InStock` para valores de opção agora respeita o status `enabled` de escopo da variante de produto.

![Correção](../assets/fix.svg) <!--DATA-5888-->Suporte adicionado para preços de produtos com até 16 dígitos e 4 casas decimais. Ressincronize a partir do [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) ou da [CLI](../landing/catalog-sync.md#command-line-interface) para aplicar as atualizações.

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

### versão v1.18

_11 de abril, 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para o PHP 8.3.

![Novas](../assets/new.svg) As consultas de [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) e [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) agora retornam dados de opções personalizáveis para produtos simples e complexos.<!--DATA-5538-->

### versão v1.17

_22 de fevereiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) O [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) agora está disponível para fluxos de dados (Product Recommendations, Live Search, Catalog Service). Requer `catalog-service` metapackage v3.1.0+.

### versão v1.16

_13 de fevereiro de 2024_

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

### versão v1.13

_12 de outubro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo oferece suporte ao sinalizador `inStock` para variantes de produtos.
![Novo](../assets/new.svg) Os campos `urlKey` e `externalId` foram adicionados ao esquema do GraphQL.
![Novos](../assets/new.svg) Produtos e cartões-presente baixáveis agora têm suporte.

### versão v1.12

_19 de setembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de catálogo agora usa a [indexação de preços SaaS](../price-index/price-indexing.md).
![Correção](../assets/fix.svg) Esta versão contém correções de erros e melhorias no lado do serviço.

### versão v1.11

_18 de julho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora dá suporte à consulta do GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para Recomendações de Produto.

### versão v1.10

_27 de junho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) A API de Serviço de Catálogo agora dá suporte a `related products`.

### versão v1.7

_12 de abril de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora limpa as variantes de produtos excluídas.
![Corrigir](../assets/fix.svg) melhorias na escalabilidade e no desempenho da infraestrutura.

### versão v1.6

_28 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Amostras adicionadas à consulta [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Novo](../assets/new.svg) Adicionou a capacidade de obter `entityId` usando a [API Mesh](mesh.md).

### versão v1.5

_6 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adicionado [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) funcionalidade GraphQL.
![Correção](../assets/fix.svg) Desempenho e escalabilidade da API aprimorados.

### versão v1.4

_7 de fevereiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) metapackage de serviço de catálogo publicado para simplificar as etapas de instalação.
![Corrigir](../assets/fix.svg) aprimoramentos de desempenho e escalabilidade da API.

### versão v1.3

_17 de janeiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Simplificou e melhorou a experiência de integração.
![Novo](../assets/new.svg) Novos pontos de extremidade de sandbox do cliente estão disponíveis para teste de pré-produção.
![Novo](../assets/new.svg) Suporte adicionado para produtos virtuais.
![Corrigir](../assets/fix.svg) aprimoramentos de desempenho e escalabilidade da API.

### versão v1.1

_18 de novembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora oferece suporte à [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) da Adobe.
![Correção](../assets/fix.svg) Aprimoramento da escalabilidade da API e desempenho geral.

### versão v1.0

_4 de outubro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Suporte para produtos agrupados e agrupados.
![Novo](../assets/new.svg) substituições de visibilidade B2B adicionadas. Agora os produtos podem ser pesquisados e adicionados ao carrinho para grupos específicos de clientes.
O serviço ![Fix](../assets/fix.svg) agora está mais estável e melhorou o desempenho.

### Versão 0.3 - Beta+

_12 de setembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novas](../assets/new.svg) imagens de variantes: imagens de produtos retornadas com base nas opções selecionadas.
![Novo](../assets/new.svg) Funções de preço: somente membros de grupos de clientes específicos podem ver os preços do produto.
![Correção](../assets/fix.svg) Estabilidade e desempenho do serviço aprimorados.
![Novas](../assets/new.svg) Atualizações são recebidas quando os produtos são excluídos do catálogo.

### Versão do Beta

_9 de agosto de 2022_

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

- Para o Adobe Commerce no local, a Adobe recomenda o uso do Composer para atualizar o metapackage do Serviço de catálogo nos ambientes de nuvem na versão mais recente.

### Versão v3.3.0

_14 de outubro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Nova](../assets/new.svg) **Atualização de serviços de dados**—`magento/data-services` dependência atualizada para ^8.0.0. Verifique o ambiente e o uso personalizado da API dos serviços de dados para obter compatibilidade com a versão 8.x antes de atualizar.
ea
![Novo](../assets/new.svg) Versão e metadados atualizados para a versão 3.3.0.

### Versão v3.2.0

_12 de abril de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Nova](../assets/new.svg) Versão e metadados atualizados para 3.2.0. Nenhuma outra alteração de dependência.

### Versão v3.1.0

_26 de janeiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adição de novas dependências de pacote:

- **Exportador de dados de permissão de categoria** (`magento/module-category-permission-data-exporter`) para exportar dados de permissão de categoria usados pelo serviço de catálogo.
- **Administrador de Sincronização de Catálogo** `magento/module-catalog-sync-admin` para interface do usuário do Administrador e configuração relacionada à sincronização de catálogo.

![Novo](../assets/new.svg) Versão e metadados atualizados para a versão 3.1.0.

## Documentação relacionada

- Para projetos implantados no **Adobe Commerce na nuvem, no local ou Adobe Commerce as a Cloud Service, consulte a seguinte documentação:

   - [Guia do Serviço de catálogo](overview.md)
   - [Referência da API GraphQL do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Guia de administração do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Guia do Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Guia do Adobe Commerce na Nuvem](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- Para projetos que usam o **Adobe Commerce Optimizer** ou o **Adobe Commerce Optimizer Connector**, consulte a seguinte documentação:

   - [Guia do desenvolvedor de serviços de merchandising](https://developer.adobe.com/commerce/services/optimizer/)
   - [Referência da API do GraphQL de merchandising](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Guia do Adobe Commerce Optimizer](../optimizer/overview.md)
