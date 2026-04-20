---
title: Regras de merchandising
description: As regras de merchandising do [!DNL Adobe Commerce Optimizer] combinam lógica com ações para moldar resultados de pesquisa, listas de produtos padrão e páginas de categoria.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: f2a9b5e8-d23d-4855-b424-ca6b40e057df
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# Regras de merchandising

As regras de merchandising combinam lógica com ações para moldar como os produtos aparecem nos **resultados de pesquisa**, em **listas de produtos padrão** (**todas as listas de produtos**) e em **páginas de categoria** ([regras de categoria](#category-rules) estão na versão beta). Você pode impulsionar, enterrar, fixar ou ocultar produtos e aplicar a **classificação inteligente** para que as listas reflitam suas metas comerciais.

Cada **regra de pesquisa** tem três componentes principais:

- **Condições** - Requisitos baseados em consultas que disparam uma ação quando a pesquisa do comprador é correspondente.
- **Eventos** - As ações que ocorrem quando as condições são atendidas (classificação manual e eventos relacionados).
- **Detalhes** - O nome da regra e o intervalo de tempo e a descrição opcionais.

**As regras de categoria** usam **seleção de categoria** em vez das condições de consulta de pesquisa; a classificação inteligente e a classificação manual funcionam da mesma forma que para pesquisa, com diferenças chamadas em [Criar e Gerenciar Regras](add.md).

É possível combinar várias condições e ações para regras de pesquisa e agendar qualquer regra para ficar ativa por um período. Você também pode definir uma **regra padrão** (**Todas as listas de produtos**) que se aplique quando não houver mais regras de pesquisa ou categoria específicas.

## Regras de categoria {#category-rules}

>[!IMPORTANT]
>
>As regras de categoria estão na versão beta.

As **Regras de categoria** controlam o pedido de produto em **páginas de categoria**. Selecione uma ou mais categorias e aplique classificação inteligente (por exemplo, mais visualizada, tendência) e ações manuais, como fixar, aumentar e atenuar. Elas não usam as condições de consulta de pesquisa. Para obter etapas de configuração, tipos de regras e como a classificação se aplica à categoria e à pesquisa, consulte [Criar e Gerenciar Regras](add.md).

## Requisitos

Uma **regra de pesquisa** simples pode ter uma única condição e um único evento, enquanto uma regra complexa pode ter até dez condições que acionam até 25 eventos. **As regras de categoria** seguem os mesmos limites de evento para classificação manual; elas não usam condições de consulta.

As regras podem ter:

- Até dez **condições** (somente regras de pesquisa)
- Até 25 **eventos**

O texto da consulta pode conter:

- Caracteres alfanuméricos (letras e números)
- Caracteres em maiúsculas ou minúsculas. Capitalização é ignorada.

## Operadores lógicos

Os operadores lógicos `AND` e `OR` unem duas condições e retornam resultados diferentes. Todos os operadores lógicos usados em uma regra com várias condições são os mesmos. Não é possível usar `AND` e `OR` na mesma regra.

### Corresponder operadores

Os operadores Match `All` e `Any` determinam o operador lógico usado para unir várias condições na regra e podem ser usados para alterar o operador existente.

- `All` - Usa o operador lógico `AND` para unir várias condições. Uma regra que usa o operador Correspondência `All` só pode ter uma condição `Search query is`.
- `Any` - Usa o operador lógico `OR` para unir várias condições.

Ao compor uma regra complexa, pode ser útil anotá-la com recuo para descrever as condições, os eventos associados e os nomes de produtos ou SKUs necessários para retornar os resultados que você deseja alcançar. Em seguida, crie a regra e teste o resultado.

## Regra padrão

Você pode definir uma regra padrão (**Todas as listagens de produtos**) que se aplica quando nenhum termo de pesquisa é fornecido ou nenhuma outra regra de pesquisa pode ser aplicada. Se você definir a regra padrão como &quot;Mais comprados&quot;, as consultas assumirão como padrão esse tipo de classificação, a menos que sejam substituídas por um termo de pesquisa mais específico. Nenhum termo de pesquisa pode ser definido para a regra padrão. **As regras de categoria** são separadas: elas se aplicam apenas às categorias selecionadas e não substituem a regra de listagem padrão.

## Ordem de precedência com várias regras

O seguinte se aplica às **regras de pesquisa** e como elas interagem para uma determinada pesquisa. **Regras de categoria** se aplicam por categoria. Consulte [Criar e Gerenciar Regras](add.md) para saber como elas se encaixam com as regras padrão e de pesquisa.

Somente uma regra de pesquisa é aplicada a um termo de pesquisa de cada vez.
Se várias regras forem consideradas aplicáveis a uma frase de pesquisa, todas elas serão aplicadas. Se houver uma colisão entre duas regras —`rule 1` que aumenta o sku1, mas `rule 2` oculta o mesmo SKU — então a regra aplicada mais recentemente (`rule 2`) tem prioridade.

- As regras são ordenadas pelo carimbo de data e hora &quot;Última modificação&quot;. A regra modificada mais recentemente é aplicada primeiro, e depois disso as regras mais antigas, na ordem do carimbo de data e hora.
- A condição `query is` tem precedência sobre outras condições. Se uma regra mais recente contiver uma condição `query contains`, mas uma regra mais antiga tiver uma condição `query is`, a regra `query is` será aplicada.

### Solicitações de vitrine

Se uma regra ativa contendo uma condição `query is` corresponder à frase de pesquisa, ela será aplicada. Se houver várias regras correspondentes com uma condição `query is`, a regra ativa atualizada mais recentemente será aplicada.
Caso contrário, a regra ativa atualizada mais recentemente será aplicada.

### Visualizar solicitações

A solicitação feita em [!DNL Adobe Commerce Optimizer] funciona de forma um pouco diferente. Ao visualizar [!DNL Adobe Commerce Optimizer], todas as regras são aplicadas, incluindo as expiradas e agendadas.

- Se a regra que está sendo visualizada tiver uma condição `query is`, ela será aplicada.
- Se a regra que está sendo visualizada não tiver uma condição `query is` e uma regra de correspondência ativa subsequente com uma condição `query is` for encontrada, a regra `query is` será aplicada.
- Se a regra que está sendo visualizada não tiver uma condição `query is` e nenhuma outra regra com uma condição `query is` for encontrada, a regra que está sendo visualizada será aplicada.
