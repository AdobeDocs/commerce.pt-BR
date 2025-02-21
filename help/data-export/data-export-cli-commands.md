---
title: Interface de linha de comando da exportação de dados SaaS
description: Saiba como usar os comandos da interface de linha de comando para gerenciar feeds e processos do  [!DNL data export extension] para serviços SaaS do Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Referência da interface de linha de comando da exportação de dados SaaS

Desenvolvedores e administradores de sistema podem gerenciar operações de sincronização para exportação de dados SaaS usando a [ferramenta de linha de comando Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). O comando `saas:resync` está incluído no pacote `magento/saas-export`.

A Adobe não recomenda usar o comando `saas:resync` regularmente. Os cenários típicos para usar o comando são:

- A sincronização inicial
- A [ID do Espaço de Dados SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) foi alterada e você precisa sincronizar os dados para o novo espaço de dados.
- Solução de problemas

## Sincronização inicial

>[!NOTE]
>Se você estiver usando o Live Search ou o Product Recommendations, não será necessário executar a sincronização inicial. O processo é iniciado automaticamente depois que você conecta o serviço à sua instância do Commerce.

Quando você aciona um `saas:resync` na linha de comando, dependendo do tamanho do catálogo, pode levar de alguns minutos a algumas horas para que os dados sejam atualizados.

Para a sincronização inicial, a Adobe recomenda executar os comandos na seguinte ordem:

```bash
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

## Exemplos de comandos

Antes de usar os comandos `saas:resync`, examine as [descrições de opção](#command-options).

- Executar uma ressincronização completa de um feed de entidade.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  Os feeds que já foram exportados com sucesso não são sincronizados novamente.

- Ressincronizar totalmente o feed especificado e os dados de limpeza

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  Use somente após executar uma operação [!DNL Data Space ID Cleanup].

- Para feeds de exportação imediatos, reenvie todos os dados para os serviços conectados da Commerce sem truncar os dados de índice na tabela de feed

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- Lista os comandos e opções disponíveis com descrições.

  ```
  bin/magento saas:resync --help
  ```

## Opções de comando

As opções a seguir estão disponíveis para gerenciar operações de `saas:resync`.

>[!NOTE]
>
>O comando `saas:resync` também oferece suporte a opções avançadas para melhorar comandos de exportação de dados, aumentando o tamanho do lote e adicionando processamento de vários threads. Consulte [Personalizar processamento de exportação](customize-export-processing.md).

### `feed`

Esta opção necessária especifica qual entidade de feed deve ser ressincronizada, como `products`.

O valor da opção `feed` pode incluir qualquer um dos feeds de entidade disponíveis:

- `products`: feed de dados do produto
- `productAttributes`: feed de dados de atributos do produto
- `categories`: feed de dados de categorias
- `variants`: feed de dados de variações de produto configuráveis
- `prices`: feed de dados de preços de produtos
- `categoryPermissions`: feed de dados de permissões de categoria
- `productOverrides`: feed de dados de permissões do produto
- `inventoryStockStatus`: feed de dados de status do estoque
- `scopesWebsite`: sites com lojas e exibições de armazenamento feed de dados
- `scopesCustomerGroup`: feed de dados de grupos de clientes
- `orders`: feed de dados de ordens de venda

Dependendo dos [Serviços Commerce](../landing/saas.md) instalados, talvez você tenha um conjunto diferente de feeds disponíveis para o comando `saas:resync`.

### `no-reindex`

Esta opção reenvia os dados existentes do catálogo para [!DNL Commerce Services] sem reindexação. Se essa opção não for especificada, o comando executará uma reindexação completa antes de sincronizar os dados.

O comportamento desta opção depende se o feed é exportado em [modo de exportação herdado ou imediato](data-synchronization.md#synchronization-modes)

- Para feeds de exportação herdados, o processo de sincronização não trunca os dados indexados na tabela de feeds. Em vez disso, ele reenvia todos os dados para o serviço Adobe Commerce.
- Para feeds de exportação imediatos, essa opção é ignorada se especificada. Para esses feeds, o processo de ressincronização não trunca o índice e só ressincroniza atualizações ou itens que falharam anteriormente.

### `cleanup`

Essa opção limpa a tabela indexadora de feed antes de uma sincronização. Quando especificado, a exportação de dados SaaS executa uma ressincronização completa para o feed especificado e limpa todos os dados existentes na tabela de feed.

A Adobe recomenda usar este comando somente após executar a operação [!DNL Data Space ID Cleanup].

>[!WARNING]
>
>**Não use esta opção regularmente**. Isso pode causar problemas de sincronização de dados nos Serviços da Adobe Commerce. Por exemplo, o `delete product event` pode não se propagar para o serviço Adobe Commerce se a opção `cleanup` for usada.

## Solução de problemas

Se você não vir os dados esperados nos Serviços Commerce conectados, solucione os problemas verificando os logs de erro da exportação de dados e usando o comando `saas:resync` com as variáveis de ambiente para revisar as cargas e os dados do criador de perfil. Consulte [Revisar logs e solucionar problemas](troubleshooting-logging.md).
