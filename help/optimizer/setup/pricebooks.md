---
title: Catálogos de Preços
description: Saiba como gerenciar catálogos de preços no [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 502d8d21ff052f4ecb212176459b38ce51f85dfc
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Catálogos de Preços

As tabelas de preços permitem definir preços de produtos para uma origem de catálogo em diferentes níveis de clientes e mercados. Os catálogos de preços suportam um modelo hierárquico, permitindo até três níveis de catálogos de preços filhos aninhados em cada catálogo de preços base. Cada catálogo de preços pode fazer referência a um catálogo de preços pai, formando uma estrutura em árvore para origens de catálogo de preços.

O catálogo de preços base define a moeda para si mesmo e para todos os seus catálogos de preços filhos. Os catálogos de preços filhos herdam essa moeda e não podem substituí-la.

Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/reference/rest/) para saber como criar, atualizar e excluir catálogos de preços para [!DNL Adobe Commerce Optimizer] usando a API de Catálogo de Preços.

## Principais conceitos

| Termo | Descrição |
|------|-------------|
| **Catálogo de Preços** | Agrupamento lógico que define preços para uma origem de catálogo; por exemplo, região específica ou nível de cliente e é usado para gerenciar preços de produtos. |
| **Catálogo de Preços de Fallback** | O catálogo de preços mais alto em uma hierarquia. Ele não tem pai e é o catálogo de preços *only* que define a moeda para ele mesmo e para todos os seus catálogos de preços descendentes.<br/><br/>Se nenhum pai for definido durante a criação do catálogo de preços (por meio da API), um novo catálogo de preços de fallback será criado. |
| **Catálogo de Preços Pai** | Um catálogo de preços de nível superior do qual um catálogo de preços filho pode herdar preços se eles não estiverem explicitamente definidos no filho. |
| **Profundidade da Hierarquia** | Máximo de três níveis (Fallback -> Filho -> Netinho)<br/><br/>não aplicados no momento da assimilação. |
| **Moeda** | Definido somente para o catálogo de preços de fallback. Herdado por todos os catálogos de preços filhos.<br/><br/>Se a moeda não for especificada durante a criação do catálogo de preços de fallback (por meio da API), a moeda assumirá USD como padrão. |
| **Preço do produto** | O preço específico atribuído a um produto (SKU) em um catálogo de preços específico. |
| **Descontos** | Os descontos são definidos no preço do produto. Não herdado. |
