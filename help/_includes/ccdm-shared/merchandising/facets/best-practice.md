---
source-git-commit: bc3ebc0514874b9678e8b632cc2c48102959d439
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%
---
# Práticas recomendadas dos aspectos

A funcionalidade de filtro e faceta é um componente essencial das experiências do Commerce, projetada para aprimorar a experiência do comprador, permitindo que os compradores restrinjam os resultados de pesquisa e localizem produtos com mais eficiência. Essa funcionalidade ajuda os compradores a classificar grandes catálogos de itens aplicando critérios específicos, tornando o processo de compra mais rápido, fácil e satisfatório. Ao implementar filtros e facetas eficazes e fáceis de comprar, você pode ajudar os clientes a encontrar exatamente o que precisam de maneira rápida e eficiente, aumentando, em última análise, as taxas de satisfação e conversão.

## Dicas para otimizar aspectos

- Determine atributos relevantes do produto, como título, categoria, marca, faixa de preços, cor e tamanho, e defina-os como [facetas dinâmicas](type.md). 
- Defina e classifique atributos de produto que sejam consistentes em todo o catálogo e altamente relevantes para seus produtos, a fim de melhorar a relevância e os recursos de filtragem para seus compradores.
- Verifique se os rótulos de facetas são fáceis de entender e nomeados de forma consistente em todo o site. Por exemplo, use `Price Range` em vez de `Cost`.
- Evite sobrecarregar os compradores, limitando o número de facetas às mais importantes. Muitas opções podem causar fadiga de decisão. A configuração de facetas aceita até 100 atributos configurados como facetas e até 100 valores por faceta. Saiba mais sobre [limitações de facetas](/help/optimizer/boundaries-limits.md#product-discovery).
- Permite que os compradores selecionem vários critérios de filtro simultaneamente para refinar os resultados. Por exemplo, permitir que os compradores selecionem as cores &quot;Vermelho&quot; e &quot;Azul&quot;.
- Exiba o número de produtos disponíveis ao lado de cada opção de faceta para dar aos compradores uma ideia dos resultados de pesquisa que eles podem esperar.
- Para manter a interface limpa e gerenciável, especialmente em dispositivos móveis, implemente seções de facetas recolhíveis.
- Permite que os compradores redefinam facetas individuais ou todos os filtros selecionados para iniciar uma nova pesquisa facilmente.
- Se você tiver um grande número de atributos, considere combinar atributos em um único metatributo. Por exemplo, sapatos têm tamanhos numéricos, enquanto camisas são comumente dimensionadas &quot;S/M/L/XL&quot;. Esses dois tipos de tamanhos podem ser combinados em um único atributo pesquisável.
