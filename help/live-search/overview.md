---
title: O que é  [!DNL Live Search]?
description: O [!DNL Live Search] do Adobe Commerce fornece uma experiência de pesquisa rápida, relevante e intuitiva.
recommendations: noCatalog
exl-id: 15399216-6a96-4d0b-bbc1-293190cb9e14
source-git-commit: d07f36a71247a96bc2dd950867c2862205238d88
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# O que é [!DNL Live Search]?

[!DNL Live Search] é um recurso que substitui os recursos de pesquisa padrão no Adobe Commerce. Quando o recurso [!DNL Live Search] é habilitado e configurado, o campo de texto de pesquisa padrão é substituído pelo campo de texto [!DNL Live Search]. O [!DNL Live Search] também inclui o widget Página de listagem de produtos (PLP), que fornece recursos de filtragem robustos para navegar pelos resultados da pesquisa.

Com [!DNL Live Search], você pode:

- Crie experiências de pesquisa significativas para ajudar compradores e compradores a encontrar o que desejam com o menor esforço possível.
- Aproveite a faceta dinâmica alimentada por IA e a reclassificação dos resultados de pesquisa em resposta aos comportamentos do comprador na sessão.
- Use um serviço leve baseado em SaaS que ofereça atualizações fáceis e esteja incluído em sua licença, reduzindo o custo total de propriedade.
- Obtenha conhecimento técnico habilitando a API do GraphQL, a flexibilidade headless, os ambientes de sandbox da API e o SaaS ultrarrápido.

>[!IMPORTANT]
>
>Quando se trata de pesquisa no site, o Adobe Commerce oferece opções. Antes da implementação, reveja as informações de [Limites e Limites](boundaries-limits.md) para garantir que o [!DNL Live Search] seja adequado às suas necessidades comerciais.

## Arquitetura

O lado Adobe Commerce da arquitetura inclui hospedar a pesquisa *Admin*, sincronizar dados de catálogo e executar o serviço de consulta. Depois que o [!DNL Live Search] for instalado e configurado, a Adobe Commerce começará a compartilhar dados de pesquisa e catálogo com os serviços SaaS. Neste ponto, os usuários administradores podem configurar, personalizar e gerenciar [aspectos](facets.md), [sinônimos](synonyms.md) e [regras de merchandising](category-merch.md) de pesquisa.

![Fluxo de Dados do Live Search](assets/ls-cs-data-flow.png)

## Tour rápido

Com foco na velocidade, relevância e facilidade de uso, o [!DNL Live Search] é um divisor de águas para compradores e comerciantes. Assista ao vídeo a seguir e faça um rápido tour pelo [!DNL Live Search] na loja.

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

Para ver um vídeo mais detalhado sobre o uso e a configuração do Live Search, consulte o tópico [Demonstração completa sobre [!DNL Live Search]](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration).

### Pesquisar enquanto digita

[!DNL Live Search] responde com produtos sugeridos e uma imagem em miniatura dos principais resultados da pesquisa em um [popover](storefront-popover.md), à medida que os compradores digitam consultas na caixa [Pesquisa](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search). A página [detalhes do produto](https://experienceleague.adobe.com/en/docs/commerce-admin/start/storefront/storefront) é exibida quando os compradores clicam em um produto sugerido ou em destaque. Um link _Exibir todos_ no rodapé do popover exibe a página de resultados da pesquisa.

[!DNL Live Search] retorna resultados de &quot;pesquisa ao digitar&quot; para uma consulta de dois ou mais caracteres. Para uma correspondência parcial, o número máximo de caracteres por palavra é 20. O número de caracteres na consulta não é configurável. O popover inclui os campos `name`, `sku` e `category_ids`.

![Exemplo de vitrine - pesquise à medida que digita](assets/storefront-search-as-you-type.png)

### Exibir todos os resultados da pesquisa

Para listar todos os produtos retornados pela consulta &quot;pesquisar ao digitar&quot;, clique em _Exibir todos_ no rodapé do popover.

![Exemplo de vitrine - aspectos do preço](assets/storefront-view-all-search-results.png)

### Como [!DNL Live Search] lida com erros de digitação

Quando uma pesquisa é feita, o [!DNL Live Search] executa uma pesquisa não difusa que não leva em conta erros de digitação. Se nenhum resultado for encontrado, [!DNL Live Search] executará uma segunda pesquisa difusa, o que leva em consideração pequenos erros de digitação. A pesquisa difusa é executada com uma distância máxima de edição de 1. Esta distância de edição usa o conceito de [Distância de Levenshtein](https://en.wikipedia.org/wiki/Levenshtein_distance) e permite três tipos de operações:

| Operação | Descrição | Exemplo |
|---|---|---|
| Inserção | Adição de um caractere. | &quot;cat&quot; -> &quot;cart&quot; |
| Exclusão | Remoção de um caractere. | &quot;cart&quot; -> &quot;cat&quot; |
| Substituição | Substituição de um caractere por outro. | &quot;cart&quot; -> &quot;cast&quot; |

Além da lógica de pesquisa difusa, transposições também são contabilizadas, ou seja, onde dois caracteres adjacentes em uma palavra são trocados, por exemplo, &quot;o&quot; em vez de &quot;o&quot;. Observe que esses limites de edição são por palavra e não pela frase como um todo.

### Pesquisa filtrada com facetas

A pesquisa filtrada usa várias dimensões de valores de atributo, ou [facetas](facets.md), como critérios de pesquisa. A seleção de filtros é definida pelo comerciante e muda de acordo com os produtos retornados, com as facetas mais usadas fixadas no topo da lista.

Use facetas como parâmetros de URL:`http://yourwebsite.com?color=red`, e o Live Search filtra os resultados com base nesses valores de atributo.

### Sinônimos

[Sinônimos](synonyms.md) expanda o alcance e ajuste a nitidez do foco das consultas ao incluir palavras que os compradores podem usar diferentes daquelas no catálogo. Você pode ajustar o dicionário de sinônimo para manter os compradores envolvidos e no caminho para comprar.

### Regras de merchandising

As [regras](rules.md) de merchandising moldam a experiência de compra com instruções if-then que adicionam lógica e eventos à pesquisa. Você pode facilmente impulsionar ou enterrar produtos para uma promoção, temporada ou outro período de tempo.

### Suporte a termos de pesquisa

[!DNL Live Search] dá suporte a [redirecionamentos de termo de pesquisa](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) do Commerce. Por exemplo, os usuários podem procurar por um termo como &quot;Taxas de envio&quot; e ser direcionados diretamente para a página de taxas de envio.

## Componentes do Live Search

- [!DNL Live Search] [widget de popover](storefront-popover.md) é a caixa que é aberta no campo de pesquisa que contém os resultados da pesquisa.
- O [widget Página de listagem de produtos](plp-styling.md) (PLP) fornece uma página de listagem de produtos pesquisável com facetas e suporte a sinônimos. O widget está instalado e ativado no Live Search 4.0.0+ e substitui o Adaptador de pesquisa.
- (**Desaprovado**) O Adaptador de Pesquisa foi o precursor do widget PLP e foi instalado com o Live Search &lt; 4.0.0. Se você estiver usando uma versão do Live Search anterior à 4.0.0, a Commerce recomenda atualizar para receber os benefícios dos recursos do widget PLP e melhorias futuras. O Search Adapter será atualizado somente para resolver problemas de segurança.

## [!DNL Live Search] espaço de trabalho

O [!DNL Live Search] [espaço de trabalho](workspace.md) é a área no Administrador em que você configura os recursos do [!DNL Live Search], como sinônimos, facetas e Categoria de Merchandising.

## Eventos

[!DNL Live Search] usa [eventos](events.md) para calcular os painéis [Merchandising inteligente](category-merch.md) e [desempenho](performance.md). O evento é fornecido com implementações padrão. O evento para frente de loja headless deve ser ativado manualmente.

## Política de retenção de dados do catálogo

Se você não enviar uma consulta de pesquisa para os dados do catálogo no ambiente de teste por 90 dias consecutivos, os dados do catálogo serão definidos para o modo de hibernação e nenhum dado será retornado para qualquer consulta de pesquisa. Os dados do catálogo em seu ambiente de produção não são afetados por essa política.

Para reativar os dados do catálogo no ambiente de teste, [envie uma solicitação de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) com o título: &quot;Reativar [!DNL Live Search]&quot; e incluir as IDs de ambiente. Os dados do catálogo no ambiente de teste devem ser restaurados em algumas horas.
