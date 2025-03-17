---
title: Visão geral de [!DNL Merchandising Services]
description: Saiba como o [!DNL Merchandising Services] for Adobe Commerce ajuda a configurar seu catálogo para corresponder ao seu modelo de negócios e à sua estratégia de entrada no mercado
recommendations: noCatalog
exl-id: afa7c148-10fb-4161-8bcc-13084f85c42c
source-git-commit: 31270ceac79977b6ecdf8043b0c162031d129de7
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---

# Visão geral de [!DNL Merchandising Services]

Um catálogo de produtos é essencial para experiências de compras online, permitindo que os clientes naveguem, pesquisem e façam compras. Para eficiência operacional, um catálogo de produtos deve refletir de perto a estrutura de negócios da empresa. As empresas geralmente precisam vender produtos a preços variáveis com base no mercado geográfico, canal de distribuição, segmento de cliente e outras variáveis. Para acomodar isso, uma plataforma de comércio eletrônico deve oferecer um modelo de dados de catálogo flexível que permita que as empresas produzam variações de seus catálogos adaptadas a esses cenários. A Adobe atende a essas necessidades oferecendo serviços de merchandising viabilizados por canais e políticas. Os Serviços de merchandising fornecem os blocos fundamentais que os comerciantes podem usar para criar e gerenciar catálogos em escala. Isso permite que as empresas configurem catálogos que se alinhem à estrutura de negócios e às estratégias de entrada no mercado.

Em um alto nível, com os Serviços de merchandising, você pode:

- Use um catálogo básico único para todas as suas necessidades de negócios. Dimensione rapidamente seu catálogo em novas marcas, mercados, unidades de negócios, canais de entrada no mercado e segmentos de clientes sem a necessidade de uma rearquitetura completa. Isso elimina a duplicação de dados e configura sua plataforma de comércio eletrônico para alta eficiência operacional.
- Desbloqueie a sindicalização de catálogos e forneça o conteúdo correto desenvolvendo seu catálogo de produtos para refletir seus negócios, incluindo produtos, clientes, preços e distribuição.
- Assimile e atualize rapidamente os dados de catálogo e forneça rapidamente as atualizações à loja para suas promoções e necessidades de campanha.
- Obtenha pontuações máximas com componentes de interface do usuário rápidos e prontos para uso alimentados pela Edge Delivery Services para navegação e recomendações ininterruptas de produtos.
- Adote uma arquitetura de composição moderna usando a arquitetura de extensibilidade do Adobe ([App Builder](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-development)) para importar dados de produtos e vitrines comerciais headless avançados usando a [API Mesh](https://experienceleague.adobe.com/en/playlists/commerce-get-started-app-builder-and-api-mesh) da Adobe.

>[!INFO]
>
>Para saber mais sobre as APIs disponíveis nos Serviços de merchandising fornecidos por Canais e políticas, consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog).

## Arquitetura

Os serviços de merchandising fornecidos por canais e políticas são um modelo de dados de catálogo altamente escalável e flexível que desbloqueia com facilidade casos de uso de várias marcas, unidades de vários negócios e vários idiomas. Esse modelo substitui o uso dos escopos de produtos clássicos do Adobe Commerce (site, loja, loja) pelos novos escopos de produtos dos Serviços de merchandising (canal, política e localidade).

O diagrama a seguir fornece uma visualização de alto nível da estrutura de merchandising.

Arquitetura ![[!DNL Merchandising Services]](assets/merchandising-svcs-architecture.png)

Na parte superior deste diagrama, os dados do catálogo (PIM, ERP e assim por diante) são assimilados na estrutura dos Serviços de merchandising. Estes dados de catálogo contêm SKUs. Cada SKU contém detalhes do escopo (localidade) e atributos do produto, que mapeiam para os novos escopos de produto dos Serviços de merchandising (canais, políticas e localidade).

Quando todos esses dados são assimilados na estrutura de merchandising, o resultado é um novo catálogo básico unificado que está disponível no pipeline de dados do Serviço de catálogo. Na próxima parte do diagrama, você verá vários canais. Cada canal representa uma unidade de negócios. Por exemplo, *varejo no Texas*, *sazonal de varejo no Texas* e assim por diante. Como você pode ver no diagrama, as localidades, as políticas e os catálogos de preços podem ser compartilhados entre canais&#x200B;

Por fim, o diagrama mostra como esses dados distintos do catálogo podem ser exibidos em vários locais, como uma vitrine do Edge Delivery Services, um marketplace, um canal de publicidade, uma microloja personalizada e assim por diante.

Para saber como assimilar seus dados de catálogo no Merchandising usando a API de assimilação de dados de catálogo e como configurar suas localidades, políticas e catálogos de preços usando a API de gerenciamento de catálogo e regras, consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog/).

Para saber mais sobre os conceitos que compõem os Serviços de merchandising, consulte as seções a seguir.

## Gerenciamento do catálogo de produtos

A gestão do catálogo de produtos abrange dois aspectos distintos: dados do produto e contexto do produto. Os Serviços de merchandising respeitam a separação dessas obrigações, oferecendo gerenciamento independente para cada um.

- **Dados do produto** - Que produto está sendo vendido e a que preço?
- **Contexto do produto** - Quem está vendendo para quem e onde?

![[!DNL Merchandising Services] aspectos](assets/merchandising-svcs-parts.png)

### Dados do produto

Os dados do produto incluem os seguintes tipos:

- **Produtos** - SKUs individuais ou coleções de SKUs que representam bens físicos ou serviços intangíveis com atributos que representam o produto, incluindo descrição, peso, tamanho, dimensões e muito mais. Os atributos também especificam os escopos de canal e política de uma SKU. Os produtos podem ser agrupados em vários tipos de produtos, como simples, configurável, pacote, pacote de pacotes, assinaturas e muito mais.
- **Metadados** - Os metadados do atributo de produto definem e gerenciam como os atributos de produto são exibidos na vitrine em listas de produtos, páginas de detalhes, resultados de pesquisa e assim por diante. Os metadados também definem como os atributos do produto são usados na pesquisa — classificação, filtragem, pesos de pesquisa e assim por diante.
- **Catálogos de preços e preços** - Determina os preços de venda dos produtos. Nos Serviços de merchandising, um SKU de produto e o preço são dissociados, portanto, você pode definir vários catálogos de preços para um único SKU. Desvinculando os preços do SKU, é possível desbloquear preços específicos de escopo em diferentes níveis de clientes, unidades de negócios e regiões geográficas. Você pode definir preços regulares e com desconto e gerenciar tudo isso em escala.
- **Assets** - Artefatos associados a produtos, como imagens, vídeos, PDFs ou outros tipos de arquivos (futuro roteiro).

### Gerenciamento de contexto de produto

O gerenciamento do contexto do produto abrange os seguintes aspectos:

- **Canal** - O canal de distribuição define o caminho pelo qual uma empresa deseja vender produtos. Um canal é a abstração de mais alto nível que encapsula códigos de idiomas e políticas.
   - Exemplo: Revendedores para a indústria automobilística. Filiais de conglomerados multimarcas. Local de fabricação para fornecedores.
- **Política** - Filtro de acesso a dados que permite entregar o conteúdo correto ao destino correto. Esse conceito habilita recursos de agregação de catálogo.
   - Exemplo: lojas físicas, mercados, pipelines de publicidade em pontos de venda (Google, Facebook, Instagram)
- **Escopo** - Representa o idioma (localidade) dos catálogos, por exemplo `en-US`. O escopo é definido em um nível SKU durante a assimilação de dados do catálogo.

Durante a assimilação e a atualização de dados do produto, um SKU contém os detalhes de escopos e atributos (os atributos são mapeados para canais e políticas). Eles definem os identificadores de contexto de produto aos quais um SKU pertence:

![[!DNL Merchandising Services] Identificadores de Contexto do Produto](assets/merchandising-svcs-product-id.png)

Na imagem acima, cada SKU fornece:

- Identificadores de escopo&#x200B;
   - Localidade: Obrigatório&#x200B;
- Atributos do produto
   - Os atributos do produto são usados para mapear aos canais e políticas relevantes&#x200B;
   - Exemplo: Como fabricante de automóveis, você pode optar por criar um canal e uma combinação de políticas para atributos do produto: (1) Revendedores (2) Marcas de carro.&#x200B;
- Preços e catálogos de preços atribuídos
   - Cada SKU pode ter vários preços definidos usando vários catálogos de preços.
   - Exemplo: você oferece aos funcionários um preço normal reduzido em autopeças com um desconto adicional de 25%. Você oferece aos clientes da VIP um preço normal mais alto com um desconto de 10%. As informações de preço do SKU do produto garantem que o preço correto seja exibido para cada segmento de cliente.

As definições de canal e política são criadas usando APIs dedicadas:

![[!DNL Merchandising Services] Mapeamento de Canal, Política e Escopo](assets/merchandising-svcs-scope-map.png)

- **Escopo** (localidade) - Definido em um nível de SKU durante a assimilação de dados do produto.&#x200B;
- **Canal** - Definição criada usando APIs dedicadas. &#x200B;
- **Política** - Definição criada usando APIs dedicadas.

## Principais recursos

| Principais recursos | Benefício |
|---|---|
| **Assimilação direta de dados do catálogo no pipeline de serviços da loja**: assimile seus dados de catálogo diretamente no pipeline de serviços de catálogo para o ciclo de vida de pesquisa e navegação da loja (Página de Exibição do Produto, Página de Lista de Produtos, Página de Resultados da Pesquisa e assim por diante). | <ul><li>Assimile diretamente dados de catálogo no pipeline de serviço da loja que possibilita: Serviço de catálogo, Descoberta de produto (Live Search) e Recomendações de produto. Com isso, você pode fornecer atualizações de catálogo em escala para milhões de SKUs. Isso desbloqueia o gerenciamento de promoções em larga escala sensíveis ao tempo. </li></ul> |
| **Novos escopos de produtos de catálogo**: canal, política e escopo são novos escopos de produtos introduzidos pelos Serviços de Merchandising. Esses escopos de produto substituem os escopos de site, loja e loja na camada de serviços da loja. [Saiba mais](#product-context-management). | <ul><li>Com os novos escopos, os Serviços de merchandising liberam a capacidade de dimensionar para casos de uso de várias regiões geográficas, unidades de vários negócios, várias marcas e vários idiomas com facilidade usando um único catálogo básico.</li><li>Elimine a redundância de dados no gerenciamento de catálogos.</li></ul> |
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

### Aonde ir daqui

- Assimilar dados nos Serviços de merchandising usando a [API de assimilação de dados](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/).
- Gerencie seu catálogo e defina os canais, políticas e escopos usando a [API de gerenciamento de catálogo](https://developer-stage.adobe.com/commerce/services/composable-catalog/admin/using-the-api/)
- [Conclua um tutorial](https://developer-stage.adobe.com/commerce/services/composable-catalog/merchandising-services-use-case/) que mostre como uma empresa com um único catálogo base pode usar as APIs de Serviços de Merchandising para adicionar dados de produtos, definir catálogos usando projeções e recuperar os dados do catálogo para exibição em uma loja headless.
