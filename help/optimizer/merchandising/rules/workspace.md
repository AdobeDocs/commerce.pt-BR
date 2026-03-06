---
title: Workspace de regras de merchandising
description: Conheça o espaço de trabalho Regras de merchandising.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 3deac529-731d-44b9-87f3-3c9cb36e28e7
source-git-commit: 9cb231055df45bbfcff3303c6e1c257c883cb852
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# Workspace de regras de merchandising

O espaço de trabalho *Regras de merchandising* lista a seleção atual de regras e seus status, e fornece acesso às ferramentas necessárias para criar e gerenciar regras. Você pode aplicar regras de escopo a todas as [exibições de catálogo](../../setup/catalog-view.md) (globais) ou a uma única exibição de catálogo. Consulte [Selecionar exibição de catálogo](#select-catalog-view) para saber como filtrar por exibição de catálogo e criar regras por exibição de catálogo. No espaço de trabalho, é possível:

- Pesquisar regras
- Exibir detalhes da regra
- Ativar/desativar regras
- Excluir regras
- Acessar o editor de regras

![Workspace de regras de merchandising](../../assets/rules-workspace.png)

## Mostrar/ocultar colunas

1. No canto superior direito, clique em **Mostrar/ocultar** ![Seletor de coluna](../../assets/btn-show-hide-columns.png) colunas.

1. No menu, siga um destes procedimentos:

   - Para mostrar uma coluna oculta, clique em qualquer nome de coluna sem uma marca de seleção.
   - Para ocultar uma coluna visível, clique em qualquer nome de coluna com uma marca de seleção.

## Filtrar regras por status

1. Se o armazenamento tiver muitas regras, você poderá filtrar as regras por status para reduzir a lista. Por padrão, a lista Regras exibe todas as regras.

1. Para listar apenas as regras com uma configuração de status específica, defina **Status** como um dos seguintes:

   - Todos
   - Ativo
   - Inativo
   - Agendado
   - Rascunho

   Você também pode filtrar por **Condições**, **Data de início**, **Data de término** e **Última atualização**.

## Exibir detalhes

O painel de detalhes mostra o nome da regra, o status, as condições e os eventos, as datas de início e término, a descrição e a data da última edição. As regras podem ser ativadas, editadas e excluídas no painel de detalhes.

1. No espaço de trabalho *Regras de merchandising*, localize a regra na grade que você deseja exibir e clique no ícone (![Mais seletor](../../assets/btn-more.png)).

   Você pode executar qualquer um dos seguintes procedimentos no menu:

   - Editar regra
   - Excluir regra
   - Ativar/desativar regra

## Descrições da coluna

| Coluna | Descrição |
|--- |--- |
| Nome | O nome da regra. |
| Última atualização | A data em que a regra foi atualizada pela última vez. |
| Data inicial | A data de início de uma regra agendada. |
| Data final | A data final de uma regra agendada. |
| Status | O status codificado por cores indica o estado atual da regra. Use o controle Status acima da grade para filtrar regras por status. Valores:<br />Todos os status - Exibe todas as regras independentemente do status.<br />Ativo (azul) - Exibe apenas as regras ativas.<br />Agendado (Laranja) - exibe somente as regras agendadas.<br />Inativo (cinza) - exibe somente regras inativas. |

## Controles

| Controle | Descrição |
|--- |--- |
| Adicionar regra | Abre o [editor de regras](add.md). |
| Exibição de catálogo | Filtra a tabela para regras que se aplicam à exibição do catálogo selecionado. Também define o escopo quando você [cria uma regra](add.md). Opções: *Todas as exibições* ou uma [exibição de catálogo](../../setup/catalog-view.md) específica. Consulte [Selecionar exibição de catálogo](#select-catalog-view). |
| Status | Filtra a lista de regras por status. Opções: Todas, Ativas, Inativas, Programadas |
| ![Seletor de coluna](../../assets/btn-show-hide-columns.png) | Especifica as colunas que ficam visíveis na grade. Opções: Última atualização, Data inicial, Data final, Status |
| Pesquisar | Pesquisa uma regra por nome completo ou correspondência parcial. |
| ![Mais seletor](../../assets/btn-more.png) | Exibe um menu de mais ações que podem ser aplicadas à regra selecionada. Opções: Editar, Exibir detalhes, Excluir |

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

## Selecionar exibição do catálogo

>[!IMPORTANT]
>
>No momento, esse recurso está na versão beta.

O seletor **[!UICONTROL Catalog view]** na página Regras de merchandising faz duas coisas:

1. **Filtra a tabela** - Mostra somente as regras (e seus detalhes) que se aplicam à exibição do catálogo selecionado.
1. **Define o escopo das novas regras** - Quando você [cria uma regra](add.md), a exibição de catálogo selecionada é usada como escopo da regra. As opções são *Todas as exibições* ou uma [exibição de catálogo](../../setup/catalog-view.md) específica.

   - **Todas as exibições** - A regra se aplica a todas as exibições de catálogo. O comportamento de pesquisa e classificação é o mesmo em todas as lojas que usam o catálogo.
   - **Exibição de catálogo** - A regra se aplica somente à exibição de catálogo selecionada (por exemplo, uma vitrine, região, revendedor ou marca). Use isso quando diferentes exibições de catálogo precisarem de lógica de merchandising diferente.

Para obter detalhes sobre como criar uma regra e definir seu escopo, consulte [Criar e gerenciar regras](add.md).

### Por que criar uma regra por exibição de catálogo?

Crie regras por exibição de catálogo quando diferentes lojas, regiões ou marcas precisarem de diferentes comportamentos de pesquisa e classificação. Exemplos:

- **Redes de distribuidor ou revendedor** - Cada distribuidor tem sua própria exibição de catálogo; você deseja produtos diferentes fixados, aumentados ou enterrados por distribuidor.
- **Várias regiões** - Exibições de catálogo separadas para a UE, os EUA ou outras regiões com regras de merchandising específicas de região.
- **Várias marcas** - Cada marca tem sua própria exibição de catálogo e você deseja regras específicas da marca (por exemplo, diferentes classificações padrão ou produtos promovidos por marca).

Os dados comportamentais que alimentam a [classificação inteligente](add.md#intelligent-ranking) (como mais vistos, mais comprados, tendências) são calculados por exibição de catálogo por padrão. As regras que usam classificação inteligente, portanto, refletem o comportamento do comprador da visualização de catálogo. Quando sua conta tem um grande número de visualizações de catálogo, o sistema pode agregar dados comportamentais globalmente para manter o desempenho; nesse caso, a classificação pode ser influenciada mais por visualizações de catálogo de alto tráfego, e a relevância para visualizações de tráfego mais baixo pode ser reduzida. Consulte [Limites e limites](../../boundaries-limits.md) para obter os limites atuais.

### Como configurar uma regra por exibição de catálogo

1. No espaço de trabalho *Regras de merchandising*, use a lista suspensa **[!UICONTROL Catalog view]** para selecionar a exibição do catálogo à qual a regra deve se aplicar.
1. Clique em **[!UICONTROL Create rule]**.

   A regra criada tem escopo para a exibição de catálogo selecionada.
1. Crie sua regra no [editor de regras](add.md).

   No editor, defina condições, eventos e detalhes. A regra se aplica somente aos resultados da pesquisa nessa exibição de catálogo.

Não é possível alterar a exibição de catálogo (escopo) de uma regra após sua criação. Para aplicar uma lógica semelhante a outra exibição de catálogo, crie uma nova regra e selecione essa exibição de catálogo antes de criar.
