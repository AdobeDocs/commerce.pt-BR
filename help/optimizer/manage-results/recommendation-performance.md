---
title: Desempenho do Recommendations
description: A página de desempenho do Recommendations fornece informações sobre o desempenho das recomendações de produtos do insight.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Desempenho do Recommendations

A página Desempenho do Recommendations exibe uma lista de recomendações configuradas, juntamente com as métricas principais, para ajudá-lo a avaliar sua eficácia. Você pode configurar a exibição para exibir métricas do dia, semana ou mês passado. Esses insights mostram a frequência com que cada unidade de recomendação é visualizada ou clicada, ajudando a avaliar o desempenho e identificar oportunidades de otimização.

>[!INFO]
>
>Uma unidade de recomendação é um widget que contém o produto recomendado _itens_.

![Desempenho de recomendações](../assets/rec-performance.png){zoomable="yes"}

## Exibir um relatório

1. Escolha a **origem do catálogo**, como `en-US` onde as recomendações se aplicam.

1. Clique em **[!UICONTROL Date Range]** e selecione um dos seguintes intervalos:

   ![Intervalo de datas das recomendações](../assets/rec-perf-date-range.png)

   A tabela de recomendações é atualizada para exibir as métricas desse intervalo de datas.

## Personalizar tabela

1. No canto superior esquerdo, clique no ícone ![Seletor de coluna](../assets/icon-show-hide-columns.png) para personalizar a tabela.

   As colunas visíveis têm uma marca de seleção.

1. No menu, siga um destes procedimentos:

   - Para mostrar uma coluna oculta, clique em qualquer nome de coluna sem uma marca de seleção.
   - Para ocultar uma coluna visível, clique em qualquer nome de coluna com uma marca de seleção.

   A tabela é atualizada para incluir apenas as colunas selecionadas.

## Exibir detalhes

1. Na tabela, clique no ícone (![Mais seletor](../assets/btn-more.png)) ao lado da recomendação que você deseja examinar.

1. Para alterar o status da recomendação, clique em **Ativar** ou **Desativar**.

## Criar ou gerenciar recomendações

Saiba como [criar uma recomendação nova ou gerenciar uma existente](../merchandising/recommendations/create.md).

## Controles do Workspace

| Controle | Descrição |
|---|---|
| ![Intervalo de datas](../assets/rec-perf-date-range.png) | Determina o intervalo de tempo usado para cálculos de métricas. |
| ![Seletor de coluna](../assets/icon-show-hide-columns.png) | Determina as colunas que aparecem na tabela Recommendations. |
| Criar recomendação | Abre a página [Criar Nova Recomendação](../merchandising/recommendations/create.md). |

## Descrições da coluna

| Coluna | Descrição |
|---|---|
| Nome | O nome da recomendação. |
| Página | A página onde a recomendação aparece. |
| Tipo | O tipo de recomendação. |
| Status | O status da recomendação. Opções: Inativo/Ativo/Rascunho |
| Criado em | A data em que a recomendação foi criada. |
| Última edição | A data em que a recomendação foi editada pela última vez. |
| Impressões | O número de vezes que uma unidade de recomendação é carregada e renderizada em uma página. Uma unidade de recomendação que está abaixo da dobra da janela de visualização do navegador é renderizada na página, mesmo se não for visualizada pelo comprador. Nesse caso, a unidade renderizada é contada como uma impressão, mas uma exibição é contada somente se o comprador rolar a unidade para visualização. |
| vImpressões | (Impressões visíveis) O número de unidades de recomendação que registram pelo menos uma visualização. Por exemplo, se a unidade de recomendação tiver duas linhas, cada uma com dois produtos, e os dois últimos produtos não forem vistos pelo comprador, mas as duas primeiras forem, a atividade ainda contará como uma impressão. |
| Visualizações | O número de unidades de recomendação exibidas na janela de visualização do navegador do comprador. Se o comprador rolar a página várias vezes para cima ou para baixo, o evento será acionado várias vezes, cada vez que a unidade estiver visível. |
| Cliques | A soma do número de vezes que um comprador clica em um item na unidade de recomendação e do número de vezes que ele clica no botão **Adicionar ao carrinho** na unidade de recomendação |
| Receita | A receita gerada pela recomendação para o intervalo de tempo atual. |
| Receita Lt | (Receita vitalícia) A receita vitalícia impulsionada por uma recomendação. |
| Visibilidade | A porcentagem de unidades de recomendação que se registram na exibição. |
| CTR | (Taxa de click-through) A porcentagem de impressões de unidade para a recomendação que registra um clique. O CTR conta todas as impressões, mesmo se a unidade não entrar na visualização do comprador. Se a unidade de recomendação não for visualizada, é improvável clicar nela. No entanto, essas impressões inéditas contam para a pontuação do CTR e reduzem a porcentagem geral de CTR. |
| vCTR | (Taxa de click-through de visualização) mede os cliques com base apenas em impressões visualizáveis (recomendações que realmente apareceram na parte visível da tela do comprador), fornecendo um indicador mais preciso do envolvimento do comprador. |
