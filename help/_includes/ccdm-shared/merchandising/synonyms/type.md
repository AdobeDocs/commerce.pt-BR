---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
Sinônimos unidirecionais e bidirecionais expandem a definição de palavras-chave. Alguns são intercambiáveis com a palavra-chave, enquanto outros representam um subconjunto da palavra-chave.

## Bidirecional

Sinônimos bidirecionais têm o mesmo significado e retornam os mesmos resultados de pesquisa. No exemplo a seguir, a primeira palavra mostrada em negrito é a palavra-chave usada no catálogo, seguida por palavras que têm o mesmo significado que a palavra-chave original. Você pode criar um par simples de sinônimos bidirecionais ou uma cadeia de vários sinônimos bidirecionais para a mesma palavra-chave.

**Jaqueta** ![Seletor bidirecional](/help/assets/ccdm-shared/synonyms/two-way.png) casaco
**calças** ![Seletor bidirecional](/help/assets/ccdm-shared/synonyms/two-way.png) pretas ![Seletor bidirecional](/help/assets/ccdm-shared/synonyms/two-way.png) calças

## Unidirecional

Um sinônimo unidirecional é um subconjunto de uma palavra-chave, mas com um significado mais específico. Por exemplo, capris e shorts são calças, mas nem todas as calças são capris ou shorts. Uma busca por calças inclui capris e shorts. No entanto, a busca por shorts não retorna capris.

**moletom** ![Seletor unidirecional](/help/assets/ccdm-shared/synonyms/one-way.png) moletom
**calças** ![Seletor unidirecional](/help/assets/ccdm-shared/synonyms/one-way.png) capris ![Seletor unidirecional](/help/assets/ccdm-shared/synonyms/one-way.png) calças de comprimento da panturrilha ![Seletor unidirecional](/help/assets/ccdm-shared/synonyms/one-way.png) flexionadores

## Comportamento de sinônimo de várias palavras

Para sinônimos de várias palavras, o sistema considera o sinônimo como uma frase. Por exemplo, se você criar um sinônimo bidirecional **mesa de jantar** ![Seletor bidirecional](/help/assets/ccdm-shared/synonyms/two-way.png) **mesa de cozinha** ![Seletor bidirecional](/help/assets/ccdm-shared/synonyms/two-way.png) **mesa de jantar**, o sistema pesquisará em todos os campos definidos como pesquisáveis para a ocorrência de **mesa de sala de jantar** ou **mesa de cozinha** ou **mesa de jantar**.

Se nenhum sinônimo for criado e um comprador procurar por **tabela de cozinha**, o sistema procurará os termos em qualquer lugar nos campos pesquisáveis, mesmo em campos diferentes, por exemplo **tabela** no campo de nome e **cozinha** na palavra-chave meta.

Depois de criar um sinônimo, o comportamento de pesquisa muda para procurar a frase exata **tabela de cozinha**. Isso pode reduzir o número de resultados, pois somente os produtos com a frase exata serão exibidos.

Se quiser que os termos sejam pesquisados separadamente como antes, você pode [criar um tíquete de suporte](https://experienceleague.adobe.com/pt-br/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide).
