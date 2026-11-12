---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---
A pesquisa semântica usa IA para entender o que os compradores significam, não apenas as palavras exatas que digitam. Consultas como &quot;vestido de casamento na praia&quot; ou &quot;sapatos confortáveis para ficar o dia todo&quot; podem retornar produtos relevantes mesmo quando seu catálogo não usa essas frases exatas.

O sistema de descoberta de produtos combina correspondência de palavras-chave e correspondência semântica em uma experiência de pesquisa. Você não gerencia palavras-chave separadas e modos semânticos na loja.

## Configurar pesquisa semântica

A pesquisa semântica é **habilitada por padrão** para catálogos em inglês qualificados. Você o gerencia na guia **[!UICONTROL Advanced search]** do espaço de trabalho [Configurações](../settings.md#advanced-search), onde pode confirmar ou alterar a configuração e, opcionalmente, ajustar o aumento semântico, o limite de similaridade e a pesquisa difusa. Consulte [Configurações](../settings.md#access-the-settings-workspace) para saber como abrir o espaço de trabalho.

Não é necessário publicar uma configuração separada ou alterar as configurações da loja depois de salvar.

## Benefícios

- **Menos páginas de pesquisa vazias**—Os compradores encontram produtos quando seus textos não correspondem exatamente ao texto do catálogo.
- **Melhor correspondência de intenção** — consultas naturais e descritivas retornam resultados úteis.
- **Menos manutenção de sinônimo**—Variações de palavras comuns (por exemplo, sofá e sofá) geralmente são tratadas sem listas de sinônimos manuais.
- **Nenhum trabalho de loja ou desenvolvedor**—A pesquisa semântica está habilitada por padrão e não requer alterações de código de tema, entrada ou API.

## Como funciona

Quando a pesquisa semântica é ativada, o sistema usa atributos de catálogo predefinidos (como nome e descrição do produto) para interpretar o significado da consulta junto com a pesquisa tradicional de palavra-chave. Você não seleciona nem prioriza atributos em Configurações.

Por exemplo:

- Uma busca por &quot;sofá de couro&quot; pode devolver produtos rotulados como &quot;sofá de couro&quot;.
- &quot;Vestido de primavera&quot; pode aparecer vestidos sazonais mesmo quando &quot;primavera&quot; não está no nome do produto.
- &quot;Sapatos para corrida de trilha&quot; pode combinar produtos descritos como off-road ou calçados para caminhada.

## O que acontece quando você habilita a pesquisa semântica

A pesquisa semântica funciona junto com a configuração de pesquisa existente. Você não substitui a pesquisa por palavra-chave nem reconfigura a loja.

Quando a pesquisa semântica estiver ativa:

- Suas [regras de merchandising](../merchandising/rules/overview.md), [sinônimos](../merchandising/synonyms/overview.md), [facetas](../merchandising/facets/overview.md), impulsos e filtros existentes continuam a ser aplicáveis.
- A pesquisa semântica adiciona a compreensão baseada em IA da intenção do comprador para melhorar a relevância do resultado ao lado da correspondência de palavras-chave.
- Os atributos de catálogo predefinidos são indexados automaticamente. Você não seleciona atributos nem publica uma configuração separada.

## Validar após ativação

Depois que a pesquisa semântica estiver ativa e a indexação for concluída, a Adobe recomenda validar o desempenho da pesquisa. Use a página [Desempenho da pesquisa](../manage-results/search-performance.md) para analisar métricas e testar consultas importantes para sua empresa.

1. Revise os principais termos pesquisados no relatório **Pesquisas exclusivas**.
1. Teste consultas históricas de resultado zero do relatório **Nenhum resultado** na loja.
1. Compare os resultados da pesquisa para as mesmas consultas antes e depois da ativação.
1. Monitore métricas de conversão e engajamento de pesquisa, incluindo taxa de cliques, taxa de conversão e taxa de resultados zero.

## Práticas recomendadas

- Use nomes e descrições de produtos claros e descritivos (idealmente, 50 a 100 palavras) para que a correspondência de palavra-chave e semântica tenha um texto de catálogo sólido para funcionar.
- Comece com a configuração padrão **[!UICONTROL Enable semantic search]** e ajuste **[!UICONTROL Semantic boost]** ou **[!UICONTROL Similarity threshold]** somente se os resultados forem muito amplos ou muito estreitos.
- Mantenha [sinônimos](../merchandising/synonyms/overview.md) altamente técnicos ou específicos da marca, nos quais a pesquisa semântica pode não abranger termos especializados.

## Solução de problemas

| Problema | O que fazer |
| --- | --- |
| Nenhuma alteração na loja logo após salvar | Aguarde a conclusão da indexação. Catálogos grandes podem demorar mais. |
| Os resultados são muito amplos | Elevar **[!UICONTROL Similarity threshold]** ou inferior **[!UICONTROL Semantic boost]** na guia **[!UICONTROL Advanced search]**. |
| Os resultados parecem muito estreitos | Baixe **[!UICONTROL Similarity threshold]** ou aumente **[!UICONTROL Semantic boost]**. |
| Pesquisa semântica não disponível | Confirmar **[!UICONTROL Language]** está definido como **inglês**. |

## Limitação {#semantic-search-limitations}

- **Idioma do catálogo:** A pesquisa semântica está disponível somente para catálogos **em inglês**.

## Mais ajuda sobre este tópico

- [Pesquisa avançada](../settings.md#advanced-search)
- [Sinônimos](../merchandising/synonyms/overview.md)
- [Desempenho da pesquisa](../manage-results/search-performance.md)
