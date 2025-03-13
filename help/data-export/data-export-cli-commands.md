---
title: Sincronizar feeds usando a CLI do Commerce
description: Saiba como usar os comandos da interface de linha de comando para gerenciar feeds e processos do  [!DNL data export extension] para serviços SaaS do Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Sincronizar feeds usando a CLI do Commerce

O comando `saas:resync` no pacote `magento/saas-export` permite gerenciar a sincronização de dados para serviços SaaS do Adobe Commerce.

A Adobe não recomenda usar o comando `saas:resync` regularmente. Os cenários típicos para usar o comando são:

- Sincronização inicial
- Sincronizar dados com o novo espaço de dados após alterar a [ID do Espaço de Dados SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Solução de problemas

Monitorar operações de sincronização no arquivo `var/log/saas-export.log`.

## Sincronização inicial

>[!NOTE]
>
>A sincronização inicial é executada automaticamente quando o Live Search ou as Recomendações de produto são ativadas. Comandos manuais não são necessários.

Quando você aciona um `saas:resync` na linha de comando, dependendo do tamanho do catálogo, pode levar de alguns minutos a algumas horas para que os dados sejam atualizados.

Para a sincronização inicial, a Adobe recomenda executar os comandos na seguinte ordem:

```shell
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

## Sincronizar usando comandos CLI

O comando `saas:resync` dá suporte a várias operações de sincronização:

- Sincronização parcial por SKU
- Retomar sincronizações interrompidas
- Validar dados sem sincronização

Exibir todas as opções disponíveis:

```shell
bin/magento saas:resync --help
```

Consulte as seções a seguir para obter descrições de opções com exemplos.


>[!NOTE]
>
>Para obter opções avançadas para gerenciar o processamento de exportação, consulte [Personalizar processamento de exportação](customize-export-processing.md).

## `--by-ids`

Ressincronizar parcialmente entidades específicas por suas IDs. Suporta feeds `products`, `productAttributes` e `productOverrides`.

Por padrão, as entidades são especificadas por SKU do produto. Em vez disso, use o `--id-type=ProductID` para usar as IDs de produto.

**Exemplos:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

Limpa a tabela indexadora de feed antes de reindexar e enviar dados para o SaaS. Suportado apenas para feeds `products`, `productOverrides` e `prices`.

>[!IMPORTANT]
>
>Use somente após a limpeza do ambiente. Pode causar problemas de sincronização de dados nos Serviços da Commerce.

**Exemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

Retoma uma operação de ressincronização interrompida. Suportado apenas para feeds `products`, `productAttributes` e `productOverrides`.

**Exemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

Executa o processo de reindexação do feed sem enviar para o SaaS ou salvar na tabela de feed. Use para validar dados.

Adicione a variável de ambiente `EXPORTER_EXTENDED_LOG=1` para salvar a carga em `var/log/saas-export.log`.

**Exemplo:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

Obrigatório. Especifica a entidade de feed a ser ressincronizada.

Feeds disponíveis:

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**Exemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

Reenvia dados existentes do catálogo para [!DNL Commerce Services] sem reindexação. Não compatível com feeds relacionados ao produto.

O comportamento varia de [modo de exportação](data-synchronization.md#synchronization-modes):

- Modo herdado: reenvia todos os dados sem truncar.
- Modo imediato: a opção é ignorada, apenas sincroniza atualizações/falhas.

**Exemplo:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## Solução de problemas

Se você não vir os dados esperados nos Serviços Commerce conectados, solucione os problemas verificando os logs de erro da exportação de dados e usando o comando `saas:resync` com as variáveis de ambiente para revisar as cargas e os dados do criador de perfil. Consulte [Revisar logs e solucionar problemas](troubleshooting-logging.md).
