---
title: Visão geral de eventos
description: Saiba mais sobre os eventos que o [!DNL Adobe Commerce Optimizer] usa para melhorar a pesquisa e as recomendações.
role: Admin, Developer
recommendations: noCatalog
exl-id: c102c558-a680-4622-80f0-6e5c34d497e9
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# Eventos

Os eventos são uma ferramenta essencial para aprimorar a experiência de compra e gerar conversões aproveitando insights de dados em tempo real.

O [!DNL Adobe Commerce Optimizer] implanta os eventos da vitrine eletrônica no site automaticamente. Esses eventos capturam dados das interações dos compradores no site. Estes dados anônimos alimentam as [recomendações](../../manage-results/recommendation-performance.md), a [descoberta de produtos](../../manage-results/search-performance.md) e as [métricas de sucesso](../../manage-results/success-metrics.md).

>[!NOTE]
>
>A coleta de dados não inclui informações de identificação pessoal (PII). Todos os identificadores de usuários, como IDs de cookies e endereços IP, são estritamente anônimos. [Saiba mais](https://www.adobe.com/privacy/experience-cloud.html).

A página **Events** permite observar os dados do evento da loja que está sendo coletado. Ter uma visualização na coleção de dados do evento permite que os comerciantes verifiquem se implementaram os eventos de vitrine corretamente e se os eventos estão sendo capturados com sucesso. Os comerciantes podem usar esta página para identificar possíveis problemas e tomar medidas para resolver quaisquer problemas de evento.

## Contagem de eventos

A guia **Contagens de eventos** rastreia as interações do comprador, como pesquisas, cliques e compras, para ajudá-lo a analisar tendências e melhorar a experiência de compras.

![Contagens de eventos](../../assets/event-counts.png){zoomable="yes"}

| Campo | Descrição |
|---|---|
| **Intervalo de datas** | Vamos especificar o intervalo de datas para ver um subconjunto específico de dados. |
| **Eventos de vitrine por hora** | Exibe um gráfico que mostra o número de eventos acionados na loja. |
| **Total de eventos de vitrine** | Uma tabela filtrável que mostra detalhes de todos os eventos acionados em sua loja. |

## Verificação de integridade

A guia **Verificação de integridade** oferece insights sobre a integridade de cada evento comportamental, garantindo uma coleta e funcionalidade precisas de dados. &#x200B;

![Verificação de integridade](../../assets/sanity-check.png){zoomable="yes"}

| Campo | Descrição |
|---|---|
| **Intervalo de datas** | Vamos especificar o intervalo de datas para ver um subconjunto específico de dados. |
| **Descoberta de produto** | Exibe os eventos necessários para personalizar os resultados da pesquisa de produtos. A coluna **Status** indica se os eventos foram recebidos. |
| **Recomendações** | Exibe os eventos necessários para personalizar as recomendações do produto. A coluna **Status** indica se os eventos foram recebidos. |

As seções a seguir descrevem detalhes do evento para [descoberta de produto](#product-discovery) e [recomendações](#recommendations).

### Descoberta de produto

A descoberta de produtos usa eventos para potencializar algoritmos de pesquisa, como &quot;Mais visualizados&quot; e &quot;Mais visualizados isto, visualizados aquilo&quot;.

Esta tabela descreve os eventos usados pela descoberta de produtos [estratégias de classificação](../../merchandising/rules/add.md#intelligent-ranking).

| Estratégia de classificação | Eventos | Página |
| --- | --- | --- |
| Mais visualizados | `page-view`<br>`product-view` | Página de detalhes do produto |
| Mais comprados | `page-view`<br>`place-order` | Carrinho/Check-out |
| Mais adicionados ao carrinho | `page-view`<br>`add-to-cart` | Página de detalhes do produto<br>Página de listagem do produto<br>Carrinho<br>Lista de desejos |
| Visualizou isto, visualizou aquilo | `page-view`<br>`product-view` | Página de detalhes do produto |

#### Eventos de painel obrigatórios

Alguns eventos são necessários para preencher o [painel de desempenho de pesquisa](../../manage-results/search-performance.md)

| Área do painel | Eventos | Ingressar no campo |
| ------------------- | ------------- | ---------- |
| Pesquisas únicas | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Nenhuma pesquisa de resultados | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |

### Recommendations

Há dois tipos de dados usados nas recomendações:

- **Comportamento** - Dados do envolvimento de um comprador no seu site, como exibições de produtos, itens adicionados ao carrinho e compras.
- **Catálogo** - Metadados do produto, como nome, preço, disponibilidade etc.

A IA do Adobe agrega os dados comportamentais e de catálogo, criando Recomendações para cada tipo de recomendação. O serviço de recomendações implanta essas recomendações na vitrine eletrônica em um widget que contém o produto recomendado _itens_.

Alguns tipos de recomendações usam dados comportamentais de seus compradores para treinar modelos de aprendizado de máquina para criar recomendações personalizadas. Outros tipos de recomendações usam apenas dados de catálogo e não usam dados comportamentais. Se você quiser começar rapidamente a usar o Recommendations em seu site, poderá usar o tipo de recomendação `More like this`.

#### Arranque a frio

Quando você pode começar a usar tipos de recomendação que usam dados comportamentais? Depende. Isso é conhecido como o problema _Cold Start_.

O problema _Cold Start_ refere-se ao tempo que um modelo leva para ser treinado e se tornar efetivo. Para recomendações, isso significa aguardar que a IA do Adobe colete dados suficientes para treinar seus modelos de aprendizado de máquina antes de implantar unidades de recomendação em seu site. Quanto mais dados os modelos tiverem, mais precisas e úteis serão as recomendações. Como a coleta de dados acontece em um site ativo, é melhor iniciar esse processo antecipadamente.

A tabela a seguir fornece algumas orientações gerais sobre o tempo necessário para coletar dados suficientes para cada tipo de recomendação:

| Tipo de recomendação | Tempo de treinamento | Notas |
|---|---|---|
| Baseado em popularidade (`Most viewed`, `Most purchased`, `Most added to cart`) | Varia | Depende do volume de eventos — as exibições são mais comuns e, portanto, aprende mais rápido; depois, adiciona ao carrinho e, em seguida, às compras |
| `Viewed this, viewed that` | Requer mais treinamento | O volume das visualizações de produto é decentemente alto |
| `Viewed this, bought that`, `Bought this, bought that` | Requer mais treinamento | Os eventos de compra são os eventos mais raros em um site de comércio, especialmente em comparação às visualizações de produto |
| `Trending` | Requer três dias de dados para estabelecer uma linha de base de popularidade | As tendências são uma medida do impulso recente na popularidade de um produto em comparação com sua própria linha de base de popularidade. A pontuação de tendência de um produto é calculada usando um conjunto de primeiro plano (popularidade recente em 24 horas) e um conjunto de segundo plano (popularidade na linha de base em 72 horas). Se a popularidade de um item aumentar significativamente em um período de 24 horas em comparação com sua popularidade na linha de base, ele receberá uma alta pontuação de tendência. Cada produto tem essa pontuação e os itens com a pontuação mais alta a qualquer momento compõem o conjunto dos principais produtos em tendência. |

Outras variáveis que podem afetar o tempo necessário para treinar:

- Maior volume de tráfego contribui para uma aprendizagem mais rápida
- Alguns tipos de recomendações são treinados mais rapidamente do que outros
- [!DNL Adobe Commerce Optimizer] recalcula dados comportamentais a cada quatro horas. As recomendações se tornam mais precisas quanto mais tempo forem usadas no site.

Para ajudá-lo a visualizar o progresso do treinamento de cada tipo de recomendação, a página [criar recomendação](../../merchandising/recommendations/create.md#readiness-indicators) exibe indicadores de preparação.

Enquanto os dados estão sendo coletados em seu site ativo e os modelos de aprendizado de máquina estão sendo treinados, você pode concluir outras tarefas de teste e configuração necessárias para definir as recomendações. Quando você terminar este trabalho, os modelos terão dados suficientes para criar recomendações úteis, permitindo que você os implante em sua loja.

Se o site não receber tráfego suficiente (exibições, compras, tendências) para a maioria dos SKUs de produtos, talvez não haja dados suficientes para concluir o processo de aprendizado. Isso pode fazer com que o indicador de prontidão no espaço de trabalho do Recommendations pareça travado. Os indicadores de prontidão devem fornecer aos comerciantes outro ponto de dados para escolher qual tipo de recomendações é melhor para sua loja. Os números são um guia e podem nunca chegar a 100%. [Saiba mais](../../merchandising/recommendations/create.md#readiness-indicators) sobre os indicadores de preparação.

#### Recomendações de backup

Se os dados de entrada forem insuficientes para fornecer todos os itens de recomendação solicitados em uma unidade, o [!DNL Adobe Commerce Optimizer] fornecerá recomendações de backup para preencher as unidades de recomendação. Por exemplo, se você implantar o tipo de recomendação `Recommended for you` na sua página inicial, um comprador novo no site não terá gerado dados comportamentais suficientes para recomendar com precisão os produtos personalizados. Neste caso, [!DNL Adobe Commerce Optimizer] exibe itens baseados no tipo de recomendação `Most viewed` para este comprador.

No caso de coleta de dados de entrada insuficiente, os seguintes tipos de recomendação fazem fallback para o tipo de recomendação `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Eventos específicos de recomendação

A tabela a seguir lista os eventos que são acionados quando os compradores interagem com as unidades de recomendação na loja. Os dados coletados do evento alimentam as [métricas](../../manage-results/recommendation-performance.md) para analisar o desempenho de suas recomendações.

| Evento | Descrição |
| --- | --- |
| `impression-render` | Enviado quando a unidade de recomendação é renderizada na página. Se uma página tiver duas unidades de recomendação (compradas, exibição), dois eventos `impression-render` serão enviados. Esse evento é usado para rastrear a métrica para impressões. |
| `rec-add-to-cart-click` | O comprador clica no botão **Adicionar ao carrinho** para um item na unidade de recomendação. |
| `rec-click` | O comprador clica em um produto na unidade de recomendação. |
| `view` | Enviado quando a unidade de recomendação se torna pelo menos 50% visível, como ao rolar a página para baixo. Por exemplo, se uma unidade de recomendação tiver duas linhas, um evento `view` será enviado quando uma linha mais um pixel da segunda linha se tornar visível para o comprador. Se o comprador rolar a página várias vezes para cima e para baixo, o evento `view` será enviado tantas vezes quanto o comprador vir toda a unidade de recomendação novamente na página. |

#### Eventos de painel obrigatórios

Os seguintes eventos são necessários para preencher o [painel de Desempenho do Recommendations](../../manage-results/recommendation-performance.md)

| Coluna do painel | Eventos | Ingressar no campo |
| ---------------- | --------- | ----------- |
| Impressões | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Visualizações | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Cliques | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Receita | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Receita LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Os seguintes eventos não são específicos do Recommendations, mas são necessários para que o Adobe AI interprete os dados do comprador corretamente:

- `view`
- `add-to-cart`
- `place-order`

#### Tipo de recomendação

Esta tabela descreve os eventos usados por cada tipo de recomendação.

| Tipo de recomendação | Eventos | Página |
| --- | --- | --- |
| Mais visualizados | `page-view`<br>`product-view` | Página de detalhes do produto |
| Mais comprados | `page-view`<br>`place-order` | Carrinho/Check-out |
| Mais adicionados ao carrinho | `page-view`<br>`add-to-cart` | Página de detalhes do produto<br>Página de listagem do produto<br>Carrinho<br>Lista de desejos |
| Visualizou isto, visualizou aquilo | `page-view`<br>`product-view` | Página de detalhes do produto |
| Visualizou isto, comprou aquilo | `page-view`<br>`product-view` | Página de detalhes do produto<br>Carrinho/Check-out |
| Comprei isto, comprei aquilo | `page-view`<br>`product-view` | Página de detalhes do produto |
| Tendências | `page-view`<br>`product-view` | Página de detalhes do produto |
| Conversão: exibir para compra | `page-view`<br>`product-view` | Página de detalhes do produto |
| Conversão: exibir para compra | `page-view`<br>`place-order` | Carrinho/Check-out |
| Conversão: exibir para carrinho | `page-view`<br>`product-view` | Página de detalhes do produto |
| Conversão: exibir para carrinho | `page-view`<br>`add-to-cart` | Página de detalhes do produto<br>Página de listagem do produto<br>Carrinho<br>Lista de desejos |

## Suporte

Se você observar discrepâncias de dados ou se as recomendações e os resultados da pesquisa não estiverem funcionando como esperado, [envie um tíquete de suporte](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
