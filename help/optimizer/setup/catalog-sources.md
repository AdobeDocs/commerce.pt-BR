---
title: Origens do catálogo
description: Saiba o que são as fontes de catálogo e como elas definem o escopo autoritativo de produtos, atributos e categorias para o comportamento de pesquisa, filtragem e classificação.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 94ba07437d532d0d101c166f58114c2aa0bd4be4
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 0%

---

# Origens do catálogo

As origens de catálogo representam escopos autoritativos de produtos, atributos e categorias. Normalmente, eles mapeiam para limites de idioma, público-alvo ou sistema de origem e determinam o comportamento de pesquisa, filtragem e classificação.

## Origens do catálogo versus conceitos relacionados

Entender como as fontes de catálogo se relacionam com outros conceitos do [!DNL Adobe Commerce Optimizer] ajuda a modelar seus dados corretamente:

* **Origem do catálogo** - O contexto de dados subjacente que fornece informações sobre o produto. Uma origem de catálogo normalmente é uma localidade (por exemplo, `en-US`, `fr-CA`) ou um sistema externo, como um PIM ou ERP. Produtos, atributos, metadados e categorias têm escopo por origem de catálogo. Pense em uma origem de catálogo como *de onde* os dados brutos do catálogo vêm e *como* eles afetam a descoberta de produtos (resultados de pesquisa, filtragem e comportamento de classificação).

* **[Exibição de catálogo](catalog-view.md)** - Uma exibição configurada do catálogo para uma necessidade comercial específica. Ao criar uma exibição de catálogo, você seleciona qual origem (ou localidade) de catálogo usar, adiciona [políticas](policies.md) para filtrar quais produtos estão visíveis e vincula [catálogos de preços](pricebooks.md) para controlar preços. Uma única fonte de catálogo pode potencializar várias exibições de catálogo (por exemplo, uma fonte `en-US` com exibições de catálogo separadas para marcas ou regiões diferentes). Pense em uma exibição de catálogo como *como* você expõe esses dados para uma vitrine, canal ou público-alvo.

* **[Camada do catálogo](catalog-layer.md)** - Uma camada aplicada sobre os dados do catálogo base para modificar atributos do produto (nome, descrição, imagens, metadados) sem alterar os dados de origem. Use camadas de catálogo quando as diferenças afetarem somente a exibição da loja, não a descoberta de produtos.

## Regras e limitações

* Cada origem de catálogo é criada ao assimilar um produto por meio da API de assimilação de dados. Consulte [Documentos do desenvolvedor - Assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) para obter mais informações.
* A exclusividade do produto é determinada pela SKU + origem do catálogo.
* Os compradores não acessam diretamente as fontes do catálogo. Os dados do catálogo são expostos à loja através de [exibições do catálogo](catalog-view.md).

## Orientação de modelagem

Use as orientações a seguir ao decidir como estruturar suas fontes de catálogo:

* Crie uma fonte de catálogo separada para cada idioma do catálogo.
* Use fontes de catálogo separadas quando as diferenças de produto e atributo afetarem o comportamento de pesquisa, filtragem ou classificação (por exemplo, capacidade de pesquisa, filtragem ou configuração de facetas diferentes para o mesmo atributo).
* Use [camadas de catálogo](catalog-layer.md) quando as diferenças de produto e atributo afetarem somente a exibição da loja, não a descoberta de produtos.

>[!MORELIKETHIS]
>
> * [Exibições de catálogo](catalog-view.md) - Configure exibições filtradas e com preços na parte superior de uma origem de catálogo
> * [Camadas do catálogo](catalog-layer.md) - Modificar a apresentação do produto sem alterar os dados de origem
> * [Políticas](policies.md) - Criar filtros baseados em atributos para exibições de catálogo
> * [Catálogos de preços](pricebooks.md) - Gerenciar estruturas de preços para diferentes segmentos de clientes

