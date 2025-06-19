---
title: Introdução ao  [!DNL Adobe Commerce Optimizer]
description: Saiba como começar a usar o  [!DNL Adobe Commerce Optimizer].
hide: true
recommendations: noCatalog
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Introdução

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

Este guia orienta você na criação e no trabalho com uma instância do [!DNL Adobe Commerce Optimizer].

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/br/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/webapi/rest/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Provisionamento

Depois que as instâncias do [!DNL Adobe Commerce Optimizer] estiverem prontas, a equipe de provisionamento do [!DNL Adobe Commerce Optimizer] fornecerá os seguintes pontos de extremidade:

| Item | Amostra do URL | Finalidade |
|---|---|---|
| IU [!DNL Adobe Commerce Optimizer] | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Acesse a interface do Commerce Optimizer para gerenciar seu catálogo em:<br>1. Regras de merchandising (descoberta de produtos, recomendações de produtos).<br>2. Gerenciamento de catálogo (criação de canal e política).<br>3. Insights de dados (veja o status de assimilação de dados do catálogo). |
| APIs da loja | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Acesse as APIs necessárias para configurar sua loja do Commerce com a tecnologia do Edge Delivery Services. |
| APIs de assimilação de dados do catálogo | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | Acesse as APIs necessárias para assimilar os dados do catálogo. |

>[!NOTE]
>
>Consulte a [documentação do desenvolvedor](https://developer-stage.adobe.com/commerce/services/composable-catalog/) para saber mais sobre as APIs necessárias para a configuração da loja e a assimilação do catálogo.

Como participante de acesso antecipado, você receberá um email com um link seguro que, junto com o token IMS, permite fazer logon no [!DNL Adobe Commerce Optimizer] ou fazer chamadas de API.

## Configurar a loja

Agora que você tem uma instância do [!DNL Adobe Commerce Optimizer], está pronto para prosseguir com a [configuração](./storefront.md) da sua Commerce Storefront habilitada pela Edge Delivery Services.

## Dados de catálogo disponíveis para os participantes de acesso antecipado

Como um participante de acesso antecipado, a instância [!DNL Adobe Commerce Optimizer] contém dados de catálogo simulados com base no [caso de uso Carvelo](./use-case/admin-use-case.md). Os dados simulados, juntamente com alguns canais e políticas pré-configurados, ajudam você a se familiarizar com a interface do usuário do [!DNL Adobe Commerce Optimizer].

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
