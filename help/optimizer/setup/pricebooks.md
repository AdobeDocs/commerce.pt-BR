---
title: Catálogos de Preços
description: Saiba como gerenciar catálogos de preços no [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Catálogos de Preços

Este artigo descreve como definir e atribuir catálogos de preços a exibições de catálogo com controles adequados de governança de dados.

Consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) para saber como assimilar informações do catálogo de preços de um sistema de terceiros no [!DNL Adobe Commerce Optimizer] usando a API do Catálogo de Preços.

Com catálogos de preços, você pode definir origens de catálogo de preços para gerenciar preços de produtos em diferentes níveis e mercados de clientes. Os catálogos de preços suportam um modelo hierárquico, permitindo até três níveis de catálogos de preços filhos aninhados em cada catálogo de preços base. Cada catálogo de preços pode fazer referência a um catálogo de preços pai, formando uma estrutura em árvore para origens de catálogo de preços.

O catálogo de preços base define a moeda para si mesmo e para todos os seus catálogos de preços filhos. Os catálogos de preços filhos herdam essa moeda e não podem substituí-la.

## Principais conceitos

| Termo | Descrição |
|------|-------------|
| **Catálogo de Preços** | Agrupamento lógico que define a origem do catálogo de preços; por exemplo, região específica ou nível do cliente e é usado para gerenciar preços de produtos. |
| **Catálogo de Preços de Fallback** | O catálogo de preços mais alto em uma hierarquia. Ele não tem pai e é o catálogo de preços *only* que define a moeda para ele mesmo e para todos os seus catálogos de preços descendentes.<br/><br/>Se nenhum pai for definido durante a criação do catálogo de preços (por meio da API), um novo catálogo de preços de fallback será criado. |
| **Catálogo de Preços Pai** | Um catálogo de preços de nível superior a partir do qual um catálogo de preços filho pode herdar preços se eles não estiverem explicitamente definidos no filho. |
| **Profundidade da Hierarquia** | Máximo de 3 níveis (Fallback → Criança → Netinho)<br/><br/>não aplicados no momento da ingestão. |
| **Moeda** | Definido somente no catálogo de preços de fallback. Herdado por todas as crianças, tabelas de preços.<br/><br/>Se a moeda não for especificada durante a criação do catálogo de preços de fallback (por meio da API), a moeda assumirá USD como padrão. |
| **Preço do produto** | O preço específico atribuído a um produto (SKU) em um catálogo de preços específico. |
| **Descontos** | Os descontos são definidos em Preço do Produto. Não herdado. |
