---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/synonyms/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Práticas recomendadas de sinônimo

A seguir há uma lista de práticas recomendadas para a criação de sinônimos.

- Por padrão, o sistema gerencia erros ortográficos. Para incluir palavras que os compradores possam usar, configure sinônimos. Essas palavras diferem das especificadas no catálogo. Você não quer perder uma venda porque alguém está procurando um &quot;sofá&quot; enquanto seu produto está listado como um &quot;sofá&quot;. Capture uma ampla variedade de termos de pesquisa inserindo todas as palavras possíveis que os clientes podem usar para encontrar seus produtos. Para melhorar os resultados, [defina sinônimos como unidirecionais ou bidirecionais](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/synonyms/add#step-2-define-the-synonym-by-type).

- Mapeie os nomes de marcas e abreviações para seus nomes completos, por exemplo &quot;HP&quot; para &quot;Hewlett-Packard&quot; e apelidos de produtos comuns, por exemplo &quot;iPhone&quot; para &quot;Apple iPhone&quot;.

- Inclua jargões específicos do setor e termos que os compradores podem usar alternadamente, por exemplo &quot;tênis&quot; e &quot;tênis de corrida&quot;.

- Atualize regularmente a lista de sinônimos com base em novas tendências de pesquisa, adições de produtos e comportamento do comprador.

- Teste a eficácia dos mapeamentos de sinônimos analisando os resultados da pesquisa e o feedback do comprador. Para melhorar a precisão e a relevância, refine os mapeamentos.

- Não use palavras de interrupção, pois elas não tornam os sinônimos mais significativos, mas aumentam a quantidade de dados que devem ser processados. Palavras de interrupção comuns em inglês são filtradas de sinônimos, como:

  a, an, and, são, como, at, be, mas, por, for, in, into, is, it, no, not, of, on, or, tal, que, o, seu, então, há, esses, eles, este, para, foi, será, com

- Não é necessário definir as formas singular e plural de uma palavra como sinônimo. Se você tiver uma mistura de termos no singular e no plural no catálogo, a Pesquisa encontrará o conjunto correto de produtos. Por exemplo, se você usar &quot;planta&quot; e um comprador procurar &quot;calças&quot;, a Pesquisa retornará os produtos corretos. O termo singular &quot;pant&quot; é frequentemente usado na indústria da moda e, às vezes, no varejo, embora a forma plural &quot;pants&quot; seja mais comumente usada em algumas áreas. (A palavra &quot;planta&quot; tecnicamente se refere à parte de uma peça de vestuário que cobre uma perna. Você precisa de um &quot;par de calças&quot; para cobrir ambas as pernas.)

- Seja consistente com a forma como a terminologia é usada em seu catálogo. Lembre-se de que existem diferenças regionais de uso e, às vezes, diferenças no setor.
