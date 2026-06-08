---
title: Pesquisa semântica
description: Habilitar a pesquisa semântica de IA em  [!DNL Adobe Commerce Optimizer]  em Configurações. Nenhuma configuração de atributo ou alteração de vitrine eletrônica é necessária.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# Pesquisa semântica

A pesquisa semântica usa IA para entender o que os compradores significam, não apenas as palavras exatas que digitam. Consultas como &quot;vestido de casamento na praia&quot; ou &quot;sapatos confortáveis para ficar o dia todo&quot; podem retornar produtos relevantes mesmo quando seu catálogo não usa essas frases exatas.

[!DNL Adobe Commerce Optimizer] combina correspondência de palavra-chave e correspondência semântica em uma experiência de pesquisa. Você não gerencia palavras-chave separadas e modos semânticos na loja. No Admin, vá para o espaço de trabalho [Configurações](../settings.md#advanced-search) para gerenciar a pesquisa semântica e, opcionalmente, ajuste os controles avançados na guia **[!UICONTROL Advanced search]**.

## Benefícios

- **Menos páginas de pesquisa vazias** — Os compradores encontram produtos quando seus textos não correspondem exatamente ao texto do catálogo.
- **Melhor correspondência de intenção** — consultas naturais e descritivas retornam resultados úteis.
- **Menos manutenção de sinônimo** — Variações de palavras comuns (por exemplo, sofá e sofá) geralmente são tratadas sem listas de sinônimos manuais.
- **Nenhum trabalho de loja ou desenvolvedor** — A pesquisa semântica está habilitada por padrão e não requer alterações de código de tema, entrada ou API.

## Como funciona

Quando a pesquisa semântica está habilitada, o [!DNL Adobe Commerce Optimizer] usa atributos de catálogo predefinidos escolhidos pelo sistema (como nome e descrição do produto) para interpretar o significado da consulta junto com a pesquisa de palavra-chave tradicional. Você não seleciona nem prioriza atributos no Administrador.

Por exemplo:

- Uma busca por &quot;sofá de couro&quot; pode devolver produtos rotulados como &quot;sofá de couro&quot;.
- &quot;Vestido de primavera&quot; pode aparecer vestidos sazonais mesmo quando &quot;primavera&quot; não está no nome do produto.
- &quot;Sapatos para corrida de trilha&quot; pode combinar produtos descritos como off-road ou calçados para caminhada.

## O que acontece quando você habilita a pesquisa semântica

A pesquisa semântica funciona com sua configuração de pesquisa [!DNL Adobe Commerce Optimizer] existente. Você não substitui a pesquisa por palavra-chave nem reconfigura a loja.

Quando a pesquisa semântica estiver ativa:

- Suas [regras de merchandising](../merchandising/rules/overview.md), [sinônimos](../merchandising/synonyms/overview.md), [facetas](../merchandising/facets/overview.md), impulsos e filtros existentes continuam a ser aplicáveis.
- A pesquisa semântica adiciona a compreensão baseada em IA da intenção do comprador para melhorar a relevância do resultado ao lado da correspondência de palavras-chave.
- Os atributos de catálogo predefinidos são indexados automaticamente. Você não seleciona atributos nem publica uma configuração separada.

## Gerenciar pesquisa semântica no Administrador

A pesquisa semântica é **habilitada por padrão** para catálogos em inglês qualificados. Vá para **[!UICONTROL Settings]** > **[!UICONTROL Advanced search]** para confirmar a configuração ou alterá-la:

1. No Administrador, vá para **[!UICONTROL Settings]**.
1. Na guia **[!UICONTROL Advanced search]**, reveja **[!UICONTROL Enable semantic search]**.

   Quando ativada, a pesquisa corresponde a produtos com base no significado e no contexto, o que pode produzir resultados mais relevantes, menos páginas de pesquisa vazias e conversões aprimoradas.

1. Clique em **[!UICONTROL Save]** se você alterar os controles de alternância ou ajuste.

   Atualização dos resultados da pesquisa após a conclusão da indexação. Para um catálogo de médio porte, a indexação pode levar até meia hora. Para catálogos grandes com milhões de produtos, pode levar algumas horas.

>[!NOTE]
>
> A pesquisa semântica está disponível somente para **catálogos em inglês**. Se você alterar **[!UICONTROL Language]** para um catálogo que não esteja em inglês, **[!UICONTROL Enable semantic search]** será desabilitado automaticamente.

Não é necessário publicar uma configuração separada ou alterar as configurações da loja depois de salvar.

## Validar após ativação

Depois que a pesquisa semântica estiver ativa e a indexação for concluída, a Adobe recomenda validar o desempenho da pesquisa. Use a página [Desempenho da pesquisa](../manage-results/search-performance.md) para analisar métricas e testar consultas importantes para sua empresa.

1. Revise os principais termos pesquisados no relatório **Pesquisas exclusivas**.
1. Teste consultas históricas de resultado zero do relatório **Nenhum resultado** na loja.
1. Compare os resultados da pesquisa para as mesmas consultas antes e depois da ativação.
1. Monitore métricas de conversão e engajamento de pesquisa, incluindo taxa de cliques, taxa de conversão e taxa de resultados zero.

## Ajuste opcional

Na guia **[!UICONTROL Advanced search]**, é possível ajustar como a pesquisa se comporta depois que a pesquisa semântica é habilitada:

- **[!UICONTROL Semantic boost]** — Aumente ou diminua a intensidade com que as correspondências baseadas em significado influenciam a classificação. Por exemplo, digamos que uma correspondência de produto recuperada por meio de pesquisa semântica seja exibida no final do resultado. Adicionar um reforço o move para cima no resultado.
- **[!UICONTROL Similarity threshold]** — Defina a proximidade de uma correspondência antes do produto aparecer. Valores mais baixos mostram mais resultados; valores mais altos mostram menos correspondências mais estreitas.
- **[!UICONTROL Fuzzy search]** e **[!UICONTROL Fuzzy search similarity threshold]** — Ajude os compradores a encontrar produtos quando as consultas incluírem pequenas diferenças de ortografia.

Consulte [Pesquisa avançada](../settings.md#advanced-search) para obter descrições de controle e orientação passo a passo.

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
