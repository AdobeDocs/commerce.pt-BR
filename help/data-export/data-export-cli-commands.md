---
title: Sincronizar feeds usando a CLI do Commerce
description: Saiba como usar os comandos da interface de linha de comando para gerenciar feeds e processos do  [!DNL data export extension] para serviços SaaS do Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 6f578dfaf3d3e77d7b541714de613025b8c789a4
workflow-type: tm+mt
source-wordcount: '526'
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

Ressincronizar parcialmente entidades específicas por suas IDs. Suporta os feeds `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions`.

Por padrão, as entidades são especificadas em uma lista separada por vírgulas por SKU do produto. Para usar IDs de produto, adicione a opção `--id-type=ProductID`.

**Exemplos:**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed= products --by-ids='1,2,3' --id-type='productId'
```


## `--cleanup-feed`

Limpe a tabela de feed da tabela indexadora de feed antes de reindexar e enviar dados para o SaaS. Com suporte somente para `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` e `categoryPermissions`.

Se usada com a opção `--dry-run`, a operação executará uma operação de ressincronização de simulação para todos os itens.

>[!IMPORTANT]
>
>Use somente após a limpeza do ambiente ou com a opção `--dry-run`. Se usada em outros casos, a operação de limpeza causa perda de dados e problemas de sincronização de dados, em que os itens que precisam ser excluídos no Adobe Commerce não serão excluídos do espaço de dados SaaS.

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
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='1,2,3'
```

### Testar todos os itens do feed

Por padrão, o feed enviado durante uma operação `resync --dry-run` inclui somente itens novos ou itens que não foram exportados anteriormente. Para incluir todos os itens no feed a serem processados, use a opção `--cleanup-feed`.

**Exemplo**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
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
bin/magento saas:resync --feed products
```

## `--no-reindex`

Reenvia dados existentes do catálogo para [!DNL Commerce Services] sem reindexação. Não compatível com feeds relacionados ao produto.

O comportamento varia de [modo de exportação](data-synchronization.md#synchronization-modes):

- Modo herdado: reenvia todos os dados sem truncar.
- Modo imediato: a opção é ignorada, apenas sincroniza atualizações/falhas.

**Exemplo:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

## `--id-type=ProductId`

Por padrão, as entidades especificadas quando você usa o comando `saas:resync feed` com a opção `--by-ids` são especificadas pelo SKU do produto. Use a opção `--id-type=ProductId` para especificar entidades por ID de produto.

```shell
bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

**Exemplo:**

## Solução de problemas

Se você não vir os dados esperados nos Serviços Commerce conectados, solucione os problemas verificando os logs de erro da exportação de dados e usando o comando `saas:resync` com as variáveis de ambiente para revisar as cargas e os dados do criador de perfil. Consulte [Revisar logs e solucionar problemas](troubleshooting-logging.md).
