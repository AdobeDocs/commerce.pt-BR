---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
As origens de catálogo representam escopos autoritativos de produtos, atributos e categorias. Normalmente, eles mapeiam para limites de idioma, público-alvo ou sistema de origem e determinam o comportamento de pesquisa, filtragem e classificação.

## Origens do catálogo versus conceitos relacionados

Entender como as fontes de catálogo se relacionam com outros conceitos de serviços de merchandising ajuda a modelar os dados corretamente:

* **Origem do catálogo** - O contexto de dados subjacente que fornece informações sobre o produto. Uma origem de catálogo geralmente representa uma localidade (por exemplo, `en-US`, `fr-CA`) ou um contexto de dados fornecido por um sistema externo, como um PIM ou ERP. Produtos, metadados de atributos e categorias têm escopo por origem de catálogo. Uma origem de catálogo define a origem de dados brutos de catálogo e seu efeito na descoberta de produtos (resultados de pesquisa, filtragem e comportamento de classificação).

* **[Exibição de catálogo](/help/optimizer/setup/catalog-view.md)** - Uma exibição configurada do catálogo para uma necessidade comercial específica. Uma exibição de catálogo seleciona origens de catálogo (ou localidade), aplica [políticas](/help/optimizer/setup/policies.md) para filtrar a visibilidade dos produtos e associa [catálogos de preços](/help/optimizer/setup/pricebooks.md) à exibição. Uma única fonte de catálogo pode potencializar várias exibições de catálogo (por exemplo, uma fonte `en-US` com exibições de catálogo separadas para marcas ou regiões diferentes). Pense em uma exibição de catálogo como *como* você expõe esses dados para uma vitrine, canal ou público-alvo.

* **[Camada do catálogo](catalog-layer.md)** - Uma camada aplicada sobre os dados do catálogo base para modificar atributos do produto (nome, descrição, imagens, metadados) sem alterar os dados de origem. Use camadas de catálogo quando as diferenças afetarem somente a exibição da loja, não a descoberta de produtos.

## Como as origens de catálogo são preenchidas

As origens de catálogo são preenchidas por meio da assimilação de dados do catálogo. A forma como você fornece esses dados depende da sua implementação:

- **Adobe Commerce as a Cloud Service com CCDM**—A sincronização nativa fornece dados de catálogo do Commerce Foundation. Gerencie os produtos subjacentes e a configuração de exibição de loja no Commerce Foundation e monitore a sincronização no espaço de trabalho [Sincronização de dados](data-sync.md). Não é necessária nenhuma integração separada da API de assimilação de dados.
- **Adobe Commerce Optimizer com back-end de terceiros**—Sua integração fornece produtos e informações de origem do catálogo por meio da [API de assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).


## Regras e limitações

* Uma origem de catálogo é criada quando os dados de catálogo de um novo local ou sistema de origem são recebidos pela primeira vez pela camada de dados de Serviços de merchandising.
* A exclusividade do produto é determinada pela SKU + origem do catálogo.
* Os compradores não acessam diretamente as fontes do catálogo. Os dados do catálogo são expostos à loja através de [exibições do catálogo](catalog-view.md).

## Orientação de modelagem

Use as orientações a seguir ao planejar a estrutura do catálogo. Para o Adobe Commerce as a Cloud Service com CCDM, gerencie a configuração subjacente no Commerce Foundation em vez de criar fontes de catálogo por meio de uma integração de assimilação separada.

* Use uma fonte de catálogo separada para cada idioma do catálogo.
* Use fontes de catálogo separadas quando as diferenças de produto e atributo afetarem o comportamento de pesquisa, filtragem ou classificação, como configurações diferentes de capacidade de pesquisa ou filtragem.
* Use [camadas de catálogo](catalog-layer.md) quando as diferenças de produto e atributo afetarem a apresentação do produto sem alterar o comportamento de pesquisa, filtragem ou classificação.

>[!MORELIKETHIS]
>
> * [Exibições de catálogo](catalog-view.md) - Configure exibições filtradas e com preços na parte superior de uma origem de catálogo
> * [Camadas do catálogo](catalog-layer.md) - Modificar a apresentação do produto sem alterar os dados de origem
> * [Políticas](policies.md) - Criar filtros baseados em atributos para exibições de catálogo
> * [Catálogos de preços](/help/optimizer/setup/pricebooks.md) - Gerenciar estruturas de preços para diferentes segmentos de clientes
> * [Chaves de acesso restrito](restricted-access-keys.md) - Proteja uma exibição de catálogo com autenticação de token assinado
