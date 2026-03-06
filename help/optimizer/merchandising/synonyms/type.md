---
title: Tipos de sinônimos
description: Saiba mais sobre os diferentes tipos de sinônimos no [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: a74e48ea-e069-4ccc-a67f-2f85be251fb5
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Tipos de sinônimos

Sinônimos unidirecionais e bidirecionais expandem a definição de palavras-chave. Alguns são intercambiáveis com a palavra-chave, enquanto outros representam um subconjunto da palavra-chave.

## Bidirecional

Sinônimos bidirecionais têm o mesmo significado e retornam os mesmos resultados de pesquisa. No exemplo a seguir, a primeira palavra mostrada em negrito é a palavra-chave usada no catálogo, seguida por palavras que têm o mesmo significado que a palavra-chave original. Você pode criar um par simples de sinônimos bidirecionais ou uma cadeia de vários sinônimos bidirecionais para a mesma palavra-chave.

**Jaqueta** ![Seletor bidirecional](../../assets/two-way.png) casaco
**calças** ![Seletor bidirecional](../../assets/two-way.png) pretas ![Seletor bidirecional](../../assets/two-way.png) calças

## Unidirecional

Um sinônimo unidirecional é um subconjunto de uma palavra-chave, mas com um significado mais específico. Por exemplo, capris e shorts são calças, mas nem todas as calças são capris ou shorts. Uma busca por calças inclui capris e shorts. No entanto, a busca por shorts não retorna capris.

**moletom** ![Seletor unidirecional](../../assets/one-way.png) moletom
**calças** ![Seletor unidirecional](../../assets/one-way.png) capris ![Seletor unidirecional](../../assets/one-way.png) calças de comprimento da panturrilha ![Seletor unidirecional](../../assets/one-way.png) empurradores de pedal

## Comportamento de sinônimo de várias palavras

Para sinônimos de várias palavras, [!DNL Adobe Commerce Optimizer] considera o sinônimo como uma frase. Por exemplo, se você criar um sinônimo bidirecional **mesa de jantar** ![Seletor bidirecional](../../assets/two-way.png) **mesa de cozinha** ![Seletor bidirecional](../../assets/two-way.png) **mesa de jantar**, o [!DNL Adobe Commerce Optimizer] pesquisará em todos os campos definidos como pesquisáveis a ocorrência de **mesa de jantar** ou **mesa de cozinha** ou **mesa de jantar**.

Se nenhum sinônimo for criado e um comprador procurar por **tabela de cozinha**, [!DNL Adobe Commerce Optimizer] procurará os termos em qualquer lugar nos campos pesquisáveis, mesmo em campos diferentes, por exemplo **tabela** no campo de nome e **cozinha** na palavra-chave meta.

Depois de criar um sinônimo, o comportamento de pesquisa muda para procurar a frase exata **tabela de cozinha**. Isso pode reduzir o número de resultados, pois somente os produtos com a frase exata serão exibidos.

Se quiser que os termos sejam pesquisados separadamente como antes, você pode [criar um tíquete de suporte](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Se houver demanda suficiente, o [!DNL Adobe Commerce Optimizer] considerará adicionar essa funcionalidade ao produto em uma versão futura.
