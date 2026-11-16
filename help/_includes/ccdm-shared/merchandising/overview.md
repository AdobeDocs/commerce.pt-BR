---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.pt-BR/blob/main/help/_includes/ccdm-shared/merchandising/overview.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Adobe Merchandising

Saiba como criar experiências personalizadas para seus compradores por meio da descoberta de produtos e de recomendações.

Estes serviços da Adobe Merchandising são criados no CCDM (modelo de dados de catálogo combinável), que separa *dados do produto* de *contexto do produto*. Os dados do produto incluem SKUs, atributos, metadados, ativos e preços. O contexto do produto define como esses dados são entregues, incluindo [exibições de catálogo](/help/optimizer/setup/catalog-view.md), [políticas de acesso a dados](/help/optimizer/setup/policies.md) e [fontes de catálogo](/help/optimizer/setup/catalog-sources.md) (localidades). Como as visualizações e políticas do catálogo controlam os dados da loja, você pode compor catálogos personalizados para modelos B2B, B2C e D2C e adaptar experiências de compra sem duplicar dados básicos.

- **Descoberta de produto**—Equipe os merchandisers com ferramentas poderosas para preparar e otimizar a experiência de compra, garantindo que os clientes encontrem os produtos certos rapidamente, na hora certa. Ao ajustar o comportamento de pesquisa, você pode influenciar diretamente a visibilidade, relevância e conversão do produto.

  Com a detecção de produtos, você pode orientar os compradores em direção aos produtos mais relevantes com o mínimo de atrito, configurando:

  - [**Regras de merchandising**](rules/overview.md)—Aumente, interrompa, fixe ou filtre produtos em resultados de pesquisa, listas de produtos padrão e páginas de categoria.
  - [**Facetas**](facets/overview.md)—Configure os filtros que os compradores usam para restringir os resultados da pesquisa e da categoria.
  - [**Sinônimos**](synonyms/overview.md) — Mapeie termos equivalentes para que palavras de pesquisa diferentes retornem os mesmos produtos.

  A pesquisa semântica, que é habilitada por padrão em [Configurações](../settings.md), melhora a relevância para consultas de linguagem natural e baseadas em intenção. Em Configurações, você também pode configurar aspectos de preço, idioma do catálogo e opções avançadas de pesquisa semântica e difusa.

- [**Recomendações**](recommendations/overview.md)—Use inteligência artificial e algoritmos de aprendizado de máquina para analisar o comportamento agregado do visitante e as interações do produto na sua loja. Combinados ao seu catálogo, esses dados fornecem experiências altamente envolventes, relevantes e personalizadas. As recomendações são exibidas na loja como unidades com rótulos, como &quot;Clientes que visualizaram este produto também visualizaram&quot;. Você pode criar, gerenciar e implantar recomendações diretamente do espaço de trabalho do Recommendations e colocá-las na jornada de compras para apoiar metas promocionais, estratégias de venda cruzada e experiências personalizadas.
