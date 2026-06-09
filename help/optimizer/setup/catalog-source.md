---
title: Origem do catálogo
description: Saiba o que são as fontes de catálogo e como elas definem o escopo autoritativo de produtos, atributos e categorias para o comportamento de pesquisa, filtragem e classificação.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Origem do catálogo

Uma origem de catálogo representa um escopo autoritativo de produtos, atributos e categorias. As fontes de catálogo normalmente mapeiam para limites de idioma, público-alvo ou sistema de origem e determinam o comportamento de pesquisa, filtro e classificação.

## Origem do catálogo versus conceitos relacionados

Entender como uma fonte de catálogo se relaciona a outros conceitos do [!DNL Adobe Commerce Optimizer] ajuda a modelar os dados corretamente:

* **Origem do catálogo** - O contexto de dados subjacente que fornece informações sobre o produto. Uma origem de catálogo normalmente é uma localidade (por exemplo, `en-US`, `fr-CA`) ou um sistema externo, como um PIM ou ERP. Produtos, atributos, metadados e categorias têm escopo por origem de catálogo. Pense em uma origem de catálogo como *de onde* os dados brutos do catálogo vêm e *como* eles afetam a descoberta de produtos (resultados de pesquisa, filtragem e comportamento de classificação).

* **[Exibição de catálogo](catalog-view.md)** - Uma exibição configurada do catálogo para uma necessidade comercial específica. Ao criar uma exibição de catálogo, você seleciona qual origem (ou localidade) de catálogo usar, adiciona [políticas](policies.md) para filtrar quais produtos estão visíveis e vincula [catálogos de preços](pricebooks.md) para controlar preços. Uma única fonte de catálogo pode potencializar várias exibições de catálogo (por exemplo, uma fonte `en-US` com exibições de catálogo separadas para marcas ou regiões diferentes). Pense em uma exibição de catálogo como *como* você expõe esses dados para uma vitrine, canal ou público-alvo.

* **[Camada do catálogo](catalog-layer.md)** - Uma camada aplicada sobre os dados do catálogo base para modificar atributos do produto (nome, descrição, imagens, metadados) sem alterar os dados de origem. Use camadas de catálogo quando as diferenças afetarem somente a exibição da loja, não a descoberta de produtos.

## Regras e limitações

* Uma origem de catálogo é criada ao assimilar um produto por meio da API de assimilação de dados. Consulte [Documentos do desenvolvedor - Assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) para obter mais informações.
* A exclusividade do produto é determinada pela SKU + origem do catálogo.
* Os compradores não acessam diretamente as fontes do catálogo. Os dados do catálogo são expostos à loja através de [exibições do catálogo](catalog-view.md).

## Orientação de modelagem

Use as orientações a seguir ao decidir como estruturar suas fontes de catálogo:

* Crie uma fonte de catálogo separada por idioma de catálogo diferente.
* Use fontes de catálogo separadas quando as diferenças de produto e atributo afetarem o comportamento de pesquisa, filtragem ou classificação (por exemplo, capacidade de pesquisa, filtragem ou configuração de facetas diferentes para o mesmo atributo).
* Use [camadas de catálogo](catalog-layer.md) quando as diferenças de produto e atributo afetarem somente a exibição da loja, não a descoberta de produtos.

>[!MORELIKETHIS]
>
> * [Exibições de catálogo](catalog-view.md) - Configure exibições filtradas e com preços na parte superior de uma origem de catálogo
> * [Camadas do catálogo](catalog-layer.md) - Modificar a apresentação do produto sem alterar os dados de origem
> * [Políticas](policies.md) - Criar filtros baseados em atributos para exibições de catálogo
> * [Catálogos de preços](pricebooks.md) - Gerenciar estruturas de preços para diferentes segmentos de clientes
