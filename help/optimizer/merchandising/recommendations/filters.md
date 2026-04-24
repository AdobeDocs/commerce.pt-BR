---
title: Filtros de recomendação
description: Saiba como usar filtros para controlar quais produtos aparecem nas  [!DNL Adobe Commerce Optimizer] recomendações.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 0%

---

# Filtrar produtos

[!DNL Adobe Commerce Optimizer] aplica automaticamente filtros padrão não configuráveis a unidades de recomendação. Se você tiver várias unidades de recomendação implantadas em uma página, o [!DNL Adobe Commerce Optimizer] filtra todos os produtos que são repetidos nas unidades. Somente a primeira referência a um produto repetido é usada para abrir espaço para outros produtos a serem recomendados. O [!DNL Adobe Commerce Optimizer] também filtra todos os produtos comprados anteriormente e aqueles que estão no carrinho.

Quando você [cria](create.md) uma unidade de recomendação, pode definir filtros que controlam quais produtos podem ser exibidos nas recomendações. Esses filtros se baseiam em um conjunto de condições de inclusão ou exclusão definidas por você. Somente os produtos que correspondem a todas as condições de inclusão aparecem nas recomendações. Os produtos que correspondem a qualquer uma das condições de exclusão não são recomendados.

Você pode configurar vários filtros e ativar apenas aqueles que desejar selecionando a alternância em cada página de filtro. Isso permite criar rascunhos de filtros para uso futuro. O número de filtros ativados é exibido em cada guia.

## Condições

As condições podem ser estáticas ou dinâmicas.

- Uma condição estática usa atributos de produto existentes para determinar quais produtos podem aparecer na unidade. Por exemplo, você pode especificar que apenas os produtos em estoque com um preço superior a US$ 25 apareçam na unidade.

- Uma condição dinâmica é destacada do contexto atual de um comprador, como a categoria ou o produto visualizado no momento. Por exemplo, ao criar uma recomendação de produto para ser implantada nas páginas de detalhes do produto, você pode criar uma condição para recomendar apenas produtos que estejam dentro de uma faixa de preço relativo do produto visualizado no momento.

### Operadores lógicos

Os operadores lógicos `AND` e `OR` são usados para unir várias condições. Se estiver usando filtros de inclusão e exclusão, as inclusões serão avaliadas primeiro para determinar todos os produtos possíveis que podem ser recomendados, e os produtos que correspondem a qualquer filtro de exclusão serão removidos da lista.

- `AND` - Associa duas condições de filtragem de inclusão
- `OR` - Adiciona duas condições de filtragem por exclusão

## Tipos de filtros

Cada tipo de filtro é direcionado a um aspecto diferente do catálogo, como produto e preço, para que você possa restringir ou ampliar quais produtos estão qualificados para uma unidade. Escolha os tipos que correspondem às suas metas de merchandising e combine as condições de inclusão e exclusão conforme necessário; as subseções abaixo descrevem como cada tipo se comporta e como [!DNL Adobe Commerce Optimizer] o aplica.

>[!NOTE]
>
>Somente produtos que correspondam aos seus filtros de **inclusão** podem ser recomendados, e qualquer produto que corresponda a um filtro de **exclusão** será removido.

### Preço

>[!IMPORTANT]
>
>O recurso a seguir está na versão beta.

A filtragem de preços usa o **preço calculado final** de cada produto para o **catálogo de preços ativo** da loja—aquele atribuído à loja onde a unidade de recomendação é renderizada. Esse valor reflete descontos, promoções e preços especiais definidos nesse catálogo de preços, não somente o preço de lista. A avaliação utiliza apenas a tabela de preços da loja; outras vitrines ou tabelas de preços não se aplicam. Como os catálogos de preços são mapeados para uma loja está configurado com o catálogo e a configuração [catálogos de preços](../../setup/pricebooks.md).

#### Como incluir e excluir regras usam preço

- **Regras de inclusão** - Somente os produtos cujo preço final **corresponda a todas** as condições de inclusão definidas permanecem qualificados. Isso inclui todos os filtros de inclusão ativados (por exemplo, seu intervalo de preços mais quaisquer outras regras de inclusão).
- **Regras de exclusão** - Os produtos cujo preço final **corresponde a qualquer condição de exclusão definida** são removidos das recomendações.

**Preço exibido** - O preço mostrado nos produtos dentro da unidade de recomendação é o mesmo **preço final** da tabela de preços dessa loja, portanto, o que os compradores veem corresponde ao valor usado para filtragem.

#### Configurar um filtro de preços

1. Ao [criar ou editar](create.md) uma unidade de recomendação, abra **[!UICONTROL Filter products]** (ou vá para a etapa _Filtros_ do fluxo de trabalho da unidade).
1. Selecione a guia **[!UICONTROL Inclusions]** ou **[!UICONTROL Exclusions]**, dependendo se você deseja permitir somente produtos em um intervalo de preços ou bloquear produtos em um intervalo. O selo em cada guia mostra quantos filtros desse tipo estão habilitados.
1. Na lista à esquerda, selecione **[!UICONTROL Price]**.
1. Ligue o **[!UICONTROL Enable filter]**.

   Os valores de preço usam a **moeda base do site**, conforme observado na página.

1. Abra **[!UICONTROL Include products based on]** (na guia **[!UICONTROL Inclusions]**) ou o controle equivalente na guia **[!UICONTROL Exclusions]** e escolha **[!UICONTROL Set price range]**.
1. Defina um **[!UICONTROL Min price]** e/ou **[!UICONTROL Max price]** opcional usando os campos ao lado do símbolo da moeda. Você pode digitar valores ou usar os controles **-** e **+** para ajustar valores. Deixe um limite vazio se não precisar de um mínimo ou máximo. O intervalo é comparado ao preço calculado final de cada produto para o catálogo de preços ativo da loja.
1. Termine de configurar a unidade de recomendação e salve ou publique como você faria normalmente para que o filtro entrasse em vigor.

![Filtro de Preços](../../assets/filter-price.png)

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
