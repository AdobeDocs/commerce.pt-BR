---
title: '[!DNL Catalog Service]'
description: Acelere sua loja do Adobe Commerce com o [!DNL Catalog Service]  - uma API GraphQL de alto desempenho que reduz o tempo de carregamento de páginas de produtos, páginas de categoria e resultados de pesquisa.
role: Admin, Developer
recommendations: noCatalog
exl-id: 525e3ff0-efa6-48c7-9111-d0b00f42957a
source-git-commit: 4f3f8accd653dbee6fec45c065f55ff04b17bd2d
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# [!DNL Catalog Service] para Adobe Commerce

A extensão do [!DNL Catalog Service] for Adobe Commerce melhora os tempos de carregamento da loja, fornecendo dados de catálogo otimizados e somente leitura por meio de uma API dedicada do GraphQL. Esse serviço foi projetado especificamente para aprimorar as experiências de página relacionadas ao produto, resultando em carregamentos de página mais rápidos e taxas de conversão aprimoradas.

Os dados avançados do modelo de exibição fornecidos pelo [!DNL Catalog Service] incluem detalhes do produto, atributos, estoque e preços, permitindo a renderização rápida de experiências da loja relacionadas ao produto, como:

- Páginas de detalhes do produto
- Páginas de lista de produtos e categoria
- Páginas de resultados da pesquisa
- Carrosséis de produtos
- Páginas de comparação do produto
- Qualquer outra página que renderize dados do produto, como carrinho, pedido e páginas de lista de desejos


## Principais benefícios e recursos

- **Carregamentos de página mais rápidos**: consultas otimizadas para uma recuperação de dados de catálogo até 10 vezes mais rápida em comparação com o sistema GraphQL principal
- **Taxas de conversão aprimoradas**: tempos de carregamento mais rápidos proporcionam uma melhor experiência ao usuário
- **Tipos de produtos simplificados**: o esquema unificado baseado em tipos de produtos simples e complexos reduz a complexidade para os desenvolvedores
- **Precisão de preço aprimorada**: suporte para valores de 16 dígitos com 4 casas decimais
- **Arquitetura dissociada**: um sistema GraphQL separado para dados de catálogo garante alto desempenho sem afetar as operações principais do Commerce
- **Sincronização de dados em tempo real**: o serviço de catálogo é mantido em sincronia com o aplicativo do Adobe Commerce por meio da extensão Exportação de dados SaaS, garantindo que as consultas retornem os dados de catálogo mais recentes
- **Painel de Gerenciamento de Dados**: Monitore e gerencie operações de sincronização de dados na interface de Administrador do Adobe Commerce
- **Integração da API Mesh**: como opção, integre-se à [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) para combinar os sistemas do Adobe Commerce GraphQL com outras APIs internas e de terceiros para estender o esquema da GraphQL do Serviço de Catálogo e adicionar dados ou funcionalidades personalizados


## Visão geral da arquitetura

>[!NOTE]
>
>Se você estiver implementando seu catálogo usando o catálogo combinável com o Adobe Commerce Optimizer ou o Adobe Commerce Optimizer Connector, consulte o [Guia do Adobe Commerce Optimizer](../optimizer/overview.md#architecture) e o Guia do Desenvolvedor dos Serviços de Merchandising.

O [!DNL Catalog Service] usa o [GraphQL](https://graphql.org/) para solicitar e receber dados de catálogo, incluindo produtos, atributos de produto, estoque e preços. O GraphQL é uma linguagem de consulta que um cliente de front-end usa para se comunicar com a API (interface de programação de aplicativos) definida em um back-end, como o Adobe Commerce. O GraphQL é um método de comunicação popular porque é leve e permite que um integrador de sistemas especifique o conteúdo e a ordem de cada resposta.

A Adobe Commerce fornece dois sistemas GraphQL que atendem a diferentes objetivos:

### Sistema GraphQL principal

- **Propósito**: API completa para todas as operações do Commerce
- **Recursos**: consultas (leitura) e mutações (gravação) para produtos, clientes, carrinho, check-out e muito mais
- **Limitação**: as consultas de produto não estão otimizadas para velocidade
- **Caso de uso**: operações gerais de Commerce e operações de gravação

### Sistema GraphQL do Serviço de Catálogo

- **Propósito**: somente consultas de catálogo de produtos de alto desempenho
- **Recursos**: consultas somente leitura de produtos, atributos, estoque e preços
- **Vantagem**: significativamente mais rápido que o sistema principal para dados de produtos
- **Caso de uso**: experiências de produto de vitrine eletrônica em que a velocidade é crítica

Os dados disponíveis para o Serviço de catálogo são fornecidos pela extensão Exportação de dados SaaS. Essa extensão sincroniza dados entre o aplicativo do Commerce e os Serviços da Commerce conectados para garantir que as consultas aos endpoints da API do GraphQL de serviços retornem os dados do catálogo mais recentes. Para obter informações sobre como gerenciar e solucionar problemas de operações de exportação de dados SaaS, consulte o [Guia de exportação de dados SaaS](../data-export/overview.md).

[!DNL Catalog Service] clientes podem usar o [indexador de preços do SaaS](../price-index/price-indexing.md), que fornece atualizações de preços e tempo de sincronização mais rápidos.

## Detalhes da arquitetura

O diagrama a seguir ilustra as diferenças de arquitetura entre o sistema GraphQL principal e o sistema GraphQL do Catalog Service, mostrando como eles trabalham juntos para otimizar o desempenho da loja:

![Diagrama de arquitetura do catálogo](assets/catalog-service-architecture.png)

### Como os sistemas funcionam

**Sistema GraphQL Principal (Abordagem Tradicional):**
O aplicativo web progressivo (PWA) envia solicitações diretamente para o aplicativo Commerce, que processa cada solicitação por meio de vários subsistemas antes de retornar uma resposta. Essa viagem de ida e volta em várias etapas pode causar tempos lentos de carregamento da página, resultando potencialmente em taxas de conversão mais baixas.

**Serviço de Catálogo (Abordagem Otimizada):**
O Serviço de catálogo atua como um Gateway de serviços de vitrine que acessa um banco de dados dedicado e otimizado contendo detalhes do produto, atributos, variantes, preços e categorias. O serviço mantém a sincronização com o Adobe Commerce por meio da indexação automatizada, ignorando o ciclo tradicional de solicitação-resposta para reduzir drasticamente a latência.

Os sistemas GraphQL principais e de serviço não se comunicam diretamente entre si. Você acessa cada sistema de um URL diferente e as chamadas do exigem informações de cabeçalho diferentes. Os dois sistemas GraphQL foram projetados para serem usados juntos. O sistema GraphQL [!DNL Catalog Service] aumenta o sistema principal para agilizar as experiências da loja de produtos.

Como opção, você pode implementar a [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/) para integrar os dois sistemas Adobe Commerce GraphQL com APIs privadas e de terceiros e outras interfaces de software usando o Adobe Developer. A malha pode ser configurada para garantir que as chamadas roteadas para cada endpoint contenham as informações de autorização corretas nos cabeçalhos.

## Detalhes da arquitetura

As seções a seguir descrevem algumas das diferenças entre os dois sistemas GraphQL.

### Gerenciamento de esquema

Como o Serviço de catálogo funciona como um serviço, os integradores não precisam se preocupar com a versão subjacente do Commerce. A sintaxe dos queries é a mesma para todas as versões. Além disso, o esquema é consistente para todos os comerciantes. Essa consistência facilita o estabelecimento de práticas recomendadas e aumenta significativamente a reutilização de widgets da loja.

### Simplificação dos tipos do produto

O esquema reduz a diversidade de tipos de produtos a dois casos de uso:

- **Produtos simples** — o Serviço de Catálogo mapeia os tipos de produtos Adobe Commerce simples, virtuais, para download e de cartão-presente para `simpleProductViews`. Esse tipo tem:
   - Um preço e uma quantidade únicos e fixos
   - Um preço normal (antes dos descontos) e preço final (após os descontos)
   - Suporte para atributos do produto, como cor, tamanho e outras características

- **Produtos complexos** — O Serviço de Catálogo mapeia os tipos de produtos configuráveis, agrupados e agrupados do Adobe Commerce para `complexProductViews`. Produtos complexos são coleções de vários produtos simples que podem ser configurados ou agrupados juntos.
   - Cada componente do produto simples pode ter seu próprio preço.
   - Os compradores podem especificar quantidades para produtos de componentes individuais.
   - As opções de produto (como tamanho, cor, material) são unificadas e funcionam da mesma maneira, independentemente do tipo de produto. Cada seleção de opção aponta para um produto simples específico com seus próprios atributos e preço. O produto final permanece indefinido até que o comprador selecione todas as opções necessárias.

#### Atributos de exibição do produto

Produtos simples e complexos têm atributos definidos pelo cliente que podem ser exibidos na loja. Estes atributos são retornados como [ProductViewAttributes](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type). No Adobe Commerce, os atributos disponíveis são definidos quando o produto é criado. Você pode adicionar atributos adicionais do back-end do Adobe Commerce ou de forma programática. Consulte [Estender e personalizar dados do feed de exportação de dados SaaS](../data-export/extensibility-and-customizations.md).

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

O processo de implementação envolve:

1. [!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."} **[Instalar e configurar o Serviço de Catálogo](installation.md)**—Instale e configure a extensão Serviço de Catálogo e configure a conexão SaaS usando o [!DNL Commerce Services Connector].
2. **Atualizar código de vitrine**: integre consultas GraphQL do Serviço de Catálogo ao seu front-end.
3. **Consultas de rota**: todas as consultas do Serviço de catálogo passam pelo gateway do GraphQL (URL fornecida durante a integração)
4. **Monitorar e solucionar problemas de sincronização de dados**: verifique o desempenho aprimorado e monitore os resultados


