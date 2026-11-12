---
title: Catálogos de Preços
description: Saiba como gerenciar catálogos de preços no [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente ao Adobe Commerce as a Cloud Service e a projetos [!DNL Adobe Commerce Optimizer] (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
TQID: https://experienceleague.adobe.com/-vL79MMePcUdhE-gPwjFJZStZUtNLKAUxpePm4Fvmfk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: cde6d0c92f4c169588164c22c948d1b287873bdd
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%
---
# Catálogos de Preços

Os catálogos de preços definem os preços do produto para uma origem de catálogo em níveis e mercados do cliente. Eles suportam um modelo hierárquico, permitindo até três níveis de catálogos de preços-filho aninhados em cada catálogo de preços-base. Cada catálogo de preços pode fazer referência a um catálogo de preços pai, formando uma estrutura em árvore para origens de catálogo de preços.

![Hierarquia do Catálogo de Preços](../assets/price-book-hier.png)

O catálogo de preços base define a moeda para si mesmo e para todos os seus catálogos de preços filhos. Os catálogos de preços filhos herdam essa moeda e não podem substituí-la.

## Principais conceitos

| Termo | Descrição |
| ------ | ------------- |
| **Catálogo de Preços** | Agrupamento lógico que define preços para uma origem de catálogo; por exemplo, região específica ou nível de cliente e é usado para gerenciar preços de produtos. |
| **Catálogo de Preços de Fallback** | O catálogo de preços mais alto em uma hierarquia. Ele não tem pai e é o catálogo de preços *only* que define a moeda para ele mesmo e para todos os seus catálogos de preços descendentes.<br/><br/>Se nenhum pai for definido durante a criação do catálogo de preços (por meio da API), um novo catálogo de preços de fallback será criado. |
| **Catálogo de Preços Pai** | Um catálogo de preços de nível superior do qual um catálogo de preços filho pode herdar preços se eles não estiverem explicitamente definidos no filho. |
| **Profundidade da Hierarquia** | Máximo de três níveis (Fallback -> Filho -> Netinho)<br/><br/>não aplicados no momento da assimilação. |
| **Moeda** | Definido somente para o catálogo de preços de fallback. Herdado por todos os catálogos de preços filhos.<br/><br/>Se a moeda não for especificada durante a criação do catálogo de preços de fallback (por meio da API), a moeda assumirá USD como padrão. |
| **Preço do produto** | O preço específico atribuído a um produto (SKU) em um catálogo de preços específico. |
| **Descontos** | Os descontos são definidos no preço do produto. Não herdado. |

## Implementação do catálogo de preços

A implementação da tabela de preços varia de acordo com a implantação do Commerce.

* Em instâncias do Adobe Commerce Optimizer com back-end de terceiros do Commerce, os catálogos de preços são criados usando a API REST de assimilação de dados. Você os atribui e gerencia no espaço de trabalho Exibição de catálogo no Commerce Optimizer Studio.

* No Adobe Commerce as a Cloud Service com o modelo de dados de catálogo combinável (CCDM), os catálogos de preços são mapeados a partir dos dados de catálogo e preço do Adobe Commerce. Você exibe os catálogos de preços atribuídos a cada exibição de catálogo do Administrador do Commerce.

* No Adobe Commerce na infraestrutura em nuvem ou em implantações locais com o Adobe Commerce Optimizer Connector, as tabelas de preços também são mapeadas a partir dos dados de catálogo e preços do Adobe Commerce. Você exibe os catálogos de preços atribuídos a cada exibição de catálogo do espaço de trabalho Exibição de Catálogo na instância conectada do Commerce Optimizer.

## Adicionar catálogos de preços

Você adiciona catálogos de preços a [!DNL Adobe Commerce Optimizer] usando a API Catálogo de Preços. Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/reference/rest/) para saber como criar, atualizar e excluir catálogos de preços para [!DNL Adobe Commerce Optimizer].

## Exibir catálogos de preços

Depois de assimilar catálogos de preços em [!DNL Adobe Commerce Optimizer], você poderá ver a lista de catálogos de preços e suas IDs correspondentes na página **Exibição de catálogo**.

>[!NOTE]
>
>Uma exibição de catálogo privado (uma com [!UICONTROL Catalog Protection] habilitada) pode fazer referência a apenas um catálogo de preços. Consulte [Restrição de catálogo de preços em exibições de catálogo privado](private-catalog-view.md#price-book-restriction-on-private-catalog-views).

1. Vá para _Configuração da loja_ e clique em **[!UICONTROL Catalog views]**.

1. Clique em **[!UICONTROL Create catalog view]**. &#x200B;

   Em configurar os detalhes de exibição do catálogo, selecione um dos catálogos de preços disponíveis.

   ![Nomes e IDs do Catálogo de Preços](../assets/price-book-name-ids.png)

## Configurar disponibilidade do catálogo de preços

Especifique os dados de precificação disponíveis para cada exibição de catálogo configurando a disponibilidade do catálogo de preços para cada exibição.

1. No espaço de trabalho **Exibição de Catálogo**, selecione a exibição de catálogo que deseja configurar.

1. Na seção [!UICONTROL Price Books], selecione as opções de catálogo de preços para configurar os preços disponíveis para lojas com suporte na exibição de catálogo.

1. Clique em **[!UICONTROL Save]** para aplicar as alterações à exibição do catálogo.
