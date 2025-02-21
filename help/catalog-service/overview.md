---
title: '[!DNL Catalog Service]'
description: O [!DNL Catalog Service] for Adobe Commerce fornece uma maneira de recuperar o conteúdo das Páginas de Exibição de Produtos e das Páginas de Listas de Produtos com muito mais rapidez do que as consultas nativas do Adobe Commerce GraphQL.
role: Admin, Developer
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---


# [!DNL Catalog Service] para Adobe Commerce

A extensão do [!DNL Catalog Service] para Adobe Commerce fornece dados avançados de catálogo do modelo de exibição (somente leitura) para renderizar experiências de vitrine relacionadas ao produto de maneira rápida e completa, incluindo:

* Páginas de detalhes do produto
* Páginas de lista de produtos e categoria
* Páginas de resultados da pesquisa
* Carrosséis de produtos
* Páginas de comparação do produto
* Qualquer outra página que renderize dados do produto, como carrinho, pedido e páginas de lista de desejos

O [!DNL Catalog Service] usa o [GraphQL](https://graphql.org/) para solicitar e receber dados de catálogo, incluindo produtos, atributos de produto, estoque e preços. O GraphQL é uma linguagem de consulta que um cliente de front-end usa para se comunicar com a API (interface de programação de aplicativos) definida em um back-end, como o Adobe Commerce. O GraphQL é um método de comunicação popular porque é leve e permite que um integrador de sistemas especifique o conteúdo e a ordem de cada resposta.

O Adobe Commerce tem dois sistemas GraphQL. O sistema GraphQL principal fornece uma ampla variedade de consultas (operações de leitura) e mutações (operações de gravação) que permitem que um comprador interaja com vários tipos de páginas, incluindo produto, conta do cliente, carrinho, check-out e muito mais. No entanto, as consultas que retornam informações do produto não são otimizadas para velocidade. O sistema GraphQL de serviços só pode executar consultas em produtos e informações relacionadas. Esses queries têm mais desempenho do que queries principais semelhantes.

Os dados disponíveis para o Serviço de catálogo são fornecidos pela extensão Exportação de dados SaaS. Essa extensão sincroniza dados entre o aplicativo do Commerce e os Serviços da Commerce conectados para garantir que as consultas aos endpoints da API do GraphQL de serviços retornem os dados do catálogo mais recentes. Para obter informações sobre como gerenciar e solucionar problemas de operações de exportação de dados SaaS, consulte o [Guia de exportação de dados SaaS](../data-export/overview.md).

[!DNL Catalog Service] clientes podem usar o [indexador de preços do SaaS](../price-index/price-indexing.md), que fornece atualizações de preços e tempo de sincronização mais rápidos.

## Arquitetura

O diagrama a seguir mostra os dois sistemas GraphQL:

![Diagrama de arquitetura do catálogo](assets/catalog-service-architecture.png)

No sistema GraphQL principal, o PWA envia uma solicitação ao aplicativo do Commerce, que recebe cada solicitação, processa-a, possivelmente enviando uma solicitação por meio de vários subsistemas, e retorna uma resposta à loja. Essa viagem de ida e volta pode causar tempos lentos de carregamento da página, resultando potencialmente em taxas de conversão mais baixas.

[!DNL Catalog Service] é um Gateway de Serviços Storefront. O serviço acessa um banco de dados separado que contém detalhes do produto e informações relacionadas, como atributos do produto, variantes, preços e categorias. O serviço mantém o banco de dados sincronizado com o Adobe Commerce por meio de indexação.
Como o serviço ignora a comunicação direta com o aplicativo, é possível reduzir a latência do ciclo de solicitação e resposta.

Os sistemas GraphQL principais e de serviço não se comunicam diretamente entre si. Você acessa cada sistema de um URL diferente e as chamadas do exigem informações de cabeçalho diferentes. Os dois sistemas GraphQL foram projetados para serem usados juntos. O sistema GraphQL [!DNL Catalog Service] aumenta o sistema principal para agilizar as experiências da loja de produtos.

Como opção, você pode implementar a [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) para integrar os dois sistemas Adobe Commerce GraphQL com APIs privadas e de terceiros e outras interfaces de software usando o Adobe Developer. A malha pode ser configurada para garantir que as chamadas roteadas para cada endpoint contenham as informações de autorização corretas nos cabeçalhos.

## Detalhes da arquitetura

As seções a seguir descrevem algumas das diferenças entre os dois sistemas GraphQL.

### Gerenciamento de esquema

Como o Serviço de catálogo funciona como um serviço, os integradores não precisam se preocupar com a versão subjacente do Commerce. A sintaxe dos queries é a mesma para todas as versões. Além disso, o esquema é consistente para todos os comerciantes. Essa consistência facilita o estabelecimento de práticas recomendadas e aumenta significativamente a reutilização de widgets da loja.

### Simplificação dos tipos do produto

O esquema reduz a diversidade de tipos de produtos a dois casos de uso:

* Produtos simples são produtos definidos com um único preço e quantidade. O Serviço de Catálogo mapeia os tipos de produtos simples, virtuais, para download e de cartão-presente para `simpleProductViews`.

* Produtos complexos são compostos de vários produtos simples. Os produtos simples componentes podem ter preços diferentes. Um produto complexo também pode ser definido para que o comprador possa especificar a quantidade de produtos simples componentes. O Serviço de Catálogo mapeia os tipos de produto configuráveis, agrupados e agrupados para `complexProductViews`.

Opções complexas de produto são unificadas e diferenciadas por seu comportamento, não pelo tipo. Cada valor de opção representa um produto simples. Esse valor de opção tem acesso aos atributos simples do produto, incluindo preço. Quando o comprador seleciona todas as opções de um produto complexo, a combinação de opções selecionadas aponta para um produto simples específico. O produto simples permanece ambíguo até que o comprador selecione um valor para todas as opções disponíveis.

#### Atributos de exibição do produto

Produtos simples e complexos têm atributos definidos pelo cliente que podem ser exibidos na loja. Estes atributos são retornados como [ProductViewAttributes](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type). No Adobe Commerce, os atributos disponíveis são definidos quando o produto é criado. Você pode adicionar atributos adicionais do back-end do Adobe Commerce ou de forma programática. Consulte [Estender e personalizar dados do feed de exportação de dados SaaS](../data-export/extensibility-and-customizations.md).

>[!TIP]
>
>Em vez de adicionar tipos de dados ao back-end do Commerce, você pode usar a [API Mesh com o Serviço de Catálogo](mesh.md) para estender o esquema do GraphQL do Serviço de Catálogo para adicionar dados ou configurar dados de catálogo existentes para habilitar novas funcionalidades.

### Preços

Produtos simples representam a unidade base de vendas com preço. [!DNL Catalog Service] calcula o preço normal antes dos descontos, bem como o preço final depois dos descontos. Os cálculos de preço podem incluir impostos fixos do produto. Eles excluem promoções personalizadas.

Um produto complexo não tem um preço definido. Em vez disso, o Serviço de catálogo retorna os preços dos simples vinculados. Como exemplo, um comerciante pode atribuir inicialmente os mesmos preços a todas as variantes de um produto configurável. Se determinados tamanhos ou cores não forem populares, o comerciante poderá reduzir os preços dessas variantes. Assim, o preço do produto complexo (configurável) inicialmente mostra uma faixa de preço, refletindo o preço de variantes padrão e impopulares. Depois que o comprador selecionar um valor para todas as opções disponíveis, a vitrine exibe um único preço.

O Serviço de catálogo garante atualizações de preços e cálculos precisos, oferecendo suporte a preços com valores grandes (até 16 dígitos) e alta precisão decimal (até 4 casas decimais).

>[!NOTE]
>
> Os clientes da Commerce com [!DNL Catalog Service] podem aproveitar as vantagens das atualizações de alterações de preço e do tempo de sincronização mais rápidos em seus sites com o [indexador de preços SaaS](../price-index/price-indexing.md).

## Implementação

O processo de instalação requer a configuração do [Commerce Services Connector](../landing/saas.md). Depois que isso for realizado, a próxima etapa é para um integrador de sistemas atualizar o código da loja para incorporar as consultas [!DNL Catalog Service]. Todas as consultas [!DNL Catalog Service] são roteadas para o gateway do GraphQL. O URL é fornecido durante o processo de integração.
