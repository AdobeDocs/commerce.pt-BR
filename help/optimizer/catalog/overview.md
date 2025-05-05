---
title: Visão geral do catálogo
description: Saiba como definir seus canais e políticas.
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 0%

---

# Visão geral do catálogo

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

Um catálogo de produtos é essencial para experiências de compras online, permitindo que os clientes naveguem, pesquisem e façam compras. Para eficiência operacional, um catálogo de produtos deve refletir de perto a estrutura de negócios da empresa. As empresas geralmente precisam vender produtos a preços variáveis com base no mercado geográfico, canal de distribuição, segmento de cliente e outras variáveis. Para acomodar isso, uma plataforma de comércio eletrônico deve oferecer um modelo de dados de catálogo flexível que permita que as empresas produzam variações de seus catálogos adaptadas a esses cenários. Adobe Systems atende a essas necessidades oferecendo serviços de comercialização fornecidos por Canais e políticas. Os serviços de merchandising fornecem blocos de construção que os comerciantes podem usar para criar e gerenciar catálogos em escala. Isso permite que as empresas configurem catálogos alinhados à sua estrutura de negócios e estratégias mercado.

Em um alto nível, com serviços de merchandising você pode:

- Use um catálogo de base único para todas as suas necessidades comerciais. Dimensione seu catálogo rapidamente em novas marcas, mercados, unidades de negócios, canais go-to-mercado e segmentos de clientes sem precisar de uma nova arquitetura completa. Isso elimina a duplicação de dados e configura sua plataforma de comércio eletrônico para ter alta eficiência operacional.
- Desbloqueie a agregação de catálogos e entregue as conteúdo certas ao criar seu catálogo de produtos para refletir seus negócios, incluindo produtos, clientes, preços e distribuição.
- Rapidamente assimilar e atualize os dados do catálogo e envie rapidamente as atualizações para a vitrine para suas promoções e necessidades campanha.
- Faça pontuações perfeitas de farol com componentes de interface prontos para uso e rápidos, alimentados pelo Edge Delivery Services para navegação perfeita de produtos e recomendações.
- Adote uma arquitetura composável moderna usando a arquitetura de extensibilidade da Adobe Systems ([aplicativo Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) para importar dados de produtos e vitrines de comércio sem periféricos usando a Malha[&#128279;](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh) da API da Adobe Systems.

>[!INFO]
>
>Para saber mais sobre as APIs disponíveis nos Serviços de merchandising fornecidos por Canais e Políticas, consulte a documentação[&#128279;](https://developer-stage.adobe.com/commerce/services/composable-catalog) do desenvolvedor.

## Arquitetura

Os serviços de merchandising fornecidos por canais e políticas são um modelo de dados de catálogo altamente escalável e flexível que desbloqueia com facilidade casos de uso de várias marcas, unidades de vários negócios e vários idiomas. Esse modelo substitui o uso dos escopos de produtos clássicos do Adobe Commerce (site, loja, loja) pelos novos escopos de produtos dos Serviços de merchandising (canal, política e localidade).

O diagrama a seguir fornece uma visualização de alto nível da estrutura de merchandising.

Arquitetura ![[!DNL Merchandising Services]](../assets/merchandising-svcs-architecture.png)

Na parte superior deste diagrama, os dados do catálogo (PIM, ERP e assim por diante) são assimilados na estrutura dos Serviços de merchandising. Estes dados de catálogo contêm SKUs. Cada SKU contém detalhes do escopo (localidade) e atributos do produto, que mapeiam para os novos escopos de produto dos Serviços de merchandising (canais, políticas e localidade).

Quando todos esses dados são assimilados na estrutura de merchandising, o resultado é um novo catálogo básico unificado que está disponível no pipeline de dados do Serviço de catálogo. Na próxima parte do diagrama, você verá vários canais. Cada canal representa uma unidade de negócios. Por exemplo, *varejo no Texas*, *sazonal de varejo no Texas* e assim por diante. Como você pode ver no diagrama, as localidades, as políticas e os catálogos de preços podem ser compartilhados entre canais&#x200B;

Por fim, o diagrama mostra como esses dados distintos do catálogo podem ser exibidos em vários locais, como uma vitrine do Edge Delivery Services, um marketplace, um canal de publicidade, uma microloja personalizada e assim por diante.

Para saber como assimilar seus dados de catálogo no Merchandising usando a API de assimilação de dados de catálogo e como configurar suas localidades, políticas e catálogos de preços usando a API de gerenciamento de catálogo e regras, consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Para saber mais sobre os conceitos que compõem os Serviços de merchandising, consulte as seções a seguir.

## Gerenciamento do catálogo de produtos

A gestão do catálogo de produtos abrange dois aspectos distintos: dados do produto e contexto do produto. Os Serviços de merchandising respeitam a separação dessas obrigações, oferecendo gerenciamento independente para cada um.

- **Dados do produto** - Que produto está sendo vendido e a que preço?
- **Contexto do produto** - Quem está vendendo para quem e onde?

![[!DNL Merchandising Services] aspectos](../assets/merchandising-svcs-parts.png)

### Dados do produto

Os dados do produto incluem os seguintes tipos:

- **Produtos** - SKUs individuais ou coleções de SKUs que representam bens físicos ou serviços intangíveis com atributos que representam o produto, incluindo descrição, peso, tamanho, dimensões e muito mais. Os atributos também especificam os escopos de canal e política de uma SKU. Os produtos podem ser agrupados em vários tipos de produtos, como simples, configurável, pacote, pacote de pacotes, assinaturas e muito mais.
- **Metadados** - Os metadados do atributo de produto definem e gerenciam como os atributos de produto são exibidos na vitrine em listas de produtos, páginas de detalhes, resultados de pesquisa e assim por diante. Os metadados também definem como os atributos do produto são usados na pesquisa — classificação, filtragem, pesos de pesquisa e assim por diante.
- **Catálogos de preços e preços** - Determina os preços de venda dos produtos. No Merchandising Services, um produto SKU e preço são dissociados, portanto, você tem o poder de definir vários livros de preços para um único SKU. Ao dissociar os preços do SKU, você pode desbloquear preços específicos escopo em diferentes níveis de clientes, unidades de negócios e geografias. Você pode definir preços regulares e com desconto e gerenciar tudo isso em escala.
- **&#x200B;**&#x200B;Assets - Artefatos associados a produtos, como imagens, vídeos, PDFs ou outros tipos de arquivos (roteiro futuro).

### Gerenciamento de contexto do produto

O gerenciamento de contexto do produto abrange os seguintes aspectos:

- **Canal** - O canal de distribuição define o caminho pelo qual uma empresa deseja vender produtos. Um canal é a abstração de mais alto nível que encapsula códigos de idiomas e políticas.
   - Exemplo: Revendedores para a indústria automobilística. Filiais de conglomerados multimarcas. Local de fabricação para fornecedores.
- **Política** - Filtro de acesso a dados que permite entregar o conteúdo correto ao destino correto. Esse conceito habilita recursos de agregação de catálogo.
   - Exemplo: lojas físicas, mercados, pipelines de publicidade em pontos de venda (Google, Facebook, Instagram)
- **Escopo** - Representa o idioma (localidade) dos catálogos, por exemplo `en-US`. O escopo é definido em um nível SKU durante a assimilação de dados do catálogo.

Durante a assimilação e a atualização de dados do produto, um SKU contém os detalhes de escopos e atributos (os atributos são mapeados para canais e políticas). Eles definem os identificadores de contexto de produto aos quais um SKU pertence:

![[!DNL Merchandising Services] Identificadores de Contexto do Produto](../assets/merchandising-svcs-product-id.png)

Na imagem acima, cada SKU fornece:

- Identificadores de escopo&#x200B;
   - Localidade: Obrigatório&#x200B;
- Atributos do produto
   - Os atributos do produto são usados para mapear para os canais e políticas relevantes
   - Exemplo: como fabricante de carros, é possível optar por criar uma canal e política combinação para atributos do produto: (1) Revendedores (2) marcas de carros.
- Preços e catálogos de preços atribuídos
   - Cada SKU pode ter vários preços definidos com vários catálogos de preços.
   - Exemplo: você oferece aos funcionários um preço normal reduzido em autopeças com um desconto adicional de 25%. Você oferece aos clientes da VIP um preço normal mais alto com um desconto de 10%. As informações de preço do SKU do produto garantem que o preço correto seja exibido para cada segmento de cliente.

As definições de canal e política são criadas usando APIs dedicadas:

![[!DNL Merchandising Services] Mapeamento de Canal, Política e Escopo](../assets/merchandising-svcs-scope-map.png)

- **Escopo** (localidade) - Definido em um nível de SKU durante a ingestão de dados do produto.
- **Channel** - Definition created using dedicated APIs.
- **Política** - Definição criada usando APIs dedicadas.

## Principais recursos

| Principais recursos | Benefício |
|---|---|
| **Assimilação direta de dados do catálogo no pipeline** de serviços de storefront: ingera os dados do catálogo diretamente no pipeline de serviços de catálogo para a navegação na vitrine e pesquisa ciclo de vida (Página de exibição de produto, Página de lista de produtos, Search Resultados Página etc.) | <ul><li>Diretamente assimilar dados de catálogo no pipeline de serviços de storefront que alimenta: Serviço de catálogo, Descoberta de produtos (Search) e Recomendações de produtos. Com isso, você pode fornecer atualizações de catálogo em escala para milhões de SKUs. Isso desbloqueia o gerenciamento de promoção de grande escala sensível ao tempo. </li></ul> |
| **Novo escopos** de produtos de catálogo: Canais, política e escopo são novos escopos de produtos introduzidos pelos Serviços de Merchandising. Esses escopos de produto substituem os escopos de site, armazenamento e storeview na camada de serviços de storefront. [Saiba mais](#product-context-management). | <ul><li>Com os novos escopos, os Serviços de merchandising liberam a capacidade de dimensionar para casos de uso de várias regiões geográficas, unidades de vários negócios, várias marcas e vários idiomas com facilidade usando um único catálogo básico.</li><li>Elimine a redundância de dados no gerenciamento de catálogos.</li></ul> |
| **Dimensionar para dezenas de milhões de SKUs** | Desbloqueie o gerenciamento de catálogos em escala. Aqui você pode assimilar e gerenciar mais de SKUs de 200 MM com facilidade. |
| **Suporte a tipo de produto** | <ul><li>Simples, configurável</li><li>Pacotes e pacotes de pacotes (futuro roteiro)</li><li>Assinaturas e planos (futuro roteiro)</li></ul> |
| **Comércio headless** | <ul><li>Suporte completo para implementações de comércio headless por meio do Serviço de catálogo, Descoberta de produto (Live Search) e APIs de recomendações de produto.</li></ul> |
| **Componentes de interface do usuário modernos com velocidade relâmpago** | <ul><li>Suporte imediato a componentes de interface do usuário para pesquisa e recomendações de produtos.</li><li>Os componentes da interface do usuário são extensíveis e flexíveis para que possam ser usados pelo Edge Delivery Service da Adobe, bem como por qualquer outra implementação de loja.</li></ul> |

## Que tipo de comerciante se beneficia mais dos Serviços de merchandising?

A tabela a seguir destaca os desafios comuns que os comerciantes encontram e como os Serviços de merchandising alimentados por Canais e políticas os abordam.

| Tipo de comerciante | Caso de uso | Problemas resolvidos |
|---|---|---|
| Conglomerado multimarcas | <ul><li>Eles vendem várias marcas</li><li>Eles vendem em vários países</li><li>Eles vendem em diferentes idiomas</li></ul> | Use um catálogo unificado de base única e obtenha eficiência operacional enquanto expande para várias marcas, regiões geográficas e idiomas. |
| Conglomerado de peças de automóveis/manufatura | <ul><li>Vende peças de automóveis ou máquinas. Os produtos são os mesmos para todos os clientes.</li><li>Diferentes revendedores vendem peças a clientes</li><li>Cada revendedor tem seus próprios preços, estoque e métodos de envio</li></ul> | Para ter diferentes integrações de envio, cada revendedor deve ter um site separado. Mas sites separados forçam o modelo de dados de catálogo típico a duplicar os dados. Então, se existem 3000 negociantes nos EUA, um comerciante cria 3000 cópias de catálogo, mesmo que o mesmo catálogo seja usado por todos os negociantes. Essa duplicação de dados interfere nos limites de desempenho. Os serviços de merchandising eliminam a duplicação de dados. |
| Empresa de embalagem/logística | <ul><li>Eles têm vários locais de envio</li><li>Eles têm um preço diferente para cada cliente</li><li>O mesmo produto disponível em 2 locais para 2 clientes têm 4 preços possíveis</li></ul> | Apesar do uso de grupos de clientes para cobrir os preços por cliente, o modelo de dados de catálogo típico não tem a capacidade de gerenciar o preço por local. Além disso, os comerciantes desejam regras de visibilidade exclusivas por local/site. O gerenciamento dessas regras complexas de preço e visibilidade pode ser desbloqueado em escala com os Serviços de merchandising. |

<!--### Where to go from here

- Ingest data into Merchandising Services using the [data ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Manage your catalog and define the channels, policies, and scopes using the [catalog management API](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Complete a tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) that shows how a company with a single base catalog can use the Merchandising Services APIs to add product data, define catalogs using projections, and retrieve the catalog data for display in a headless storefront.-->
