---
title: Insights e governança de orientação
description: Saiba mais sobre o modelo de governança interna para obter insights e orientação. Não publicado no Experience League.
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%
---

# Insights e governança de orientação

Esta é uma referência interna para a equipe de documentação. Ela não está listada em `TOC.md`, portanto, não é compilada ou publicada no Experience League. Mantenha-o aqui para que ele fique perto do conteúdo que rege. Para obter a governança do Centro de Informações como um todo, consulte [governance.md](../governance.md).

## Propriedade

Os insights e artigos de orientação são de propriedade do autor ou da equipe de publicação responsável por manter a precisão e a moeda do artigo. Esses artigos estão atualmente hospedados no repositório `commerce.en`. A equipe de Documentação do Commerce ajuda a garantir a qualidade do conteúdo e a publicar o artigo na produção.

## O que pertence aos Insights e à orientação

- **Pertence aqui**—Orientação estratégica e whitepapers para Soluções da Commerce que abrangem orientação de implementação com base em cenários do mundo real. Inclua links para as páginas relevantes da documentação do Commerce para suporte.

- **Em vez disso, pertence ao repo do produto**: configuração passo a passo, tutoriais, material de referência (referência de API/CLI/config) e solução de problemas. Se uma publicação aqui começar a acumular esse tipo de detalhes, mova-o para o guia do produto relevante e vincule-o.

## Adição de novo conteúdo

Crie um tíquete COMDOX JIRA para o artigo a ser publicado. Copie `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` na descrição do tíquete e preencha-o: ele solicita que o solicitante identifique o público-alvo, sinalize se o conteúdo é temporário (com uma data de expiração) e confirme se ele pertence a insights e orientações, e não à documentação do produto do Commerce.

Depois que o escopo do tíquete for definido, inicie o artigo a partir de um modelo em `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`—não publicado, copie o artigo relevante no arquivo de destino e exclua os comentários de espaço reservado do próprio modelo). Adicione uma entrada a `help/information-center/TOC.md` em Insights e orientações assim que o conteúdo estiver pronto para publicação.

- **A nova seção de nível superior** (por exemplo, Insights > Gerenciamento de catálogo) requer análise de IA antes da adição, pois altera a forma de navegação do guia. Execute um loop em quem possui a revisão de IA do Commerce para a história ou tarefa.

- **Adicionar ao Sumário** — Adicione o novo tópico ao Sumário antes de publicar. Se necessário, use ocultar metadados para publicar um artigo oculto acessível somente a pessoas que têm o link. Consulte [Ocultar conteúdo](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) no Guia do Autor do ExL.

## Revisar cadência

Analise o conteúdo do artigo quando novas Soluções da Commerce forem renomeadas ou atualizadas, ou quando os insights não forem mais relevantes.
