---
title: Adicionar regras
description: Saiba como criar regras de merchandising de pesquisa.
exl-id: 7175ccf7-d838-43b0-a176-957e7db040e0
source-git-commit: 449b281e46d16de56f4c3d2e01e7165c59ee78a2
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 0%

---

# Adicionar regras

Para criar uma regra, a primeira etapa é usar o editor de regras para definir as condições no texto de query do comprador que acionam os eventos associados. Em seguida, complete os detalhes da regra, teste os resultados e publique a regra.

## Adicionar uma regra

1. No Administrador, vá para **Marketing** > SEO e pesquisa > **[!DNL Live Search]**.
1. Defina o **Escopo** para identificar a [exibição de repositório](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) onde a regra se aplica.
1. Clique no espaço de trabalho **Pesquisar Merchandising**.
1. Clique em **Adicionar regra** para iniciar o editor de regras.

## Tipo de regra

Uma Consulta de pesquisa é onde você define um termo de pesquisa, condições e tipos de classificação específicos.

Uma regra padrão pode ser definida, que é aplicada a todas as consultas, a menos que uma consulta de pesquisa mais específica seja definida. Somente uma regra padrão pode ser definida e não pode conter condições. Se você selecionar Padrão, a interface Condições não será exibida.
Escolha o tipo de classificação Inteligente padrão e qualquer classificação manual que quiser aplicar a todas as pesquisas padrão. As classificações manuais são sempre aplicadas.

## Condições

As condições são os requisitos para acionar um evento. Uma regra pode ter até dez condições e 25 eventos. Uma regra padrão não pode ter condições.

![Regra - Crie sua regra](assets/rules-add-workspace.png)

>[!NOTE]
>
>Atualmente, não é possível direcionar regras a um grupo de clientes específico.

### Condição única

1. Em *Criar sua regra*, selecione a **Condição** a ser atendida e siga as instruções para concluir a instrução.

   * A consulta de pesquisa contém - Digite a sequência de texto que deve estar na consulta do comprador. A configuração Corresponder determina o grau em que a consulta do comprador corresponde ao catálogo. Opções:<br /> Qualquer - Qualquer parte do texto de consulta do comprador pode corresponder à condição.<br />Todas - Todas as consultas do comprador devem corresponder à condição.
   * A consulta de pesquisa é - Digite uma sequência de texto que corresponda exatamente à consulta do comprador. Por exemplo: &quot;calças de ioga&quot;. Regras com `Search query is` e Correspondência `All` podem ter apenas uma condição.
   * Pesquisar consulta começa com - Insira um caractere ou sequência de texto que deve estar no início da consulta do comprador.
   * A consulta de pesquisa termina com - Digite um caractere ou sequência de texto que deve estar no final da consulta do comprador.

   Os resultados são exibidos imediatamente no painel *Testar sua regra* e são numerados por prioridade. Você pode usar o controle deslizante *Resultados por linha* na parte superior    direito para alterar o número de produtos em cada linha.

   ![Regra - simples](assets/rule-simple-test.png)

1. Para testar outras consultas, altere o texto da consulta na caixa de pesquisa *Testar sua regra* e pressione **Retornar**.
Inicialmente, o painel de teste renderiza a consulta na caixa de pesquisa Condições. Mas agora ele está renderizando a consulta a partir da caixa de query de teste. O painel de teste renderiza apenas uma consulta por vez.
1. Se você gostar do resultado, atualize o texto na caixa de pesquisa *Condições*. Em seguida, clique em qualquer lugar na página para atualizar os resultados no painel de teste.
1. Para criar uma regra simples com uma condição, vá para a Etapa 3: [Adicionar eventos](#events).

### Várias condições

1. Para criar uma regra com várias condições, clique em **Adicionar condição**.
Uma regra pode ter até dez condições. O operador lógico que junta duas condições se baseia na configuração *Correspondência* atual. Por padrão, *Correspondência* é `All` e o operador lógico é `AND`.

1. Selecione a segunda condição e insira o texto de consulta necessário.

1. Para alterar a lógica da regra, altere a configuração **Corresponder** para determinar com que proximidade os critérios de pesquisa do comprador devem corresponder à condição de consulta. Defina **Correspondência** para um dos seguintes:

   * Qualquer - (Padrão) Todos os operadores lógicos na regra são definidos como `OR` e os resultados são exibidos no painel de teste.
   * Todos - Todos os operadores lógicos na regra são definidos como `AND` e os resultados são exibidos no painel de teste.

   O valor *Match* determina o operador lógico usado para unir várias condições. A alteração da configuração *Correspondência* altera todos os operadores lógicos na regra. Não é possível combinar `AND` e `OR` na mesma regra.

   Neste exemplo, em vez de procurar por &quot;calças de ioga&quot;, há duas consultas separadas que procuram por &quot;ioga&quot; ou &quot;calças&quot;. Essa regra é menos específica e é acionada com mais frequência na loja do que na outra.

   ![Regras - Correspondência](assets/rules-match.png)

1. Para adicionar outra condição, clique em **Adicionar condição** e repita o processo.

## Classificação inteligente

A classificação inteligente combina comportamentos de usuário e estatísticas do site para determinar a classificação do produto.
Os proprietários de lojas podem configurar os seguintes tipos de estratégias de classificação:

![Regras - Correspondência](assets/rules-ranking-type.png)

* Mais comprados: classifica os produtos por total de compras por SKU nos 7 dias anteriores.
* Mais adicionados ao carrinho - Classificações na ordem do total de atividades &quot;Adicionar ao carrinho&quot; nos 7 dias anteriores.
* Mais visualizados: classificação do total de visualizações por SKU nos 7 dias anteriores.
* Recomendado para você - Usa o ponto de dados `viewed-viewed` - Os compradores que visualizaram este SKU também visualizaram esses outros SKUs.
* Tendência: retroage aos eventos de exibição de página nas últimas 72 horas para eventos em segundo plano e 24 horas para eventos em primeiro plano.
* Nenhum: os produtos são ordenados por Relevância.

Selecione o tipo de estratégia para a regra. A janela **Testar sua regra** exibe os resultados esperados.

### Avisos

* Apóstrofos e citações em queries podem levar a alguns problemas menores com classificação e relevância em alguns idiomas.
* Para garantir que a classificação inteligente funcione corretamente, verifique se o **Peso da Pesquisa** para qualquer atributo de produto usado para pesquisa ou filtragem (facetas) é `5` ou menos. Para localizar esta configuração no [!DNL Commerce] Admin:

   1. Selecione **Lojas** > _Atributos_ > **Produto**.
   1. Procure o atributo, como &quot;nome&quot;.
   1. Na página **Informações do Atributo** > **Propriedades da vitrine**, defina o peso da pesquisa como menor ou igual a `5`.

      ![Produto - Peso de Pesquisa](assets/set-search-weight.png)

## Classificação manual

Classificação manual (anteriormente conhecida como Eventos) são ações que modificam os resultados da pesquisa quando condições definidas são atendidas. Uma única regra pode ter até 25 eventos.

* Aumentar - Move um produto para cima nos resultados da pesquisa.
* Enterro - Move um SKU para baixo nos resultados da pesquisa.
* Fixar um produto - O produto é exibido na &quot;Posição&quot; selecionada na página.
* Ocultar um produto - Exclui um SKU dos resultados da pesquisa.

A maneira mais fácil de fixar um produto é arrastando e soltando.

1. Clique e arraste um produto no Painel de teste. Arraste e solte-o na posição desejada. Os campos Produto e Posição são automaticamente preenchidos no painel Eventos.

   ![Regras - Correspondência](assets/rule-event-pin-product.png)

Você também pode clicar no ícone de pino para fixar um produto no local atual. Use o menu de contexto de reticências para &quot;Fixar na parte superior&quot; ou &quot;Fixar na parte inferior&quot;.

>[!NOTE]
>
>Você só pode fixar produtos retornados na query.

Ou eventos podem ser definidos manualmente:

1. Em *Eventos*, escolha o **Evento** que ocorrerá quando as condições associadas forem atendidas.

   Por exemplo, escolha `Hide a product`. Em seguida, insira o nome do produto que deseja ocultar. Os produtos são sugeridos à medida que você digita.

1. Para vários eventos, escolha outros eventos que deseja acionar quando as condições forem atendidas.

## Detalhes adicionais

As informações inseridas aqui aparecem no painel [Detalhes da Regra](rules-workspace.md).

1. Em *Detalhes*, insira um **Nome** para a regra. Todos os nomes de regras devem ser exclusivos.
1. Insira uma breve **Descrição** da regra.
1. Insira a **Data de Início** e a **Data de Término** para que a regra fique ativa ou escolha as datas no calendário.

   Para selecionar um intervalo de datas, clique na primeira data e arraste para selecionar o intervalo.

   ![Regra - Concluída](assets/rule-add-details.png)

## Finalização da regra

1. Examine os resultados da regra no painel de teste.
1. Se a regra tiver várias consultas, teste cada uma que possa ser afetada pela regra.
1. Ao concluir, clique em **Salvar e publicar**.

   A regra é adicionada à lista no espaço de trabalho *Regras*.

1. Embora as regras ativas entrem em vigor imediatamente, talvez seja necessário aguardar até 15 minutos para que os resultados da consulta em cache na loja sejam atualizados.

>[!NOTE]
>
>As regras e os produtos classificados manualmente são aplicados aos resultados da pesquisa quando a ordem de classificação padrão, &quot;Classificar por: Mais relevante&quot;, é selecionada. Se um comprador alterar a ordem de classificação para algo como classificar por nome ou preço, as regras e as classificações manuais não estarão mais em vigor.

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
| Data de início | A data de início da regra, se programada. |
| Data final | A data final da regra, se programada. |
| Descrição | Uma breve descrição da regra. |
