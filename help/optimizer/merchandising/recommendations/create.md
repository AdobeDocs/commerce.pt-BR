---
title: Criar e gerenciar recomendações
description: Saiba como criar e gerenciar recomendações.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 7cee0a37-4d43-4ee9-889d-9a0ab9684bb8
source-git-commit: 032a19183b79cea1bfe27e8a4e20c60ba5ac6b8b
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Criar e gerenciar recomendações

Ao criar uma recomendação, você cria uma _unidade de recomendação_, ou widget, que contém o produto recomendado _itens_.

![Unidade de recomendação](../../assets/unit.png)
_Unidade de recomendação_

Quando você ativa a unidade de recomendação, o Adobe Commerce começa a [coletar dados](../../manage-results/recommendation-performance.md) para medir impressões, exibições, cliques e assim por diante. A tabela Recomendações exibe as métricas de cada unidade de recomendação para ajudá-lo a tomar decisões de negócios informadas.

1. Na barra lateral _Adobe Commerce Optimizer_, vá para _Merchandising_ > **Recommendations** para exibir o espaço de trabalho _Recommendations_.

1. Clique em **Criar recomendação**.

1. Na seção _Nomeie sua recomendação_, digite um nome descritivo para referência interna, como `Home page most popular`.

1. Na seção _Selecionar tipo de recomendação_, especifique o [tipo de recomendação](types.md) desejado com base em sua estratégia.

1. Na seção _Rótulo de exibição da vitrine_, digite o [rótulo](best-practice.md#recommendation-labels) que está visível para os seus compradores, como &quot;Mais vendidos&quot;.

1. Na seção _Escolher número de produtos_, use o controle deslizante para especificar quantos produtos você deseja exibir na unidade de recomendação.

   O padrão é `5`, com um máximo de `20`.

1. (Opcional) Na seção _Filtros_, [aplique filtros](filters.md) para controlar quais produtos aparecem na unidade de recomendação.

1. Quando terminar, clique em uma das opções a seguir:

   - **Salvar como rascunho** para editar a unidade de recomendação mais tarde. Não é possível modificar o tipo de recomendação para uma unidade de recomendação em um estado de rascunho.

   - **Ative** para habilitar a unidade de recomendação na sua vitrine eletrônica.

1. Quando solicitado, copie a ID da recomendação. Use essa ID para ajudar a identificar qual unidade de recomendação está sendo usada no menu suspenso de recomendações na sua loja do Edge Delivery Services.

>[!NOTE]
>
> É possível criar até 50 unidades de recomendação ativas.

>[!IMPORTANT]
>
>Alguns navegadores podem bloquear scripts críticos que impedem o funcionamento do Recommendations como esperado.

## Gerenciar recomendações existentes

É possível editar, desativar ou excluir uma recomendação existente.

1. Na barra lateral _Adobe Commerce Optimizer_, vá para _Merchandising_ > **Recommendations**.

1. Selecione a recomendação que deseja modificar.

1. Clique no (![Mais seletor](../../assets/btn-more.png)) mais seletor.

1. No menu, você pode **Desativar**, **Excluir** ou **Editar** a recomendação. Se você selecionar **Editar**, poderá ajustar as seguintes configurações, conforme necessário:

   - Nome da recomendação
   - Rótulo da vitrine
   - Número de produtos
   - Filtrar produtos

   Não é possível alterar o tipo de recomendação.

1. Quando terminar, clique em **Salvar alterações**.

## Indicadores de disponibilidade

Os indicadores de disponibilidade mostram quais tipos de recomendação terão melhor desempenho com base no catálogo e nos dados comportamentais disponíveis. Você também pode usar indicadores de disponibilidade para determinar se tem problemas com a [coleção de eventos](../../setup/events/overview.md) ou se não tem tráfego suficiente para preencher o tipo de recomendação.

Os indicadores de prontidão são categorizados como [baseados em estática](#static-based) ou [baseados em dinâmica](#dynamic-based). Baseado em estática usa somente dados de catálogo; enquanto que os dados comportamentais do uso baseado em dinâmica de seus compradores. Esses dados comportamentais são usados para [treinar modelos de aprendizado de máquina](../../setup/events/overview.md) para criar recomendações personalizadas e calcular sua pontuação de preparação.

### Como os indicadores de disponibilidade são calculados

Os indicadores de prontidão são uma indicação do quanto o modelo é treinado. Os indicadores dependem dos tipos de eventos coletados, da amplitude de produtos com os quais o interagiu e do tamanho do catálogo.

A porcentagem do indicador de disponibilidade é derivada de um cálculo que indica quantos produtos podem ser recomendados, dependendo do tipo de recomendação. As estatísticas são aplicadas a produtos com base no tamanho geral do catálogo, no volume de interações (como exibições, cliques, adicionar a carrinhos) e na porcentagem de SKUs que registram esses eventos em uma determinada janela de tempo. Por exemplo, durante o pico do tráfego na temporada de festas, os indicadores de disponibilidade podem mostrar valores mais altos do que nos momentos de volume normal.

Como resultado dessas variáveis, o percentual do indicador de disponibilidade pode flutuar. Isso explica por que você pode ver que os tipos de recomendação entram e saem do estado &quot;Pronto para implantar&quot;.

Os indicadores de prontidão são calculados com base em dois fatores:

- Tamanho suficiente do conjunto de resultados: há resultados suficientes sendo retornados na maioria dos cenários para evitar o uso de [recomendações de backup](../../setup/events/overview.md#backuprecs)?
- Variedade suficiente do conjunto de resultados: os produtos retornados representam uma variedade de produtos do catálogo? O objetivo com esse fator é evitar que uma minoria de produtos seja os únicos itens recomendados no site.

Com base nos fatores acima, um valor de disponibilidade é calculado e exibido da seguinte maneira:

- 75% ou mais significa que as recomendações sugeridas para esse tipo de recomendação serão altamente relevantes.
- Pelo menos 50% significa que as recomendações sugeridas para esse tipo de recomendação serão menos relevantes.
- Menos de 50% significa que as recomendações sugeridas para esse tipo de recomendação podem não ser relevantes. Neste caso, [recomendações de backup](../../setup/events/overview.md#backuprecs) são usadas.

Saiba mais sobre [por que os indicadores de disponibilidade podem estar baixos](#what-to-do-if-the-readiness-indicator-percent-is-low).

### Baseado em estática

Os seguintes tipos de recomendações são baseados em estática porque exigem apenas dados de catálogo. Nenhum dado comportamental é usado.

- _Mais itens similares_

### Baseado em dinâmico

Os tipos de recomendações a seguir são baseados em dinâmica porque usam dados comportamentais de vitrine.

Últimos seis meses de dados comportamentais da loja:

- _Visualizou isto, visualizou aquilo_
- _Visualizou isto, comprou aquilo_
- _Comprei isto, comprei aquilo_
- _Recomendado para você_

Últimos sete dias de dados comportamentais da loja:

- _Mais visualizados_
- _Mais comprados_
- _Mais adicionados ao carrinho_
- _Tendências_
- _Exibir para conversão de compra_
- _Conversão de Visualização em Carrinho_

Dados comportamentais mais recentes do comprador (somente visualizações):

- _Visualizado recentemente_

### Visualizar progresso

Para ajudá-lo a visualizar o progresso do treinamento de cada tipo de recomendação, a seção _Selecionar tipo de Recomendação_ exibe uma medida de prontidão para cada tipo.

![Tipo de recomendação](../../assets/create-recommendation-select-type.png)
_Tipo de recomendação_

>[!NOTE]
>
>Os indicadores podem nunca atingir 100%.

O percentual do indicador de disponibilidade para tipos de recomendação que dependem dos dados do catálogo não muda muito, pois o catálogo do comerciante não muda com frequência. Mas a porcentagem do indicador de disponibilidade para tipos de recomendação com base nos dados comportamentais do comprador pode mudar com frequência, dependendo da atividade diária do comprador.

#### O que fazer se a porcentagem do indicador de disponibilidade estiver baixa

Uma baixa porcentagem de prontidão indica que não há muitos produtos do catálogo elegíveis para serem incluídos nas recomendações para esse tipo de recomendação. Isso significa que há uma alta probabilidade de [recomendações de backup](../../setup/events/overview.md#backuprecs) serem retornadas se você implantar esse tipo de recomendação mesmo assim.

>[!IMPORTANT]
>
>Não há suporte para _Pacotes_, _agrupados_ e tipos de produtos personalizados. Se seu catálogo contiver um grande número desses tipos de produtos, você poderá esperar uma baixa pontuação de preparação. Além disso, qualquer SKU com espaços pode reduzir a relevância da recomendação e deve ser evitada.

A seguir, uma lista de possíveis motivos e soluções para pontuações comuns de baixa disponibilidade:

- **Baseado em estática** - Baixo percentual para esses indicadores pode ser causado pela falta de dados de catálogo para os produtos exibíveis. Se forem menores do que o esperado, uma sincronização completa pode corrigir esse problema.
- **Baseado em dinâmico** - Baixo percentual para indicadores baseados em dinâmico pode ser causado por:

   - Campos ausentes nos [eventos de loja](../../setup/events/overview.md) necessários para os respectivos tipos de recomendação (requestId, contexto do produto e assim por diante).
   - Baixo tráfego na loja, portanto, o volume de eventos comportamentais que recebemos é baixo.
   - A variedade de eventos comportamentais de vitrine em diferentes produtos em sua loja é baixa. Por exemplo, se apenas 10% dos seus produtos forem visualizados ou comprados na maior parte do tempo, os respectivos indicadores de disponibilidade serão baixos.

## Visualizar recomendações

O painel _Visualização de produtos recomendada_ está sempre disponível com uma amostra de seleção de produtos que podem aparecer na unidade de recomendação quando ela for implantada na loja.

![Visualização do Recommendations](../../assets/rec-preview.png)

Para testar uma recomendação ao trabalhar em um ambiente de não produção, você pode buscar dados de recomendação de uma fonte diferente. Isso permite que os comerciantes experimentem com regras e visualizem as recomendações antes de implantar na produção.

| Campo | Descrição |
|---|---|
| Nome | O nome do produto. |
| SKU | A Unidade de Manutenção de Estoque atribuída ao produto |
| Preço | O preço do produto. |
| Tipo de resultado | Principal - indica que há dados de treinamento suficientes coletados para exibir uma recomendação.<br />Backup - indica que não há dados de treinamento suficientes coletados, portanto, uma recomendação de backup é usada para preencher o slot. Acesse [Dados comportamentais](../../setup/events/overview.md) para saber mais sobre modelos de aprendizado de máquina e recomendações de backup. |

À medida que você cria sua unidade de recomendação, experimente o tipo de recomendação e os filtros para obter feedback imediato em tempo real sobre os produtos que serão incluídos. À medida que você começa a entender quais produtos aparecem, é possível configurar a unidade de recomendação para atender às suas necessidades comerciais.

[!DNL Adobe Commerce Optimizer] [filtra](filters.md) recomendações para evitar a exibição de produtos duplicados quando várias unidades de recomendação são implantadas em uma única página. Como resultado, os produtos exibidos no painel de visualização podem ser diferentes daqueles exibidos na loja.
