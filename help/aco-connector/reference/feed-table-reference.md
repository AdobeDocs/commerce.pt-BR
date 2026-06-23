---
title: Referência do esquema da tabela do feed
description: Saiba mais sobre o esquema de tabela de feed usado pelo  [!DNL Adobe Commerce Optimizer Connector]  para rastrear o estado do item de feed, o status de exportação e os detalhes do erro.
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# Referência de esquema de tabela de feed

Cada feed tem uma tabela MySQL dedicada no banco de dados [!DNL Adobe Commerce]. Todas as tabelas de feed compartilham a mesma estrutura de coluna.

## Feeds suportados

Para obter a lista completa de feeds com suporte a pontos de extremidade de API, limites de lote, nomes de indexador e nomes de tabela de feed, consulte [Módulos de conector e pontos de extremidade de feed](connector-reference.md#supported-feeds).

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
| `status` | INT | Código de status do envio da última tentativa de exportação. Consulte [Envio de feed e tratamento de erros](../connector-sync-pipeline.md#feed-submission-and-error-handling). |
| `errors` | TEXTO | Detalhes de erros codificados em JSON retornados pela API [!DNL Commerce Optimizer] para este item |
| `metadata` | JSON | Sinalizadores de sincronização interna e informações de metadados de bloqueio usados pela estrutura de exportação |

## Consultas de diagnóstico comuns

Use as seguintes consultas SQL para inspecionar diretamente o estado da tabela de feed. A coluna `feed_data` armazena dados no formato de API [!DNL Adobe Commerce Optimizer]. Substitua valores de espaço reservado como `<SKU>`, `<ATTRIBUTE_CODE>`, `<SLUG>` e `<PRICE_BOOK_ID>` por valores reais do seu ambiente.

**Feed de produtos - por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Feed de atributos do produto - por código de atributo:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**Feed de categorias - por caminho de URL:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**Feed de preços - por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Feed de catálogos de preços - por ID de catálogo de preços:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [Módulos de conector e pontos de extremidade de feed](connector-reference.md)
>- [Pipeline de sincronização do conector](../connector-sync-pipeline.md)
>- [Gerenciar sincronização](../data-sync-manage.md)
>- [Mapeamento de campos para feeds de conector](field-mapping.md)
