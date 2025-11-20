---
title: Notas de versão do [!DNL Catalog Service]
description: As informações da versão mais recente do  [!DNL Catalog Service] para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 93adab667d1d8ed40c9d5668db376493bd8ae684
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Notas de versão do [!DNL Catalog Service]

Essas notas de versão descrevem as versões mais recentes do [!DNL Catalog Service].
O suporte é fornecido para a versão principal atual lançada. As notas de versão para versões mais antigas são fornecidas para referência.
As atualizações incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos

## Versão principal atual

### Versão V1.26

_22 de outubro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) O esquema do GraphQL agora inclui o atributo `lastModifiedAt` nas informações do produto. Esse carimbo de data e hora preciso ajuda os clientes a garantir que os mapas de site reflitam com precisão as atualizações mais recentes de seus produtos. Também ajuda os mecanismos de pesquisa como o Google a determinar quando a reindexação é necessária, otimizando o processo de rastreamento e evitando problemas relacionados às datas agressivas da última modificação usadas quando informações precisas não estão disponíveis. <!--DATA-6209-->

## Versões anteriores

+++ Versões anteriores

### Versão V1.23

_22 de agosto de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Agora é possível recuperar informações do produto sem dados de substituição de produto (preços). Em versões anteriores, essas consultas retornavam o seguinte erro:
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### Versão V1.22

_13 de agosto de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para recuperar todas as variantes por SKU de produto. Consulte a [Referência da API do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Versão V1.22

_13 de agosto de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para recuperar todas as variantes por SKU de produto. Consulte a [Referência da API do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Versão V1.19

_23 de maio de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes


![Correção](../assets/fix.svg) <!--DATA-5033-->O sinalizador `InStock` para valores de opção agora leva em consideração o status `enabled` de escopo da variante de produto.

![Correção](../assets/fix.svg) <!--DATA-5888-->Adicione suporte para preços de produtos que exigem números grandes (até 16 dígitos) e maior precisão decimal (até 4 casas decimais). Para aplicar as atualizações de configuração de preço ao catálogo existente, ressincronize os dados do catálogo no [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) ou usando a [interface de linha de comando do Adobe Commerce](../landing/catalog-sync.md#command-line-interface).

#### Limitações conhecidas

Os seguintes recursos ainda não são compatíveis:

* O tamanho máximo da carga dos atributos dinâmicos é de 9 MB.
* O preço do produto do Grupo pode ser calculado com preços simples do produto.
* Em uma matriz de imagens, somente a primeira imagem contém funções.

Resolva as seguintes limitações usando a API Mesh e a API Core GraphQL:

* Preço Mínimo Anunciado
* Nível de preços
* Pacote de produtos com preços fixos

Para obter detalhes e exemplos, consulte [Serviço de Catálogo e API Mesh](mesh.md)

### Versão V1.18

_11 de abril, 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para o PHP 8.3.

![Novas](../assets/new.svg) As consultas de [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) e [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) agora retornam dados de opções personalizáveis para produtos simples e complexos.<!--DATA-5538-->

### Versão V1.17

_22 de fevereiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) O [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) está disponível agora. Este painel renovado fornece informações sobre fluxos de dados para [!DNL Product Recommendations], [!DNL Live Search] e [!DNL Catalog Service]. O suporte para este recurso foi introduzido na v3.1.0 do metapackage `catalog-service`.

### Versão V1.16

_13 de fevereiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

Os vídeos de produtos ![Novos](../assets/new.svg) agora têm suporte da API de Serviço de Catálogo.
![Correção](../assets/fix.svg) As opções indisponíveis agora são mostradas no widget PDP.

#### Limitações conhecidas

Estes recursos ainda não são compatíveis:

* O tamanho máximo da carga dos atributos dinâmicos é de 9 MB.
* Preço de produto de grupo. Esse valor pode ser calculado com preços simples do produto.
* Em uma matriz de imagens, somente a primeira imagem contém funções.

As seguintes limitações podem ser resolvidas usando a API Mesh e a Core GraphQL API:

* Preço Mínimo Anunciado
* [Nível de preços](mesh.md)

### Versão V1.13

_12 de outubro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo oferece suporte ao sinalizador `inStock` para variantes de produtos.
![Novo](../assets/new.svg) Os campos `urlKey` e `externalId` foram adicionados ao esquema do GraphQL.
![Novos](../assets/new.svg) Produtos e cartões-presente baixáveis agora têm suporte.

### Versão V1.12

_19 de setembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de catálogo agora usa a [indexação de preços SaaS](../price-index/price-indexing.md).
![Correção](../assets/fix.svg) Esta versão contém correções de erros e melhorias no lado do serviço.

### Versão V1.11

_18 de julho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora dá suporte à consulta do GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para Recomendações de Produto.

### Versão V1.10

_27 de junho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) A API de Serviço de Catálogo agora dá suporte a `related products`.

### Versão V1.7

_12 de abril de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora limpa as variantes de produtos excluídas.
![Corrigir](../assets/fix.svg) melhorias na escalabilidade e no desempenho da infraestrutura.

### Versão V1.6

_28 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Amostras adicionadas à consulta [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Novo](../assets/new.svg) Adicionou a capacidade de obter `entityId` usando a [API Mesh](mesh.md).

### Versão V1.5

_6 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adicionado [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) funcionalidade GraphQL.
![Correção](../assets/fix.svg) Desempenho e escalabilidade da API aprimorados.

### Versão V1.4

_7 de fevereiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) metapackage de serviço de catálogo publicado para simplificar as etapas de instalação.
![Corrigir](../assets/fix.svg) aprimoramentos de desempenho e escalabilidade da API.

### Versão V1.3

_17 de janeiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Simplificou e melhorou a experiência de integração.
![Novo](../assets/new.svg) Novos pontos de extremidade de sandbox do cliente estão disponíveis para teste de pré-produção.
![Novo](../assets/new.svg) Suporte adicionado para produtos virtuais.
![Corrigir](../assets/fix.svg) aprimoramentos de desempenho e escalabilidade da API.

### Versão V1.1

_18 de novembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

O ![Novo](../assets/new.svg) Serviço de Catálogo agora oferece suporte à [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) da Adobe.
![Correção](../assets/fix.svg) Aprimoramento da escalabilidade da API e desempenho geral.

### Versão V1.0

_4 de outubro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Agora oferece suporte a produtos agrupados.
![Novo](../assets/new.svg) substituições de visibilidade B2B adicionadas. Agora os produtos podem ser pesquisados e adicionados ao carrinho para grupos específicos de clientes.
O serviço ![Fix](../assets/fix.svg) agora está mais estável e melhorou o desempenho.

### Versão 0.3 - Beta+

_12 de setembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Suporte a novas](../assets/new.svg) imagens para variantes: as imagens do produto são retornadas com base nas opções selecionadas
![Novas](../assets/new.svg) funções para suporte a preços: permitir que somente membros de grupos de clientes específicos vejam o preço dos produtos
![Correção](../assets/fix.svg) Estabilidade e desempenho do serviço aprimorados
![Novas](../assets/new.svg) atualizações são recebidas quando produtos são excluídos do catálogo

### Versão do Beta

_9 de agosto de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) As consultas `products` e `refineProduct` retornam os seguintes dados:

* Atributos de produto predefinidos (sistema).
* Atributos dinâmicos do produto e filtrá-los por função (página de exibição do produto/página da lista de produtos).
* Opções de produto.
* Imagens de produto e filtrá-las por função (PDP/PLP).
* Um preço específico para produtos simples e faixas de preço para produtos configuráveis.
* Preços de grupo e faixas de preços do cliente. Eles retornam um preço padrão de fallback para os compradores sem um grupo de clientes.
* Tipos de produto que usam preços específicos do cliente B2B.
