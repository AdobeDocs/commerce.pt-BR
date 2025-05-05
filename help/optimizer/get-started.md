---
title: Introdução com [!DNL Adobe Commerce Optimizer]
description: Aprenda a começar com [!DNL Adobe Commerce Optimizer] isso.
hide: true
recommendations: noCatalog
source-git-commit: d716dd9d75beb642bfad30271b6ecd3490ee7328
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Começar

>[!NOTE]
>
>Esta documentação descreve um produto no desenvolvimento de acesso antecipado e não reflete todas as funcionalidade destinadas à disponibilidade geral.

Este guia o conduz a criar e trabalhar com um [!DNL Adobe Commerce Optimizer] instância.

<!--Click the tabs below to see high-level workflow overviews for the following user types:

- Administrators
- Merchants
- Developers

>[!BEGINTABS]

>[!TAB Administrator and merchant workflow]

This diagram provides a high-level overview of how administrators and merchants access and manage [!DNL Adobe Commerce Optimizer] instances. See the [Adobe Admin Console Guide](https://helpx.adobe.com/enterprise/admin-guide.html) for more information about administrator workflows.

NEED DIAGRAM

>[!TAB Developer workflow]

This diagram provides a high-level overview of how developers create integrations for [!DNL Adobe Commerce Optimizer] using App Builder. See the [API documentation](https://developer.adobe.com/commerce/services/cloud/) for more information.

NEED DIAGRAM

>[!ENDTABS]
-->

## Provisionamento

Depois que as [!DNL Adobe Commerce Optimizer] instâncias estiverem prontas, o [!DNL Adobe Commerce Optimizer] provisionamento equipe fornece os seguintes endpoints:

| Item | Amostra URL | Propósito |
|---|---|---|
| [!DNL Adobe Commerce Optimizer] UI | `https://experience.adobe.com/#/@commerceprojectbeacon/commerce-optimizer-studio?tenant=<tenantId>` | Acesse o interface do Comércio Optimizer para gerenciar o catálogo em:<br>1. Regras de comercialização (Product Discovery, Product recomendações).<br>2. Gerenciamento de catálogos (criação de canais e políticas).<br>3. Insights de dados (Exibir o status de ingestão de dados do catálogo). |
| APIs de vitrine | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/graphql` | Acesse as APIs necessárias para configurar sua vitrine Comércio fornecida pelos Serviços de entrega do Edge. |
| APIs de ingestão de dados de catálogo | `https://na1-sandbox.api.commerce.adobe.com/<tenantId>/v1/catalog/<entity>` | Acesse as APIs necessárias para assimilar os dados do catálogo. |

Como participante de acesso antecipado, você receberá um e-mail com uma link segura que, juntamente com o token IMS, permite fazer logon [!DNL Adobe Commerce Optimizer] ou fazer chamadas de API.

## Configurar a vitrine

Agora que tem uma [!DNL Adobe Commerce Optimizer] instância, você está pronto para continuar [configurando](./storefront.md) seu Comércio Storefront fornecido pelos Serviços de Entrega de Edge.

## Dados de catálogo disponíveis para participantes do acesso antecipado

Como participante do acesso antecipado, o [!DNL Adobe Commerce Optimizer] instância contém dados simulados do catálogo baseados no caso[&#128279;](./use-case/admin-use-case.md) de uso do Carvelo. Os dados simulados, juntamente com alguns canais e políticas pré-configurados, ajudam você a se familiarizar com as [!DNL Adobe Commerce Optimizer] interface.

<!--Ingest catalog data

By default, [!DNL Adobe Commerce Optimizer] instances do not include any product data.

See the [Ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) documentation to learn how you can import your catalog data into [!DNL Adobe Commerce Optimizer].

The catalog data that you ingest is visible in the [data insights](./insights-overview.md) page. Additionally, you can use the [Catalog](./catalog-overview.md) page to define the channels and policies.-->
