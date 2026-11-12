---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%
---
>[!IMPORTANT]
>
>O seguinte recurso está em [beta privado](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/beta).

Os Serviços de merchandising com o modelo de dados de catálogo combinável (CCDM) classificam os resultados para que os compradores vejam os produtos mais relevantes primeiro. O serviço melhora os produtos cujo texto de catálogo **corresponde diretamente** à consulta do comprador, favorece correspondências em que os termos aparecem juntos e, por fim, inclui correspondências mais amplas.

## Como as correspondência são priorizadas

A relevância usa três camadas de intensidade correspondente (além de outros fatores de pontuação descritos abaixo):

1. **Correspondência de frase exata e próxima** — A frase de pesquisa completa corresponde ao texto do catálogo ou a uma correspondência próxima após a normalização, como a origem (por exemplo, formas singular e plural resolvidas na mesma raiz). Essas correspondências recebem o aumento de relevância mais alto.

1. **Todas as palavras no mesmo campo** — Todas as palavras de consulta aparecem em um atributo pesquisável (por exemplo, `red` e `pants` no produto **nome**). Essa camada recebe o próximo aumento mais alto.

1. **Palavras em diferentes campos** — Os termos da consulta aparecem em diferentes atributos pesquisáveis (por exemplo, `red` em **cor** e `pants` em **nome**). Essa camada de correspondência é a mais ampla e recebe o menor aumento de relevância. Também pode corresponder a consultas parciais usadas pelo preenchimento automático, por exemplo, quando um comprador digita `red pan` antes de terminar `pants`. Para catálogos em alemão, consulte [Decomposição (Alemão)](#decompounding-german).

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

Defina **Idioma** como **Alemão** na guia [Idioma](../settings.md#language) em [Configurações](../settings.md) para que as regras de decomposição sejam aplicadas. Valide consultas alemãs de alto valor em uma loja de preparo antes de habilitar as alterações na produção.

A decomposição se baseia em regras e pode adicionar casos de borda nesta camada. Se uma subpalavra estiver ausente no dicionário, a geração de tokens estará incompleta e retornará correspondências mais amplas do que o esperado; por exemplo, **gas** ausentes de **gaszähler** emitirá somente **zahl** ou **stat** ausentes de **termostato**. O lematizador também pode produzir raízes inesperadas (por exemplo, **schrauber** resultante de **schraub** ou **schelle** a **schell**). O Adobe atualiza o dicionário e as substituições da raiz para casos conhecidos à medida que problemas são identificados.

## O que mais afeta a classificação

A correspondência de frases por si só não determina a relevância. Vários sinais interagem:

- Aumentar com base na frase **exata / próxima** correspondente
- Impulsionar quando **todos os termos da consulta** aparecem no campo **igual**
- **Classificação inteligente** (quando habilitada), que mescla relevância textual com sinais comportamentais — consulte [Como funciona a pontuação de classificação inteligente](../merchandising/rules/add.md#how-intelligent-ranking-scoring-works-search)
- **[Pesquise peso](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/catalog/search/search-results)** em cada atributo e outros fatores de relevância textual (por exemplo, a frequência com que os termos ocorrem em nome ou tamanho de descrição). Em *Configurações*, configure quais atributos participam da pesquisa por palavra-chave e seus **[pesos da pesquisa por palavra-chave](../settings.md)** relativos.
- **[Regras de merchandising](../merchandising/rules/overview.md)**, como fixar, aumentar e atenuar

Como os sinais interagem, uma correspondência ampla às vezes fica acima de uma correspondência de frase mais estreita quando **os pesos de pesquisa** ou a frequência de termos ultrapassam uma correspondência de frase mais fraca.

**Exemplo:** se **calças vermelhas** aparecer na **descrição** com **peso de pesquisa = 1**, mas **calças vermelhas** e **calças** aparecer separadamente no **nome** e na **cor** com **peso de pesquisa = 10**, a correspondência de divisão ultrapassará a correspondência de frase.

As regras manuais de **pin** e **bury** permanecem fortes; as regras de **boost** podem exigir ajuste para superar novos aumentos de frase e de mesmo campo. Validar consultas importantes após alterar pesos ou regras.

### Peso de pesquisa 1 e indexação combinada

Atributos com **peso mínimo de pesquisa** (peso **1**) e nenhum modo de correspondência especial são combinados em um único campo interno (`defaultSearchField`) para reduzir a sobrecarga de mapeamento. Trate-a como uma superfície pesquisável para correspondência de **mesmo-campo**: os tokens que chegam somente nesses campos combinados de baixo peso são avaliados juntos em vez de campos separados por atributo. A Adobe pode refinar essa otimização ao longo do tempo, à medida que a correspondência evolui.

## Tópicos relacionados

- [Configurações](../settings.md)
- [Desempenho da pesquisa](search-performance.md)
- [Visão geral das regras de merchandising](../merchandising/rules/overview.md)
- [Adicionar regras de pesquisa](../merchandising/rules/add.md)
- [Visão geral dos sinônimos](../merchandising/synonyms/overview.md)
