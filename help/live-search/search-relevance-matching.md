---
title: Pesquisar correspondência e classificação
description: Saiba como o  [!DNL Live Search] prioriza correspondências exatas e próximas, correspondências de mesmo campo e correspondências entre campos e como a classificação interage com pesos de pesquisa, classificação inteligente e regras de merchandising.
role: Admin, Developer
recommendations: noCatalog
hide: true
autotag-review: '2026-06-12T19:48:33.569Z'
TQID: 'https://experienceleague.adobe.com/v4T99FG9mFhlgbb-xDqR-C1tVvCmHDry5lxhSDaKg-4'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2: id: faf75e43-5608-48b8-8169-3f8a9b8a5caf
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2: id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: da5950c0f2071f48f163dd02f6c38953804ae152
workflow-type: tm+mt
source-wordcount: 914
ht-degree: 0%

---

# Pesquisar correspondência e classificação

>[!IMPORTANT]
>
>O seguinte recurso está em [beta privado](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta).

[!DNL Live Search] classifica os resultados para que os compradores vejam primeiro os produtos mais relevantes. O serviço oferece o maior impulso aos produtos cujo texto de catálogo **corresponde melhor** ao que o comprador digita, favorece correspondências em que os termos de consulta aparecem juntos de maneira significativa e, finalmente, inclui correspondências mais amplas (incluindo comportamento que oferece suporte à correspondência de estilo de preenchimento automático).

## Como as correspondência são priorizadas

Em um nível alto, a relevância usa três camadas de força correspondente (além de outros fatores de pontuação descritos abaixo):

1. **Correspondência de frase exata e próxima** — A frase de pesquisa completa corresponde ao texto do catálogo ou a uma correspondência próxima após a normalização, como a origem (por exemplo, formas singular e plural resolvidas na mesma raiz). Essas correspondências recebem o aumento de relevância mais alto.

1. **Todas as palavras no mesmo campo** — Todas as palavras da consulta aparecem em um atributo pesquisável (por exemplo, `red` e `pants` no produto **nome**). Essa camada recebe o próximo aumento mais alto.

1. **Palavras em diferentes campos** — Os termos da consulta aparecem em diferentes atributos pesquisáveis (por exemplo, `red` em **cor** e `pants` em **nome**). Essa é a camada de correspondência mais ampla e recebe o menor aumento de relevância. Também pode corresponder a consultas parciais usadas pelo preenchimento automático, por exemplo, quando um comprador digita `red pan` antes de terminar `pants`. Para catálogos em alemão, consulte [Decomposição (Alemão)](#decompounding-german).

### Exemplo

Para uma consulta como `red pants`:

- Os produtos com a frase exata **calças vermelhas** (ou uma variante próxima) estão na **primeira** posição.
- Os produtos em que **vermelho** e **calças** aparecem no **mesmo campo** (por exemplo, **nome**) posição a seguir.
- Os produtos cujos termos aparecem em **campos diferentes** (por exemplo, **cor** e **nome**) seguem.

### Decomposto (Alemão) {#decompounding-german}

Catálogos alemães usam muitas palavras compostas. Por exemplo, o **spülbecken** e o **spül becken** podem se decompor em tokens como o **spul** e o **beck** (após o stemming) para que um comprador que pesquisa o **spul becken** ainda possa encontrar o **Spülbecken**. Nessa camada, subpalavras decompostas de um termo composto devem aparecer no mesmo campo. Outros termos de consulta podem corresponder em campos diferentes.

Este requisito **AND** filtra correspondências irrelevantes onde apenas uma subpalavra está presente. Por exemplo, uma pesquisa por **Brauseschlauch** não retorna mais **Schlauchstück** quando apenas parte do composto corresponde. Uma pesquisa por **spülbecken** ainda pode corresponder a **spülbeckventil** porque a palavra mais longa contém todos os tokens esperados.

>[!NOTE]
>
>A correspondência de frase exata e próxima e a correspondência de mesmo campo usam as regras descritas acima sem decomposição.

#### Exemplo

Para uma frase de pesquisa como `Brauseschlauch chrom`:

- **Correspondência de frase exata e próxima** — Procura a frase completa **brauseschlauch chrom** como digitada, sem decomposição (a origem ainda se aplica).
- **Todas as palavras no mesmo campo** — Procura por **brauseschlauch** e **chrom** no atributo pesquisável **same**, ainda sem decomposição (por exemplo, ambos em **name**).
- **Palavras em diferentes campos** — Decompõe **Brauseschlauch** em **brause** e **schlauch**. Esses tokens devem aparecer no campo **same** (não necessariamente como uma frase adjacente). **chrom** pode corresponder em um campo **different** (por exemplo, **brause** e **schlauch** em **name**, **chrom** em **color**).

Defina **Idioma** como **Alemão** no espaço de trabalho [Configurações](settings.md#language) para que as regras de decomposição sejam aplicadas. Valide consultas alemãs de alto valor em uma loja de preparo antes de habilitar as alterações na produção.

A decomposição se baseia em regras e pode adicionar casos de borda nesta camada. Se uma subpalavra estiver ausente no dicionário, a geração de tokens poderá estar incompleta e retornar correspondências mais amplas do que o esperado; por exemplo, **gas** ausentes de **gaszähler** poderão emitir apenas **zahl** ou **stat** ausentes do **termostato**. O lematizador também pode produzir raízes inesperadas (por exemplo, **schrauber** resultante de **schraub** ou **schelle** a **schell**). O Adobe atualiza o dicionário e as substituições da raiz para casos conhecidos à medida que problemas são identificados.

## O que mais afeta a classificação

A relevância não é determinada pela correspondência de frases isoladamente. Vários sinais interagem:

- Aumentar com base na frase **exata / próxima** correspondente
- Impulsionar quando **todos os termos da consulta** aparecem no campo **igual**
- **Classificação inteligente** (quando habilitada), que mescla relevância textual com sinais comportamentais — consulte [Como funciona a pontuação de classificação inteligente](rules-add.md#how-intelligent-ranking-scoring-works)
- **[Pesquise peso](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)** em cada atributo e outros fatores de relevância textual (por exemplo, a frequência com que os termos ocorrem e o comprimento do nome ou da descrição). No Administrador [!DNL Adobe Commerce], configure **Usar na Pesquisa** e **Pesar na Pesquisa** para atributos de produto.
- **[Pesquisar regras de merchandising](rules.md)**, como fixar, impulsionar e enterrar

Como esses sinais interagem, um produto que corresponde somente no nível mais amplo pode, às vezes, ser classificado acima de uma correspondência de frase mais estreita, por exemplo, quando **pesos de pesquisa** ou frequência de termo em um campo de alto peso superam uma correspondência de frase mais fraca em outro lugar.

**Exemplo:** se **calças vermelhas** aparecer como uma frase na **descrição** com **peso de pesquisa = 1**, mas **calças vermelhas** e **calças** aparecer separadamente no **nome** e na **cor** com **peso de pesquisa = 10**, a correspondência de frases na **descrição** poderá não superar a correspondência de divisão, dependendo da pontuação geral.

As regras manuais de **pin** e **bury** permanecem fortes; as regras de **boost** podem exigir ajuste para superar novos aumentos de frase e de mesmo campo. Validar consultas importantes após alterar pesos ou regras.

### Peso de pesquisa 1 e indexação combinada

Atributos configurados com o **peso mínimo de pesquisa** (peso **1**) e **não** configurados para modos de correspondência especiais (como contém ou começa com) podem ser combinados no índice de pesquisa em um único campo interno (`defaultSearchField`) para reduzir a sobrecarga de mapeamento de campo. Trate-a como uma superfície pesquisável para correspondência de **mesmo-campo**: os tokens que chegam somente nesses campos combinados de baixo peso são avaliados juntos em vez de campos separados por atributo. A Adobe pode refinar essa otimização ao longo do tempo, à medida que a correspondência evolui.

## Tópicos relacionados

- [Indexação](indexing.md)
- [Práticas recomendadas](best-practice.md)
- [Adicionar regras de pesquisa](rules-add.md)
- [Sinônimos](synonyms.md)
