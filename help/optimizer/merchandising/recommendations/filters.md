---
title: Filtros de recomendação
description: Saiba como usar filtros para controlar quais produtos aparecem nas  [!DNL Adobe Commerce Optimizer] recomendações.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: 032a19183b79cea1bfe27e8a4e20c60ba5ac6b8b
workflow-type: tm+mt
source-wordcount: '403'
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

![Filtros](../../assets/rec-conditions.png)

### Produto

Os filtros de produto especificam quais produtos específicos estão qualificados ou não para serem exibidos nas recomendações. Você não pode selecionar produtos que estão desativados ou que não estão visíveis individualmente porque esses produtos nunca podem aparecer nas recomendações.

>[!NOTE]
>
>Os produtos derivados de um produto configurável não são exibidos em uma unidade de recomendação porque esses produtos secundários têm a visibilidade de _Não visível individualmente_.

<!--### Price

A filter based on the product price uses the final price to perform the comparison. The final price includes any discounts or special pricing available to anonymous shoppers.

### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
