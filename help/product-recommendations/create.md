---
title: Criar nova recomendação
description: Saiba como criar uma unidade de recomendação de produto.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# Criar nova recomendação

Ao criar uma recomendação, você cria uma _unidade de recomendação_, ou widget, que contém o produto recomendado _itens_.

![Unidade de recomendação](assets/unit.png)
_Unidade de recomendação_

Quando você ativa a unidade de recomendação, o Adobe Commerce começa a [coletar dados](workspace.md) para medir impressões, exibições, cliques e assim por diante. A tabela [!DNL Product Recommendations] exibe as métricas de cada unidade de recomendação para ajudá-lo a tomar decisões de negócios conscientes.

>[!NOTE]
>
>As métricas de Recomendação de produto são otimizadas para vitrines da Luma. Se sua loja não for baseada em Luma, a forma como as métricas rastreiam os dados dependerá de como você [implementa a coleção de eventos](events.md).

1. Na barra lateral _Administrador_, vá para **Marketing** > _Promoções_ > **Recomendações de Produtos** para exibir o espaço de trabalho _Recomendações de Produtos_.

1. Especifique o [Modo de Exibição de Armazenamento](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/websites-stores-views) onde deseja que as recomendações sejam exibidas.

   >[!NOTE]
   >
   > As unidades de recomendação do Page Builder devem ser criadas na exibição de armazenamento padrão, mas podem ser usadas em qualquer lugar. Para saber mais sobre como criar recomendações de produto com o Page Builder, consulte [Adicionar conteúdo - Recomendações de produto](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations).

1. Clique em **Criar recomendação**.

1. Na seção _Nomeie sua recomendação_, digite um nome descritivo para referência interna, como `Home page most popular`.

1. Na seção _Selecionar tipo de página_, selecione a página na qual deseja que a recomendação seja exibida a partir das seguintes opções:

   >[!NOTE]
   >
   > As Recomendações de Produto não são suportadas na página Carrinho quando sua loja está configurada para [exibir a página do carrinho de compras imediatamente após adicionar um produto ao carrinho](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration).

   * Página inicial
   * Categoria
   * Detalhes do produto
   * Carrinho
   * Confirmação
   * [Construtor de páginas](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)

   Você pode criar até cinco unidades de recomendação ativas para cada tipo de página e até 25 para o Page Builder. O tipo de página fica esmaecido quando o limite é atingido.

   ![Nome e página de recomendação](assets/create-recommendation.png)
   _Nome de recomendação e posicionamento da página_

1. Na seção _Selecionar tipo de recomendação_, especifique o [tipo de recomendação](type.md) que você deseja exibir na página selecionada. Para algumas páginas, o [posicionamento](placement.md) das recomendações está limitado a certos tipos.

1. Na seção _Rótulo de exibição da vitrine_, digite o [rótulo](placement.md#recommendation-labels) que está visível para os seus compradores, como &quot;Mais vendidos&quot;.

1. Na seção _Escolher número de produtos_, use o controle deslizante para especificar quantos produtos você deseja exibir na unidade de recomendação.

   O padrão é `5`, com um máximo de `20`.

1. Na seção _Selecionar posicionamento_, especifique o local em que a unidade de recomendação deve aparecer na página.

   * Na parte inferior do conteúdo principal
   * Na parte superior do conteúdo principal

1. (Opcional) Para alterar a ordem das recomendações, selecione e mova as linhas na tabela _Escolher posição_.

   A seção _Escolher posição_ exibe todas as recomendações (se houver) criadas para o tipo de página selecionado.

   ![Ordem de recomendação](assets/create-recommendation-select-placement.png)
   _Ordem de recomendação na página_

1. (Opcional) Na seção _Filtros_, [aplique filtros](filters.md) para controlar quais produtos aparecem na unidade de recomendação.

   ![Filtros de recomendação](assets/create-recommendation-filter-products.png)
   _Filtros de produto de recomendação_

1. Quando terminar, clique em uma das opções a seguir:

   * **Salvar como rascunho** para editar a unidade de recomendação mais tarde. Não é possível modificar o tipo de página ou de recomendação de uma unidade de recomendação em um estado de rascunho.

   * **Ative** para habilitar a unidade de recomendação na sua vitrine eletrônica.

## Indicadores de disponibilidade

Os indicadores de disponibilidade mostram quais tipos de recomendação terão melhor desempenho com base no catálogo e nos dados comportamentais disponíveis. Você também pode usar indicadores de prontidão para determinar se tem problemas com seu [evento](events.md) ou se não tem tráfego suficiente para preencher o tipo de recomendação.

Os indicadores de prontidão são categorizados como [baseados em estática](#static-based) ou [baseados em dinâmica](#dynamic-based). Baseado em estática usa somente dados de catálogo; enquanto que os dados comportamentais do uso baseado em dinâmica de seus compradores. Esses dados comportamentais são usados para [treinar modelos de aprendizado de máquina](events.md) para criar recomendações personalizadas e calcular sua pontuação de preparação.

### Como os indicadores de disponibilidade são calculados

Os indicadores de prontidão são uma indicação do quanto o modelo é treinado. Os indicadores dependem dos tipos de eventos coletados, da amplitude de produtos com os quais o interagiu e do tamanho do catálogo.

A porcentagem do indicador de disponibilidade é derivada de um cálculo que indica quantos produtos podem ser recomendados, dependendo do tipo de recomendação. As estatísticas são aplicadas a produtos com base no tamanho geral do catálogo, no volume de interações (como exibições, cliques, adicionar a carrinhos) e na porcentagem de SKUs que registram esses eventos em uma determinada janela de tempo. Por exemplo, durante o pico do tráfego na temporada de festas, os indicadores de disponibilidade podem mostrar valores mais altos do que nos momentos de volume normal.

Como resultado dessas variáveis, o percentual do indicador de disponibilidade pode flutuar. Isso explica por que você pode ver que os tipos de recomendação entram e saem do estado &quot;Pronto para implantar&quot;.

Os indicadores de prontidão são calculados com base em dois fatores:

* Tamanho suficiente do conjunto de resultados: há resultados suficientes sendo retornados na maioria dos cenários para evitar o uso de [recomendações de backup](events.md#backuprecs)?

* Variedade suficiente do conjunto de resultados: os produtos retornados representam uma variedade de produtos do catálogo? O objetivo com esse fator é evitar que uma minoria de produtos seja os únicos itens recomendados no site.

Com base nos fatores acima, um valor de disponibilidade é calculado e exibido da seguinte maneira:

* 75% ou mais significa que as recomendações sugeridas para esse tipo de recomendação serão altamente relevantes.
* Pelo menos 50% significa que as recomendações sugeridas para esse tipo de recomendação serão menos relevantes.
* Menos de 50% significa que as recomendações sugeridas para esse tipo de recomendação podem não ser relevantes. Neste caso, [recomendações de backup](events.md#backuprecs) são usadas.

Saiba mais sobre [por que os indicadores de disponibilidade podem estar baixos](#what-to-do-if-the-readiness-indicator-percent-is-low).

### Baseado em estática

Os seguintes tipos de recomendações são baseados em estática porque exigem apenas dados de catálogo. Nenhum dado comportamental é usado.

* _Mais itens similares_
* _Similaridade visual_

### Baseado em dinâmico

Os tipos de recomendações a seguir são baseados em dinâmica porque usam dados comportamentais de vitrine.

Últimos seis meses de dados comportamentais da loja:

* _Visualizou isto, visualizou aquilo_
* _Visualizou isto, comprou aquilo_
* _Comprei isto, comprei aquilo_
* _Recomendado para você_

Últimos sete dias de dados comportamentais da loja:

* _Mais visualizados_
* _Mais comprados_
* _Mais adicionados ao carrinho_
* _Tendências_
* _Exibir para conversão de compra_
* _Conversão de Visualização em Carrinho_

Dados comportamentais mais recentes do comprador (somente visualizações):

* _Visualizado recentemente_

### Visualizar progresso

Para ajudá-lo a visualizar o progresso do treinamento de cada tipo de recomendação, a seção _Selecionar tipo de Recomendação_ exibe uma medida de prontidão para cada tipo.

![Tipo de recomendação](assets/create-recommendation-select-type.png)
_Tipo de recomendação_

>[!NOTE]
>
>Os indicadores podem nunca atingir 100%.

O percentual do indicador de disponibilidade para tipos de recomendação que dependem dos dados do catálogo não muda muito, pois o catálogo do comerciante não muda com frequência. Mas a porcentagem do indicador de disponibilidade para tipos de recomendação com base nos dados comportamentais do comprador pode mudar com frequência, dependendo da atividade diária do comprador.

#### O que fazer se a porcentagem do indicador de disponibilidade estiver baixa

Uma baixa porcentagem de prontidão indica que não há muitos produtos do catálogo elegíveis para serem incluídos nas recomendações para esse tipo de recomendação. Isso significa que há uma alta probabilidade de [recomendações de backup](events.md#backuprecs) serem retornadas se você implantar esse tipo de recomendação mesmo assim.

>[!IMPORTANT]
>
>Não há suporte para _Pacotes_, _agrupados_ e tipos de produtos personalizados. Se seu catálogo contiver um grande número desses tipos de produtos, você poderá esperar uma baixa pontuação de preparação. Além disso, qualquer SKU com espaços pode reduzir a relevância da recomendação e deve ser evitada.

A seguir, uma lista de possíveis motivos e soluções para pontuações comuns de baixa disponibilidade:

* **Baseado em estática** - Baixo percentual para esses indicadores pode ser causado pela falta de dados de catálogo para os produtos exibíveis. Se forem menores do que o esperado, uma sincronização completa pode corrigir esse problema.
* **Baseado em dinâmico** - Baixo percentual para indicadores baseados em dinâmico pode ser causado por:

   * Campos ausentes nos [eventos de loja](events.md) necessários para os respectivos tipos de recomendação (requestId, contexto do produto e assim por diante).
   * Baixo tráfego na loja, portanto, o volume de eventos comportamentais que recebemos é baixo.
   * A variedade de eventos comportamentais de vitrine em diferentes produtos em sua loja é baixa. Por exemplo, se apenas 10% dos seus produtos forem visualizados ou comprados na maior parte do tempo, os respectivos indicadores de disponibilidade serão baixos.

## Visualizar recomendações {#preview}

O painel _Visualização de produtos recomendada_ está sempre disponível com uma amostra de seleção de produtos que podem aparecer na unidade de recomendação quando ela for implantada na loja.

Para testar uma recomendação ao trabalhar em um ambiente de não produção, você pode buscar dados de recomendação de uma [fonte diferente](settings.md). Isso permite que os comerciantes experimentem com regras e visualizem as recomendações antes de implantar na produção.

| Campo | Descrição |
|---|---|
| Nome | O nome do produto. |
| SKU | A Unidade de Manutenção de Estoque atribuída ao produto |
| Preço | O preço do produto. |
| Tipo de resultado | Principal - indica que há dados de treinamento suficientes coletados para exibir uma recomendação.<br />Backup - indica que não há dados de treinamento suficientes coletados, portanto, uma recomendação de backup é usada para preencher o slot. Acesse [Dados comportamentais](events.md) para saber mais sobre modelos de aprendizado de máquina e recomendações de backup. |

À medida que você cria sua unidade de recomendação, experimente o tipo de página, o tipo de recomendação e os filtros para obter feedback imediato em tempo real sobre os produtos que serão incluídos. À medida que você começa a entender quais produtos aparecem, é possível configurar a unidade de recomendação para atender às suas necessidades comerciais.

Recomendações de [filtros](filters.md) do Adobe Commerce para evitar a exibição de produtos duplicados quando várias unidades de recomendação são implantadas em uma única página. Como resultado, os produtos exibidos no painel de visualização podem ser diferentes daqueles exibidos na loja.

>[!NOTE]
>
> Você não pode visualizar o tipo de recomendação `Recently viewed` porque os dados não estão disponíveis no Administrador.
