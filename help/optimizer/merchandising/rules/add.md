---
title: Criar e gerenciar regras
description: Saiba como criar e gerenciar regras de merchandising.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '1767'
ht-degree: 0%

---

# Criar e gerenciar regras

Para criar uma regra, a primeira etapa é usar o editor de regras para definir as condições no texto de query do comprador que acionam os eventos associados. Em seguida, complete os detalhes da regra, teste os resultados e publique a regra.

## Criar uma regra

1. No painel à esquerda, vá para _Merchandising_ > **Regras de comercialização**.
1. Clique em **Criar regra** para iniciar o editor de regras.

![Criar regra](../../assets/create-rule.png)

Na seção **Criar regra**, você define critérios de pesquisa, condições e tipos de classificação específicos.

1. No campo **[!UICONTROL Name]**, digite um nome para a regra. Todos os nomes de regras devem ser exclusivos.
1. No campo **[!UICONTROL Description]**, insira uma descrição para a regra.
1. No campo **[!UICONTROL Date range]**, especifique a data ou o intervalo de datas em que deseja que a regra fique ativa.
1. Na seção **[!UICONTROL Rule applies to]**, você tem duas opções: **[!UICONTROL All product listings]** ou **[!UICONTROL Specific conditions]**.

   - **Todas as listagens de produtos** - Esta é essencialmente a sua regra padrão e é aplicada a todas as consultas de pesquisa, a menos que uma consulta de pesquisa mais específica seja definida. Você pode criar apenas uma regra padrão e ela não pode conter condições. Escolha o tipo de classificação Inteligente e qualquer classificação manual que quiser aplicar a todas as pesquisas padrão.
   - **Condições específicas** - Consulte a próxima seção para saber mais sobre os tipos de condições que você pode definir para sua regra.

### Condições

As condições são os requisitos para acionar um evento. Uma regra pode ter até dez condições e 25 eventos. Uma regra padrão não pode ter condições.

![Selecionar Condição de Regra](../../assets/rule-set-condition.png)

#### Condição única

1. Em *Criar sua regra*, selecione a **Condição** a ser atendida e siga as instruções para concluir a instrução.

   - A consulta de pesquisa contém - Digite a sequência de texto que deve estar na consulta do comprador. A configuração Corresponder determina o grau em que a consulta do comprador corresponde ao catálogo. Opções:<br /> Qualquer - Qualquer parte do texto de consulta do comprador pode corresponder à condição.<br />Todas - Todas as consultas do comprador devem corresponder à condição.
   - A consulta de pesquisa é - Digite uma sequência de texto que corresponda exatamente à consulta do comprador. Por exemplo: &quot;calças de ioga&quot;. Regras com `Search query is` e Correspondência `All` podem ter apenas uma condição.
   - Pesquisar consulta começa com - Insira um caractere ou sequência de texto que deve estar no início da consulta do comprador.
   - A consulta de pesquisa termina com - Digite um caractere ou sequência de texto que deve estar no final da consulta do comprador.

   Os resultados são exibidos imediatamente no painel *Testar sua regra* e são numerados por prioridade. Você pode usar o controle deslizante *Resultados por linha* no canto superior direito para alterar o número de produtos em cada linha.

1. Para testar outras consultas, altere o texto da consulta na caixa de pesquisa *Testar sua regra* e pressione **Retornar**.
Inicialmente, o painel de teste renderiza a consulta na caixa de pesquisa Condições. Mas agora ele está renderizando a consulta a partir da caixa de query de teste. O painel de teste renderiza apenas uma consulta por vez.
1. Se você gostar do resultado, atualize o texto na caixa de pesquisa *Condições*. Em seguida, clique em qualquer lugar na página para atualizar os resultados no painel de teste.

#### Várias condições

1. Para criar uma regra com várias condições, clique em **Adicionar condição**.
Uma regra pode ter até dez condições. O operador lógico que junta duas condições se baseia na configuração *Correspondência* atual. Por padrão, *Correspondência* é `All` e o operador lógico é `AND`.

1. Selecione a segunda condição e insira o texto de consulta necessário.

1. Para alterar a lógica da regra, altere a configuração **Corresponder** para determinar com que proximidade os critérios de pesquisa do comprador devem corresponder à condição de consulta. Defina **Correspondência** para um dos seguintes:

   - Qualquer - (Padrão) Todos os operadores lógicos na regra são definidos como `OR` e os resultados são exibidos no painel de teste.
   - Todos - Todos os operadores lógicos na regra são definidos como `AND` e os resultados são exibidos no painel de teste.

   O valor *Match* determina o operador lógico usado para unir várias condições. A alteração da configuração *Correspondência* altera todos os operadores lógicos na regra. Não é possível combinar `AND` e `OR` na mesma regra.

   Neste exemplo, em vez de procurar por &quot;calças de ioga&quot;, há duas consultas separadas que procuram por &quot;ioga&quot; ou &quot;calças&quot;. Essa regra é menos específica e é acionada com mais frequência na loja do que na outra.

1. Para adicionar outra condição, clique em **Adicionar condição** e repita o processo.

### Classificação inteligente

A classificação inteligente combina comportamentos de usuário e estatísticas do site para determinar a classificação do produto.
Os proprietários de lojas podem configurar os seguintes tipos de estratégias de classificação:

![Classificações inteligentes](../../assets/rule-intelligent-ranking.png)

- Mais comprados: classifica os produtos por total de compras por SKU nos 7 dias anteriores.
- Mais adicionados ao carrinho - Classificações na ordem do total de atividades &quot;Adicionar ao carrinho&quot; nos 7 dias anteriores.
- Mais visualizados: classificação do total de visualizações por SKU nos 7 dias anteriores.
- Recomendado para você - Usa o ponto de dados `viewed-viewed` - Os compradores que visualizaram este SKU também visualizaram esses outros SKUs.
- Tendência: retroage aos eventos de exibição de página nas últimas 72 horas para eventos em segundo plano e 24 horas para eventos em primeiro plano.
- Nenhum: os produtos são ordenados por Relevância.

Selecione o tipo de estratégia para a regra. A janela **Testar sua regra** exibe os resultados esperados.

#### Avisos

- Apóstrofos e citações em queries podem levar a alguns problemas menores com classificação e relevância em alguns idiomas.
- Para garantir que a classificação inteligente funcione corretamente, verifique se o **Peso da Pesquisa** para qualquer atributo usado para pesquisa ou filtragem (facetas) é `5` ou menos.

Para obter informações sobre como definir pesos de pesquisa, consulte a [API de metadados](https://developer.adobe.com/commerce/services/reference/rest/).

### Classificação manual

**Classificação manual** são ações que modificam os resultados da pesquisa quando as condições definidas são atendidas. Uma única regra pode ter até 25 eventos.

- Aumentar - Move um produto para cima nos resultados da pesquisa.
- Enterro - Move um SKU para baixo nos resultados da pesquisa.
- Fixar um produto - O produto é exibido na &quot;Posição&quot; selecionada na página.
- Ocultar um produto - Exclui um SKU dos resultados da pesquisa.

A maneira mais fácil de fixar um produto é arrastando e soltando.

1. Clique e arraste um produto no Painel de teste. Arraste e solte-o na posição desejada. Os campos Produto e Posição são automaticamente preenchidos no painel Eventos.

Você também pode clicar no ícone de pino para fixar um produto no local atual. Use o menu de contexto de reticências para &quot;Fixar na parte superior&quot; ou &quot;Fixar na parte inferior&quot;.

>[!NOTE]
>
>Você só pode fixar produtos retornados na query.

Ou eventos podem ser definidos manualmente:

1. Em *Eventos*, escolha o **Evento** que ocorrerá quando as condições associadas forem atendidas.

   Por exemplo, escolha `Hide a product`. Em seguida, insira o nome do produto que deseja ocultar. Os produtos são sugeridos à medida que você digita.

1. Para vários eventos, escolha outros eventos que deseja acionar quando as condições forem atendidas.

### Finalização da regra

1. Examine os resultados da regra no painel de teste.
1. Se a regra tiver várias consultas, teste cada uma que possa ser afetada pela regra.
1. Ao concluir, clique em **Salvar e publicar**.

   A regra é adicionada à lista no espaço de trabalho *Regras*.

1. Embora as regras ativas entrem em vigor imediatamente, talvez seja necessário aguardar até 15 minutos para que os resultados da consulta em cache na loja sejam atualizados.

>[!NOTE]
>
>As regras e os produtos classificados manualmente são aplicados aos resultados da pesquisa quando a ordem de classificação padrão, &quot;Classificar por: Mais relevante&quot;, é selecionada. Se um comprador alterar a ordem de classificação para algo como classificar por nome ou preço, as regras e as classificações manuais não estarão mais em vigor.

## Editar, exibir e excluir regras

Siga estas instruções para atualizar as propriedades das regras existentes.

### Editar regra

1. No espaço de trabalho *Regras de merchandising*, encontre a regra na grade que você deseja editar e clique em **Mais** (...) opções.
1. Clique em **Editar** para acessar o editor de regras.
1. Atualize as condições, os operadores e os eventos, conforme necessário.
1. Atualize os campos nome, data inicial e final e descrição, conforme necessário. Todos os nomes de regras devem ser exclusivos.
1. Teste a regra.
1. Publique as alterações.
A regra é adicionada à lista no espaço de trabalho *Regras*. Embora as regras ativas entrem em vigor imediatamente, pode levar até 15 minutos para que os resultados da consulta em cache na loja sejam atualizados.

### Exibir detalhes

Esta opção fornece uma maneira rápida de ver todos os parâmetros de regra, enquanto permanece na tabela *Regras*.

1. No espaço de trabalho *Regras de merchandising*, encontre a regra na grade que você deseja editar e clique em **Mais** (...) opções.
1. Clique em **Exibir detalhes** para exibir os parâmetros da regra.
1. Escolha **Editar** ou **Excluir** ou clique no X para fechar o painel.

### Excluir regra

1. No espaço de trabalho *Regras*, localize a regra na grade que você deseja editar e clique em **Mais** opções...
1. Clique em **Excluir**.

## Descrições dos campos

### Condições (if)

| Condição | Descrição |
|--- |--- |
| A consulta de pesquisa contém | Um caractere ou sequência de texto incluída na consulta do comprador. A consulta do comprador precisa corresponder apenas a um único caractere para atender a essa condição. |
| A consulta de pesquisa é | Um caractere ou sequência de texto que corresponde exatamente à consulta do comprador. Consultas complexas com várias condições não podem ser compostas quando essa condição é usada. |
| A consulta de pesquisa começa com | A consulta do comprador começa com esse caractere ou sequência de texto. |
| A consulta de pesquisa termina com | A consulta do comprador termina com esse caractere ou sequência de texto. |

### Operadores lógicos

| Operador | Descrição |
|--- |--- |
| OU | (Padrão) O operador lógico `OR` compara duas condições e atende aos requisitos para acionar um evento se pelo menos uma condição for verdadeira. |
| E | O operador lógico `AND` compara duas condições e atende aos requisitos para acionar um evento se ambas as condições forem verdadeiras. |

### Corresponder operadores

| Operador | Descrição |
|--- |--- |
| Qualquer | Altera todos os operadores lógicos na regra para `OR` e retorna o conjunto de produtos correspondentes. |
| Todos | Altera todos os operadores lógicos na regra para `AND` e retorna o conjunto de produtos correspondentes. |

### Classificação manual

| Evento | Descrição |
|--- |--- |
| Aumentar | Move um SKU ou intervalo de SKUs para cima nos resultados da pesquisa. Cada uma é marcada com um selo de visualização &quot;aumentada&quot; nos resultados da pesquisa de teste. |
| Enterro | Move um SKU ou intervalo de SKUs para baixo nos resultados da pesquisa. Cada uma está marcada com um selo de visualização &quot;entranhado&quot; nos resultados de pesquisa de teste. |
| Fixar um produto | Anexa um único SKU a uma posição específica nos resultados da pesquisa. O produto é marcado com um selo de visualização &quot;fixado&quot; nos resultados da pesquisa de teste. |
| Ocultar um produto | Exclui um SKU, ou intervalo de SKUs, dos resultados da pesquisa. |

### Detalhes

| Campo | Descrição |
|--- |--- |
| Nome | O nome da regra. Rule names must be unique. |
| Tipo de regra | Padrão ou Consulta. O padrão é aplicado a todas as regras, a menos que uma regra de Query mais específica seja definida. |
| Data inicial | A data de início da regra, se programada. |
| Data final | A data final da regra, se programada. |
| Descrição | Uma breve descrição da regra. |
