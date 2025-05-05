---
title: Tipos de sinônimos
description: Sinônimos unidirecionais e bidirecionais [!DNL Live Search]  expandem a definição de palavras-chave.
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Tipos de sinônimos

Sinônimos unidirecionais e bidirecionais expandem a definição de palavras-chave. Alguns são intercambiáveis com a palavra-chave, enquanto outros representam um subconjunto da palavra-chave.

## Bidirecional

Sinônimos bidirecionais têm o mesmo significado e retornam os mesmos resultados de pesquisa. No exemplo a seguir, a primeira palavra mostrada em negrito é a palavra-chave usada no catálogo, seguida por palavras que têm o mesmo significado que a palavra-chave original. Você pode criar um par simples de sinônimos bidirecionais ou uma cadeia de vários sinônimos bidirecionais para a mesma palavra-chave.

**Jaqueta** ![Seletor bidirecional](assets/btn-two-way.png) casaco
**calças** ![Seletor bidirecional](assets/btn-two-way.png) pretas ![Seletor bidirecional](assets/btn-two-way.png) calças

## Unidirecional

Um sinônimo unidirecional é um subconjunto de uma palavra-chave, mas com um significado mais específico. Por exemplo, capris e shorts são calças, mas nem todas as calças são capris ou shorts. Uma busca por calças inclui capris e shorts. No entanto, a busca por shorts não retorna capris.

**moletom** ![Seletor unidirecional](assets/btn-one-way.png) moletom
**calças** ![Seletor unidirecional](assets/btn-one-way.png) capris ![Seletor unidirecional múltiplo](assets/btn-multiple-one-way.png) calças de comprimento da panturrilha ![Seletor unidirecional múltiplo](assets/btn-multiple-one-way.png) empurradores de pedal

## Práticas recomendadas

Lembre-se das seguintes práticas recomendadas para obter o máximo de [!DNL Live Search] sinônimos.

### Evitar &quot;palavras de interrupção&quot;

[!DNL Live Search] filtra as &quot;palavras de interrupção&quot; comuns em inglês de sinônimos, como:

a, an, and, são, como, at, be, mas, por, for, in, into, is, it, no, not, of, on, or, tal, que, o, seu, então, há, esses, eles, este, para, foi, será, com

As palavras de interrupção não tornam os sinônimos mais significativos, mas aumentam a quantidade de dados que devem ser processados.

### Uso do singular e do plural

Não é necessário definir as formas singular e plural de uma palavra como sinônimo. Se você tiver uma mistura de termos no singular e no plural no catálogo, a Pesquisa encontrará o conjunto correto de produtos. Por exemplo, se você usar a palavra &quot;pant&quot; no nome do produto e um comprador procurar &quot;pants&quot;, o conjunto correto de produtos será retornado e a palavra singular &quot;pant&quot; será oferecida como uma sugestão. O termo singular &quot;pant&quot; é frequentemente usado na indústria da moda e, às vezes, no varejo, embora a forma plural &quot;pants&quot; seja mais comumente usada em algumas áreas. (A palavra &quot;calça&quot; tecnicamente se refere à parte de uma peça de vestuário que cobre uma perna, por isso você precisa de um &quot;par de calças&quot; para cobrir ambas as pernas.)

### Consistência

Seja consistente com a forma como a terminologia é usada em seu catálogo. Lembre-se de que pode haver diferenças regionais no uso e, às vezes, diferenças em um setor.

## Comportamento de sinônimo de várias palavras

Para sinônimos de várias palavras, a Commerce considera o sinônimo como uma frase. Por exemplo, se você criar um sinônimo bidirecional **mesa de jantar** ![Seletor bidirecional](assets/btn-two-way.png) **mesa de cozinha** ![Seletor bidirecional](assets/btn-two-way.png) **mesa de jantar**, o Commerce pesquisará em todos os campos definidos como pesquisáveis para a ocorrência de **mesa de sala de jantar** ou **mesa de cozinha** ou **mesa de jantar**.

Se nenhum sinônimo for criado e um comprador procurar por **tabela de cozinha**, o Commerce procurará os termos em qualquer lugar nos campos pesquisáveis, mesmo em campos diferentes, por exemplo **tabela** no campo de nome e **cozinha** na palavra-chave meta.

Depois de criar um sinônimo, o comportamento de pesquisa muda para procurar a frase exata **tabela de cozinha**. Isso pode reduzir o número de resultados, pois somente os produtos com a frase exata serão exibidos.

Se quiser que os termos sejam pesquisados separadamente como antes, você pode [criar um tíquete de suporte](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Se houver demanda suficiente, a Commerce considerará adicionar essa funcionalidade ao produto em uma versão futura.
