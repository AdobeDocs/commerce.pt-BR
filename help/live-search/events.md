---
title: '[!DNL Live Search] Eventos'
description: Saiba como os eventos coletam dados para  [!DNL Live Search].
feature: Services, Eventing
exl-id: a9f4f254-d8ff-46f1-8deb-a75b90d70d52
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search] Eventos

[!DNL Live Search] usa eventos para potencializar algoritmos de pesquisa como &quot;Mais visualizados&quot; e &quot;Visualizou isto, Visualizou aquilo&quot;. Embora o [tema Luma de amostra do Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/design/themes/themes#the-default-theme) obtenha eventos por padrão, o headless e outras implementações personalizadas precisam implementar eventos para suas próprias necessidades.

Esta tabela descreve os eventos usados por [!DNL Live Search] [estratégias de classificação](rules-add.md#intelligent-ranking).

| Estratégia de classificação | Eventos | Página |
| --- | --- | --- |
| Mais visualizados | `page-view`<br>`product-view` | Página de detalhes do produto |
| Mais comprados | `page-view`<br>`place-order` | Carrinho/Check-out |
| Mais adicionados ao carrinho | `page-view`<br>`add-to-cart` | Página de detalhes do produto<br>Página de listagem do produto<br>Carrinho<br>Lista de desejos |
| Visualizou isto, visualizou aquilo | `page-view`<br>`product-view` | Página de detalhes do produto |

>[!NOTE]
>
>A coleta de dados para os fins de [!DNL Live Search] não inclui informações de identificação pessoal (PII). Todos os identificadores de usuários, como IDs de cookies e endereços IP, são estritamente anônimos. [Saiba mais](https://www.adobe.com/privacy/experience-cloud.html).

## Eventos de painel obrigatórios

Alguns eventos são necessários para preencher o [painel do Live Search](performance.md)

| Área do painel | Eventos | Ingressar no campo |
| ------------------- | ------------- | ---------- |
| Pesquisas únicas | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Nenhuma pesquisa de resultados | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Taxa de resultados zero | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Pesquisas populares | `page-view`, `search-request-sent`, `search-response-received` | `searchRequestId` |
| Média posição do clique | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| Taxa de cliques | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`, `sku`, `parentSku` |
| Índice de conversão | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`, `sku`, `parentSku` |

### Contextos obrigatórios

Todos os eventos exigem os contextos `Page` e `Storefront`. Isso deve acontecer no nível da página/camada do aplicativo da loja em vez de ao gerar eventos individuais (por exemplo, em uma loja PHP, o contêiner do aplicativo PHP é responsável por configurá-los no tempo de execução).

## Uso

Esta é uma amostra de implementação do evento `search-request-sent`:

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## Avisos

- Os bloqueadores de anúncios e as configurações de privacidade podem impedir que eventos sejam capturados e podem fazer com que as [métricas](performance.md) de envolvimento e receita sejam reportadas incorretamente. Além disso, alguns eventos podem não ser enviados porque os compradores saem da página ou por problemas de rede.
- As implementações headless devem implementar eventos para potencializar o merchandising inteligente.

>[!NOTE]
>
>Se o [Modo de restrição de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=pt-BR) estiver habilitado, a Adobe Commerce não coletará dados comportamentais até que o comprador consente em usar cookies. Se o Modo de restrição de cookie estiver desativado, o Adobe Commerce coletará dados comportamentais por padrão.
