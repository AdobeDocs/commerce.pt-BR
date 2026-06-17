---
title: '[!DNL Adobe Commerce Optimizer Connector] Módulos e Pontos de Extremidade de Feed'
description: Saiba mais sobre  [!DNL Adobe Commerce Optimizer Connector] módulos, pontos de extremidade da API de feed de catálogo, limites de lote e caminhos de configuração core_config_data para  [!DNL Adobe Commerce].
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 296
ht-degree: 1%

---

# Módulos de conector e endpoints de feed

Esta referência lista os pacotes de módulo [!DNL Adobe Commerce Optimizer Connector], pontos de extremidade de API de feed com suporte e caminhos de chave de configuração armazenados em `core_config_data`. Para saber como esses componentes funcionam juntos durante a sincronização, consulte [Pipeline de sincronização do conector](../connector-sync-pipeline.md).

## Módulos

O conector inclui vários módulos do Magento que coletam dados de catálogo, mapeiam dados de feed para o formato compatível com a API [!DNL Commerce Optimizer] e gerenciam o envio e o controle de escopo. A tabela a seguir resume cada módulo e sua função.

| Módulo | Função |
| ------ | ---- |
| `DataExporterAdapter` | Mapeia feeds [!DNL Adobe Commerce] para o formato exigido pela API [!DNL Adobe Commerce Optimizer]. Substitui o pool de feeds e a configuração de esquema. |
| `SaasExportAdapter` | Roteia feeds [!DNL Commerce Optimizer] para a API de assimilação e bloqueia o envio de feeds sem suporte. |
| `CommerceAcoExporter` | Gerencia credenciais do [!DNL Commerce Optimizer] e fornece comandos de configuração da CLI |
| `CommerceAdapter` | Camada de compatibilidade de API [!DNL Commerce Optimizer] (GraphQL, pacote, suplemento ao carrinho, interface de configuração) |
| `PriceBookDataExporter` | Feed do catálogo de preços indexado por site e grupo de clientes |
| `SaasPriceBook` | Infraestrutura SaaS para envio da tabela de preços |
| `CommerceOptimizerScopeMapper` | Ativação de sincronização por site e por visualização de loja |

## Feeds suportados

O conector envia vários tipos de feed para o [!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}. A tabela abaixo lista cada feed com seu ponto de extremidade, limite de lote, nome do indexador e tabela de feed em [!DNL Adobe Commerce].

| Feed | Ponto de Extremidade de API [!DNL Commerce Optimizer] | Limite do lote | Nome do índice de CA | Tabela de feed |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

Os feeds `products`, `productAttributes`, `categories` e `prices` reutilizam dados coletados por [!DNL SaaS Data Export] indexadores. O conector gera o feed `priceBooks` do site e da configuração do grupo de clientes e não depende de um indexador [!DNL SaaS Data Export].

Para obter detalhes de mapeamento em nível de campo para cada feed, consulte [Mapeamento de campo para [!DNL Commerce Optimizer Connector] feeds](field-mapping.md).
Para estimar quanto tempo uma sincronização levará com base no tamanho do catálogo, consulte [Estimar volume de dados e tempo de sincronização](estimate-data-volume-sync-time.md).

## Caminhos de configuração

[!DNL Commerce Optimizer Connector] credenciais e URLs de serviço estão armazenadas em `core_config_data` sob o prefixo de caminho `aco_exporter/general/`. Execute `bin/magento aco:config:show` para revisar os valores atuais. O comando não exibe o segredo do cliente.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
