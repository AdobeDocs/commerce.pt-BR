---
title: Filtrar produtos
description: Defina condições que incluam ou excluam produtos de serem usados como recomendações.
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
source-git-commit: 59aa4ae67a1a8a853b72d78cd65a6cc44a6bc662
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---

# Filtrar produtos

O Adobe Commerce aplica automaticamente filtros padrão não configuráveis a unidades de recomendação. Se você tiver várias unidades de recomendação implantadas em uma página, o Adobe Commerce filtra todos os produtos que são repetidos nas unidades. Somente a primeira referência a um produto repetido é usada para abrir espaço para outros produtos a serem recomendados. O Adobe Commerce também filtra todos os produtos comprados anteriormente e aqueles que estão no carrinho.

Quando você [cria](create.md) uma unidade de recomendação, pode definir filtros que controlam quais produtos podem ser exibidos nas recomendações. Esses filtros se baseiam em um conjunto de condições de inclusão ou exclusão definidas por você. Somente os produtos que correspondem a todas as condições de inclusão aparecem nas recomendações. Os produtos que correspondem a qualquer uma das condições de exclusão não são recomendados.

Você pode configurar vários filtros e ativar apenas aqueles que desejar selecionando a alternância em cada página de filtro. Isso permite criar rascunhos de filtros para uso futuro. O número de filtros ativados é exibido em cada guia.

## Condições

As condições podem ser estáticas ou dinâmicas.

- Uma condição estática usa atributos de produto existentes para determinar quais produtos podem aparecer na unidade. Por exemplo, você pode especificar que apenas os produtos em estoque com um preço superior a US$ 25 apareçam na unidade. As condições estáticas estão disponíveis em todos os tipos de página.

- Uma condição dinâmica é destacada do contexto atual de um comprador, como a categoria ou o produto visualizado no momento. Por exemplo, ao criar uma recomendação de produto para ser implantada nas páginas de detalhes do produto, você pode criar uma condição para recomendar apenas produtos que estejam dentro de uma faixa de preço relativo do produto visualizado no momento. As condições dinâmicas estão disponíveis em todos os tipos de página, exceto a Página inicial, e em páginas com recomendações inseridas com o Page Builder.

### Operadores lógicos

Os operadores lógicos `AND` e `OR` são usados para unir várias condições. Se estiver usando filtros de inclusão e exclusão, as inclusões serão avaliadas primeiro para determinar todos os produtos possíveis que podem ser recomendados, e os produtos que correspondem a qualquer filtro de exclusão serão removidos da lista.

- `AND` - Associa duas condições de filtragem de inclusão
- `OR` - Adiciona duas condições de filtragem por exclusão

>[!NOTE]
>
> Os filtros de inclusão e exclusão substituem as exclusões de categoria herdada nas versões 3.2.2 e posteriores do módulo `magento/product-recommendations`. Consulte as [notas de versão](release-notes.md) para saber mais sobre as versões do Adobe Commerce.

## Tipos de filtros {#filtertypes}

![Filtros](assets/rec-conditions.png)

### Categoria

[!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."}

Filtra produtos com base em suas categorias. O filtro de categoria usa atribuições de categoria diretas e suas subcategorias. Por exemplo, habilitar uma condição de exclusão para a categoria `Gear` exclui produtos atribuídos a `Gear` e todas as suas subcategorias como `Gear/Bags` ou `Gear/Fitness Equipment`. O mesmo se aplica a um filtro de inclusão em uma categoria. Por exemplo, habilitar uma condição de inclusão para a categoria `Gear` inclui produtos atribuídos a `Gear` e todas as suas subcategorias como `Gear/Bags` ou `Gear/Fitness Equipment`.

O campo de categoria exibe categorias que pertencem à loja atual.

>[!NOTE]
>
>Para comerciantes B2B, o filtro Categoria adere a qualquer [categoria de produto específica do cliente](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=pt-BR) configurada.

A Adobe Commerce recomenda usar a seguinte configuração de filtro de categoria ao implantar recomendações para seus tipos de página:

| Página | Filtrar por |
|---|---|
| Início | Não filtre produtos. |
| Categoria | Filtrar produtos na categoria específica. |
| Detalhes do produto | Filtrar produtos nas mesmas categorias. |
| Carrinho | Filtre categorias de produtos no carrinho. |
| Confirmação do pedido | Filtrar categorias de produtos comprados. |

### Produto

Os filtros de produto especificam quais produtos específicos estão qualificados ou não para serem exibidos nas recomendações. Você não pode selecionar produtos que estão desativados ou que não estão visíveis individualmente porque esses produtos nunca podem aparecer nas recomendações.

>[!NOTE]
>
>Os produtos derivados de um produto configurável não são exibidos em uma unidade de recomendação porque esses produtos secundários têm a visibilidade de _Não visível individualmente_.

### Tipo

[!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."}

Um filtro com base no tipo de produto inclui ou exclui todos os produtos de um tipo específico. Os tipos suportados incluem _simple_, _configurable_, _virtual_, _downloadable_ ou _vale-presente_. Não há suporte para _Pacotes_, _agrupados_ e tipos de produtos personalizados.

### Visibilidade

[!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."}

Filtra produtos com base na visibilidade, como: _Catálogo_, _Pesquisa_ ou ambos.

### Preço

Um filtro com base no preço do produto usa o preço final para executar a comparação. O preço final inclui descontos ou preços especiais disponíveis para compradores anônimos. Para comerciantes B2B, o preço exibido reflete o [preço de grupo específico do cliente](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=pt-BR) que você configurou.

### Status do estoque

Os seguintes filtros de exclusão podem ser usados para filtrar produtos com base no status do estoque:

- Fora de estoque - (Somente exclusão) Exclui produtos que estão fora de estoque.
- Baixo em estoque - (Somente exclusão) Exclui produtos com baixo estoque. O status de estoque baixo é baseado no valor _Somente X limite à esquerda_ na [Configuração de inventário](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html?lang=pt-BR).
