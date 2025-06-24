---
title: Práticas recomendadas de sinônimo
description: Saiba mais sobre as práticas recomendadas para implementar sinônimos em sua loja.
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Práticas recomendadas de sinônimo

A seguir há uma lista de práticas recomendadas para a criação de sinônimos.

- [!DNL Adobe Commerce Optimizer] gerencia erros ortográficos por padrão. Você pode configurar sinônimos para incluir palavras que os compradores podem usar que diferem das palavras especificadas em seu catálogo. Você não quer perder uma venda porque alguém está procurando um &quot;sofá&quot;, enquanto seu produto está listado como um &quot;sofá&quot;. Você pode capturar uma ampla variedade de termos de pesquisa inserindo todas as palavras possíveis que os clientes podem usar para encontrar seus produtos. Você pode [definir sinônimos como unidirecionais ou bidirecionais](add.md#step-2-define-the-synonym-by-type) para melhorar os resultados.

- Mapeie os nomes de marcas e abreviações para seus nomes completos, por exemplo &quot;HP&quot; para &quot;Hewlett-Packard&quot; e apelidos de produtos comuns, por exemplo &quot;iPhone&quot; para &quot;Apple iPhone&quot;.

- Inclua jargões específicos do setor e termos que os compradores podem usar alternadamente, por exemplo &quot;tênis&quot; e &quot;tênis de corrida&quot;.

- Atualize regularmente a lista de sinônimos com base em novas tendências de pesquisa, adições de produtos e comportamento do comprador.

- Teste a eficácia dos mapeamentos de sinônimos analisando os resultados da pesquisa e o feedback do comprador. Refine mapeamentos para melhorar a precisão e a relevância.

- Evite usar palavras de interrupção, pois elas não tornam os sinônimos mais significativos, mas aumentam a quantidade de dados que devem ser processados. [!DNL Adobe Commerce Optimizer] filtra as &quot;palavras de interrupção&quot; comuns em inglês de sinônimos, como:

  a, an, and, são, como, at, be, mas, por, for, in, into, is, it, no, not, of, on, or, tal, que, o, seu, então, há, esses, eles, este, para, foi, será, com

- Não é necessário definir as formas singular e plural de uma palavra como sinônimo. Se você tiver uma mistura de termos no singular e no plural no catálogo, a Pesquisa encontrará o conjunto correto de produtos. Por exemplo, se você usar a palavra &quot;pant&quot; no nome do produto e um comprador procurar &quot;pants&quot;, o conjunto correto de produtos será retornado e a palavra singular &quot;pant&quot; será oferecida como uma sugestão. O termo singular &quot;pant&quot; é frequentemente usado na indústria da moda e, às vezes, no varejo, embora a forma plural &quot;pants&quot; seja mais comumente usada em algumas áreas. (A palavra &quot;calça&quot; tecnicamente se refere à parte de uma peça de vestuário que cobre uma perna, por isso você precisa de um &quot;par de calças&quot; para cobrir ambas as pernas.)

- Seja consistente com a forma como a terminologia é usada em seu catálogo. Lembre-se de que pode haver diferenças regionais no uso e, às vezes, diferenças em um setor.
