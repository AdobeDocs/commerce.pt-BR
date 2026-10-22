---
title: Melhore a descoberta de produtos com o Adobe Commerce Live Search
description: Saiba como usar insights de desempenho de pesquisa e pesquisa semântica para ajudar os compradores a encontrar produtos relevantes.
audience: Merchandisers, commerce administrators, and store owners
autotag-review: '2026-10-21T12:57:39.807Z'
TQID: 'https://experienceleague.adobe.com/vUbbKdcd7RFb3YUNNjlW4u7AgtiXJKeZeRs9uJwxYyY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: cdfd3bc1-dc23-5cf0-b965-d3c0c55cde67
    internal-label: Best Practices
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: 125c1f49-aefd-5f34-a252-288937f95f6b
    internal-label: Marketing Tools
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%
---

# Melhore a descoberta de produtos com o Adobe Commerce Live Search

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Retrato de Sandra Gonzalez Mangana" src="../../assets/guidance-and-insights/live-search-author-avatar-sgonzalezmangana.png" width="96"><br><strong>Sandra Gonzalez Mangana</strong><br><em>Gerente de Produto Sênior</em></td>
</tr>
</table>

*Ajude os compradores a encontrar os produtos necessários com insights de desempenho de pesquisa e pesquisa semântica.*

Ter os produtos certos em seu catálogo é apenas parte da experiência de compra. Os compradores também precisam encontrar esses produtos usando as palavras, frases e perguntas que eles naturalmente usam.

O Adobe Commerce Live Search fornece insights de desempenho de pesquisa que podem ajudá-lo a detectar problemas de descoberta e refinar a experiência. Use esses insights para investigar onde os compradores têm dificuldade, não apenas se a pesquisa retorna resultados.

## Procure sinais no desempenho da pesquisa

No espaço de trabalho Desempenho do Live Search, analise métricas como pesquisas exclusivas, pesquisas sem resultados, resultados populares, taxa de click-through, taxa de conversão e posição média do clique. Use-as para identificar tendências e decidir quais consultas ou produtos precisam de atenção. [Desempenho](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/performance)

![Espaço de trabalho Desempenho do Live Search mostrando pesquisas exclusivas, posição média de cliques, taxa de cliques, taxa de conversão e taxa de resultados zero, com guias para pesquisas exclusivas, resultados zero e resultados populares](../../assets/guidance-and-insights/live-search-performance-dashboard.png){width="800" zoomable="yes"}

*O espaço de trabalho Desempenho do Live Search mostra as métricas a serem revisadas. Os valores mostrados são dados de exemplo.*

Considere estes sinais:

- **Pesquisas sem resultados:** consultas sem resultados podem apontar para lacunas no catálogo, nas informações do produto ou na configuração da pesquisa. O objetivo é manter pesquisas com resultados nulos abaixo de 5%. Uma taxa acima desse limite é um sinal que vale a pena investigar.
- **Poucos click-throughs ou cliques fracos:** Os compradores podem estar vendo resultados que não correspondem às suas necessidades ou os produtos relevantes podem não ser suficientemente proeminentes. Para garantir o engajamento, direcione pelo menos 50% das pesquisas para resultar em um clique no produto.
- **Baixa conversão da pesquisa:** verifique se a pesquisa está ajudando os compradores a moverem de uma consulta para uma compra. Objetivo: uma taxa de conversão superior a 3 %.

Trate-os como um referencial e sinais de diagnóstico, não como uma falha ou aprovação universal. O desempenho varia de acordo com o setor, a complexidade do catálogo, o comportamento do cliente e a forma como cada métrica é medida. Estabeleça uma linha de base para sua loja e compare o desempenho ao longo do tempo. Os resultados podem variar de acordo com o catálogo, os compradores e como você avalia os resultados.

## Combinar a intenção do comprador, não apenas palavras exatas

Nem sempre os compradores descrevem os produtos usando a terminologia do catálogo. Alguém que procura &quot;sapatos confortáveis para ficar o dia todo&quot;, por exemplo, pode estar interessado em produtos descritos como &quot;tênis para caminhada acolchoados&quot;.

A pesquisa semântica usa significado e contexto juntamente com a correspondência de palavras-chave, ajudando a conectar consultas em linguagem natural a produtos relevantes, mesmo quando a consulta não corresponde exatamente ao texto do catálogo. O Live Search combina palavra-chave e correspondência semântica em uma experiência de pesquisa. [Pesquisa semântica](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)

A correspondência semântica pode ajudar com pesquisas exploratórias, mas a relevância ainda depende dos produtos e das informações disponíveis em seu catálogo. Para pesquisas envolvendo um modelo exato, especificação ou requisito de compatibilidade, verifique se os resultados permanecem precisos.

## Verifique a pesquisa semântica para sua implantação

A configuração depende do produto Adobe Commerce que você usa:

- **Adobe Commerce na infraestrutura de nuvem ou no local:** A pesquisa semântica do Live Search está disponível para o Adobe Commerce 2.4.4 e posterior. No Admin, vá para Marketing > SEO &amp; Search > Live Search, abra Configurações, ative a pesquisa semântica e salve. É compatível com catálogos em inglês. [Configurações—Pesquisa semântica](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/settings)
- **Adobe Commerce as a Cloud Service:** o sistema habilita a pesquisa semântica por padrão. É compatível com catálogos em inglês. [Pesquisa semântica](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/semantic-search)
- **Adobe Commerce Optimizer:** o sistema habilita a pesquisa semântica por padrão. Opcionalmente, é possível ajustar controles como aumento semântico e o limite de similaridade. As configurações também incluem opções de pesquisa difusa. [Pesquisa Semântica](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/semantic-search) · [Configurações—Ajuste opcional](https://experienceleague.adobe.com/en/docs/commerce/optimizer/settings)

## Transformar insights de pesquisa em ação

Use um ciclo de análise contínua para melhorar a descoberta de produtos:

1. **Localizar consultas para investigar.** Revise pesquisas sem resultados, consultas populares e pesquisas com baixo engajamento.
2. **Verifique o que o comprador está solicitando.** Determine se a consulta aponta para um produto ausente, uma incompatibilidade de texto ou dados de produto não claros.
3. **Melhore as informações sobre o produto.** Torne os atributos e descrições do produto precisos e úteis para os termos que os compradores usam. Para o Live Search, a Adobe recomenda configurar os atributos e pesos pesquisáveis apropriados e garantir que os dados do atributo sejam relevantes. [Práticas recomendadas do Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
4. **Refine a experiência de pesquisa.** Quando apropriado, use regras de pesquisa, sinônimos e aspectos para ajudar os compradores a encontrar e restringir resultados relevantes. [Práticas recomendadas do Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/best-practice)
5. **Revise os resultados e repita.** Monitore as mesmas consultas e sinais de desempenho após fazer alterações e ajuste com base no que os compradores fazem.

## Faça com que cada pesquisa conte

Uma consulta de pesquisa é um sinal do que um comprador deseja. Ao emparelhar os insights de desempenho de pesquisa com informações relevantes sobre o produto e os recursos de pesquisa certos, é possível facilitar para os compradores a descoberta de produtos que atendem às suas necessidades.

### Saiba mais

- [O que é o Live Search?](../../../live-search/overview.md)
- [Práticas recomendadas do Live Search](../../../live-search/best-practice.md)
- [Pesquisa semântica](../../../live-search/semantic-search.md) do Adobe Commerce na infraestrutura em nuvem
- [Pesquisa semântica](../../../optimizer/setup/semantic-search.md) do Adobe Commerce Optimizer
