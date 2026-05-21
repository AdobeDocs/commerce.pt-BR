---
title: Editar recomendação
description: Saiba como editar uma recomendação de produto.
exl-id: 57bc68c0-03ba-4b66-8c75-14e49176670b
TQID: https://experienceleague.adobe.com/iynpVCKsygJXg2v-Djctfb4bhV9FMheA0ab66IBOvCg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: null
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 0%

---

# Editar recomendação

A página Editar recomendação oferece a capacidade de ajustar as configurações individuais que compõem a recomendação. Todas as configurações podem ser editadas, exceto o tipo de página e o tipo de recomendação. As seguintes configurações podem ser editadas:

- [Nome da recomendação](#name)
- [Rótulo da vitrine](#label)
- [Número de produtos](#number)
- [Posicionamento e Posição](#placement)
- [Filtrar produtos](#filters)

A visualização no lado direito da página mostra como a recomendação com as configurações atuais pode aparecer na loja. A _Visualização de produtos recomendada_ permanece visível para referência à medida que você rolar pela página. A visualização exibe uma imagem do produto em miniatura, o nome do produto, SKU, preço e tipo de resultado para cada produto retornado. O tipo de resultado indica se há dados comportamentais primários suficientes para gerar a recomendação ou se está usando dados comportamentais de backup.

![Editar Recomendações](assets/edit-recommendation.png)

## Editar uma recomendação

1. Na barra lateral _Administrador_, vá para **Marketing** > _Promoções_ > **Recomendações de Produto**.

1. Selecione a recomendação que deseja editar.

1. Clique em **Editar**. Em seguida, siga as instruções abaixo para fazer as alterações necessárias.

1. Quando terminar, clique em **Salvar alterações**.

### Nome da recomendação {#name}

Escolha um nome descritivo que indique a finalidade da recomendação. O nome é para referência interna e não aparece na loja.

![Editar nome](assets/edit-name.png)

### Rótulo da vitrine {#label}

Insira o texto que deseja usar como rótulo para a unidade de recomendação na vitrine.

![Editar rótulo](assets/edit-storefront-label.png)

### Número de produtos {#number}

Ajuste o controle deslizante para exibir até 20 produtos na unidade de recomendação.

![Editar número de produtos](assets/edit-number-of-products.png)

### Posicionamento e posição {#placement}

1. Escolha o local da página onde a unidade de recomendação deve aparecer na loja.

   - Na parte inferior do conteúdo principal
   - Na parte superior do conteúdo principal

   ![Editar posicionamento](assets/edit-placement.png)

1. Para alterar a ordem das recomendações incluídas na unidade, use o controle **Mover** ![Mover seletor](assets/icon-move.png) para arrastar as recomendações para a posição.

   ![Editar posição](assets/edit-position.png)

### Filtrar produtos {#filters}

Todas as alterações feitas nos [filtros](filters.md) do produto serão refletidas na _Visualização de produtos recomendada_. Somente os produtos que correspondem aos filtros de inclusão podem ser recomendados. Os produtos que correspondem a qualquer filtro de exclusão não são recomendados.

As guias _Inclusões_ e _Exclusões_ listam os filtros disponíveis de cada tipo. Na lista, cada filtro ativo é marcado com um ponto azul.

- Para exibir os detalhes sobre cada filtro, clique no nome do filtro.
- Para alterar o status do filtro, defina a opção **Habilitar filtro** para a posição `on` ou `off`.

![Editar filtros](assets/edit-filters.png)

As configurações de filtro descrevem os produtos a serem incluídos ou excluídos na unidade de recomendação. Por exemplo, as configurações de inclusão de filtro _Categoria_ instruem o sistema a incluir produtos somente das categorias selecionadas.

![Editar filtro de categoria](assets/edit-filter-category.png)
