---
title: Desempenho
description: O espaço de trabalho Desempenho [!DNL Live Search] fornece o insight nos termos de pesquisa que os compradores usam.
exl-id: 07a63df8-b981-4913-841a-7e81ec634281
source-git-commit: 5978a400d985e3099962af8bcefdd6f29f687d67
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Desempenho

O espaço de trabalho *Desempenho* fornece o insight nos termos de pesquisa que os compradores usam. As informações podem ser usadas para identificar tendências, aumentar o click-through e melhorar o índice de conversão. O espaço de trabalho Desempenho fornece um instantâneo das métricas de pesquisa para um intervalo de datas específico e inclui os seguintes relatórios:

* Pesquisas únicas
* Zero resultados
* Resultados populares

![Desempenho](assets/performance-unique-searches.png)

Você também pode consultar o [Painel de gerenciamento de dados](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) para obter mais dados sobre a sincronização de dados.

>[!NOTE]
>
>O espaço de trabalho de desempenho é atualizado a cada 12 horas.

## Exibir um relatório

1. Para inserir o **Intervalo de datas**, clique no calendário (![Calendário](assets/btn-calendar.png)) e siga um destes procedimentos:

   * Para especificar uma única data, clique duas vezes na data no calendário.
   * Para especificar um intervalo de datas, clique na primeira e na última data do calendário.

>[!NOTE]
>
>O intervalo de datas não pode exceder um ano.

## Descrições dos campos

| Dados de instantâneo | Descrição | Exemplo de cálculo |
|--- |--- |--- |
| Pesquisas únicas | O número total de pesquisas exclusivas para o intervalo de datas especificado. Várias pesquisas pelo mesmo comprador, mesmo para a mesma consulta, são consideradas exclusivas se enviadas com mais de uma hora de intervalo. | **Exemplo:**<br /> Pesquisas:<br />- &quot;calças&quot; às 10:00 AM<br />- &quot;calças&quot; às 10:30 AM (em 1 hora → não exclusivo)<br />- &quot;calças&quot; às 12:00 PM (após 1 hora → exclusivo)<br />- &quot;camisa&quot; às 1:00 PM <br /><br />**Total de pesquisas exclusivas = 3** |
| Índice de click-through | A porcentagem de pesquisas que concluem com o comprador clicando em um produto. Por exemplo, a taxa de cliques é de 50% se o comprador procurar &quot;calças&quot; e &quot;camisa&quot; e clicar em um resultado na pesquisa &quot;camisa&quot;. | **Fórmula:**<br /> Taxa de click-through = Pesquisas com ≥1 clique ÷ Total de pesquisas exclusivas <br /><br />**Exemplo:**<br /> Total de pesquisas exclusivas = 4<br />Pesquisas com pelo menos um clique = 2<br /><br />CTR = 2 ÷ 4 = **50%** |
| Índice de conversão | A porcentagem de produtos que o comprador compra em comparação ao número de produtos em que ele clica para o intervalo de datas especificado. Por exemplo, a taxa de conversão da interação é de 100% se o comprador visualizar seis produtos no popover, clicar em um e fizer uma compra. <br /><br />A taxa de conversão não é afetada pelo número de visualizações de um determinado produto. Por exemplo, a taxa de conversão permanecerá a mesma se o comprador usar pesquisa, mas não clicar em nenhum produto. | **Fórmula:**<br /> Taxa de conversão = Total de produtos comprados ÷ Total de produtos clicados <br /><br />**Exemplo 1:**<br /> Produtos clicados = 5<br />Produtos comprados = 2<br /><br />CVR = 2 ÷ 5 = **40%**<br /><br />**Exemplo 2 (agregação de 5 horas):**<br /> Cliques por hora: 4, 5, 6, 10, 2<br />Compras por hora: 1, 3, 0, 4, 1<br /><br />Total de cliques = 4 + 5 + 6 + 10 + 2 = 27<br />Total de compras = 1 + 3 + 0 + 4 + 1 = 9<br /><br />CVR = 9 ÷ 27 = **33,33%** |
| Taxa de resultados zero | A porcentagem de pesquisas exclusivas que não retorna resultados para o intervalo de datas especificado. Por exemplo, a taxa de resultados zero é de 66,67% se o comprador procurar &quot;fjjajfjfjf&quot; duas vezes (sem resultados) e &quot;calças&quot; uma vez (com resultados). | **Fórmula:**<br /> Taxa de resultados zero = Pesquisas exclusivas com zero resultados ÷ Total de pesquisas exclusivas <br /><br />**Exemplo:**<br /> Total de pesquisas exclusivas = 3<br />Pesquisas com zero resultados = 2<br /><br />Taxa de resultados zero = 2 ÷ 3 = **66.67%** |
| Média posição do clique | A posição relativa da taxa média de cliques com base em pesquisas exclusivas para o intervalo de datas especificado. | **Fórmula:**<br /> Posição média do clique = Soma das posições do clique ÷ Total de cliques <br /><br />**Exemplo:**<br /> Cliques nas posições: 1, 3, 2<br /><br />Posição média do clique = (1 + 3 + 2) ÷ 3 = **2** |

| Relatórios | Descrição |
|--- |--- |
| Pesquisas únicas | Lista as consultas de pesquisa exclusivas usadas durante o intervalo de datas especificado. Os dados do relatório são calculados da mesma forma que os dados de instantâneo de pesquisa exclusiva. Se um comprador digitar a mesma consulta de pesquisa duas vezes, mas com mais de uma hora de diferença, a pesquisa será considerada duas pesquisas exclusivas. <br />**Limite de relatório:** os 500 termos principais ao gerar o arquivo CSV. |
| Zero resultados | Lista as consultas de pesquisa que não retornam resultados e o número de vezes usadas durante o intervalo de datas especificado. <br />**Limite de relatório:** os 500 termos principais ao gerar o arquivo CSV. |
| Resultados populares | Lista os nomes dos produtos que receberam mais visualizações durante o intervalo de datas especificado. Os resultados populares são calculados somente com base em impressões e não são afetados pelo número de cliques ou pela receita gerada. <br />**Limite de relatório:** os 500 termos principais ao gerar o arquivo CSV. |
