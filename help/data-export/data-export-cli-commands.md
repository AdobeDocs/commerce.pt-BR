---
title: Sincronizar feeds usando a CLI do Commerce
description: Saiba como usar comandos da CLI do Commerce para gerenciar feeds e processos de sincronização do  [!DNL data export extension]  nos serviços SaaS do Adobe Commerce.
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 670
ht-degree: 0%

---

# Sincronizar feeds usando a CLI do Commerce

O comando `saas:resync` no pacote `magento/saas-export` permite gerenciar a sincronização de dados para serviços SaaS [!DNL Adobe Commerce].

>[!NOTE]
>
>O comando `saas:resync` também se aplica aos feeds [!DNL Adobe Commerce Optimizer Connector], como `products`, `categories` e `priceBooks`. Consulte [Feeds com suporte](../aco-connector/reference/connector-reference.md#supported-feeds) para obter a lista completa de feeds de conector e nomes de indexador.

A Adobe não recomenda usar o comando `saas:resync` regularmente. Os cenários típicos para usar o comando são:

- Sincronização inicial
- Sincronizar dados com um novo espaço de dados após alterar a [ID do Espaço de Dados SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Solução de problemas

Monitorar operações de sincronização no arquivo `var/log/saas-export.log`.

## Sincronização inicial

>[!NOTE]
>
>A sincronização inicial é executada automaticamente quando o Live Search ou as Recomendações de produto são ativadas. Comandos manuais não são necessários.
>
>Para [!DNL Adobe Commerce Optimizer Connector] implantações, o comando `aco:config:init` agenda a sincronização completa inicial, invalidando todos os indexadores de feed de conector. Consulte [Habilitar a [!DNL Commerce Optimizer] integração](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration) e [Gerenciar sincronização com [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md).

Quando você aciona um `saas:resync` na linha de comando, dependendo do tamanho do catálogo, pode levar de alguns minutos a algumas horas para que os dados sejam atualizados.

As sincronizações de feed podem ser executadas em qualquer ordem - não há dependências permanentes entre elas. A sequência a seguir começa com os dados do escopo primeiro, que é um ponto de partida lógico, pois os escopos definem as exibições de armazenamento referenciadas por outros feeds.

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>Seu ambiente pode não incluir todos os feeds nesta sequência. Consulte [Feeds com suporte](reference/feed-table-reference.md#supported-feeds) para obter a lista de feeds completos, os nomes de feeds CLI e os requisitos de módulo.

## Opções de comando

O comando `saas:resync` dá suporte a várias operações de sincronização:

- Sincronização parcial por SKU
- Retomar sincronizações interrompidas
- Validar dados sem sincronização

Exibir todas as opções e sinalizadores de comando:

```shell
bin/magento saas:resync --help
```

Consulte as seções a seguir para obter descrições de opções com exemplos.

>[!NOTE]
>
>Para obter opções avançadas para gerenciar o processamento de exportação, consulte [Personalizar processamento de exportação](customize-export-processing.md).

## `--feed`

Obrigatório. Especifica a entidade de feed a ser ressincronizada.

`bin/magento saas:resync --help` opções e sinalizadores de comando de documentos. Ele não lista cada feed disponível em seu ambiente. Para obter a lista completa de feeds com nomes de CLI, IDs de indexador e tabelas de feed, consulte [Feeds com suporte](reference/feed-table-reference.md#supported-feeds).

>[!NOTE]
>
>Os módulos instalados determinam quais feeds você pode sincronizar novamente. Por exemplo, `productOverrides` exige [!DNL Adobe Commerce] na nuvem, no local ou Commerce as a Cloud Service, e `orders` exige o módulo de Ordens de Venda.

**Exemplo:**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

Ressincronizar parcialmente entidades específicas por suas IDs. Suporta os feeds `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions`.

Por padrão, ao usar a opção `--by-ids`, você especifica valores usando valores de SKU do produto. Para usar IDs de produto, adicione a opção `--id-type=productId`.

**Exemplos:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

Limpe a tabela indexadora de feed antes de reindexar e enviar dados para o SaaS. Com suporte somente para `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions`.

Se usada com a opção `--dry-run`, a operação executará uma operação de ressincronização de simulação para todos os itens.

>[!WARNING]
>
>O uso do comando resync com a opção `cleanup-feed` limpa o estado de exportação do feed local e pode levar à sincronização incompleta. Por exemplo, as exclusões de entidade em [!DNL Adobe Commerce] podem não ser refletidas nos Serviços Commerce conectados, ou entidades obsoletas podem permanecer nos índices remotos dos Serviços Commerce mesmo que tenham sido excluídas ou atualizadas em [!DNL Adobe Commerce]. Use essa opção somente para recriações completas do ambiente, como após uma limpeza de espaço de dados SaaS.

**Exemplo:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

Retoma uma operação de ressincronização interrompida. Suportado apenas para feeds `products`, `productAttributes` e `productOverrides`.

**Exemplo:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

Executa o processo de reindexação do feed sem enviá-lo para o SaaS e sem salvá-lo na tabela de feed. Essa opção é útil para identificar quaisquer problemas com seu conjunto de dados.

Adicione a variável de ambiente `EXPORTER_EXTENDED_LOG=1` para salvar a carga em `var/log/saas-export.log`.

**Exemplo:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### Testar itens específicos do feed

Teste itens específicos do feed adicionando a opção `--by-ids` com a coleção de logs estendidos para ver a carga gerada no arquivo `var/log/saas-export.log`.

**Exemplo:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### Testar todos os itens do feed

Por padrão, o feed enviado durante uma operação `resync --dry-run` inclui somente itens novos ou itens que não foram exportados anteriormente. Para incluir todos os itens no feed a serem processados, use a opção `--cleanup-feed`.

**Exemplo:**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

Reenvia dados existentes do catálogo para [!DNL Commerce Services] sem reindexação. Não compatível com feeds relacionados ao produto.

O comportamento varia de [modo de exportação](sync-overview.md#synchronization-modes):

- Modo herdado: reenvia todos os dados sem truncar.
- Modo imediato: a opção é ignorada, apenas sincroniza atualizações/falhas.

**Exemplo:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [Revisar logs e solucionar problemas](troubleshooting/logging.md) — Diagnosticar erros de exportação de dados e exportação de SaaS.
> - [Cenários de solução de problemas](troubleshooting/troubleshooting-scenarios.md) — Resolva erros de configuração e resultados de sincronização inesperados.
> - [Como a sincronização funciona](sync-overview.md) — Saiba mais sobre os modos de sincronização e o comportamento de repetição.
