---
title: Workspace [!DNL Product Recommendations]
description: Saiba como configurar, gerenciar e monitorar o desempenho de recomendações de produtos.
exl-id: eaf1f0b2-9d9d-4069-8269-06f30166f788
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# Workspace [!DNL Product Recommendations]

O espaço de trabalho [!DNL Product Recommendations] exibe uma lista de recomendações configuradas anteriormente com métricas que ajudam você a monitorar o sucesso de cada recomendação. A lista pode ser configurada para calcular métricas do último dia, semana ou mês. Você pode usar as métricas para criar insights acionáveis com base na frequência com que uma unidade de recomendação é visualizada ou clicada, ou para analisar o desempenho de suas recomendações.

>[!INFO]
>
>Uma unidade de recomendação é um widget que contém o produto recomendado _itens_.

![Espaço de trabalho de recomendações](assets/workspace.png)
_Workspace de recomendações_

## Coleção de dados

Para garantir que cada área funcional do espaço de trabalho contenha os dados corretos, é necessário configurar a coleta de dados com base na implementação de vitrine selecionada:

1. Luma - A coleção de dados está disponível e pronta para uso.
1. Headless - a coleta de dados deve ser configurada manualmente, dependendo da implementação da loja.

Se você estiver usando uma loja headless, consulte a seguinte documentação para obter mais informações sobre os eventos necessários que precisam ser adicionados:

- [Eventos necessários](events.md) para o painel Recomendações de Produto.
- [Coletor de eventos de vitrine](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) que precisa ser adicionado como pré-requisito.
- [Exemplos](https://github.com/adobe/commerce-events/tree/main/examples) da estrutura de eventos.

## Definir o escopo

Inicialmente, o [escopo](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) de todas as configurações de recomendação está definido como `Default Store View`. Se a instalação do Commerce incluir vários modos de exibição de armazenamento, defina o **Escopo** como [modo de exibição de armazenamento](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) ao qual as recomendações se aplicam.

## Definir intervalo de datas das métricas

1. Clique no controle **Seletor de** Calendário![&#x200B; &#x200B;](assets/icon-calendar.png).

1. Escolha uma das seguintes opções:

   - Últimas 24 horas
   - Últimos 7 dias
   - Últimos 30 dias

   Os valores calculados nas colunas de métricas são alterados para refletir o intervalo de datas atual.

   >[!NOTE]
   >
   >As métricas de Recomendação de produto são otimizadas para vitrines da Luma. Se sua loja não for baseada em Luma, a forma como as métricas rastreiam os dados dependerá de como você [implementa a coleção de eventos](events.md).

## Mostrar/ocultar colunas

1. No canto superior esquerdo, clique em **Mostrar/ocultar** ![Seletor de coluna](assets/icon-show-hide-columns.png) colunas.

   As colunas visíveis têm uma marca de seleção azul.

1. No menu, siga um destes procedimentos:

   - Para mostrar uma coluna oculta, clique em qualquer nome de coluna sem uma marca de seleção.
   - Para ocultar uma coluna visível, clique em qualquer nome de coluna com uma marca de seleção.

   A tabela é atualizada para incluir apenas as colunas selecionadas.

   ![Espaço de trabalho de recomendações](assets/workspace-select-columns.png)
   _Mostrar/ocultar colunas_

## Configurações

As configurações determinam o espaço de dados SaaS que fornece os dados comportamentais de recomendação.

- Para alterar o local de origem dos dados comportamentais de recomendação, escolha um espaço de dados SaaS diferente.

- Para configurar um novo espaço de dados SaaS, clique em **Editar configuração**. Para saber mais, consulte [Configurações](settings.md).

![Configurações de recomendações](assets/settings.png)
_Configurações de recomendações_

## Exibir detalhes

1. Na tabela, clique na recomendação que deseja examinar.

   ![Espaço de trabalho de recomendações](assets/recommendation-detail.png)
   _Detalhes do Índice de Conversão da Página Inicial_

1. Para alterar o status da recomendação, clique em **Ativar** ou **Desativar**.

## Editar recomendação

Na página de detalhes da recomendação, clique em **Editar**. Para saber mais, acesse [Editar Recomendações](edit.md).

## Criar recomendação

Na página de detalhes da recomendação, clique em **Criar**. Para saber mais, acesse [Criar Recomendações](create.md).

## Controles do Workspace

| Controle | Descrição |
|---|---|
| ![Seletor de calendário](assets/icon-calendar.png) | Determina o intervalo de tempo usado para cálculos de métricas. Opções: 24 horas/7 dias/30 dias |
| ![Seletor de coluna](assets/icon-show-hide-columns.png) | Determina as colunas que aparecem na tabela [!DNL Product Recommendations]. |
| Configurações | Determina o espaço de dados SaaS onde os dados comportamentais de recomendação são obtidos e também ativa o tipo de recomendação de semelhança visual. |
| Criar recomendação | Abre a página [Criar Nova Recomendação](create.md). |

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
