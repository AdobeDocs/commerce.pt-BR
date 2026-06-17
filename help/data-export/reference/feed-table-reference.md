---
title: Referência do esquema da tabela do feed
description: Saiba mais sobre o esquema de tabela de feed usado por [!DNL SaaS Data Export] para rastrear o estado do item de feed, o status de exportação e os detalhes do erro.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 416
ht-degree: 0%

---


# Referência de esquema de tabela de feed

Cada feed tem uma tabela MySQL dedicada no banco de dados [!DNL Adobe Commerce]. Todas as tabelas de feed compartilham a mesma estrutura de coluna. A tabela abaixo lista cada feed com seu nome de feed CLI, ID do indexador e nome de tabela de feed.

## Feeds suportados

A lista real de feeds depende do pacote [!DNL SaaS Data Export] instalado.


| Feed (`--feed`) | Finalidade | ID do Indexador | Tabela de feed | Modo de exportação |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | Catálogo de produtos (atributos, categorias, imagens etc.) | `catalog_data_exporter_products` | `cde_products_feed` | Imediato |
| `productAttributes` | Definições de atributos e metadados. Usado para definir o esquema de pesquisa. | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | Imediato |
| `categories` | Dados de categorias | `catalog_data_exporter_categories` | `cde_categories_feed` | Imediato |
| `prices` | Preços de produtos com preços de grupo de clientes e preços de nível | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | Imediato |
| `variants` | Variantes de produtos configuráveis | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | Imediato |
| `scopesWebsite` | Site com códigos de exibição de loja | `scopes_website_data_exporter` | `scopes_website_data_exporter` | Herdados |
| `scopesCustomerGroup` | Definições de grupo de clientes | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | Herdados |
| `productOverrides` | Permissões de produto calculadas | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | Imediato |
| `categoryPermissions` *(EE)* | Dados brutos de permissões de categoria | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | Imediato |
| `orders` | Status das ordens de venda | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | Herdados |

A coluna **Modo de Exportação** indica como cada feed coleta e envia dados:

- **Feeds de modo imediato** — Colete dados, ignore itens inalterados usando hashes de conteúdo (desduplicação de hash) e envie atualizações na mesma execução do indexador.
- **Feeds do modo herdado** (`scopesWebsite`, `scopesCustomerGroup`, `orders`) — Primeiro armazene os dados montados na tabela de feed e envie-os por meio de um trabalho cron separado.

Consulte [Modos de sincronização](../sync-overview.md#synchronization-modes).

## Esquema

| Coluna | Tipo | Descrição |
| --- | --- | ---------------- |
| `id` | INT (PK) | Chave primária de incremento automático |
| `source_entity_id` | INT | ID de entidade da tabela de origem do Commerce (por exemplo, `catalog_product_entity.entity_id`) |
| `feed_id` | VARCHAR | Identificador exclusivo de um item de feed. Calculado como um hash dos campos de identidade do item (por exemplo, `sku + storeViewCode`), não como um valor de incremento automático. |
| `feed_data` | JSON | Carga do feed deste item. Somente informações mínimas como identificador de entidade e escopo são preenchidas. Quando `PERSIST_EXPORTED_FEED=1` é definido, a carga completa é armazenada. |
| `feed_hash` | VARCHAR | Hash de conteúdo usado para detecção de alterações. Calculado a partir da carga, excluindo carimbos de data e hora (`modifiedAt`, `updatedAt`). Se o hash corresponder à exportação anterior, o item não será reenviado. |
| `is_deleted` | TINYINT | Marcador de exclusão reversível. Defina como `1` quando a entidade for excluída no Commerce. |
| `modified_at` | CARIMBO DE DATA E HORA | Última vez que este item de feed foi modificado |
| `status` | INT | Código de status do envio da última tentativa de exportação. Consulte [Envio de feed e tratamento de erros HTTP](../sync-overview.md#feed-submission-and-http-error-handling). |
| `errors` | TEXTO | Detalhes de erro codificados em JSON retornados pelo serviço SaaS para este item |
| `metadata` | JSON | Sinalizadores de sincronização interna e informações de metadados de bloqueio usados pela estrutura de exportação |

## Consultas de diagnóstico comuns

Use as seguintes consultas SQL para inspecionar diretamente o estado da tabela de feed. Substitua `cde_products_feed` pela tabela do feed que você está investigando. Consulte [Feeds com suporte](#supported-feeds) para obter a lista completa de nomes de tabela.

**Localizar todos os itens que não foram exportados com êxito:**

```sql
SELECT source_entity_id, status, errors, modified_at
FROM cde_products_feed
WHERE status != 200
ORDER BY modified_at DESC
LIMIT 50;
```

**Verifique o status de exportação de uma SKU específica em todos os escopos:**

```sql
SELECT p.sku, f.status, f.modified_at, f.is_deleted, f.feed_data, f.errors
FROM catalog_product_entity p
LEFT JOIN cde_products_feed f ON f.source_entity_id = p.entity_id
WHERE p.sku = 'ADB295';
```


>[!MORELIKETHIS]
>
>- [Sincronizar dados com a Exportação de dados SaaS](../sync-overview.md)
>- [Exibir e gerenciar a sincronização](../data-sync-manage.md)
>- [Sincronizar feeds usando a CLI do Commerce](../data-export-cli-commands.md)
