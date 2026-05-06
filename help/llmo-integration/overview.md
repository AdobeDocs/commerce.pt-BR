---
title: Integrar [!DNL Adobe Commerce] com [!DNL Adobe LLM Optimizer]
description: Conecte [!DNL Adobe Commerce] a [!DNL Adobe LLM Optimizer] para monitorar sinais de catálogo em LLMs e implantar otimizações de catálogo aprovadas.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Integrar [!DNL Adobe Commerce] a [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>O acesso a essa integração é restrito. Entre em contato com o Gerente técnico de conta para obter mais detalhes.

O [!DNL Adobe LLM Optimizer] é uma solução corporativa que ajuda as marcas a monitorar, analisar e otimizar como seu conteúdo aparece nas respostas de modelos de idiomas grandes (LLMs) e assistentes de IA. À medida que os compradores usam cada vez mais as ferramentas de IA para pesquisa e descoberta de produtos, o LLM Optimizer ajuda a garantir que sua marca e catálogo sejam citados com precisão e exibidos em contexto.

Este guia descreve como o **[!DNL Adobe Commerce]** se encaixa nesse fluxo de trabalho quando o catálogo de produtos é armazenado no Commerce. Você aprenderá quais recursos ficam disponíveis, qual configuração é necessária e como as otimizações implantadas se comportam no Administrador e nos canais de assimilação.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] é uma solução autônoma do Adobe. Os fluxos de trabalho de oportunidade e monitoramento principal não exigem o [!DNL Adobe Experience Manager] (AEM) ou outros aplicativos da Adobe. As ações de implantação específicas da Commerce se aplicam apenas quando seu catálogo está conectado ao LLM Optimizer e você escolhe enviar as alterações aprovadas para o [!DNL Adobe Commerce].

## O que a integração permite {#what-integration-enables}

Conectar o LLM Optimizer ao catálogo do [!DNL Adobe Commerce] permite mover de insights de conteúdo amplos para **recomendações com reconhecimento de catálogo**:

- **Identifique** lacunas e inconsistências nos dados de catálogo — como títulos, descrições e sinais estruturados — que afetam como os LLMs interpretam seus produtos.
- **Revisão** sugeriu melhorias com o contexto de suporte, incluindo justificativas e comparações antes e depois.
- **Implante** otimizações selecionadas, como atualizações de nome e descrição do produto, diretamente no catálogo da Commerce, garantindo que os fluxos de trabalho de administração, grades e dados voltados para a loja permaneçam alinhados.

Quando a origem do catálogo é [!DNL Adobe Commerce], o Adobe pode oferecer suporte ao fluxo de trabalho completo: identificar oportunidades automaticamente, sugerir alterações e aplicar correções aprovadas. Para catálogos originados fora do Commerce, o LLM Optimizer ainda pode analisar e sugerir melhorias, mas a aplicação de alterações depende do seu modelo de integração (por exemplo, um catálogo espelhado ou atualizações manuais). Consulte [Limites e limites de integração](boundaries-limits.md).

## Quem é este {#who-this-is-for}

- **Comerciantes e comerciantes digitais** que desejam que os dados do produto sejam precisos e consistentes em respostas orientadas por LLM e precisam de uma maneira controlada para melhorar a cópia do catálogo em escala.
- **Administradores do Commerce** que são proprietários de integridade de catálogo, processos de administração e integrações (API, CSV, PIM) que alimentam atributos de produto.

## Pré-requisitos {#prerequisites}

Os seguintes pré-requisitos se aplicam quando você tem **acesso** à integração do Adobe Commerce com o Adobe LLM Optimizer. Entre em contato com o Gerente técnico de conta para obter mais detalhes.

- Sua loja pode ser rastreada por bots orientados a LLM e de agilidade, nos quais esse recurso de rastreo faz parte de sua estratégia de medição e otimização da LLM Optimizer (um pré-requisito geral para insights sensíveis a catálogos).
- Para fluxos de trabalho de implantação com suporte da Commerce, os serviços necessários da Commerce e a conectividade de catálogo estão habilitados e íntegros. A configuração no nível da tarefa é descrita em [Conectar o Adobe Commerce ao LLM Optimizer](get-started/connect-to-llmo.md).

Você também deve entender como os dados se movimentam entre sistemas:

### Fluxo de dados de alto nível {#high-level-data-flow}

Conceitualmente, as otimizações de catálogo seguem dois padrões (seu projeto pode usar um ou ambos, dependendo da capacidade):

| Direção | Finalidade |
| --- | --- |
| **Catálogo do Commerce -> LLM Optimizer** | O catálogo e os sinais de URL alimentam oportunidades e sugestões na interface do usuário do LLM Optimizer. |
| **LLM Optimizer -> Commerce** | Depois de aprovar uma ação de implantação, as atualizações no nome e na descrição do produto são gravadas no catálogo principal do Commerce para que o administrador e a loja reflitam os valores otimizados. |

### [!DNL Adobe Commerce] comparado a catálogos de terceiros {#commerce-vs-third-party}

| Origem do catálogo | Cobertura típica do LLM Optimizer |
| --- | --- |
| **[!DNL Adobe Commerce]** | Forte suporte para identificação e sugestões, além da implantação de atualizações de campo de catálogo aprovadas que você configura. |
| **Comércio de terceiros** | A identificação e as sugestões são aceitas; a implantação automatizada no sistema comerciante depende de fluxos de trabalho de exportação, espelhamento ou parceiros, em vez de gravações diretas no catálogo de origem do comerciante. |

## Agente de catálogo, Storefront MCP e LLM Optimizer {#catalog-agent-and-mcp}

Seu [!DNL Adobe Commerce] **catálogo de produtos** é o sistema de registro de dados de produtos: nomes, descrições, atributos, preços e estoque. Para potencializar a descoberta e a otimização assistidas por IA, o **MCP do Adobe Commerce Storefront** (Model Context Protocol) é uma interface estruturada entre os dados de catálogo em tempo real do Commerce e as experiências do Adobe AI.

O **Agente de Catálogo** fica na parte superior do MCP de vitrine. O Agente de Catálogo permite que [!DNL Adobe LLM Optimizer] consulte, enriqueça e atue no contexto do catálogo e PDP ao identificar lacunas, propor melhorias e implantar alterações quando você aprová-las. Esses recursos aparecem nos fluxos de trabalho do LLM Optimizer descritos em [Usar o LLM Optimizer com o Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Como o Catalog Agent melhora o Commerce para LLMs {#catalog-agent-optimizations}

O Agente de catálogo aborda a descoberta por meio de duas otimizações complementares: enriquecimento da página de detalhes do produto e enriquecimento do catálogo de produtos.

### Enriquecimento da página de detalhes do produto {#pdp-enrichment-overview}

O **enriquecimento da PDP (Product Detail Page, página de detalhes do produto)** sugere refinamentos no conteúdo da página do produto para que a mercadoria seja lida com mais clareza quando os compradores descobrirem produtos por meio de assistentes de IA e ferramentas semelhantes. O objetivo é melhorar a clareza e a consistência sem alterar o layout da loja, pois sua equipe já foi comercializada. Você revisa sugestões no LLM Optimizer e implanta quando estiver pronto.

Depois de implantar, verifique a página do produto ao vivo para confirmar se a experiência de compra ainda é exibida conforme esperado.

### Enriquecimento do catálogo de produtos {#catalog-enrichment-overview}

O **Enriquecimento do catálogo de produtos** sugere **nomes de produtos** e **descrições de produtos** mais claros, nos quais a cópia é fina, vaga ou inconsistente. Cada sugestão inclui contexto para que sua equipe possa decidir o que alterar. Ao aprovar uma atualização, ela pode ser aplicada ao catálogo [!DNL Adobe Commerce] para que o Administrador, a loja e outras experiências que usam esses campos reflitam a mesma redação.

Como esses campos residem no Commerce, melhorar um nome ou uma descrição uma vez pode beneficiar cada canal que lê esses dados do produto (dependendo de como e quando seus sistemas são atualizados).

## Tópicos relacionados {#related-topics}

- [Conectar o Adobe Commerce ao LLM Optimizer](get-started/connect-to-llmo.md)
- [Usar o LLM Optimizer com o Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Limites e limites de integração](boundaries-limits.md)
