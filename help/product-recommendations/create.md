---
title: Criar nova recomendação
description: Saiba como criar uma unidade de recomendação de produto.
exl-id: 1d5f83c4-1613-4236-9d98-d455f45a47da
TQID: https://experienceleague.adobe.com/K3cKFg-m22bUzlupyhsHgDVxaJka7xhOvFnOt8wDdII
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 1491
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
   * [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)

   É possível criar até 50 unidades de recomendação ativas para cada tipo de página. O tipo de página fica esmaecido quando o limite é atingido.

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

1. (Opcional) Para controlar quais produtos aparecem na unidade de recomendação, [aplique filtros](filters.md) na seção _Filtros_.

   ![Filtros de recomendação](assets/create-recommendation-filter-products.png)
   _Filtros de produto de recomendação_

1. Quando terminar, clique em uma das opções a seguir:

   * **Salvar como rascunho** para editar a unidade de recomendação mais tarde. Não é possível modificar o tipo de página ou de recomendação de uma unidade de recomendação em um estado de rascunho.

   * **Ative** para habilitar a unidade de recomendação na sua vitrine eletrônica.

>[!IMPORTANT]
>
>Alguns navegadores podem bloquear scripts críticos que impedem que o Product Recommendations funcione como esperado.

## Indicadores de disponibilidade

Os indicadores de disponibilidade mostram quais tipos de recomendação têm melhor desempenho com seus dados comportamentais e de catálogo disponíveis. Use-as para identificar problemas de eventos ou tráfego insuficiente para preencher um tipo de recomendação.

Os indicadores de disponibilidade dividem-se em duas categorias: [baseado em estática](#static-based) e [baseado em dinâmica](#dynamic-based). As recomendações baseadas em estática usam apenas dados de catálogo. As recomendações baseadas em modo dinâmico usam os dados comportamentais dos compradores para treinar modelos de aprendizado de máquina, gerar recomendações personalizadas e calcular a pontuação de disponibilidade de cada recomendação.

### Como os indicadores de disponibilidade são calculados

Os indicadores de prontidão são uma indicação do quanto o modelo é treinado. Os indicadores dependem dos tipos de eventos coletados, da amplitude de produtos com os quais o interagiu e do tamanho do catálogo.

O percentual do indicador de prontidão estima a proporção de produtos que podem ser recomendados para um determinado tipo de recomendação. É calculada usando o tamanho do catálogo, o volume de interação e a porcentagem de SKUs que registram os eventos relevantes em uma janela de tempo definida. Por exemplo, os indicadores de prontidão podem ser mais altos durante picos de tráfego de feriados do que durante períodos de tráfego normal.

Como resultado dessas variáveis, o percentual do indicador de disponibilidade pode flutuar. Isso explica por que os tipos de recomendação flutuam entre estar &quot;pronto para implantar&quot;.

Os indicadores de prontidão são calculados com base em dois fatores:

* Tamanho suficiente do conjunto de resultados: há resultados suficientes sendo retornados na maioria dos cenários para evitar o uso de [recomendações de backup](events.md#backuprecs)?

* Os produtos devolvidos representam uma variedade de produtos do seu catálogo? Esse fator ajuda a garantir que as recomendações no site não sejam limitadas a um pequeno subconjunto de produtos.

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

A porcentagem de preparação para tipos de recomendação baseados em catálogo geralmente muda pouco, pois os catálogos são relativamente estáveis. Por outro lado, o percentual de prontidão para tipos de recomendação com base nos dados comportamentais do comprador pode mudar com frequência com a atividade diária do comprador.

#### O que fazer se a porcentagem do indicador de disponibilidade estiver baixa

Uma baixa porcentagem de prontidão indica que não há muitos produtos do catálogo elegíveis para serem incluídos nas recomendações para esse tipo de recomendação. Isso significa que há uma alta probabilidade de [recomendações de backup](events.md#backup-recommendations) serem retornadas se você implantar esse tipo de recomendação mesmo assim.

>[!IMPORTANT]
>
>Não há suporte para _Pacotes_, _agrupados_ e tipos de produtos personalizados. Se seu catálogo contiver um grande número desses tipos de produtos, você poderá esperar uma baixa pontuação de preparação. Além disso, qualquer SKU com espaços pode reduzir a relevância da recomendação e deve ser evitada.

A seguir, uma lista de possíveis motivos e soluções para pontuações comuns de baixa disponibilidade:

* **Baseado em estática** - A ausência de dados de catálogo para os produtos exibíveis causa porcentagens baixas para esses indicadores. Se forem menores do que o esperado, uma sincronização completa pode corrigir esse problema.
* **Baseado em dinâmico** - Os seguintes fatores causam porcentagens baixas para indicadores baseados em dinâmico:

  * Campos ausentes nos [eventos de loja](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations) necessários para os respectivos tipos de recomendação (requestId, contexto do produto e assim por diante).
  * Baixo tráfego na loja, portanto, o volume de eventos comportamentais que recebemos é baixo.
  * A variedade de eventos comportamentais de vitrine em diferentes produtos em sua loja é baixa. Por exemplo, se apenas 10% dos seus produtos forem visualizados ou comprados na maior parte do tempo, os respectivos indicadores de disponibilidade serão baixos.

## Visualizar recomendações {#preview}

O painel _Visualização de produtos recomendada_ está sempre disponível com uma amostra de seleção de produtos que aparecem na unidade de recomendação quando ela é implantada na loja.

Para testar uma recomendação ao trabalhar em um ambiente de não produção, você pode buscar dados de recomendação de uma [fonte diferente](settings.md). Isso permite que os comerciantes experimentem com regras e visualizem as recomendações antes de implantar na produção.

| Campo | Descrição |
|---|---|
| Nome | O nome do produto. |
| SKU | A Unidade de Manutenção de Estoque atribuída ao produto |
| Preço | O preço do produto. |
| Tipo de resultado | Principal - indica que há dados de treinamento suficientes coletados para exibir uma recomendação.<br />Backup - indica que não há dados de treinamento suficientes coletados, portanto, uma recomendação de backup é usada para preencher o slot. Acesse [Dados comportamentais](events.md) para saber mais sobre modelos de aprendizado de máquina e recomendações de backup. |

Para ver quais produtos uma unidade de recomendação inclui em tempo real, experimente o tipo de página, o tipo de recomendação e os filtros à medida que você os cria. Em seguida, configure a unidade para atender às suas necessidades comerciais com base nos produtos devolvidos.

Quando várias unidades de recomendação são implantadas na mesma página, o Adobe Commerce usa [filtros](#filters.md) para remover produtos duplicados das recomendações exibidas. Como resultado, o painel de visualização pode mostrar um conjunto de produtos diferente da loja.

>[!NOTE]
>
> Você não pode visualizar o tipo de recomendação `Recently viewed` porque os dados não estão disponíveis no Administrador.
