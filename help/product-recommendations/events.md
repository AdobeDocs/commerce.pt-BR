---
title: Coletar dados
description: Saiba como os eventos coletam dados para  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# Coletar dados

Quando você instala e configura o [[!DNL Product Recommendations]](install-configure.md), o módulo implanta a coleta de dados comportamentais na vitrine. Esse mecanismo coleta dados comportamentais anônimos de seus compradores e habilita o [!DNL Product Recommendations]. Por exemplo, o evento `view` é usado para calcular o tipo de recomendação `Viewed this, viewed that`, e o evento `place-order` é usado para calcular o tipo de recomendação `Bought this, bought that`.

Para saber mais sobre os dados comportamentais que os eventos do [!DNL Product Recommendations] coletam, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

>[!NOTE]
>
>A coleta de dados para os fins de [!DNL Product Recommendations] não inclui informações de identificação pessoal (PII). Todos os identificadores de usuários, como IDs de cookies e endereços IP, são estritamente anônimos. Saiba [mais](https://www.adobe.com/privacy/experience-cloud.html).

## Clientes da área de saúde

Se você for um cliente da área de saúde e tiver instalado a [extensão HIPAA do Data Services](../data-connection/hipaa-readiness.md#installation), que está incluída na [conexão de dados](../data-connection/overview.md), a [!DNL Product Recommendations] interromperá a coleta de dados do evento da loja porque são gerados no lado do cliente.

Para continuar coletando e enviando dados do evento da loja, habilite novamente a coleta de eventos para [!DNL Product Recommendations]. Para obter mais informações, consulte [Configuração geral](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Tipos de dados e eventos

Há dois tipos de dados usados nas Recomendações de produto:

- **Comportamento** - Dados do envolvimento de um comprador no seu site, como exibições de produtos, itens adicionados ao carrinho e compras.
- **Catálogo** - Metadados do produto, como nome, preço, disponibilidade etc.

Quando você instala o módulo `magento/product-recommendations`, o Adobe AI agrega os dados comportamentais e de catálogo, criando Recomendações de Produto para cada tipo de recomendação. O serviço de Recomendações de Produto implanta essas recomendações na vitrine eletrônica em um widget que contém os _itens_ de produto recomendados.

Alguns tipos de recomendações usam os dados comportamentais dos compradores para treinar modelos de aprendizado de máquina e gerar recomendações personalizadas. Outros dependem apenas dos dados do catálogo. Para começar a usar as Recomendações de Produto rapidamente, escolha um dos seguintes tipos de recomendação somente para catálogo:

- `More like this`
- `Visual similarity`

### Arranque a frio

Quando você pode começar a usar tipos de recomendação que usam dados comportamentais? Depende. Essa situação é conhecida como o problema _Cold Start_.

O problema _Início a Frio_ é o tempo necessário para o treinamento de um modelo de aprendizado de máquina, antes que ele possa produzir recomendações eficazes. Para o Product Recommendations, a Adobe AI deve coletar dados suficientes para treinar seus modelos antes de implantar unidades de recomendação. Mais dados geralmente melhoram a precisão e a utilidade da recomendação. Como a coleta de dados ocorre no site ativo, inicie esse processo antecipadamente instalando e configurando o módulo `magento/product-recommendations`.

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

Enquanto seu site ativo coleta dados e o treinamento de modelos de aprendizado de máquina, conclua as tarefas restantes de teste e configuração. Quando os modelos tiverem dados suficientes para gerar recomendações úteis, implante as unidades de recomendação na loja.

Se o site não receber tráfego suficiente (exibições, compras ou tendências) para a maioria dos SKUs de produtos, o processo de aprendizado pode não ser concluído, fazendo com que os indicadores de prontidão no Administrador pareçam travados. Os indicadores de prontidão ajudam os comerciantes a escolher o melhor tipo de recomendação para sua loja, mas eles são apenas um guia e podem nunca chegar a 100%. Saiba mais sobre os indicadores de disponibilidade. [Saiba mais](create.md#readiness-indicators) sobre os indicadores de preparação.

### Recomendações de backup {#backuprecs}

Quando dados de entrada insuficientes impedem que uma unidade de recomendação retorne todos os itens solicitados, o Adobe Commerce os preenche com recomendações de backup. Por exemplo, depois de implantar o tipo de recomendação `Recommended for you` na página inicial, um comprador pela primeira vez pode não ter gerado dados comportamentais suficientes para recomendações personalizadas. Nesse caso, o Adobe Commerce exibe itens com base no tipo de recomendação `Most viewed `.

Se a coleta de dados de entrada for insuficiente, os seguintes tipos de recomendação farão fallback para o tipo de recomendação `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Avisos

- Os bloqueadores de anúncios e as configurações de privacidade podem impedir que eventos sejam capturados e podem fazer com que as [métricas](workspace.md#column-descriptions) de envolvimento e receita sejam reportadas incorretamente. Além disso, alguns eventos não são enviados porque os compradores saem da página ou por problemas de rede.
- [As implementações headless](headless.md) devem implementar eventos para potencializar o painel Recomendações de produto.
- Para produtos configuráveis, as Recomendações de produto usam a imagem do produto principal. Se o produto principal não tiver imagem, ele não aparecerá na unidade de recomendação.

>[!NOTE]
>
>Se o [Modo de restrição de cookies](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law) estiver habilitado, a Adobe Commerce não coletará dados comportamentais até que o comprador consente em usar cookies. Se o Modo de restrição de cookie estiver desativado, o Adobe Commerce coletará dados comportamentais por padrão.
