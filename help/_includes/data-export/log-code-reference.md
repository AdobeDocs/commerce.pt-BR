---
source-git-commit: 1b8a6de3a35a626f211089955029207f8a88414c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---
# Referência de códigos de log do MDEE

Formato de código de log: `CDE<group_id>-<log_id>` (por exemplo, `CDE01-02`)

Fontes: `commerce-data-export`, `commerce-data-export-ee`, `saas-export`

Os códigos são atribuídos somente a mensagens de log de nível `error`, `warning` e `critical`. As mensagens de nível `info`, `notice` e `debug` são excluídas.

## Grupo 01 - Fase de coleta de dados

Códigos de log relacionados a erros ou avisos que ocorrem ao coletar dados de entidades de origem, normalmente em provedores de dados.
- As entidades afetadas podem ser processadas com dados parciais ou ignoradas totalmente se ocorrer um erro. Consulte a mensagem de log para obter detalhes.
- Os avisos podem indicar integração incorreta com a extensão Exportação de dados por módulos de terceiros; no entanto, as operações de sincronização normalmente continuam.

| Código de log | Nível | Mensagem |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|
| CDE01-01 | erro | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | aviso | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | aviso | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | erro | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | erro | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | erro | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | erro | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | erro | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | erro | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | erro | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | erro | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | aviso | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | erro | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | erro | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | erro | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | erro | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | aviso | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | aviso | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | aviso | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | aviso | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | erro | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | erro | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |

## Grupo 02 - Fase de envio de dados para SaaS

Códigos de log relacionados a erros ou avisos que ocorrem ao enviar dados de feed para endpoints SaaS.
- Os erros normalmente indicam falhas durante solicitações HTTP, tratamento de resposta ou validação de dados que impedem a aceitação de dados.
- Os avisos geralmente indicam condições transitórias (como limitação de taxa ou erros de servidor), em que as solicitações são repetidas automaticamente.

| Código de log | Nível | Mensagem |
|-----------|---------|---------|
| CDE02-01 | erro | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | erro | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | aviso | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | erro | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | erro | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | erro | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | aviso | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | aviso | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | erro | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | aviso | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | aviso | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | erro | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | aviso | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## Grupo 03 - Sincronização de Agendamento na Atualização da Entidade

Códigos de log relacionados a erros ou avisos que ocorrem ao agendar ou acionar a sincronização em resposta a alterações de entidade.
- Erros podem impedir que a sincronização incremental seja agendada e geralmente exigem uma ressincronização completa ou parcial para a recuperação.
- Os avisos indicam que uma operação de sincronização foi ignorada ou adiada devido a entradas não suportadas, identificadores ausentes ou problemas de configuração.

| Código de log | Nível | Mensagem |
|----------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| CDE03-01 | erro | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | aviso | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | erro | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | erro | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | erro | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | erro | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | aviso | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | erro | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | aviso | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
| CDE03-10 | aviso | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | erro | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | aviso | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | erro | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | erro | `CDE03-14 Failed to read config values. Indexer invalidation skipped. Error: {error_message}` |
| CDE03-15 | erro | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | erro | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | crítico | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | crítico | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | erro | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | erro | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |
| CDE03-21 | erro | `CDE03-21 Product sync scheduling error on attribute {%s} option change. Run resync. Error: %s` |
| CDE03-22 | aviso | `CDE03-22 StagedCategoryUrlKeyChangeDetector: no active row at version {version_id} for entity_id(s) [{entity_ids}]; skipping.` |
| CDE03-23 | erro | `CDE03-23 StagedCategoryUrlKeyChangeDetector: catalog_category url_key attribute not found; failing open.` |
| CDE03-24 | erro | `CDE03-24 InvalidateProductFeedOnCategoryUrlKeyChange: scheduler failed for path "{path}": {error_message}` |
| CDE03-25 | erro | `CDE03-25 InvalidateProductFeedOnCategoryUrlKeyChange: gate query failed: {error_message}` |
| CDE03-26 | erro | `CDE03-26 InvalidateProductFeedOnCategoryUrlKeyChange: unable to expand staged url_key category reindex scope: {error_message}` |
| CDE03-27 | erro | `CDE03-27 Failed to invalidate indexers after config "{config_section}" change. Error: {error_message}` |
| CDE03-28 | aviso | `CDE03-28 StagedCategoryUrlKeyChangeDetector: catalog category staging schema is not present; skipping staged url_key change detection.` |

## Grupo 04 - Erros Gerais Relacionados à Indexação ou Configuração

Códigos de log relacionados a erros durante o processo de indexação ou devido a uma configuração incorreta.

| Código de log | Nível | Mensagem |
|-----------|---------|---------|
| CDE04-02 | erro | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | aviso | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | erro | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | erro | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | erro | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | erro | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | erro | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | erro | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | erro | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | aviso | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | aviso | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | erro | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | erro | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | aviso | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | aviso | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | aviso | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | aviso | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | aviso | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | aviso | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
| CDE04-21 | erro | `CDE04-21 Failed to clean up deleted feed items for feed "{feed_name}". Error: {error_message}` |
