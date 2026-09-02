---
title: Desenvolvimento de administradores de recomendações de produtos
description: Uma visão geral da arquitetura de recomendações de produtos e recursos de desenvolvimento.
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 127067a1ef47c7d9e51c5792e03b568dd818fe8e
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 0%

---

# Desenvolvimento de administradores de recomendações de produtos

As Recomendações de produto são uma poderosa ferramenta de marketing que pode ser usada para aumentar as conversões, aumentar a receita e estimular o engajamento do comprador. As Recomendações de produto são exibidas na loja na forma de unidades, como &quot;Clientes que visualizaram este produto também visualizaram&quot;, &quot;Clientes que compraram este produto também compraram&quot;, &quot;Recomendado para você&quot; e assim por diante. O [Adobe AI](https://business.adobe.com/ai.html) habilita o Adobe Commerce Product Recommendations, que usa inteligência artificial e algoritmos de aprendizado de máquina para executar uma análise profunda de dados agregados de compradores. Esses dados, quando combinados com seu catálogo do Commerce, resultam em experiências altamente envolventes, relevantes e personalizadas para o comprador.

>[!NOTE]
>
>Se sua loja for implementada com o PWA Studio, consulte a [documentação do PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Saiba como integrar as Recomendações de produto em um ambiente [headless](headless.md) se você usar uma tecnologia de front-end personalizada, como React ou Vue JS. As instâncias headless devem implementar eventos para potencializar o espaço de trabalho de recomendação do produto.

## Visão geral da arquitetura

Em um alto nível, as Recomendações de produto do Commerce são implantadas como SaaS. O lado do Commerce inclui a loja, que contém o coletor de eventos e o modelo de layout de recomendações, e o back-end, que inclui os módulos Data Services, SaaS Export e a interface do usuário do administrador. Os serviços de inteligência da Adobe AI são aproveitados no lado do SaaS.

![Diagrama de arquitetura de recomendações de produto](assets/arch-diag-sensei.svg)

Depois de instalados e configurados, os módulos de recomendação permitem que a loja colete dados comportamentais. A Adobe AI combina esses dados com os dados do catálogo para calcular as associações de produtos usadas pelo serviço do Recommendations. Em seguida, você pode criar, gerenciar e implantar unidades de recomendação de produto diretamente da interface do usuário do administrador.

## Próximas etapas

Leia os seguintes tópicos para começar a usar as Recomendações de produto:

- [Como implementar as recomendações de produtos](implementation-workflow.md)

- [Instalar e configurar as Recomendações de produto](install-configure.md)

- [Criar recomendações de produtos](create.md)
