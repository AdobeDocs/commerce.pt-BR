---
title: Criar e gerenciar regras
description: Saiba como criar e gerenciar regras de merchandising para páginas de pesquisa, listas de produtos padrão e de categoria.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
source-git-commit: 0d1ebaddada8be82645164368ebfbb6dd0a569cd
workflow-type: tm+mt
source-wordcount: '2714'
ht-degree: 0%

---

# Criar e gerenciar regras

Para criar uma regra, abra o editor de regras, escolha um **tipo de regra** (condições de pesquisa, listagem padrão ou páginas de categoria), defina condições e a classificação onde elas se aplicam, teste os resultados e publique a regra.

## Criar uma regra {#create-a-rule}

1. No painel à esquerda, vá para _Merchandising_ > **Regras de comercialização**.
1. (Opcional) Use a lista suspensa **Exibição de catálogo** para selecionar a exibição de catálogo à qual a regra deve se aplicar. O escopo da regra criada é o da exibição selecionada (ou de todas as exibições de catálogo se **Todas as exibições** estiver selecionado). Consulte [Selecionar exibição de catálogo](workspace.md#select-catalog-view) para saber como funciona o escopo de exibição de catálogo.

   >[!IMPORTANT]
   >
   >As exibições de catálogo estão atualmente em [beta](https://experienceleague.adobe.com/en/docs/commerce-operations/release/beta#merchandising-rules-globally-and-per-catalog-view-public-beta). Os participantes do Beta precisarão recriar quaisquer regras de merchandising existentes para aproveitar o novo escopo de exibição do catálogo.

1. Clique em **[!UICONTROL Create rule]** para iniciar o editor de regras.

![Criar regra](../../assets/create-rule.png)

### Tipos de regra

Cada tipo de regra tem um ícone de informações no editor com uma breve explicação. Use o tipo que corresponde ao local em que os compradores devem ver a lógica de merchandising:

| Tipo de regra | Finalidade |
| --- | --- |
| **Regra de todos os produtos** | Classificação e merchandising padrão em listas de produtos quando não há mais pesquisa específica ou regra de categoria aplicável. Você só pode criar uma dessas regras; ela não pode conter condições. |
| **Regra de categoria** (Beta) | Aplica merchandising e classificação a uma ou mais categorias selecionadas, controlando o pedido do produto nessas páginas de categoria. |
| **Regra de pesquisa** | Aplica merchandising e classificação quando os compradores executam uma pesquisa que corresponde às condições de consulta da regra. |

Na seção **Criar regra**, você define o nome da regra, o agendamento, se a regra se aplica a todas as listas ou a condições de pesquisa e tipos de classificação específicos.

1. No campo **[!UICONTROL Name]**, digite um nome para a regra. Todos os nomes de regras devem ser exclusivos.
1. No campo **[!UICONTROL Description]**, insira uma descrição para a regra.
1. No campo **[!UICONTROL Date range]**, especifique a data ou o intervalo de datas em que deseja que a regra fique ativa.
1. Na seção **[!UICONTROL Rule applies to]**, selecione o [tipo de regra](#rule-types) que deseja usar.

>[!BEGINTABS]

>[!TAB Regra de pesquisa]

Uma regra de pesquisa aplica lógica de merchandising e classificação quando os compradores realizam uma pesquisa que corresponde às condições definidas.

As condições são os requisitos para acionar um evento. Uma regra pode ter até dez condições e 25 eventos. Uma regra padrão não pode ter condições.

![Selecionar Condição de Regra](../../assets/rule-set-condition.png)

**Condição única**

1. Em *Criar sua regra*, selecione a **Condição** a ser atendida e siga as instruções para concluir a instrução.

   - A consulta de pesquisa contém - Digite a sequência de texto que deve estar na consulta do comprador. A configuração Corresponder determina o grau em que a consulta do comprador corresponde ao catálogo. Opções:<br /> Qualquer - Qualquer parte do texto de consulta do comprador pode corresponder à condição.<br />Todas - Todas as consultas do comprador devem corresponder à condição.
   - A consulta de pesquisa é - Digite uma sequência de texto que corresponda exatamente à consulta do comprador. Por exemplo: &quot;calças de ioga&quot;. Regras com `Search query is` e Correspondência `All` podem ter apenas uma condição.
   - Pesquisar consulta começa com - Insira um caractere ou sequência de texto que deve estar no início da consulta do comprador.
   - A consulta de pesquisa termina com - Digite um caractere ou sequência de texto que deve estar no final da consulta do comprador.

   Os resultados são exibidos imediatamente no painel *Testar sua regra* e são numerados por prioridade. Você pode usar o controle deslizante *Resultados por linha* no canto superior direito para alterar o número de produtos em cada linha.

1. Para testar outras consultas, altere o texto da consulta na caixa de pesquisa *Testar sua regra* e pressione **Retornar**.
Inicialmente, o painel de teste renderiza a consulta na caixa de pesquisa Condições. Mas agora ele está renderizando a consulta a partir da caixa de query de teste. O painel de teste renderiza apenas uma consulta por vez.
1. Se você gostar do resultado, atualize o texto na caixa de pesquisa *Condições*. Em seguida, clique em qualquer lugar na página para atualizar os resultados no painel de teste.
1. Defina a [Classificação inteligente](#intelligent-ranking) e a [Classificação manual](#manual-ranking) conforme descrito nas seções a seguir. Os mesmos controles se aplicam às páginas de categoria, com todas as diferenças chamadas.

**Várias condições**

1. Para criar uma regra com várias condições, clique em **Adicionar condição**.
Uma regra pode ter até dez condições. O operador lógico que junta duas condições se baseia na configuração *Correspondência* atual. Por padrão, *Correspondência* é `All` e o operador lógico é `AND`.

1. Selecione a segunda condição e insira o texto de consulta necessário.

1. Para alterar a lógica da regra, altere a configuração **Corresponder** para determinar com que proximidade os critérios de pesquisa do comprador devem corresponder à condição de consulta. Defina **Correspondência** para um dos seguintes:

   - Qualquer - (Padrão) Todos os operadores lógicos na regra são definidos como `OR` e os resultados são exibidos no painel de teste.
   - Todos - Todos os operadores lógicos na regra são definidos como `AND` e os resultados são exibidos no painel de teste.

   O valor *Match* determina o operador lógico usado para unir várias condições. A alteração da configuração *Correspondência* altera todos os operadores lógicos na regra. Não é possível combinar `AND` e `OR` na mesma regra.

   Neste exemplo, em vez de procurar por &quot;calças de ioga&quot;, há duas consultas separadas que procuram por &quot;ioga&quot; ou &quot;calças&quot;. Essa regra é menos específica e é acionada com mais frequência na loja do que na outra.

1. Para adicionar outra condição, clique em **Adicionar condição** e repita o processo.
1. Defina a [Classificação inteligente](#intelligent-ranking) e a [Classificação manual](#manual-ranking) conforme descrito nas seções a seguir. Os mesmos controles se aplicam às páginas de categoria, com todas as diferenças chamadas.

>[!TAB Regra de categoria]

>[!IMPORTANT]
>
>As regras de categoria estão na versão beta.

As regras de categoria controlam como os produtos são ordenados em **páginas de categoria**. Você combina **regras de categoria** com **classificação inteligente** (incluindo sinais orientados por IA) e **ações manuais**, como fixar, aumentar e enterrar, para poder preparar descobertas, executar promoções e alinhar páginas de categoria com a sua estratégia sem depender de ferramentas externas.

1. Em **Categorias**, selecione a(s) categoria(s) à(s) qual(is) a regra deve ser aplicada. As categorias selecionadas aparecem abaixo do controle para que você possa confirmar o escopo.
1. Na lista de categorias exibida, clique nos três pontos e selecione para:

   - **Excluir** - Remove a categoria da regra.
   - **Aplicar às subcategorias** - Aplica a regra às subcategorias que ainda não têm uma regra de merchandising ativa definida.
   - **Visualizar** - mostra como a página de categoria apareceria na sua vitrine.

1. Defina a [Classificação inteligente](#intelligent-ranking) e a [Classificação manual](#manual-ranking) conforme descrito nas seções a seguir. Os mesmos controles se aplicam às regras de pesquisa, com todas as diferenças chamadas.

>[!ENDTABS]

### Classificação inteligente {#intelligent-ranking}

A classificação inteligente solicita produtos usando **sinais comportamentais** e, quando aplicável, IA. Aplica-se a **regras de pesquisa**, **todas as listas de produtos** (regras padrão) e **regras de categoria** (páginas de categoria). Para **pesquisas** do comprador, a classificação também pesa **relevância textual** para a consulta; as **páginas de categoria** não usam o texto da consulta da mesma maneira; o editor focaliza estratégias comportamentais.

Os proprietários de lojas podem definir estratégias como as seguintes. Os rótulos exatos e as janelas de tempo correspondem ao editor de regras e podem ser um pouco diferentes de acordo com o tipo de regra.

![Classificações inteligentes](../../assets/rule-intelligent-ranking.png)

- **Mais comprados** / **Mais comprados** — Classificações por frequência de compra por SKU em uma janela recente (por exemplo, os 7 dias anteriores para contextos de pesquisa).
- **Mais adicionados ao carrinho** — Classificações por atividade total de adição ao carrinho em uma janela recente (por exemplo, os 7 dias anteriores para contextos de pesquisa).
- **Mais visualizados** — Classificações por exibições por SKU em uma janela recente (por exemplo, os 7 dias anteriores para contextos de pesquisa).
- **Recomendado para você** — Usa o sinal `viewed-viewed`: os compradores que visualizaram este SKU também visualizaram outros SKUs; oferece suporte à ordenação personalizada em páginas de categoria, quando disponíveis.
- **Tendências** — enfatiza a popularidade recente (para pesquisa, exibições de página nas últimas 72 horas para eventos em segundo plano e 24 horas para eventos em primeiro plano).
- **Nenhum** — Para pesquisa e listagens padrão, os produtos são ordenados por **Relevância**. Para **regras de categoria**, o usa a ordem de merchandising padrão para a categoria quando você não escolhe outra estratégia inteligente.

Selecione a estratégia para sua regra. O painel **Testar sua regra** mostra os resultados esperados para regras orientadas por pesquisa; as **regras de categoria** usam a visualização de categoria.

#### Como funciona a pontuação inteligente de classificação (pesquisa)

Para **resultados de pesquisa** (e a consulta de teste no editor de regras), a classificação inteligente determina a ordem final do produto ao combinar dois fatores principais: **relevância textual** e **sinais comportamentais**. Entender como esses fatores interagem ajuda a definir expectativas realistas para os resultados da pesquisa.

**Componentes de pontuação:**

- **Relevância textual**: o fator dominante na pontuação. Isso mede o nível de correspondência entre o nome, a descrição e os atributos de um produto e a consulta de pesquisa. A pontuação de relevância do texto é ilimitada (não tem limite superior específico) e é influenciada por fatores como:

   - Frequência de ocorrência de palavras correspondentes.
   - Comprimento (por palavras) dos nomes/descrições dos produtos.

- **Sinais comportamentais**: um aumento limitado aplicado sobre a pontuação de relevância do texto. Ao selecionar uma estratégia de classificação inteligente como &quot;Mais visualizados&quot; ou &quot;Mais comprados&quot;, os produtos com sinais comportamentais mais altos recebem um aumento fixo em suas pontuações. No entanto, esse reforço tem um limite definido.

**Por que o produto mais exibido pode não aparecer primeiro:**

A relevância textual normalmente domina a classificação porque sua pontuação é ilimitada, enquanto os aumentos comportamentais são fixos. Como resultado, os produtos com texto forte corresponde muitas vezes mais do que aqueles com sinais de engajamento mais altos. Os aumentos comportamentais por si só podem não compensar grandes lacunas na relevância do texto. A classificação inteligente aborda isso considerando a qualidade da correspondência e a interação do comprador, melhorando a relevância geral. No entanto, a qualidade da correspondência de texto continua sendo o principal impulsionador da classificação.

**Exemplo:**

Um comerciante usa a estratégia de classificação inteligente &quot;Mais visto&quot; e pesquisa por &quot;vela&quot;. Eles esperam que o SKU YAN-K-E-512 do produto apareça no topo dos resultados porque ele tem a maior contagem de visualizações. No entanto, outros produtos têm classificação mais alta:

- **Vela do Texas** (1ª posição): tem um nome de produto mais curto e limpo que cria uma pontuação de relevância de texto muito alta. Mesmo que tenha menos visualizações do que YAN-K-E-512, sua correspondência de texto superior supera o impulso comportamental.

- **YAN-K-E-512** (posição inferior): apesar de ter o maior percentil de exibição nos dados comportamentais &quot;Mais visualizados&quot;, seu nome complexo baseado em SKU gera uma pontuação de relevância de texto mais baixa. O impulso comportamental fixo não é suficiente para superar essa lacuna de relevância do texto.

Consulte [regras de pesquisa](./best-practice.md#tips-to-optimize-search-rules) para saber como melhorar a localização de produtos usando regras.

#### Avisos

- Apóstrofos e citações em queries podem levar a alguns problemas menores com classificação e relevância em alguns idiomas.
- Para garantir que a classificação inteligente funcione corretamente para **pesquisa**, verifique se o **Peso de Pesquisa** para qualquer atributo usado para pesquisa ou filtragem (facetas) é `5` ou menos. (Esta orientação se aplica à indexação de pesquisa, não a fluxos de merchandising somente de categoria.)

Para obter informações sobre como definir pesos de pesquisa, consulte a [API de metadados](https://developer.adobe.com/commerce/services/reference/rest/).

### Classificação manual {#manual-ranking}

Os eventos de **Classificação manual** ajustam o pedido de produtos para **resultados de pesquisa** (quando as condições da sua regra são atendidas), para **listas de produtos padrão** e para as listas da **página de categoria**. Uma única regra pode ter até 25 eventos.

- **Aumentar** — Move um produto para uma posição superior na lista.
- **Busca** — Move uma SKU para baixo na listagem.
- **Fixar um produto** — Corrige um produto na posição selecionada na lista.
- **Ocultar um produto** — Exclui uma SKU dos resultados (orientado para pesquisa; confirmar comportamento para regras de categoria no editor).

A maneira mais fácil de fixar um produto é arrastando e soltando.

1. Clique e arraste um produto no Painel de teste. Arraste e solte-o na posição desejada. Os campos Produto e Posição são automaticamente preenchidos no painel Eventos.

Você também pode clicar no ícone de pino para fixar um produto no local atual. Use o menu de contexto de reticências para &quot;Fixar na parte superior&quot; ou &quot;Fixar na parte inferior&quot;.

>[!NOTE]
>
>**Regras de pesquisa** — Você só pode fixar produtos que aparecem nos resultados da pesquisa para a consulta configurada e as condições da regra. Os produtos devem ser indexados, visíveis, em estoque e atender a todos os filtros de regra para terem direito a fixação. Se um produto não aparecer na visualização ou nos resultados da regra, a fixação não terá efeito.
>
>**Classificação padrão** — As posições manuais se aplicam quando o comprador usa a classificação padrão: **Classificar por: Mais Relevante** para pesquisa ou **relevância** / **posição** para listagens de categoria. Se o comprador mudar de classificação; por exemplo, por nome, o comportamento fixado, impulsionado, enterrado ou oculto pode não corresponder mais à visualização.

Ou eventos podem ser definidos manualmente:

1. Em *Eventos*, escolha o **Evento** que ocorrerá quando as condições associadas forem atendidas.

   Por exemplo, escolha `Hide a product`. Em seguida, insira o nome do produto que deseja ocultar. Os produtos são sugeridos à medida que você digita.

1. Para vários eventos, escolha outros eventos que deseja acionar quando as condições forem atendidas.

### Finalização da regra {#finalizing-the-rule}

1. Examine os resultados da regra no painel de teste.
1. Se a regra tiver várias consultas, teste cada uma que possa ser afetada pela regra.
1. Ao concluir, clique em **Salvar e publicar**.

   A regra é adicionada à lista no espaço de trabalho *Regras*.

1. Embora as regras ativas entrem em vigor imediatamente, talvez seja necessário aguardar até 15 minutos para que os resultados da consulta em cache na loja sejam atualizados.

>[!NOTE]
>
>As regras e os produtos classificados manualmente são aplicados aos resultados da **pesquisa** quando a ordem de classificação padrão, &quot;Classificar por: Mais Relevante&quot;, é selecionada. Se um comprador alterar a ordem de classificação para algo como classificar por nome, as regras e as classificações manuais não estarão mais em vigor. Para as listagens de **categoria**, o comportamento de classificação padrão é descrito em [Classificação manual](#manual-ranking).

## Editar, exibir e excluir regras {#edit-view-and-delete-rules}

Siga estas instruções para atualizar as propriedades das regras existentes. Não é possível alterar a exibição de catálogo (escopo) de uma regra após sua criação; o escopo é definido quando você cria a regra. Consulte [Selecionar exibição de catálogo](workspace.md#select-catalog-view).

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

## Descrições dos campos {#field-descriptions}

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

### Eventos de classificação manual

| Evento | Descrição |
|--- |--- |
| Aumentar | Move um SKU ou intervalo de SKUs para cima na lista (pesquisa ou categoria). Cada uma é marcada com um selo de visualização &quot;impulsionado&quot; nos resultados do teste. |
| Enterro | Move um SKU ou intervalo de SKUs para baixo na lista. Cada uma está marcada com um selo de visualização &quot;enterrado&quot; nos resultados do teste. |
| Fixar um produto | Anexa um único SKU a uma posição específica na lista. O produto é marcado com um selo de visualização &quot;fixado&quot; nos resultados do teste. |
| Ocultar um produto | Exclui um SKU, ou intervalo de SKUs, dos resultados (orientado para pesquisa; confirme as regras de categoria no editor). |

### Detalhes

| Campo | Descrição |
|--- |--- |
| Nome | O nome da regra. Rule names must be unique. |
| Tipo de regra | **Padrão** (todas as listas de produtos), **Consulta** (condições de pesquisa específicas) ou **Categoria** (páginas de categoria), dependendo da **Regra aplica-se a**. |
| Data inicial | A data de início da regra, se programada. |
| Data final | A data final da regra, se programada. |
| Descrição | Uma breve descrição da regra. |
