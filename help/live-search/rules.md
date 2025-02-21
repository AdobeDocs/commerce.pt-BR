---
title: Pesquisar merchandising
description: As regras de merchandising do [!DNL Live Search] combinam lógica e ações para moldar a experiência de compra.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---

# Pesquisar merchandising

Merchandising de pesquisa refere-se a um conjunto de regras que combinam lógica e ações para moldar a experiência de pesquisa de um comprador em sua loja. Você pode usar regras de merchandising para impulsionar, enterrar, fixar ou ocultar produtos a fim de calibrar os resultados da pesquisa em tempo real para apoiar suas metas comerciais.

Cada regra tem três componentes principais:

* Condições - as condições que acionam uma ação.
* Eventos - As ações que ocorrem quando as condições são atendidas.
* Detalhes - O nome da regra e o intervalo de tempo e a descrição opcionais.

É possível combinar várias condições e ações e agendar uma regra para ficar ativa por um período. Você também pode definir uma regra padrão que é aplicada mesmo quando nenhum termo de pesquisa é definido.

## Requisitos

Uma regra de pesquisa simples pode ter uma única condição e um único evento, enquanto uma regra complexa pode ter até dez condições que acionam até 25 eventos.
As regras podem ter:

* Até dez condições
* Até 25 eventos

O texto da consulta pode conter:

* Caracteres alfanuméricos (letras e números)
* Caracteres em maiúsculas ou minúsculas. Capitalização é ignorada.

## Operadores lógicos

Os operadores lógicos `AND` e `OR` unem duas condições e retornam resultados diferentes. Todos os operadores lógicos usados em uma regra com várias condições são os mesmos. Não é possível usar `AND` e `OR` na mesma regra.

### Operadores de correspondência

Os operadores Match `All` e `Any` determinam o operador lógico usado para unir várias condições na regra e podem ser usados para alterar o operador existente.

* `All` - Usa o operador lógico `AND` para unir várias condições. Uma regra que usa o operador Correspondência `All` só pode ter uma condição `Search query is`.
* `Any` - Usa o operador lógico `OR` para unir várias condições.

Ao compor uma regra complexa, pode ser útil anotá-la com recuo para descrever as condições, os eventos associados e os nomes de produtos ou SKUs necessários para retornar os resultados que você deseja alcançar. Em seguida, crie a regra e teste o resultado.

## Regra padrão

Você pode definir uma regra padrão que é aplicada quando nenhum termo de pesquisa é fornecido, ou nenhuma outra regra de pesquisa pode ser aplicada. Se você definir a regra padrão como &quot;Mais comprados&quot;, todas as consultas assumirão como padrão esse tipo de classificação, a menos que sejam supercedidas por um termo de pesquisa mais específico. Nenhum termo de pesquisa pode ser definido para a regra padrão.

## Ordem de precedência com várias regras

Somente uma regra de pesquisa é aplicada a um termo de pesquisa de cada vez.
Se várias regras forem consideradas aplicáveis a uma frase de pesquisa, todas elas serão aplicadas. Se houver uma colisão entre duas regras —`rule 1` que aumenta o sku1, mas `rule 2` oculta o mesmo SKU — então a regra aplicada mais recentemente (`rule 2`) tem prioridade.

* As regras são ordenadas pelo carimbo de data e hora &quot;Última modificação&quot;. A regra modificada mais recentemente é aplicada primeiro, e depois disso as regras mais antigas, na ordem do carimbo de data e hora.
* A condição `query is` tem precedência sobre outras condições. Se uma regra mais recente contiver uma condição `query contains`, mas uma regra mais antiga tiver uma condição `query is`, a regra `query is` será aplicada.

### Solicitações de vitrine

Se uma regra ativa contendo uma condição `query is` corresponder à frase de pesquisa, ela será aplicada. Se houver várias regras correspondentes com uma condição `query is`, a regra ativa atualizada mais recentemente será aplicada.
Caso contrário, a regra ativa atualizada mais recentemente será aplicada.

### Visualizar solicitações

A solicitação feita no Administrador funciona de forma um pouco diferente. Ao visualizar no Admin, todas as regras são aplicadas, incluindo as expiradas e programadas.

* Se a regra que está sendo visualizada tiver uma condição `query is`, ela será aplicada.
* Se a regra que está sendo visualizada não tiver uma condição `query is` e uma regra de correspondência ativa subsequente com uma condição `query is` for encontrada, a regra `query is` será aplicada.
* Se a regra que está sendo visualizada não tiver uma condição `query is` e nenhuma outra regra com uma condição `query is` for encontrada, a regra que está sendo visualizada será aplicada.

## Merchandising de categoria e atribuições de produto de categoria

[!DNL Live Search] permite que você filtre por Categorias. Consulte [Merchandising de categoria](category-merch.md) para obter mais informações.
No entanto, no Adobe Commerce, você pode criar uma categoria virtual com [Atribuições de produto de categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/products-in-category/categories-product-assignments.html). Esse tipo de categoria é criado no tempo de execução e não existe no banco de dados de categorias. Portanto, [!DNL Live Search] não pode ler ou usar este tipo de categoria.
