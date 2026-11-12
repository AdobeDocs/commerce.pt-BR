---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 0%
---
Ao criar uma recomendação, você cria uma _unidade de recomendação_, ou widget, que contém o produto recomendado _itens_.

![Unidade de recomendação](/help/assets/ccdm-shared/recommendations/unit.png)
_Unidade de recomendação_

Quando você ativa a unidade de recomendação, o Adobe Commerce começa a [coletar dados](/help/optimizer/manage-results/recommendation-performance.md) para medir impressões, exibições, cliques e assim por diante. A tabela Recomendações exibe as métricas de cada unidade de recomendação para ajudá-lo a tomar decisões de negócios informadas.

1. No menu, vá para _Merchandising_ > **Recommendations** para exibir o espaço de trabalho _Recommendations_.

1. No campo **Exibição de catálogo**, selecione a exibição de catálogo na qual deseja que a recomendação fique disponível. Saiba mais sobre [como usar exibições de catálogo para recomendações](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view).

1. Clique em **Criar recomendação**.

   A recomendação criada está disponível na exibição de catálogo selecionada anteriormente.

1. Na seção _Nomeie sua recomendação_, digite um nome descritivo para referência interna, como `Home page most popular`.

1. Na seção **Referência da loja**, insira uma chave de referência para identificar esta unidade de recomendação na configuração da loja. Depois de criar a recomendação, você pode [copiar seu valor](#get-the-storefront-reference-key) dos **detalhes da Unidade de Recomendação** e usá-lo como `referenceKey` no bloco de recomendações. A chave de referência é para a configuração da loja; o rótulo de exibição da loja é o texto que os compradores veem.

1. Na seção _Selecionar tipo de recomendação_, especifique o [tipo de recomendação](types.md) desejado com base em sua estratégia.

1. Na seção _Rótulo de exibição da vitrine_, digite o [rótulo](best-practice.md#recommendation-labels) que está visível para os seus compradores, como &quot;Mais vendidos&quot;.

1. Na seção _Escolher número de produtos_, use o controle deslizante para especificar quantos produtos você deseja exibir na unidade de recomendação.

   O padrão é `5`, com um máximo de `20`.

1. (Opcional) Na seção _Filtros_, [aplique filtros](filters.md) para controlar quais produtos aparecem na unidade de recomendação.

1. Use o painel _Visualização de produtos recomendada_ para entender melhor como os filtros afetam quais produtos são exibidos na unidade de recomendação. Saiba como [visualizar recomendações](#preview-recommendations).

1. Quando terminar, clique em uma das opções a seguir:

   - **Salvar como rascunho** para editar a unidade de recomendação mais tarde. Não é possível modificar o tipo de recomendação para uma unidade de recomendação em um estado de rascunho.

   - **Ative** para habilitar a unidade de recomendação na sua vitrine eletrônica.

   Sua recomendação aparece no espaço de trabalho do Recommendations. Para usar sua recomendação na loja, você precisa da [ID da recomendação ou chave de referência](#get-the-storefront-reference-key).

>[!NOTE]
>
>É possível criar até 50 unidades de recomendação ativas. Consulte [Limites e limites](/help/optimizer/boundaries-limits.md) para obter detalhes.

>[!IMPORTANT]
>
>Alguns navegadores podem bloquear scripts críticos que impedem o funcionamento do Recommendations como esperado.

## Visualizar recomendações

O painel _Visualização de produtos recomendada_ está sempre disponível com uma amostra de seleção de produtos que podem aparecer na unidade de recomendação quando ela for implantada na loja.

![Visualização do Recommendations](/help/assets/ccdm-shared/recommendations/rec-preview.png)

Para testar uma recomendação ao trabalhar em um ambiente de não produção, você pode buscar dados de recomendação de uma fonte diferente. Isso permite que os comerciantes experimentem com regras e visualizem as recomendações antes de implantar na produção.

| Campo | Descrição |
|---|---|
| Exibição de catálogo |  |
| Nome | O nome do produto. |
| SKU | A Unidade de Manutenção de Estoque atribuída ao produto |
| Preço | O preço do produto. |
| Tipo de resultado | Principal - Indica que há dados de treinamento suficientes coletados para exibir uma recomendação.<br />Backup - Indica que não há dados de treinamento suficientes coletados, portanto, uma recomendação de backup é usada para preencher o slot. Acesse [Dados comportamentais](/help/optimizer/setup/events/overview.md) para saber mais sobre modelos de aprendizado de máquina e recomendações de backup. |

Para obter feedback imediato em tempo real sobre os produtos que serão incluídos, experimente o tipo de recomendação e os filtros enquanto cria sua unidade de recomendação. Para atender às suas necessidades de negócios, configure a unidade de recomendação à medida que você começa a entender quais produtos aparecem.

[!DNL Product Recommendations] [filtrar](filters.md) recomendações para evitar a exibição de produtos duplicados quando várias unidades de recomendação forem implantadas em uma única página. Como resultado, os produtos exibidos no painel de visualização podem ser diferentes daqueles exibidos na loja.

Para configurações de várias lojas, vários idiomas ou várias marcas, você pode configurar se cada recomendação se aplica a todas as exibições de catálogo (global) ou a uma única [exibição de catálogo](/help/optimizer/setup/catalog-view.md). Saiba mais sobre como [definir a exibição do catálogo](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view) ao trabalhar com recomendações.

## Obter a chave de referência da loja

Depois de criar uma recomendação, use sua chave de referência para configurar a unidade de recomendação na loja.

1. Na página **Recommendations**, clique no ícone de informações (![ícone de informações](/help/assets/ccdm-shared/recommendations/info-icon.png)) ao lado do nome da recomendação para abrir a página **Detalhes da Unidade de Recomendação**.

   ![Obter ID da Recomendação](/help/assets/ccdm-shared/recommendations/get-ref-id.png)

1. Copie o valor da seção **Chave de referência da loja**.

1. No bloco `product-recommendations` da vitrine eletrônica, use esta chave de referência para configurar o [menu suspenso de recomendações](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/blocks/product-recommendations/) na sua vitrine do Edge Delivery Services.

## Gerenciar recomendações existentes

É possível editar, desativar ou excluir uma recomendação existente.

1. No menu, vá para _Merchandising_ > **Recommendations**.

1. Selecione a recomendação que deseja modificar.

1. Clique no (![Mais seletor](/help/assets/ccdm-shared/recommendations/btn-more.png)) mais seletor.

1. No menu, você pode **Desativar**, **Excluir** ou **Editar** a recomendação. Se você selecionar **Editar**, poderá ajustar as seguintes configurações, conforme necessário:

   - Nome da recomendação
   - Chave de referência
   - Rótulo da vitrine
   - Número de produtos
   - Filtrar produtos

   Não é possível alterar o tipo de recomendação ou a exibição do catálogo. A exibição de catálogo é definida quando você cria a recomendação. Para saber mais, consulte [selecionar exibição de catálogo](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view).

1. Quando terminar, clique em **Salvar alterações**.

## Indicadores de disponibilidade

Os indicadores de disponibilidade mostram quais tipos de recomendação têm melhor desempenho com base no catálogo e nos dados comportamentais disponíveis. Eles também podem ajudar a identificar possíveis problemas com a [coleção de eventos](/help/optimizer/setup/events/overview.md) ou determinar se um tipo de recomendação não está recebendo tráfego suficiente para gerar resultados.

Os indicadores de prontidão são categorizados como [baseados em estática](#static-based) ou [baseados em dinâmica](#dynamic-based). As recomendações baseadas em estática usam apenas dados de catálogo; enquanto as recomendações baseadas em dinâmica usam dados comportamentais de seus compradores. Esses dados comportamentais são usados para [treinar modelos de aprendizado de máquina](/help/optimizer/setup/events/overview.md) para criar recomendações personalizadas e calcular sua pontuação de preparação.

### Como os indicadores de disponibilidade são calculados

Os indicadores de prontidão são uma indicação do quanto o modelo é treinado. Os indicadores dependem dos tipos de eventos coletados, da amplitude de produtos com os quais o interagiu e do tamanho do catálogo.

A porcentagem do indicador de disponibilidade é derivada de um cálculo que indica quantos produtos podem ser recomendados, dependendo do tipo de recomendação. As estatísticas são aplicadas a produtos com base no tamanho geral do catálogo, no volume de interação (exibições, cliques, adicionar a carrinhos) e na porcentagem de SKUs que registram esses eventos em uma determinada janela de tempo. Por exemplo, durante o pico do tráfego na temporada de festas, os indicadores de disponibilidade podem mostrar valores mais altos do que nos momentos de volume normal.

Como resultado dessas variáveis, o percentual do indicador de disponibilidade pode flutuar. Essa flutuação explica por que os tipos de recomendação mudam entre estar &quot;pronto para implantar&quot; e não.

Os indicadores de prontidão são calculados com base em vários fatores:

- Tamanho suficiente do conjunto de resultados: há resultados suficientes sendo retornados na maioria dos cenários para evitar o uso de [recomendações de backup](/help/optimizer/setup/events/overview.md#backup-recommendations)?
- Variedade suficiente do conjunto de resultados: os produtos retornados representam uma variedade de produtos do catálogo? O objetivo com esse fator é evitar ter uma minoria de produtos como os únicos itens recomendados no site.

Com base nos fatores acima, um valor de disponibilidade é calculado e exibido da seguinte maneira:

- 75% ou mais significa que as recomendações sugeridas para esse tipo de recomendação são altamente relevantes.
- Pelo menos 50% significa que as recomendações sugeridas para esse tipo de recomendação são menos relevantes.
- Menos de 50% significa que as recomendações sugeridas para esse tipo de recomendação podem não ser relevantes. Neste caso, [recomendações de backup](/help/optimizer/setup/events/overview.md#backup-recommendations) são usadas.

Saiba mais sobre [por que os indicadores de disponibilidade podem estar baixos](#what-to-do-if-the-readiness-indicator-is-low).

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

![Tipo de recomendação](/help/assets/ccdm-shared/recommendations/create-recommendation-select-type.png)
_Tipo de recomendação_

>[!NOTE]
>
>Os indicadores podem nunca atingir 100%.

O indicador de prontidão para tipos de recomendação que dependem dos dados do catálogo não muda muito, pois o catálogo do comerciante raramente muda. Mas o indicador de disponibilidade para tipos de recomendação com base nos dados comportamentais do comprador pode mudar com frequência, dependendo da atividade diária do comprador.

#### O que fazer se o indicador de disponibilidade estiver baixo

Uma baixa porcentagem de prontidão indica que não há muitos produtos do catálogo elegíveis para serem incluídos nas recomendações para esse tipo de recomendação. Isso significa que há uma alta probabilidade de [recomendações de backup](/help/optimizer/setup/events/overview.md#backup-recommendations) serem retornadas se você implantar esse tipo de recomendação mesmo assim.

>[!IMPORTANT]
>
>Quaisquer SKUs com espaços podem reduzir a relevância da recomendação e devem ser evitadas.

A seguir, uma lista de possíveis motivos e soluções para pontuações comuns de baixa disponibilidade:

- **Baseado em estática**—A ausência de dados de catálogo para os produtos exibíveis causa porcentagens baixas para esses indicadores. Se forem menores do que o esperado, uma sincronização completa pode corrigir esse problema.
- **Baseado em dinâmico**—Os seguintes fatores causam porcentagens baixas para os indicadores baseados em dinâmico:

  - Campos ausentes nos [eventos de loja](/help/optimizer/setup/events/overview.md) necessários para os respectivos tipos de recomendação (requestId, contexto do produto, etc.).
  - Tráfego baixo para o armazenamento; portanto, o volume de eventos comportamentais recebidos é baixo.
  - A variedade de eventos comportamentais de vitrine em diferentes produtos em sua loja é baixa. Por exemplo, se apenas 10% dos seus produtos forem visualizados ou comprados na maior parte do tempo, os respectivos indicadores de disponibilidade serão baixos.
