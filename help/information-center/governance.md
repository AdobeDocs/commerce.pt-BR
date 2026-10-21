---
title: Controle do Commerce Information Center
description: Saiba mais sobre o modelo de controle interno do Centro de informações da Commerce. Não publicado no Experience League.
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Governança do Commerce Information Center

Essa referência interna para a equipe de documentação não está listada em `TOC.md`, portanto, não foi publicada na Adobe Experience League.

## Propriedade

A equipe de documentação da Adobe Commerce é proprietária do Centro de Informações. Foi criado em `Adobe-Enterprise-Docs/commerce.en`, o repositório listado como `git-repo` em `metadata.md`.

Nenhuma equipe de produto é proprietária porque é multiproduto. Escalone as correções específicas do produto para o contato de documentos da equipe de produtos responsável, em vez de corrigi-las aqui.

## O que pertence ao Centro de informações

| Pertence aqui | Pertence ao repo do produto |
| --- | --- |
| Conteúdo que abrange mais de um produto ou serviço, como orientação de seleção de produtos, jornadas de implementação entre produtos, padrões de arquitetura e white papers | Conteúdo de produto único, como configuração passo a passo, referência de API/CLI/configuração e solução de problemas |
| Páginas de curadoria curta que se vinculam a documentos autorizados do produto | |

- Se uma página aqui acumular detalhes de um único produto, mova-a para o guia do produto e vincule-a a ela.
- O Centro de informações não consolida nem migra a documentação do produto e não documenta recursos de produtos individuais. Vincule ao conteúdo autoritativo existente antes de escrever algo novo.

## Adição de novo conteúdo

### Artigos em uma seção existente

1. Adicione o arquivo à pasta que corresponde à seção.
1. Adicione uma entrada a `TOC.md` nessa seção.

Nenhuma aprovação é necessária além da revisão normal de PR.

| Seção do sumário | Pasta |
| --- | --- |
| Explorar plataformas e serviços da Commerce | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| Introdução por função | `get-started/` |
| Insights e orientação | `guidance-and-insights/` |
| Arquitetura | `architecture-options/` |
| Migração e adoção | `migration-adoption/` |
| Guias de implementação | `implementation-guides/` |

### Insights e artigos de orientação

1. Copiar `whitepaper-template.md` ou `security-guidance-template.md` de `guidance-and-insights/templates/` para `guidance-and-insights/`. Os modelos não são publicados. Para ver o processo de criação completo, incluindo o tíquete de entrada COMDOX, consulte [readme.md](guidance-and-insights/readme.md).
1. Exclua os comentários do espaço reservado do modelo.
1. Adicione uma entrada `TOC.md` em Insights e orientações quando o conteúdo estiver pronto para publicação.

### Seções de nível superior

Um novo grupo de nível superior no `TOC.md` altera a navegação do guia; portanto, requer revisão de IA. Entre em contato com o proprietário do Commerce IA Review. Reutilize uma seção existente primeiro, como Começar por função para parceiro ou conteúdo de ativação.

### URLs publicados

As URLs são criadas a partir da ID do guia, das IDs de seção em `TOC.md` (por exemplo, `{#insights-and-guidance}`) e do nome do arquivo. Os nomes das pastas não aparecem no URL. Forneça uma ID exclusiva a cada seção e verifique se dois artigos não são resolvidos para o mesmo URL.

## Revisar cadência

- **Orientado a eventos**—revise as seções Explorar plataformas e serviços da Commerce, Introdução a funções, Arquitetura, Migração e adoção e Guias de implementação quando um produto da Commerce é renomeado, iniciado ou descontinuado, ou sua disponibilidade é alterada. Por exemplo, analise-as se o Adobe Commerce as a Cloud Service e o Adobe Commerce Optimizer obtiverem uma integração. Essas páginas se tornam desatualizadas primeiro.
- **Agendado**—para detectar imprecisões técnicas, de marca ou de terminologia desatualizadas, execute uma auditoria de conteúdo automatizada e revise a cada seis meses.

## Relação com ajuda/aterrissagem/

`help/landing/` (&quot;Guias de Serviços da Adobe Commerce&quot;) é um guia separado que não faz parte da Central de Informações. Ele se concentra em serviços da Commerce, como Serviço de catálogo, Live Search, Recomendações de produto e Serviços de pagamento, e os links do Centro de informações para obter detalhes. Redefinir o escopo ou consolidar os dois é uma decisão de acompanhamento que este guia não resolve.
