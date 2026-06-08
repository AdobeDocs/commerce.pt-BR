---
title: Pesquisa semântica
description: Habilitar a pesquisa semântica de IA para  [!DNL Live Search]  em Configurações. Nenhuma configuração de atributo ou alteração de vitrine eletrônica é necessária.
role: Admin
recommendations: noCatalog
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 0%

---

# Pesquisa semântica

A pesquisa semântica usa IA para entender o que os compradores significam, não apenas as palavras exatas que digitam. Consultas como &quot;vestido de casamento na praia&quot; ou &quot;sapatos confortáveis para ficar o dia todo&quot; podem retornar produtos relevantes mesmo quando seu catálogo não usa essas frases exatas.

[!DNL Live Search] combina correspondência de palavra-chave e correspondência semântica em uma experiência de pesquisa. Você não gerencia palavras-chave separadas e modos semânticos na loja. [!DNL Live Search] não oferece controles semânticos avançados (por exemplo, controles deslizantes de reforço ou similaridade) no Administrador. Você pode ativar ou desativar a pesquisa semântica.

## Ativação por implantação

A pesquisa semântica é gerenciada no espaço de trabalho **Configurações** no [!DNL Live Search] Administrador (**Marketing** > *SEO e Pesquisa* > **[!DNL Live Search]**). [!DNL Adobe Commerce as a Cloud Service] usa essa mesma interface [!DNL Live Search] que os comerciantes PaaS.

## Benefícios

- **Menos pesquisas sem resultados** — Os compradores encontram produtos quando seus textos não correspondem exatamente ao texto do catálogo.
- **Resultados mais relevantes** — consultas naturais e descritivas retornam correspondências úteis com base no significado e no contexto.
- **Menos manutenção de sinônimo** — Variações de palavras comuns (por exemplo, sofá e sofá) geralmente são tratadas sem listas de sinônimos manuais.
- **Nenhum trabalho de vitrine ou desenvolvedor** — A pesquisa semântica não requer alterações de código de tema, widget ou API. Os comerciantes do PaaS habilitam esse recurso em Configurações; [!DNL Adobe Commerce as a Cloud Service] clientes o recebem habilitado por padrão.

## Como funciona

Quando a pesquisa semântica está habilitada, o [!DNL Live Search] usa atributos de catálogo predefinidos escolhidos pelo sistema (como nome e descrição do produto) para interpretar o significado da consulta junto com a pesquisa de palavra-chave tradicional. Você não seleciona nem prioriza atributos no Administrador.

Por exemplo:

- Uma busca por &quot;sofá de couro&quot; pode devolver produtos rotulados como &quot;sofá de couro&quot;.
- &quot;Vestido de primavera&quot; pode aparecer vestidos sazonais mesmo quando &quot;primavera&quot; não está no nome do produto.
- &quot;Sapatos para corrida de trilha&quot; pode combinar produtos descritos como off-road ou calçados para caminhada.

## O que acontece quando você habilita a pesquisa semântica

A pesquisa semântica funciona com sua configuração [!DNL Live Search] existente. Você não substitui a pesquisa por palavra-chave nem reconfigura a loja.

Quando a pesquisa semântica estiver ativa:

- Suas [regras de pesquisa](rules.md), [sinônimos](synonyms.md), [facetas](facets.md), impulsos e configurações de [merchandising de categoria](category-merch.md) existentes continuam a ser aplicadas.
- A pesquisa semântica adiciona a compreensão baseada em IA da intenção do comprador para melhorar a relevância do resultado ao lado da correspondência de palavras-chave.
- Os atributos de catálogo predefinidos são indexados automaticamente. Você não seleciona atributos nem publica uma configuração separada.

## Gerenciar pesquisa semântica no Administrador

Vá para o espaço de trabalho [Configurações](settings.md#semantic-search) para exibir ou alterar a opção **[!UICONTROL Semantic search]**.

>[!NOTE]
>
> A pesquisa semântica está disponível somente para **catálogos em inglês**. Se você alterar **Idioma** para um catálogo que não esteja em inglês no espaço de trabalho **Configurações**, o **[!UICONTROL Semantic search]** será desabilitado automaticamente.

### Para comerciantes PaaS

O Adobe Commerce na nuvem e os comerciantes locais devem habilitar a pesquisa semântica manualmente:

1. No Administrador, vá para **Marketing** > *SEO e pesquisa* > **[!DNL Live Search]**.
1. No espaço de trabalho **Configurações**, habilite **[!UICONTROL Semantic search]**.

   Quando ativada, a pesquisa corresponde a produtos com base no significado e no contexto, o que pode produzir resultados mais relevantes, menos pesquisas com resultados nulos e conversão aprimorada.

1. Clique em **[!UICONTROL Save]**.

   Atualização dos resultados da pesquisa após a conclusão da indexação. Para um catálogo de médio porte, a indexação pode levar até meia hora. Para catálogos grandes com milhões de produtos, pode levar algumas horas.

### Para clientes do ACCS

[!DNL Adobe Commerce as a Cloud Service] clientes usam o mesmo espaço de trabalho de **Configurações** no Administrador [!DNL Live Search]. A pesquisa semântica é **habilitada por padrão** para catálogos em inglês qualificados. Confirme se **[!UICONTROL Semantic search]** está habilitado ou desabilite-o se não quiser correspondência semântica na loja.

Você não precisa de uma etapa de publicação ou configuração de vitrine separada depois de salvar uma alteração.

## Validar após ativação

Depois que a pesquisa semântica estiver ativa e a indexação for concluída, a Adobe recomenda validar o desempenho da pesquisa. Use o espaço de trabalho [Desempenho](performance.md) para revisar métricas e testar consultas importantes para sua empresa. Isso se aplica se a pesquisa semântica foi habilitada por padrão ou se você a habilitou manualmente.

1. Revise os principais termos pesquisados no relatório **Pesquisas exclusivas**.
1. Teste consultas históricas de resultado zero do relatório **Nenhum resultado** na loja.
1. Compare os resultados da pesquisa para as mesmas consultas antes e depois da ativação.
1. Monitore métricas de conversão e engajamento de pesquisa, incluindo taxa de cliques, taxa de conversão e taxa de resultados zero.

## Práticas recomendadas

- Use nomes e descrições de produtos claros e descritivos (idealmente, 50 a 100 palavras) para que a correspondência de palavra-chave e semântica tenha um texto de catálogo sólido para funcionar.
- Mantenha [sinônimos](synonyms.md) altamente técnicos ou específicos da marca, nos quais a pesquisa semântica pode não abranger termos especializados.

## Solução de problemas

| Problema | O que fazer |
| --- | --- |
| Nenhuma alteração na loja logo após salvar | Aguarde a conclusão da indexação. Catálogos grandes podem demorar mais. |
| A pesquisa semântica não está disponível ou está desabilitada automaticamente | Confirmar **Idioma** no espaço de trabalho **Configurações** está definido como **Inglês**. |
| Os resultados ainda não têm termos comuns | Adicionar [sinônimos](synonyms.md) para pesquisa semântica de termos de marca ou setor pode não resolver. |

## Limitação {#semantic-search-limitations}

- **Idioma do catálogo:** A pesquisa semântica está disponível somente para catálogos **em inglês**.
- **Controles de administrador:** [!DNL Live Search] fornece somente um controle habilitar/desabilitar. Não é possível ajustar o aumento semântico, o limite de similaridade ou a pesquisa difusa do espaço de trabalho **Configurações**.

## Mais ajuda sobre este tópico

- [Configurações](settings.md#semantic-search)
- [Sinônimos](synonyms.md)
- [Desempenho](performance.md)
