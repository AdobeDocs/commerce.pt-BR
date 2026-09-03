---
title: Governança da documentação do Commerce
description: Saiba mais sobre o modelo de governança interna do Commerce Insights. Não publicado no Experience League — mantido fora do TOC.md intencionalmente.
source-git-commit: 1da6d9753acbeadf3a0df5fae86a9386643c6d6d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Governança da documentação do Commerce

Esta é uma referência interna para a equipe de documentação. Ela não está listada em `TOC.md`, portanto, não é compilada ou publicada no Experience League. Mantenha-o aqui para que ele fique perto do conteúdo que rege.

## Propriedade

Os artigos do Commerce Insights são de propriedade do autor ou da equipe de publicação responsável por manter a precisão e a moeda do artigo. Esses artigos estão atualmente hospedados no repositório `commerce.en`. A equipe de Documentação do Commerce ajuda a garantir a qualidade do conteúdo e a publicar o artigo na produção.

## O que pertence ao Commerce Insights

- **Pertence aqui**: orientações estratégicas e whitepapers para Soluções da Commerce que abrangem orientação de implementação com base em cenários do mundo real. Inclua links para as páginas relevantes da documentação do Commerce para suporte.

- **Em vez disso, pertence ao repo do produto**: configuração passo a passo, tutoriais, material de referência (referência de API/CLI/config) e solução de problemas. Se uma publicação aqui começar a acumular esse tipo de detalhes, mova-o para o guia do produto relevante e vincule-o.

## Adição de novo conteúdo

Crie um tíquete COMDOX JIRA para o artigo a ser publicado. Copie `[templates/comdox-intake-template.md](templates/comdox-intake-template.md)` na descrição do tíquete e preencha-o: ele solicita que o solicitante identifique o público-alvo, sinalize se o conteúdo é temporário (com uma data de expiração) e confirme se ele pertence ao Guia de Insights, e não à documentação do produto Commerce.

Depois que o escopo do tíquete for definido, inicie o artigo a partir de um modelo em `templates/` (`whitepaper-template.md`, `security-guidance-template.md`, `insight-perspective-template.md`—não publicado, copie o artigo relevante no arquivo de destino e exclua os comentários de espaço reservado do próprio modelo). Adicione uma entrada `TOC.md` quando o conteúdo estiver pronto para publicação.

- **A nova seção de nível superior** (por exemplo, Insights > Gerenciamento de catálogo) requer análise de IA antes da adição, pois altera a forma de navegação do guia. Execute um loop em quem possui a revisão de IA do Commerce para a história ou tarefa.

- **Adicionar ao sumário** - Adicione um novo tópico ao sumário antes de publicar. Se necessário, use ocultar metadados para publicar um artigo oculto acessível somente a pessoas que têm o link. Consulte [Ocultar conteúdo](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/hiding-files) no Guia do Autor do ExL.

## Revisar cadência

Analise o conteúdo do artigo quando novas Soluções da Commerce forem renomeadas ou atualizadas, ou quando os insights não forem mais relevantes.
