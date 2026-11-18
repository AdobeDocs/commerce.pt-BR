---
source-git-commit: 3478e3f0162b553d03c4ac4f5b3000b8aabd8c66
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%
---
As regras de merchandising combinam lógica com ações para moldar como os produtos aparecem nos **resultados da pesquisa**, nas **listas de produtos padrão** por meio da **regra de pesquisa padrão** e nas **páginas de categoria**. Você pode impulsionar, enterrar, fixar ou ocultar produtos e aplicar a **classificação inteligente** para que as listas reflitam suas metas comerciais. Use as **regras de supressão de pesquisa** para impedir que as consultas de pesquisa correspondentes retornem resultados.

Cada **regra de pesquisa** tem três componentes principais:

- **Condições** - Requisitos baseados em consultas que disparam uma ação quando a pesquisa do comprador é correspondente.
- **Eventos** - As ações que ocorrem quando as condições são atendidas (classificação manual e eventos relacionados).
- **Detalhes** - O nome da regra e o intervalo de tempo e a descrição opcionais.

**As regras de categoria** usam **seleção de categoria** em vez das condições de consulta de pesquisa; a classificação inteligente e a classificação manual funcionam da mesma forma que para pesquisa, com diferenças chamadas em [Criar e Gerenciar Regras](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/merchandising/rules/add).

É possível combinar várias condições e ações para regras de pesquisa e regras de agendamento para ficarem ativas por um período. As regras de supressão de pesquisa usam condições de consulta para bloquear resultados em vez de classificar produtos. Você também pode definir uma **regra de pesquisa padrão** que se aplique quando nenhuma outra pesquisa ou regra de categoria específica se aplicar.

## Pesquisar regras de supressão {#search-suppression-rules}

As regras de supressão de pesquisa são um tipo de regra de merchandising que bloqueia os resultados para consultas correspondentes do comprador. Essas pesquisas não retornam produtos na loja. Depois que a regra se tornar ativa, verifique a apresentação sem resultados real da loja.

Use a supressão de pesquisa para restrições de pesquisa normativa, restrições de marca ou termos específicos que não devem retornar resultados. Suporte a condições **A consulta é**, **a consulta contém**, **a consulta começa com** e **a consulta termina com**. Para obter etapas de configuração e gerenciamento, consulte [Criar e gerenciar regras de supressão de pesquisa](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules). Para obter exemplos, consulte [Práticas recomendadas](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/merchandising/rules/best-practice#search-suppression-best-practices).

A supressão de pesquisa afeta somente a experiência de pesquisa. Isso não altera a visibilidade do produto por meio da navegação de categoria, páginas de merchandising, recomendações ou URLs diretos do produto. Ele não substitui a visibilidade do produto em todo o catálogo nem os controles de acesso.

### Interação com outros recursos de merchandising

| Recurso | Interação com supressão de pesquisa |
| --- | --- |
| Pesquisar regras | Para uma consulta correspondida por uma regra de supressão de pesquisa ativa, a loja exibe uma página de resultados de pesquisa com zero produtos. As ações de classificação em uma regra de pesquisa não substituem a supressão. As consultas que não estão bloqueadas continuam a usar as regras de merchandising aplicáveis. |
| Regras de categoria | A navegação de categoria e o merchandising de categoria não são afetados pela supressão de pesquisa. Um produto pode permanecer visível em uma categoria mesmo quando uma consulta de pesquisa para ele estiver bloqueada. |
| Regra de pesquisa padrão | A supressão de pesquisa bloqueia consultas correspondentes, enquanto a regra de pesquisa padrão define a classificação padrão e as exclusões de produtos. A classificação padrão não restaura os resultados de uma consulta bloqueada. |
| Eventos de merchandising baseados em atributos | Esses eventos aplicam ações a produtos que correspondem às condições de atributo, conforme descrito em [Classificação de atributo](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/merchandising/rules/add#attribute-ranking). Em vez disso, a supressão de pesquisa bloqueia os resultados de uma consulta correspondente, independentemente de quais produtos seriam correspondentes. |

Os produtos excluídos pela **regra de pesquisa padrão**, por meio de exclusões manuais ou pelos **Eventos de Merchandising baseados em atributos** com uma ação **Ocultar**, também são excluídos das **sugestões de pesquisa e preenchimento automático**. Isso mantém as exclusões de produtos consistentes em toda a experiência de pesquisa e é separado do bloqueio de uma consulta com uma regra de supressão de pesquisa.

## Regras de categoria {#category-rules}

As **Regras de categoria** controlam o pedido de produto em **páginas de categoria**. Selecione uma ou mais categorias e aplique classificação inteligente (por exemplo, mais visualizada, tendência) e ações manuais, como fixar, aumentar e atenuar. Elas não usam as condições de consulta de pesquisa. Para obter etapas de configuração, tipos de regras e como a classificação se aplica à categoria e à pesquisa, consulte [Criar e Gerenciar Regras](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/merchandising/rules/add).

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

- `All` — Usa o operador lógico `AND` para unir várias condições. Uma regra que usa o operador Correspondência `All` só pode ter uma condição `Search query is`.
- `Any` — Usa o operador lógico `OR` para unir várias condições.

Ao compor uma regra complexa, pode ser útil anotá-la com recuo para descrever as condições, os eventos associados e os nomes de produtos ou SKUs necessários para retornar os resultados que você deseja alcançar. Em seguida, crie a regra e teste o resultado.

## Regra padrão

Você pode definir uma **regra de pesquisa padrão** que se aplica quando nenhum termo de pesquisa é fornecido, ou nenhuma outra regra de pesquisa pode ser aplicada. Se você definir a regra padrão como &quot;Mais comprados&quot;, as consultas assumirão como padrão esse tipo de classificação, a menos que sejam substituídas por um termo de pesquisa mais específico. Nenhum termo de pesquisa pode ser definido para a regra padrão. **As regras de categoria** são separadas: elas se aplicam apenas às categorias selecionadas e não substituem a regra de listagem padrão.

## Ordem de precedência com várias regras

Esta seção explica como as regras de pesquisa de classificação se aplicam à consulta de um comprador e interagem entre si. A classificação de regra de pesquisa não substitui a supressão de pesquisa: quando uma regra de supressão ativa corresponde a uma consulta, a loja não retorna produtos para essa pesquisa. As regras de categoria se aplicam às categorias selecionadas. Consulte [Criar e Gerenciar Regras](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/merchandising/rules/add) para obter detalhes sobre pesquisa, categoria e regras de pesquisa padrão.

Somente uma regra de pesquisa é aplicada a um termo de pesquisa de cada vez.
Se várias regras forem consideradas aplicáveis a uma frase de pesquisa, todas elas serão aplicadas. Se houver uma colisão entre duas regras —`rule 1` que aumenta o sku1, mas `rule 2` oculta o mesmo SKU — então a regra aplicada mais recentemente (`rule 2`) tem prioridade.

- As regras são ordenadas pelo carimbo de data e hora &quot;Última modificação&quot;. A regra modificada mais recentemente é aplicada primeiro, e depois disso as regras mais antigas, na ordem do carimbo de data e hora.
- A condição `query is` tem precedência sobre outras condições. Se uma regra mais recente contiver uma condição `query contains`, mas uma regra mais antiga tiver uma condição `query is`, a regra `query is` será aplicada.

### Solicitações de vitrine

Se uma regra ativa contendo uma condição `query is` corresponder à frase de pesquisa, ela será aplicada. Se houver várias regras correspondentes com uma condição `query is`, a regra ativa atualizada mais recentemente será aplicada.
Caso contrário, a regra ativa atualizada mais recentemente será aplicada.

### Visualizar solicitações

As solicitações feitas na visualização funcionam de forma um pouco diferente. Ao visualizar, todas as regras são aplicadas, incluindo as expiradas e programadas.

- Se a regra que está sendo visualizada tiver uma condição `query is`, ela será aplicada.
- Se a regra que está sendo visualizada não tiver uma condição `query is` e uma regra de correspondência ativa subsequente com uma condição `query is` for encontrada, a regra `query is` será aplicada.
- Se a regra que está sendo visualizada não tiver uma condição `query is` e nenhuma outra regra com uma condição `query is` for encontrada, a regra que está sendo visualizada será aplicada.
