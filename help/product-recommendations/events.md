---
title: Coletar dados
description: Saiba como os eventos coletam dados para  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Coletar dados

Quando você instala e configura recursos do Adobe Commerce baseados em SaaS, como [[!DNL Product Recommendations]](install-configure.md) ou [[!DNL Live Search]](../live-search/install.md), os módulos implantam a coleção de dados comportamentais na loja. Esse mecanismo coleta dados comportamentais anônimos de seus compradores e habilita o [!DNL Product Recommendations]. Por exemplo, o evento `view` é usado para calcular o tipo de recomendação `Viewed this, viewed that`, e o evento `place-order` é usado para calcular o tipo de recomendação `Bought this, bought that`.

>[!NOTE]
>
>A coleta de dados para os fins de [!DNL Product Recommendations] não inclui informações de identificação pessoal (PII). Todos os identificadores de usuários, como IDs de cookies e endereços IP, são estritamente anônimos. Saiba [mais](https://www.adobe.com/privacy/experience-cloud.html).

## Clientes da área de saúde

Se você for um cliente da área de saúde e tiver instalado a [extensão HIPAA do Data Services](../data-connection/hipaa-readiness.md#installation), que faz parte da [conexão de dados](../data-connection/overview.md), os dados do evento de vitrine usados por [!DNL Product Recommendations] não serão mais capturados. Isso ocorre porque os dados do evento da loja são gerados no lado do cliente. Para continuar capturando e enviando dados do evento da loja, habilite novamente a coleção de eventos para [!DNL Product Recommendations]. Consulte [configuração geral](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services) para saber mais.

## Tipos de dados e eventos

Há dois tipos de dados usados nas Recomendações de produto:

- **Comportamento** - Dados do envolvimento de um comprador no seu site, como exibições de produtos, itens adicionados ao carrinho e compras.
- **Catálogo** - Metadados do produto, como nome, preço, disponibilidade etc.

Quando você instala o módulo `magento/product-recommendations`, o Adobe Sensei agrega os dados comportamentais e de catálogo, criando Recomendações de Produto para cada tipo de recomendação. O serviço de Recomendações de Produto implanta essas recomendações na vitrine eletrônica em um widget que contém os _itens_ de produto recomendados.

Alguns tipos de recomendações usam dados comportamentais de seus compradores para treinar modelos de aprendizado de máquina para criar recomendações personalizadas. Outros tipos de recomendações usam apenas dados de catálogo e não usam dados comportamentais. Se você quiser começar rapidamente a usar o Product Recommendations em seu site, poderá usar os seguintes tipos de recomendações somente de catálogo:

- `More like this`
- `Visual similarity`

### Arranque a frio

Quando você pode começar a usar tipos de recomendação que usam dados comportamentais? Depende. Isso é conhecido como o problema _Cold Start_.

O problema _Cold Start_ refere-se ao tempo que um modelo leva para ser treinado e se tornar efetivo. Para recomendações de produtos, isso significa aguardar que o Adobe Sensei colete dados suficientes para treinar seus modelos de aprendizado de máquina antes de implantar unidades de recomendação em seu site. Quanto mais dados os modelos tiverem, mais precisas e úteis serão as recomendações. Como a coleta de dados ocorre em um site ativo, é melhor iniciar esse processo antecipadamente instalando e configurando o módulo `magento/production-recommendations`.

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
- O Adobe Commerce recalcula dados comportamentais a cada quatro horas. As recomendações se tornam mais precisas quanto mais tempo forem usadas no site.

Para ajudá-lo a visualizar o progresso do treinamento de cada tipo de recomendação, a página [criar recomendação](create.md#readiness-indicators) exibe indicadores de preparação.

Enquanto os dados estão sendo coletados em seu site ativo e os modelos de aprendizado de máquina estão sendo treinados, você pode concluir outras tarefas de teste e configuração necessárias para definir as recomendações. Quando você terminar este trabalho, os modelos terão dados suficientes para criar recomendações úteis, permitindo que você os implante em sua loja.

Se o site não receber tráfego suficiente (exibições, compras, tendências) para a maioria dos SKUs de produtos, talvez não haja dados suficientes para concluir o processo de aprendizado. Isso pode fazer com que o indicador de prontidão do Administrador pareça travado. Os indicadores de prontidão devem fornecer aos comerciantes outro ponto de dados para escolher qual tipo de recomendações é melhor para sua loja. Os números são um guia e podem nunca chegar a 100%. [Saiba mais](create.md#readiness-indicators) sobre os indicadores de preparação.

### Recomendações de backup {#backuprecs}

Se os dados de entrada forem insuficientes para fornecer todos os itens de recomendação solicitados em uma unidade, a Adobe Commerce fornecerá recomendações de backup para preencher as unidades de recomendação. Por exemplo, se você implantar o tipo de recomendação `Recommended for you` na sua página inicial, um comprador novo no site não terá gerado dados comportamentais suficientes para recomendar com precisão os produtos personalizados. Nesse caso, o Adobe Commerce exibe itens baseados no tipo de recomendação `Most viewed` para esse comprador.

No caso de coleta de dados de entrada insuficiente, os seguintes tipos de recomendação fazem fallback para o tipo de recomendação `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### Eventos

O [Coletor de Eventos da Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) lista todos os eventos implantados na sua loja. Nessa lista, há um subconjunto de eventos específicos para [!DNL Product Recommendations]. Esses eventos coletam dados quando os compradores interagem com as unidades de recomendação na loja e alimentam as métricas para analisar o desempenho de suas recomendações.

| Evento | Descrição |
| --- | --- |
| `impression-render` | Enviado quando a unidade de recomendação é renderizada na página. Se uma página tiver duas unidades de recomendação (compradas, exibição), dois eventos `impression-render` serão enviados. Esse evento é usado para rastrear a métrica para impressões. |
| `rec-add-to-cart-click` | O comprador clica no botão **Adicionar ao carrinho** para um item na unidade de recomendação. |
| `rec-click` | O comprador clica em um produto na unidade de recomendação. |
| `view` | Enviado quando a unidade de recomendação se torna pelo menos 50% visível, como ao rolar a página para baixo. Por exemplo, se uma unidade de recomendação tiver duas linhas, um evento `view` será enviado quando uma linha mais um pixel da segunda linha se tornar visível para o comprador. Se o comprador rolar a página várias vezes para cima e para baixo, o evento `view` será enviado tantas vezes quanto o comprador vir toda a unidade de recomendação novamente na página. |

>[!NOTE]
>
>As métricas de Recomendação de produto são otimizadas para vitrines da Luma. Se sua loja for implementada com o PWA Studio, consulte a [documentação do PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se você usa uma tecnologia de front-end personalizada, como o React ou o Vue JS, saiba como integrar o [Product Recommendations em um ambiente headless](headless.md).

#### Eventos de painel obrigatórios

Os seguintes eventos são necessários para preencher o [[!DNL Product Recommendations] painel](workspace.md)

| Coluna do painel | Eventos | Ingressar no campo |
| ---------------- | --------- | ----------- |
| Impressões | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Visualizações | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Cliques | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Receita | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Receita LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Os seguintes eventos não são específicos das Recomendações de produto, mas são necessários para que o Adobe Sensei interprete os dados do comprador corretamente:

- `view`
- `add-to-cart`
- `place-order`

#### Tipo de recomendação

Esta tabela descreve os eventos usados por cada tipo de recomendação.

| Tipo de recomendação | Eventos | Página |
| --- | --- | --- |
| Mais visualizados | `page-view`<br>`product-view` | Página de detalhes do produto |
| Mais comprados | `page-view`<br>`complete-checkout` | Carrinho/Check-out |
| Mais adicionados ao carrinho | `page-view`<br>`add-to-cart` | Página de detalhes do produto<br>Página de listagem do produto<br>Carrinho<br>Lista de desejos |
| Visualizou isto, visualizou aquilo | `page-view`<br>`product-view` | Página de detalhes do produto |
| Visualizou isto, comprou aquilo | Registros de produto | `page-view`<br>`product-view` | Página de detalhes do produto<br>Carrinho/Check-out |
| Comprei isto, comprei aquilo | Registros de produto | `page-view`<br>`product-view` | Página de detalhes do produto |
| Tendências | `page-view`<br>`product-view` | Página de detalhes do produto |
| Conversão: exibir para compra | Registros de produto | `page-view`<br>`product-view` | Página de detalhes do produto |
| Conversão: exibir para compra | Registros de produto | `page-view`<br>`complete-checkout` | Carrinho/Check-out |
| Conversão: exibir para carrinho | Registros de produto | `page-view`<br>`product-view` | Página de detalhes do produto |
| Conversão: exibir para carrinho | Registros de produto | `page-view`<br>`add-to-cart` | Página de detalhes do produto<br>Página de listagem do produto<br>Carrinho<br>Lista de desejos |

#### Avisos

- Os bloqueadores de anúncios e as configurações de privacidade podem impedir que eventos sejam capturados e podem fazer com que as [métricas](workspace.md#column-descriptions) de envolvimento e receita sejam reportadas incorretamente. Além disso, alguns eventos podem não ser enviados porque os compradores saem da página ou por problemas de rede.
- [As implementações headless](headless.md) devem implementar eventos para potencializar o painel Recomendações de produto.
- Para produtos configuráveis, as Recomendações de produto usam a imagem do produto principal na unidade de recomendação. Se o produto configurável não tiver uma imagem especificada, a unidade de recomendação ficará vazia para esse produto específico.

>[!NOTE]
>
>Se o [Modo de restrição de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) estiver habilitado, a Adobe Commerce não coletará dados comportamentais até que o comprador consente em usar cookies. Se o Modo de restrição de cookie estiver desativado, o Adobe Commerce coletará dados comportamentais por padrão.
