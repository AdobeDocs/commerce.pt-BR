---
title: Pesquisar Workspace de merchandising
description: Saiba mais sobre o espaço de trabalho de Merchandising de pesquisa.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---

# Pesquisar Workspace de merchandising

O espaço de trabalho *Merchandising de Pesquisa* lista a seleção atual de regras e seus status, e fornece acesso às ferramentas necessárias para criar e gerenciar regras. No espaço de trabalho, é possível:

* Pesquisar regras
* Exibir detalhes da regra
* Ativar/desativar regras
* Excluir regras
* Acessar o editor de regras

![Pesquisar Workspace de merchandising](assets/rules-workspace.png)

## Definir o escopo

Se a instalação do Adobe Commerce incluir vários modos de exibição de armazenamento, defina o **Escopo** como [modo de exibição de armazenamento](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) ao qual as regras se aplicam.

## Mostrar/ocultar colunas

1. No canto superior direito, clique em **Mostrar/ocultar** ![Seletor de coluna](assets/btn-show-hide-columns.png) colunas.
As colunas visíveis têm uma marca de seleção azul no menu de opções. O nome da regra é a única coluna que não pode ser oculta.

1. No menu, siga um destes procedimentos:

   * Para mostrar uma coluna oculta, clique em qualquer nome de coluna sem uma marca de seleção.
   * Para ocultar uma coluna visível, clique em qualquer nome de coluna com uma marca de seleção.

## Filtrar regras por status

1. Se o armazenamento tiver muitas regras, você poderá filtrar as regras por status para reduzir a lista. Por padrão, a lista Regras exibe todas as regras.

1. Para listar apenas as regras com uma configuração de status específica, defina **Status** como um dos seguintes:

   * Todos
   * Ativo
   * Inativo
   * Agendado

## Localizar regras de pesquisa por nome

Comece digitando o nome da regra ou qualquer palavra no nome da regra.
A pesquisa encontra as regras correspondentes à medida que você digita. A sequência de caracteres correspondentes é realçada no nome de cada regra encontrada.

![Regras - localizar pelo nome](assets/rules-workspace-search-name.png)

## Exibir detalhes

O painel de detalhes mostra o nome da regra, o status, as condições e os eventos, as datas de início e término, a descrição e a data da última edição. As regras podem ser ativadas, editadas e excluídas no painel de detalhes.

1. No espaço de trabalho *Pesquisar Merchandising*, localize a regra na grade que você deseja exibir e clique em **Mais** (...).
1. Clique em **Exibir detalhes**.
Você pode executar qualquer um dos seguintes procedimentos a partir do painel Exibir detalhes:

   * Editar regra
   * Excluir regra
   * Ativar/desativar regra

1. Para fechar o painel *Exibir detalhes*, clique em **Fechar** (X) no canto superior direito.

   ![Regra - detalhes](assets/rules-workspace-details.png)

## Descrições da coluna

| Coluna | Descrição |
|--- |--- |
| Nome | O nome da regra. |
| Última atualização | A data em que a regra foi atualizada pela última vez. |
| Data de início | A data de início de uma regra agendada. |
| Data final | A data final de uma regra agendada. |
| Status | O status codificado por cores indica o estado atual da regra. Use o controle Status acima da grade para filtrar regras por status. Valores:<br />Todos os status - Exibe todas as regras independentemente do status.<br />Ativo (azul) - Exibe apenas as regras ativas.<br />Agendado (Laranja) - exibe somente as regras agendadas.<br />Inativo (cinza) - exibe somente regras inativas. |

## Controles

| Controle | Descrição |
|--- |--- |
| Adicionar regra | Abre o [editor de regras](rules-add.md). |
| Status | Filtra a lista de regras por status. Opções: Todas, Ativas, Inativas, Programadas |
| ![Seletor de coluna](assets/btn-show-hide-columns.png) | Especifica as colunas que ficam visíveis na grade. Opções: Última atualização, Data inicial, Data final, Status |
| Pesquisar | Pesquisa uma regra por nome completo ou correspondência parcial. |
| ![Mais seletor](assets/btn-more.png) | Exibe um menu de mais ações que podem ser aplicadas à regra selecionada. Opções: Editar, Exibir detalhes, Excluir |

## Detalhes da regra

| Campo | Descrição |
|--- |--- |
| Status | O status atual da regra. |
| Condições | A consulta de pesquisa que descreve as condições associadas à regra. |
| Data de início | A data em que a regra entra em vigor, se programada. |
| Data final | A data em que a regra expira, se programada. |
| Descrição | Uma breve descrição da regra. |
| Última atualização | A data e a hora em que a regra foi atualizada pela última vez. |
| Ativado | Um controle que altera o status da regra. Opções: Ativado / Desativado |
