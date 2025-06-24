---
title: Práticas recomendadas dos aspectos
description: Conheça as práticas recomendadas para implementar aspectos na sua loja.
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Práticas recomendadas dos aspectos

A funcionalidade de filtro e faceta é um componente crítico do site [!DNL Adobe Commerce Optimizer], projetada para aprimorar a experiência do comprador permitindo que ele restrinja os resultados da pesquisa e localize produtos com mais eficiência. Essa funcionalidade ajuda os compradores a classificar grandes catálogos de itens aplicando critérios específicos, tornando o processo de compra mais rápido, fácil e satisfatório. Ao implementar filtros e facetas eficazes e fáceis de comprar, você pode ajudar os clientes a encontrar exatamente o que precisam de maneira rápida e eficiente, aumentando, em última análise, as taxas de satisfação e conversão.

## Dicas para otimizar aspectos

- Determine os atributos mais relevantes e úteis para seus produtos, como título, categoria, marca, faixa de preços, cor e tamanho, e defina-os como [facetas dinâmicas](type.md). 
- Defina e classifique atributos de produto que sejam consistentes em todo o catálogo e altamente relevantes para seus produtos, a fim de melhorar a relevância e os recursos de filtragem para seus compradores.
- Verifique se os rótulos de facetas são fáceis de entender e nomeados de forma consistente em todo o site. Por exemplo, use &quot;Intervalo de preços&quot; em vez de &quot;Custo&quot;.
- Evite sobrecarregar os compradores, limitando o número de facetas às mais importantes. Muitas opções podem causar fadiga de decisão. Por padrão, [!DNL Adobe Commerce Optimizer] está limitado a no máximo 100 atributos configurados como facetas e 30 compartimentos retornados em cada faceta. Saiba mais sobre [limitações de facetas](../../boundaries-limits.md#catalog-views-and-policies). 
- Permite que os compradores selecionem vários critérios de filtro simultaneamente para refinar os resultados. Por exemplo, permitir que os compradores selecionem as cores &quot;Vermelho&quot; e &quot;Azul&quot;.
- Exiba o número de produtos disponíveis ao lado de cada opção de faceta para dar aos compradores uma ideia dos resultados de pesquisa que eles podem esperar.
- Implemente seções de facetas recolhíveis para manter a interface limpa e gerenciável, especialmente em dispositivos móveis.
- Permita que os compradores redefinam facilmente facetas individuais ou todos os filtros selecionados para iniciar uma nova pesquisa.
- Se você tiver um grande número de atributos com os quais lidar, considere combinar atributos em um único &quot;metatributo&quot;. Por exemplo, sapatos geralmente têm tamanhos numéricos, enquanto camisas são comumente dimensionadas &quot;S/M/L/XL&quot;. Esses dois tipos de tamanhos podem ser combinados em um único atributo pesquisável.
