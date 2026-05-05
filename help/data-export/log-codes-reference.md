---
title: Referência de códigos de log da [!Data Export]
description: Lista de referência para códigos, mensagens e níveis de gravidade do log de exportação de dados para solucionar problemas de sincronização e decidir quando uma ressincronização parcial ou completa é necessária.
feature: Services
exl-id: c1341863-1ec4-4d67-8ff2-821ef0a61f33
source-git-commit: c3c0574667e49a2449858f992983df404b90fc07
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# Referência de códigos de log [!DNL Data Export]

Esta página fornece uma referência para as mensagens de log da Exportação de Dados para ajudar a solucionar problemas de sincronização e determinar quando uma ressincronização parcial ou completa é necessária. Inclui apenas códigos de log críticos, de erro e de aviso emitidos pela extensão [!DNL Data Export].

Consulte [Revisar logs e solucionar problemas](troubleshooting-logging.md) para obter informações sobre arquivos de log e orientações sobre solução de problemas.

## Detalhes do código de log

<!--
Source of truth: https://github.com/magento-commerce/commerce-data-export (docs/log-codes.md)
When log codes, messages, or log levels change in that repository, update this page to match.
Only columns retained here: Log Code, Message, Level. File paths are intentionally omitted.
-->

**Formato de código de log:** `CDE<group_id>-<log_id>` (por exemplo, `CDE01-02`)

**Fontes:** `commerce-data-export`, `commerce-data-export-ee`, `saas-export`

Os códigos são atribuídos somente a mensagens de log de nível `error`, `warning` e `critical`, e mensagens de nível `info`, `notice` e `debug` são excluídas.

## Grupo 01 - Fase de coleta de dados

Códigos de log relacionados a erros ou avisos que ocorrem ao coletar dados de entidades de origem, normalmente em provedores de dados.
- As entidades afetadas podem ser processadas com dados parciais ou ignoradas totalmente se ocorrer um erro. Consulte a mensagem de log para obter detalhes.
- Os avisos podem indicar integração incorreta com a extensão Exportação de dados por módulos de terceiros; no entanto, as operações de sincronização normalmente continuam.

| Código de log | Nível | Mensagem | Caminho do arquivo |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| CDE01-01 | erro | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` | `commerce-data-export/ExtraProductAttributes/Provider/AdvancedInventoryProvider.php:69` |
| CDE01-02 | aviso | `CDE01-02 Field "{field}" is missing in row {row_data}` | `commerce-data-export/ExtraProductAttributes/Provider/AdvancedInventoryProvider.php:101` |
| CDE01-03 | aviso | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` | `commerce-data-export/ExtraProductAttributes/Provider/AdvancedInventoryProvider.php:146` |
| CDE01-04 | erro | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` | `commerce-data-export/ExtraProductAttributes/Provider/AttributeSetProvider.php:55` |
| CDE01-05 | erro | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` | `commerce-data-export/DataExporter/Export/Processor.php:94` |
| CDE01-06 | erro | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` | `commerce-data-export/DataExporter/Export/Processor.php:127` |
| CDE01-07 | erro | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` | `commerce-data-export/DataExporter/Model/Indexer/DataSerializer.php:123` |
| CDE01-08 | erro | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` | `commerce-data-export/CatalogInventoryDataExporter/Model/Query/InventoryData.php:125` |
| CDE01-09 | erro | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` | `commerce-data-export/ConfigurableProductDataExporter/Model/Provider/Product/Options.php:434` |
| CDE01-10 | erro | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` | `commerce-data-export-ee/GiftCardProductDataExporter/Model/Provider/Product/Options.php:148` |
| CDE01-11 | erro | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` | `commerce-data-export-ee/GiftCardProductDataExporter/Model/Provider/Product/ShopperInputOptions.php:119` |
| CDE01-12 | aviso | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Model/Provider/ConfigurationProvider.php:183` |
| CDE01-13 | erro | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Model/Provider/ConfigurationProvider.php:245` |
| CDE01-14 | erro | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` | `commerce-data-export/DataExporter/Uuid/UuidManager.php:90` |
| CDE01-15 | erro | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` | `commerce-data-export/DataExporter/Uuid/UuidManager.php:106` |
| CDE01-16 | erro | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` | `commerce-data-export/DataExporter/Model/FeedHashBuilder.php:82` |
| CDE01-17 | aviso | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` | `commerce-data-export/CatalogDataExporter/Service/SystemAttributeRegistrar.php:182` |
| CDE01-18 | aviso | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` | `commerce-data-export/ProductPriceDataExporter/Model/Query/DateWebsiteProvider.php:75` |
| CDE01-19 | aviso | `CDE01-19 GiftCard {sku} does not have shopper input options` | `commerce-data-export-ee/GiftCardProductDataExporter/Plugin/GiftCardAsAttribute.php:102` |
| CDE01-20 | aviso | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` | `commerce-data-export-ee/GiftCardProductDataExporter/Plugin/GiftCardAsAttribute.php:131` |
| CDE01-21 | erro | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` | `commerce-data-export/CatalogDataExporter/Model/Provider/Categories.php:204` |
| CDE01-22 | erro | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` | `commerce-data-export/CatalogDataExporter/Model/Provider/Product/CategoryData.php:96` |

## Grupo 02 - Fase de envio de dados para SaaS

Códigos de log relacionados a erros ou avisos que ocorrem ao enviar dados de feed para endpoints SaaS.
- Os erros normalmente indicam falhas durante solicitações HTTP, tratamento de resposta ou validação de dados que impedem a aceitação de dados.
- Os avisos geralmente indicam condições transitórias (como limitação de taxa ou erros de servidor), em que as solicitações são repetidas automaticamente.

| Código de log | Nível | Mensagem | Caminho do arquivo |
|-----------|---------|---------|-----------|
| CDE02-01 | erro | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:261` |
| CDE02-02 | erro | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:280` |
| CDE02-03 | aviso | `CDE02-03 Cannot parse the API response because the request was not successful.` | `saas-export/SaaSCommon/Model/Http/ResponseParser.php:81` |
| CDE02-04 | erro | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` | `saas-export/SaaSCommon/Cron/SubmitFeed.php:206` |
| CDE02-05 | erro | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` | `saas-export/SaaSCommon/Cron/SubmitFeed.php:310` |
| CDE02-06 | erro | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` | `saas-export/SaaSCommon/Cron/SubmitFeed.php:257` |
| CDE02-07 | aviso | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:351` |
| CDE02-08 | aviso | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:356` |
| CDE02-09 | erro | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:362` |
| CDE02-10 | aviso | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:368` |
| CDE02-11 | aviso | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:374` |
| CDE02-12 | erro | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:379` |
| CDE02-13 | aviso | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` | `saas-export/SaaSCommon/Model/Http/Converter/Factory.php:96` |

## Grupo 03 - Sincronização de Agendamento na Atualização da Entidade

Códigos de log relacionados a erros ou avisos que ocorrem ao agendar ou acionar a sincronização em resposta a alterações de entidade.
- Erros podem impedir que a sincronização incremental seja agendada e geralmente exigem uma ressincronização completa ou parcial para a recuperação.
- Os avisos indicam que uma operação de sincronização foi ignorada ou adiada devido a entradas não suportadas, identificadores ausentes ou problemas de configuração.

| Código de log | Nível | Mensagem | Caminho do arquivo |
|-----------|----------|---------|-----------|
| CDE03-01 | erro | `CDE03-01 Cannot schedule resync for feeds` | `commerce-data-export/DataExporter/Service/FeedItemsResyncScheduler.php:119` |
| CDE03-02 | aviso | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ScheduleProductUpdateOnCategoryChange.php:55` |
| CDE03-03 | erro | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ReindexCategoryFeedOnSave.php:64` |
| CDE03-04 | erro | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ResyncProductsOnCategoryChange.php:71` |
| CDE03-05 | erro | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ResyncProductsOnCategoryChange.php:115` |
| CDE03-06 | erro | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Eav/Attribute/ProductAttributeDelete.php:102` |
| CDE03-07 | aviso | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` | `commerce-data-export/CatalogInventoryDataExporter/Model/Plugin/ScheduleProductUpdate.php:61` |
| CDE03-08 | erro | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` | `commerce-data-export/ProductVariantDataExporter/Plugin/ReindexVariantsAfterSave.php:76` |
| CDE03-09 | aviso | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` | `saas-export/SaaSCommon/Model/ResyncManager.php:295` |
| CDE03-10 | aviso | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` | `saas-export/SaaSCommon/Model/ResyncManager.php:313` |
| CDE03-11 | erro | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Plugin/MarkEntityAsDeletedOnCategoryRemove.php:86` |
| CDE03-12 | aviso | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/Indexer/Category/TriggerFullResync.php:58` |
| CDE03-13 | erro | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` | `commerce-data-export/DataExporter/Service/IndexInvalidationManager.php:58` |
| CDE03-14 | erro | `CDE03-14 Failed to read config values. Indexer invalidation for event "{event_name}" skipped. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Index/InvalidateOnConfigChange.php:80` |
| CDE03-15 | erro | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Plugin/InvalidateOnConfigChange.php:120` |
| CDE03-16 | erro | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Plugin/GlobalConfigurationReindex.php:73` |
| CDE03-17 | crítico | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterChangeCustomerGroup.php:61` |
| CDE03-18 | crítico | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterChangeCustomerGroup.php:85` |
| CDE03-19 | erro | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterTableMaintenance.php:69` |
| CDE03-20 | erro | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterTableMaintenance.php:93` |

## Grupo 04 - Erros Gerais Relacionados à Indexação ou Configuração

Códigos de log relacionados a erros durante o processo de indexação ou devido a uma configuração incorreta.

| Código de log | Nível | Mensagem | Caminho do arquivo |
|-----------|---------|---------|-----------|
| CDE04-02 | erro | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` | `commerce-data-export/DataExporter/Setup/Recurring.php:84` |
| CDE04-03 | aviso | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` | `commerce-data-export/DataExporter/Plugin/MviewUpdatePlugin.php:63` |
| CDE04-04 | erro | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` | `commerce-data-export/DataExporter/Service/FeedIndexerProvider.php:50` |
| CDE04-05 | erro | `CDE04-05 Cannot load feed indexer for feed` | `commerce-data-export/DataExporter/Service/FeedIndexerProvider.php:60` |
| CDE04-06 | erro | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` | `commerce-data-export/CatalogDataExporter/Plugin/DDLTrigger/ResetTriggers.php:73` |
| CDE04-07 | erro | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` | `commerce-data-export/DataExporter/Model/Batch/FeedChangeLog/Generator.php:104` |
| CDE04-08 | erro | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` | `commerce-data-export/DataExporter/Model/Batch/Feed/Generator.php:94` |
| CDE04-09 | erro | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` | `commerce-data-export/DataExporter/Model/Batch/FeedSource/Generator.php:97` |
| CDE04-10 | erro | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdate.php:172` |
| CDE04-11 | aviso | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdate.php:232` |
| CDE04-12 | aviso | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/ViewMaterializer.php:170` |
| CDE04-13 | erro | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/FeedUpdater.php:125` |
| CDE04-14 | erro | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdateDelete.php:98` |
| CDE04-15 | aviso | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` | `commerce-data-export/DataExporter/Model/FeedExportStatus.php:93` |
| CDE04-16 | aviso | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` | `commerce-data-export/DataExporter/Model/Batch/BatchTable.php:130` |
| CDE04-17 | aviso | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` | `commerce-data-export/DataExporter/Plugin/ForceExporterIndexerModeOnSchedule.php:59` |
| CDE04-18 | aviso | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` | `commerce-data-export/CatalogDataExporter/Plugin/FilterChangeLogTable.php:43` |
| CDE04-19 | aviso | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdate.php:439` |
| CDE04-20 | aviso | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexer.php:204` |
