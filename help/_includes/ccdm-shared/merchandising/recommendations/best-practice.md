---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.pt-BR/blob/main/help/_includes/ccdm-shared/merchandising/recommendations/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Práticas recomendadas do Recommendations

A Adobe recomenda as seguintes diretrizes ao usar as recomendações:

- Diversifique seus tipos de recomendação. Os clientes começam a ignorar as recomendações se sugerirem os mesmos produtos repetidamente.

- Não implante as mesmas recomendações na página do carrinho e na página de confirmação de pedido. Considere usar `Most Added to Cart` para a página do carrinho e `Bought This, Bought That` para a página de confirmação de pedido.

- Mantenha seu site organizado. Não implante mais de três unidades de recomendação na mesma página.

- Se sua loja vende roupas, a recomendação `More like this` pode sugerir produtos específicos de gênero que não correspondem ao gênero do produto que está sendo visualizado. Considere usar esse tipo de recomendação somente para categorias que não sejam de roupas.

## Posicionamento

Com tantos tipos de recomendações para escolher, qual você deve usar em cada página? Se não tiver certeza de onde começar, tente o seguinte:

| Página | Tipo de recomendação |
|---|---|
| Home page | `Recommended for you` |
| Página do produto | `Viewed this, viewed that` |
| Carrinho | `Bought this, bought that` |

Você pode acompanhar as [métricas](/help/optimizer/manage-results/recommendation-performance.md) e ajustar, se necessário. Lembre-se de que a experimentação é a chave.

## Rótulos de recomendação

O rótulo atribuído a uma recomendação na loja afeta como os compradores interpretam sua relevância para eles. Os rótulos a seguir são usados com frequência para cada tipo de recomendação.

| Tipo de recomendação | Rótulos recomendados |
|---|---|
| Mais visualizados<br> Mais adicionados ao carrinho<br>Mais comprados<br>Conversão (exibir para carrinho)<br>Conversão (exibir para compra) | <br>Itens mais populares<br>Tendências<br>Populares no momento<br>Recentemente populares<br>Itens populares inspirados por este item (PDP)<br>Mais vendidos<br>Talvez você esteja interessado em |
| Recomendado para você | Apenas para você<br>Recomendado para você<br>Inspirado pelas suas tendências de compras |
| Visualizou Isso, Visualizou Aquilo | Os clientes que visualizaram este item também visualizaram<br>Os clientes também visualizaram<br>itens relacionados |
| Visualizou Isto, Comprou Aquilo | Clientes que visualizaram este item acabaram comprando<br>Clientes comprados<br>O que outros compram depois de visualizar este item? |
| Comprei isto, comprei aquilo | Obtenha tudo o que precisa<br>Não se esqueça disso<br>Comprados com frequência |
| Mais artigos como este | Mais itens como este<br>Semelhantes a este |
| Genérico | Você também pode gostar de<br>Compradores também curtiram<br>Opções semelhantes<br>Itens relacionados |
| Tendências | Tendências<br>Tendências atuais<br>Tendências recentes<br>Itens importantes<br>Produtos relacionados às tendências (PDP) |
| Visualizado recentemente | Visualizado recentemente<br>Dê outra olhada |
