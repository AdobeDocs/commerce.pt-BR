---
title: Desempenho do Recommendations
description: A página de desempenho do Recommendations fornece informações sobre o desempenho das recomendações de produtos do insight.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
source-git-commit: 9cb231055df45bbfcff3303c6e1c257c883cb852
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# Desempenho do Recommendations

A página Desempenho do Recommendations exibe uma lista de recomendações configuradas, juntamente com as métricas principais, para ajudá-lo a avaliar sua eficácia. Você pode configurar a exibição para exibir métricas do dia, semana ou mês passado. Esses insights mostram a frequência com que cada unidade de recomendação é visualizada ou clicada, ajudando a avaliar o desempenho e identificar oportunidades de otimização.

>[!INFO]
>
>Uma unidade de recomendação é um widget que contém o produto recomendado _itens_.

![Desempenho de recomendações](../assets/rec-performance.png){zoomable="yes"}

## Exibir um relatório

1. Escolha a **Exibição de catálogo**, como *Todas as exibições* às quais as recomendações se aplicam.

   Saiba mais sobre [exibições de catálogo](#select-catalog-view) em recomendações.

1. Clique em **[!UICONTROL Date Range]** e selecione um dos seguintes intervalos:

   ![Intervalo de datas das recomendações](../assets/rec-perf-date-range.png)

   A tabela de recomendações é atualizada para exibir métricas para esse intervalo de datas e exibição de catálogo.

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
| [Exibição de catálogo](#select-catalog-view) | Selecione a exibição de catálogo para filtrar a tabela e mostrar apenas as recomendações que se aplicam à exibição de catálogo selecionada. Esta seleção também é usada como exibição de catálogo quando você [cria](../merchandising/recommendations/create.md) uma nova recomendação. As opções são *Todas as exibições* ou uma [exibição de catálogo](../setup/catalog-view.md) específica. |

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

## Selecionar exibição do catálogo

>[!IMPORTANT]
>
>No momento, esse recurso está na versão beta.

O seletor **[!UICONTROL Catalog view]** na página **Recommendations** faz duas coisas:

1. **Filtra a tabela** - Mostra somente recomendações (e suas métricas) que se aplicam à exibição do catálogo selecionado.
1. **Define o escopo para novas recomendações** - Quando você [cria](../merchandising/recommendations/create.md) uma recomendação, a exibição de catálogo selecionada é usada como o escopo da unidade. As opções são *Todas as exibições* ou uma [exibição de catálogo](../setup/catalog-view.md) específica.

   - **Todas as exibições** - A recomendação se aplica a todas as exibições de catálogo (a disponibilidade do produto ainda é filtrada por exibição).
   - **Exibição de catálogo** - A recomendação se aplica somente à exibição de catálogo selecionada (por exemplo, uma vitrine, idioma ou marca).

Especificando uma exibição de catálogo para cada recomendação, você pode:

- Configure recomendações para todas as exibições de catálogo (global) ou para uma exibição de catálogo.
- Visualize e filtre produtos por exibição de catálogo na página de recomendação [criar](../merchandising/recommendations/create.md).
- Mostrar apenas os produtos disponíveis em cada vitrine.
- Exibir métricas e comportamento da loja por exibição de catálogo.

### Como a exibição de catálogo filtra produtos

A disponibilidade do produto é imposta por exibição de catálogo, mesmo para unidades de recomendação na seleção **Todas as exibições**. Isso funciona além de qualquer [filtro de inclusão ou exclusão](../merchandising/recommendations/filters.md) definido na unidade de recomendação.

**Exemplo: recomendação com filtros de inclusão na seleção Todas as exibições**

- **Todas as exibições** recomendadas incluem SKUs: SKU_ABC, SKU_CDE, SKU_XYZ.
- **Exibição de catálogo: Kingsbluff** não pode vender SKU_ABC ou SKU_CDE. **Exibido:** SKU_XYZ mais quaisquer outras SKUs válidas para Kingsbluff.
- **Exibição de catálogo: a Arkbridge** não pode vender nenhuma das SKUs incluídas. **Mostrado:** somente SKUs permitidas pela Arkbridge. Se não houver nenhuma disponível, a unidade de recomendação não aparecerá nessa vitrine.
