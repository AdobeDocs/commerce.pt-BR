---
title: Desenvolvimento de administradores de recomendações de produtos
description: Uma visão geral da arquitetura de recomendações de produtos e recursos de desenvolvimento.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Desenvolvimento de administradores de recomendações de produtos

As Recomendações de produto são uma poderosa ferramenta de marketing que pode ser usada para aumentar as conversões, aumentar a receita e estimular o engajamento do comprador. As Recomendações de produto são exibidas na loja na forma de unidades, como &quot;Clientes que visualizaram este produto também visualizaram&quot;, &quot;Clientes que compraram este produto também compraram&quot;, &quot;Recomendado para você&quot; e assim por diante. As Recomendações de Produto do Adobe Commerce são viabilizadas pela [IA do Adobe](https://business.adobe.com/ai.html), que usa inteligência artificial e algoritmos de aprendizado de máquina para executar uma análise detalhada de dados agregados do comprador. Esses dados, quando combinados com seu catálogo do Commerce, resultam em experiências altamente envolventes, relevantes e personalizadas para o comprador.

>[!NOTE]
>
>Se sua loja for implementada com o PWA Studio, consulte a [documentação do PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se você usa uma tecnologia de front-end personalizada, como o React ou o Vue JS, consulte o guia do usuário para saber como integrar as Recomendações de produto em um ambiente [headless](headless.md). As instâncias headless devem implementar eventos para potencializar o espaço de trabalho de recomendação do produto.

## Visão geral da arquitetura

Em um alto nível, as Recomendações de produto do Commerce são implantadas como SaaS. O lado do Commerce inclui a loja, que contém o coletor de eventos e o modelo de layout de recomendações, e o back-end, que inclui os módulos Data Services, SaaS Export e a interface do usuário do administrador. Os serviços de inteligência de IA do Adobe são aproveitados no lado do SaaS.

![Diagrama de arquitetura de recomendações de produto](assets/arch-diag-sensei.svg)

Depois que os módulos de recomendação forem instalados e configurados, sua loja começará a coletar dados comportamentais. A IA do Adobe processa esses dados comportamentais junto com seus dados de catálogo e calcula associações de produtos que são aproveitadas pelo serviço de recomendações. Neste ponto, o comerciante pode criar, gerenciar e implantar unidades de recomendação de produto em sua vitrine diretamente da interface do usuário do administrador.

## Próximas etapas

Leia os seguintes tópicos para começar a usar as Recomendações de produto:

- [Como implementar as recomendações de produtos](implementation-workflow.md)

- [Instalar e configurar as Recomendações de produto](install-configure.md)

- [Criar recomendações de produtos](create.md)
