---
title: Filtros de recomendação
description: Saiba como usar filtros para controlar quais produtos aparecem nas  [!DNL Adobe Commerce Optimizer] recomendações.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
TQID: https://experienceleague.adobe.com/-pmVrAgEsSkn66K00-eaoQ4TF-7Xyxuwlniip1cR4HM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 116d8bd804df364ddc9cb1175525f08fd32c01bf
workflow-type: tm+mt
source-wordcount: 1919
ht-degree: 0%

---

# Filtrar produtos

[!DNL Adobe Commerce Optimizer] aplica automaticamente filtros padrão não configuráveis a unidades de recomendação. Se você tiver várias unidades de recomendação implantadas em uma página, o [!DNL Adobe Commerce Optimizer] filtra todos os produtos que são repetidos nas unidades. Somente a primeira referência a um produto repetido é usada para abrir espaço para outros produtos a serem recomendados. O [!DNL Adobe Commerce Optimizer] também filtra todos os produtos comprados anteriormente e aqueles que estão no carrinho.

Quando você [cria](create.md) uma unidade de recomendação, pode definir filtros que controlam quais produtos podem ser exibidos nas recomendações. Esses filtros se baseiam em um conjunto de condições de inclusão ou exclusão definidas por você. Somente os produtos que correspondem a todas as condições de inclusão aparecem nas recomendações. Os produtos que correspondem a qualquer uma das condições de exclusão não são recomendados.

Você pode configurar vários filtros e ativar apenas aqueles que desejar selecionando a alternância em cada página de filtro. Isso permite criar rascunhos de filtros para uso futuro. O número de filtros ativados é exibido em cada guia.

## Condições

As condições podem ser estáticas ou dinâmicas.

- Uma condição estática usa atributos de produto existentes para determinar quais produtos podem aparecer na unidade. Por exemplo, você pode especificar que apenas os produtos em estoque com um preço superior a US$ 25 apareçam na unidade.

- Uma condição dinâmica é destacada do contexto atual de um comprador, como a categoria ou o produto visualizado no momento. Por exemplo, ao criar uma recomendação de produto para ser implantada nas páginas de detalhes do produto, você pode usar um [filtro de preço dinâmico](#dynamic-price-filters-relative-to-current-product) para incluir ou excluir produtos dentro de um intervalo de preço relativo do produto visualizado no momento.

### Operadores lógicos

Os operadores lógicos `AND` e `OR` são usados para unir várias condições. Se estiver usando filtros de inclusão e exclusão em todos os tipos de filtros, as inclusões serão avaliadas primeiro para determinar todos os produtos possíveis que podem ser recomendados, e os produtos que correspondem a quaisquer filtros de exclusão serão removidos da lista. Os filtros **Preço** usam uma ordem diferente entre as regras de preço: exclusões primeiro e, em seguida, inclusões. Consulte [Como incluir e excluir regras usam o preço](#how-include-and-exclude-rules-use-price).

- `AND` - Associa duas condições de filtragem de inclusão
- `OR` - Adiciona duas condições de filtragem por exclusão

## Tipos de filtros

Cada tipo de filtro é direcionado a um aspecto diferente do catálogo, como produto e preço, para que você possa restringir ou ampliar quais produtos estão qualificados para uma unidade. Escolha os tipos que correspondem às suas metas de merchandising e combine as condições de inclusão e exclusão conforme necessário; as subseções abaixo descrevem como cada tipo se comporta e como [!DNL Adobe Commerce Optimizer] o aplica.

>[!NOTE]
>
>Somente produtos que correspondam aos seus filtros de **inclusão** podem ser recomendados, e qualquer produto que corresponda a um filtro de **exclusão** será removido.

### Preço {#price}

>[!IMPORTANT]
>
>A filtragem de preço está em beta.

A filtragem de preços usa o **preço calculado final** de cada produto do **catálogo de preços ativo** da loja, que é o catálogo de preços atribuído à loja onde a unidade de recomendação é renderizada.

Esse valor:

- **Inclui** descontos, promoções e preços especiais definidos nesse catálogo de preços (não apenas o preço de lista).
- **Exclui** ajustes no nível de remessa e carrinho.
- **Aplica-se somente** ao catálogo de preços ativo para essa vitrine; outras vitrines ou catálogos de preços não são usados.

Configure como os catálogos de preços são mapeados para uma loja em seu catálogo e a configuração [catálogos de preços](../../setup/pricebooks.md).

#### Como incluir e excluir regras usam preço {#how-include-and-exclude-rules-use-price}

- **Regras de exclusão** - Os produtos cujo preço final **corresponde a qualquer** exclusão de preço definida são removidos primeiro.
- **Regras de inclusão** - Entre os candidatos restantes, somente os produtos cujo preço final **corresponda a todos** as condições de inclusão de preço definidas permanecem qualificados. Isso inclui todos os filtros de inclusão ativados (por exemplo, sua regra de preço mais quaisquer outras regras de inclusão).

As regras de preço **filtram** o conjunto de candidatos a recomendação; eles **não** reclassificam os produtos. O mecanismo produz uma lista classificada, as regras de inclusão e exclusão de preço removem os produtos dessa lista e a ordem relativa dos produtos restantes permanece a mesma. Se menos produtos forem qualificados do que as solicitações de unidade, somente os itens válidos serão mostrados. Se nenhuma for qualificada, a unidade não será renderizada (nenhum espaço reservado vazio).

O preço mostrado nos produtos dentro da unidade de recomendação é o mesmo **preço final** da tabela de preços dessa loja, portanto, o que os compradores veem corresponde ao valor usado para filtragem. Na visualização de Administrador, os produtos configuráveis podem mostrar um intervalo de preço quando os preços da variante forem diferentes; consulte [Produtos configuráveis na visualização](#configurable-products-in-preview).

#### Faixa de preços estática

Use um filtro de preço **estático** quando quiser um mínimo ou máximo fixo na moeda base da sua loja, independentemente do produto que um comprador está visualizando.

##### Configurar um filtro de preço estático

1. Ao [criar ou editar](create.md) uma unidade de recomendação, abra **[!UICONTROL Filter products]** (ou vá para a etapa _Filtros_ do fluxo de trabalho da unidade).
1. Selecione a guia **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]**, dependendo se você deseja permitir somente produtos em um intervalo de preços ou bloquear produtos em um intervalo. O selo em cada guia mostra quantos filtros desse tipo estão habilitados.
1. Na lista à esquerda, selecione **[!UICONTROL Price]**.
1. Ligue o **[!UICONTROL Enable filter]**.

   Os valores de preço usam a **moeda base do site**, conforme observado na página.

1. Abra **[!UICONTROL Include products based on]** (na guia **[!UICONTROL Inclusions]**) ou o controle equivalente na guia **[!UICONTROL Exclusions]** e escolha **[!UICONTROL Set price range]**.
1. Defina um **[!UICONTROL Min price]** e/ou **[!UICONTROL Max price]** opcional usando os campos ao lado do símbolo da moeda. Você pode digitar valores ou usar os controles **-** e **+** para ajustar valores. Deixe um limite vazio se não precisar de um mínimo ou máximo. O intervalo é comparado ao preço calculado final de cada produto para o catálogo de preços ativo da loja.
1. Termine de configurar a unidade de recomendação e salve ou publique como você faria normalmente para que o filtro entrasse em vigor.

![Filtro de Preços](../../assets/filter-price.png)

#### Filtros de preço dinâmicos (em relação ao produto atual) {#dynamic-price-filters-relative-to-current-product}

Use um filtro de preço **dinâmico** quando as recomendações tiverem que ser limitadas em relação ao **produto exibido no momento** em uma PDP (página de detalhes do produto). O filtro usa o preço final desse produto como uma **âncora** e compara os produtos recomendados com os limites que você define.

Os operadores dinâmicos estão disponíveis somente para [tipos de recomendação relacionados ao SKU](types.md) executados em um contexto de produto, como:

- Visualizou isto, visualizou aquilo
- Visualizou isto, comprou aquilo
- Comprei isto, comprei aquilo
- Veja mais aqui
- Semelhança visual

Eles **não** estão disponíveis para tipos com base em popularidade (por exemplo, **Mais visualizados** ou **Mais comprados**) porque essas unidades não têm um único produto atual para ancorar o filtro.

Na loja, o menu suspenso de recomendações lê o preço do produto atual no contexto PDP e o envia com a solicitação de recomendação. [!DNL Adobe Commerce Optimizer] usa esse valor como âncora ao avaliar as regras de preço dinâmicas. Para produtos configuráveis, a âncora é a **variante mais baixa** preço final (`priceRange.minimum`).

##### Operadores

Em **[!UICONTROL Include products based on]** (ou no equivalente de exclusões), você pode escolher:

| Operador | Finalidade |
| --- | --- |
| **Menor que ou igual ao preço atual do produto** | Incluir ou excluir produtos em ou abaixo de um limite derivado do preço âncora mais uma compensação. |
| **Maior que ou igual ao preço atual do produto** | Incluir ou excluir produtos em ou acima de um limite derivado do preço âncora mais uma compensação. |
| **Dentro de um intervalo de valores do produto atual** | Incluir ou excluir produtos cujo preço final esteja dentro de uma faixa de moeda fixa ao redor da âncora (compensações do preço atual). |
| **Dentro de um intervalo de porcentagem do produto atual** | Inclua ou exclua produtos cujo preço final esteja dentro de uma faixa de porcentagem ao redor da âncora. |

##### Semântica de deslocamento

Para **Menor que ou igual ao preço atual do produto** e **Maior que ou igual ao preço atual do produto**, o valor inserido é um **deslocamento numérico adicionado ao preço âncora** para formar o limite:

- Um deslocamento **negativo** move o limite **abaixo** do preço atual do produto.
- Um deslocamento **positivo** move o limite **acima** do preço atual do produto.
- **Vazio** ou **0** significa **sem limite** nesse lado; o back-end trata todos da mesma forma.
- Você não pode usar **0** para significar &quot;exatamente o preço atual do produto&quot; como o limite.

Isto corresponde a [!DNL Product Recommendations] no PaaS. Os rótulos no Administrador refletem essa semântica diretamente.

##### Configurar um filtro de preço dinâmico

1. [Crie ou edite](create.md) uma unidade de recomendação **relacionada ao SKU** que esteja implantada na página **detalhes do produto** (ou outro posicionamento em que um produto atual esteja sempre em contexto).
1. Abra **[!UICONTROL Filter products]** e selecione a guia **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]**.
1. Selecione **[!UICONTROL Price]** e ative **[!UICONTROL Enable filter]**.
1. Abra **[!UICONTROL Include products based on]** (ou o equivalente de exclusões) e escolha um operador dinâmico (por exemplo, **Dentro de um intervalo de valores do produto atual**).
1. Informe deslocamentos ou valores de faixa, conforme solicitado. Use a visualização para confirmar os resultados de um produto de amostra.
1. Salve ou publique a unidade.

Valores inválidos (valores não numéricos, combinações sem suporte ou intervalos nos quais o mínimo é maior que o máximo) bloqueiam o salvamento e mostram erros de validação; **[!UICONTROL Save]** permanece desabilitado até que o filtro seja válido.

##### Quando nenhum preço de âncora está disponível

Se um filtro de preço dinâmico estiver habilitado, mas a loja não puder fornecer um preço de produto atual (por exemplo, a unidade é renderizada fora de um contexto PDP), [!DNL Adobe Commerce Optimizer] não retorna recomendações não filtradas. A unidade não mostra **nenhuma recomendação**, pois mostrar resultados não filtrados não corresponderia à regra que você configurou.

##### Produtos configuráveis na visualização {#configurable-products-in-preview}

No painel **visualização** do Administrador, os preços recomendados do produto são exibidos da seguinte maneira:

- **Produtos simples** - Preço final único da resposta da GraphQL.
- **Produtos configuráveis** - Se os preços mínimos e máximos da variante forem diferentes, a visualização mostrará um intervalo (por exemplo, `$min – $max`). Se forem iguais, será mostrado um único preço.

O preço de referência usado para cálculos de filtros dinâmicos em um produto configurável é sempre o preço final da variante **mínimo**, consistente com a loja.

#### Exemplos de filtro de preço

Os exemplos a seguir usam o preço atual de **$500**. Ajuste a inclusão versus a exclusão para corresponder à sua meta de merchandising.

| Operador | Guia | Meta | Exemplo de limite |
| --- | --- | --- | --- |
| Menor que ou igual ao preço atual do produto | Exclusões | Promova a venda adicional ocultando alternativas com preços mais baixos | Excluir produtos ≤ $500 |
| Menor que ou igual ao preço atual do produto | Inclusões | Oferecer alternativas econômicas | Incluir produtos ≤ $500 |
| Maior que ou igual ao preço atual do produto | Exclusões | Evite vendas adicionais em um fluxo focado em orçamento | Excluir produtos ≥ US$ 500 |
| Maior que ou igual ao preço atual do produto | Inclusões | Alternativas premium de superfície | Incluir produtos ≥ US$ 500 |
| Dentro de uma faixa de valores do produto atual | Exclusões | Diversificar para fora de pontos de preços semelhantes | Excluir de US$ 400 a US$ 600 |
| Dentro de uma faixa de valores do produto atual | Inclusões | Mostrar alternativas comparáveis em uma faixa estreita | Incluir de US$ 400 a US$ 600 |
| Dentro de um intervalo de porcentagem do produto atual | Exclusões | Reduzir itens com preços semelhantes (por exemplo, ±20%) | Excluir aproximadamente de US$ 400 a US$ 600 |
| Dentro de um intervalo de porcentagem do produto atual | Inclusões | Comparação equitativa dentro de uma faixa comparável | Incluem aproximadamente de US$ 400 a US$ 600 |

### Produto

Os filtros de produto visam itens de catálogo individuais por **SKU**. Você adiciona um ou mais SKUs para permitir somente esses produtos (**Inclusões**) ou bloqueá-los (**Exclusões**), usando a mesma página **[!UICONTROL Filter products]** que [filtros de preço](#price). Não é possível exibir produtos desativados ou produtos que não estão visíveis individualmente em uma unidade de recomendação; esses produtos nunca aparecem na loja, independentemente dos filtros.

#### Configurar um filtro de produto

1. Ao [criar ou editar](create.md) uma unidade de recomendação, abra **[!UICONTROL Filter products]** (ou vá para a etapa _Filtros_ do fluxo de trabalho da unidade).
1. Selecione a guia **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]**. O selo em cada guia mostra quantos filtros desse tipo estão habilitados.
1. Na lista à esquerda, selecione **[!UICONTROL Product]**.
1. Ligue o **[!UICONTROL Enable filter]**.

   O cabeçalho do painel direito reflete a guia, por exemplo **[!UICONTROL Product inclusions]** ou o equivalente para exclusões.

1. Em **[!UICONTROL Product SKU]**, insira um SKU e clique em **[!UICONTROL Add]**. Repita para adicionar mais SKUs.

   Em **[!UICONTROL Product SKUs]**, cada SKU aparece como uma marca removível. Clique em **X** em uma marca para remover essa SKU ou clique em **[!UICONTROL Clear All]** para remover cada SKU da lista.

1. Termine de configurar a unidade de recomendação e salve ou publique como você faria normalmente para que o filtro entrasse em vigor.

Para **inclusões**, somente os produtos cujos SKUs estão listados (e que satisfazem aos outros filtros de inclusão habilitados) podem ser recomendados. Para **exclusões**, qualquer produto cujo SKU esteja listado não é recomendado, mesmo que ele seja qualificado de outra forma.

![Filtro de Produtos](../../assets/filter-product.png)

>[!NOTE]
>
>Os produtos derivados de um produto configurável não são exibidos em uma unidade de recomendação porque esses produtos secundários têm a visibilidade de _Não visível individualmente_.

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
