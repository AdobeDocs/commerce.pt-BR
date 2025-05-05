---
title: Desempenho
description: O espaço de trabalho Desempenho [!DNL Live Search] fornece informações sobre os termos de pesquisa que os compradores usam.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Desempenho

O espaço de trabalho *Desempenho* fornece informações sobre os termos de pesquisa que os compradores usam. As informações podem ser usadas para identificar tendências, aumentar o click-through e melhorar o índice de conversão. O espaço de trabalho Desempenho fornece um instantâneo das métricas de pesquisa para um intervalo de datas específico e inclui os seguintes relatórios:

* Pesquisas únicas
* Zero resultados
* Resultados populares

![Desempenho](assets/performance-unique-searches.png)

Você também pode consultar o [Painel de gerenciamento de dados](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=pt-BR) para obter mais dados sobre a sincronização de dados.

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

| Dados de instantâneo | Descrição |
|--- |--- |
| Pesquisas únicas | O número total de pesquisas exclusivas para o intervalo de datas especificado. Várias pesquisas pelo mesmo comprador, mesmo para a mesma consulta, são consideradas exclusivas se enviadas com mais de uma hora de intervalo. |
| Taxa de cliques | A porcentagem de pesquisas que concluem com o comprador clicando em um produto. Por exemplo, a taxa de cliques é de 50% se o comprador procurar &quot;calças&quot; e &quot;camisa&quot; e clicar em um resultado na pesquisa &quot;camisa&quot;. |
| Índice de conversão | A porcentagem de produtos que o comprador compra em comparação ao número de produtos em que ele clica para o intervalo de datas especificado. Por exemplo, a taxa de conversão da interação é de 100% se o comprador visualizar seis produtos no popover, clicar em um e fizer uma compra. <br /><br />A taxa de conversão não é afetada pelo número de visualizações de um determinado produto. Por exemplo, a taxa de conversão permanecerá a mesma se o comprador usar pesquisa, mas não clicar em nenhum produto. |
| Taxa de resultados zero | A porcentagem de pesquisas exclusivas que não retorna resultados para o intervalo de datas especificado. Por exemplo, a taxa de resultados zero é de 66,67% se o comprador procurar &quot;fjjajfjfjf&quot; duas vezes (sem resultados) e &quot;calças&quot; uma vez (com resultados). |
| Média posição do clique | A posição relativa da taxa média de cliques com base em pesquisas exclusivas para o intervalo de datas especificado. |

| Relatórios | Descrição |
|--- |--- |
| Pesquisas únicas | Lista as consultas de pesquisa exclusivas usadas durante o intervalo de datas especificado. Os dados do relatório são calculados da mesma forma que os dados de instantâneo de pesquisa exclusiva. Se um comprador digitar a mesma consulta de pesquisa duas vezes, mas com mais de uma hora de diferença, a pesquisa será considerada duas pesquisas exclusivas. Limite de relatório: 500 termos principais |
| Zero resultados | Lista as consultas de pesquisa que não retornam resultados e o número de vezes usadas durante o intervalo de datas especificado. Limite de relatório: 500 termos principais |
| Resultados populares | Lista os nomes dos produtos que receberam mais visualizações durante o intervalo de datas especificado. Os resultados populares são calculados somente com base em impressões e não são afetados pelo número de cliques ou pela receita gerada. Limite de relatório: 500 termos principais |
