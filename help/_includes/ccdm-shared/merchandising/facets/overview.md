---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%
---
Facetas é um método de filtragem de alto desempenho que usa várias dimensões de valores de atributo como critérios de pesquisa.

![Resultados de pesquisa filtrados](/help/assets/ccdm-shared/facets/storefront-search-results-run.png)

Em uma faceta, os compradores podem selecionar várias opções, como &quot;Básico&quot; e &quot;Consolado&quot; em &quot;Estilo&quot; e os resultados da pesquisa são atualizados para exibir apenas esses estilos. Da mesma forma, se um comprador selecionar &quot;Básico&quot; em &quot;Estilo&quot; e &quot;Interno&quot; em &quot;Clima&quot;, os resultados da pesquisa exibirão essas seleções.

Qualquer faceta definida pode ser usada como um parâmetro de URL e os resultados são filtrados com base nos valores de parâmetro, por exemplo: `http://yourstore.com?brand=acme&color=red`.

## Agregação de facetas

A agregação de facetas é executada da seguinte maneira: se a loja tiver três facetas (categorias, cor e preço) e os filtros do comprador nos três (cor = azul, preço vai de $10,00 a $50,00, `categories` = `promotions`)

- Agregação `categories` — Agrega `categories`, e aplica os filtros `color` e `price`, mas não o filtro `categories`.
- Agregação `color` — Agrega `color`, e aplica os filtros `price` e `categories`, mas não o filtro `color`.
- Agregação `price` — Agrega `price`, e aplica os filtros `color` e `categories`, mas não o filtro `price`.

## Valores de atributo padrão

O sistema ativa os seguintes atributos de produto por padrão.

| Propriedade | Descrição | Atributo |
|---|---|---|
| Classificável | Usado para Classificação na Lista de Produtos | `price` |
| Pesquisável | Usar na pesquisa | `price` <br />`sku`<br />`name` |

Saiba mais sobre os atributos do produto e suas propriedades:

- Para implantações conectadas a um back-end do Adobe Commerce, consulte [Visão geral dos atributos de produto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/product-attributes)
- Para implantações que usam um back-end Commerce de terceiros, consulte a [API de metadados de assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata).

## Pesquisa em camadas e expansão de tipos de pesquisa

A pesquisa em camadas, ou pesquisa dentro de uma pesquisa, é um sistema de filtragem baseado em atributos que estende a funcionalidade de pesquisa tradicional para incluir parâmetros de pesquisa adicionais. Esses parâmetros de pesquisa adicionais permitem uma descoberta de produtos mais precisa e flexível.

Com a pesquisa em camadas, é possível:

- Permitir que os compradores pesquisem nos resultados da pesquisa.
- Refine ainda mais os resultados usando a indexação de pesquisa `startsWith` e `contains` na segunda camada da pesquisa em camadas.

Os recursos de pesquisa avançada são implementados por meio do parâmetro `filter` na [`productSearch` query](https://developer.adobe.com/commerce/services/reference/graphql/#productsearch) usando operadores específicos:

- **Pesquisa em camadas**—Pesquise em outro contexto de pesquisa—Com esse recurso, você pode executar até duas camadas de pesquisa para suas consultas de pesquisa. Por exemplo:

  - **Pesquisa de Camada 1**—Procure por &quot;motor&quot; em `product_attribute_1`.
  - **Pesquisa de camada 2**—Procure por &quot;número de peça 123&quot; em `product_attribute_2`. Este exemplo procura por &quot;número de peça 123&quot; nos resultados por &quot;motor&quot;.

  A pesquisa em camadas está disponível para a indexação de pesquisa `startsWith` e a indexação de pesquisa `contains` na segunda camada da pesquisa em camadas, conforme descrito abaixo:

- **startsWith indexação de pesquisa** — Pesquise usando a indexação `startsWith`. Esse recurso permite:

  - Procurando produtos em que o valor do atributo começa com uma string especificada.
  - Configurar uma pesquisa &quot;termina com&quot; para que os compradores possam pesquisar produtos em que o valor do atributo termina com uma determinada string.
    - Para ativar uma pesquisa &quot;termina com&quot;, assimile o atributo do produto no modo reverso e use uma string reversa para a chamada de API. Por exemplo, se você deseja procurar um nome de produto que termine com &quot;calças&quot;, é necessário enviá-lo como &quot;stnap&quot;.

- **contém indexação de pesquisa**—Pesquise um atributo usando a indexação contains. Esse novo recurso permite:

  - Procurando uma consulta em uma cadeia de caracteres maior. Por exemplo, se um comprador procurar o número de produto &quot;PE-123&quot; na cadeia de caracteres &quot;HAPE-123&quot;.

    - Observação: este tipo de pesquisa é diferente da [pesquisa de frase](https://developer.adobe.com/commerce/services/reference/graphql/#productsearch) existente, que executa uma pesquisa de preenchimento automático. Por exemplo, se o valor do atributo do seu produto for &quot;calças de ar livre&quot;, uma pesquisa de frase retornará uma resposta para &quot;fora da panela&quot;, mas não retornará uma resposta para &quot;ou formigas&quot;. A contém busca, no entanto, retorna uma resposta para &quot;ou formigas&quot;.

Essas novas condições aprimoram o mecanismo de filtragem de consultas de pesquisa para refinar os resultados da pesquisa. Essas novas condições não afetam a consulta de pesquisa principal.

### Implementação

1. [Definir atributos como pesquisáveis](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

1. Especifique o recurso de pesquisa para esse atributo, como **Contém** (padrão) ou **Começa com**. Para habilitar **Contém** e **Começa com**, especifique no máximo seis atributos para cada um. Além disso, para a indexação **Contains**, o comprimento da sequência de caracteres é limitado a 50 caracteres ou menos.

1. Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/reference/graphql/#productsearch) para obter exemplos de como atualizar suas chamadas de API do Adobe Merchandising Services GraphQL usando os novos recursos de pesquisa do `contains` e do `startsWith`.

   Você pode implementar essas novas condições na página de resultados da pesquisa. Por exemplo, você pode adicionar uma nova seção na página, onde o comprador pode refinar ainda mais os resultados da pesquisa. Você pode permitir que os compradores selecionem atributos específicos do produto, como &quot;Fabricante&quot;, &quot;Número da peça&quot; e &quot;Descrição&quot;. A partir daí, eles pesquisam dentro desses atributos usando as condições `contains` ou `startsWith`.

### Quando usar a pesquisa em camadas em vez de facetas

A pesquisa em camadas e os aspectos atendem a diferentes objetivos na descoberta de produtos, e escolher entre eles depende do seu caso de uso específico:

**Usar pesquisa em camadas para:**

- Pesquisar nos resultados da pesquisa usando vários critérios
- Trabalhar com números de peça, SKUs ou especificações técnicas onde os usuários tenham conhecimento de informações parciais
- Permitir que os compradores reduzam os resultados passo a passo com critérios aninhados
- Reduza o número de chamadas de API combinando vários critérios de pesquisa em uma única consulta
- Implementar padrões de pesquisa específicos da empresa que vão além da navegação padrão facetada

**Usar facetas para:**

- Fornecer filtragem típica de categoria, preço, marca e atributo
- Ofereça opções de filtro intuitivas que os usuários podem entender e selecionar facilmente
- Mostrar opções disponíveis com base nos resultados da pesquisa atual
- Exibir contagens e intervalos de filtros que ajudam os usuários a entender as opções disponíveis
- Trabalhe com características comuns do produto, como cor, tamanho e material

**Prática recomendada:** use a pesquisa em camadas para pesquisas técnicas complexas em que os usuários tenham critérios específicos, e use aspectos para filtragem padrão de comércio eletrônico em que os usuários desejam explorar e refinar opções visualmente.
