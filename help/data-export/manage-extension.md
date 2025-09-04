---
title: '[!DNL Manage the Data Export extension]'
description: Saiba como atualizar a extensão  [!DNL Data Export]  e remover ou desabilitar serviços de exportação de dados que não são necessários.
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
source-git-commit: c7a08cabe07ec94e31e9f4c27448ee0862e62cf2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Gerenciar a extensão de exportação de dados SaaS

A extensão [!DNL data export] para serviços SaaS é uma coleção de módulos que permitem a coleta e a sincronização de dados entre o Adobe Commerce e os Commerce Services conectados.

Módulos específicos são incluídos nos metapackages para extensões dos Serviços da Adobe Commerce, como
como [Live Search](/help/live-search/overview.md), [Recomendações de Produto](/help/product-recommendations/overview.md) e [Serviço de Catálogo](/help/catalog-service/overview.md). Se você estiver usando esses serviços, nenhuma instalação separada será necessária para habilitar a extensão Exportação de dados.

## Remova ou desative os recursos de exportação de dados do Commerce

Se você não precisar de um dos módulos de exportação de dados de comércio instalados, use o comando da CLI `magento:module:disable` para desabilitá-lo.

Por exemplo, há uma [API de Categorias](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) que usa os dados de feed de permissões de categorias internamente. Se você não estiver usando essa API, poderá desativar a exportação de dados para o feed de permissões de categorias.

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Atualizar um módulo para uma versão específica

Você pode atualizar qualquer um dos módulos de exportação de dados de comércio instalados usando o Composer. Por exemplo, você pode atualizar um módulo para uma versão especificada e também atualizar quaisquer dependências necessárias.

1. Faça logon no servidor de aplicativos do Commerce.

1. Na linha de comando, atualize o módulo usando o Composer:

   ```bash
   composer require magento/commerce-data-export:103.4.11 --with-all-dependencies
   ```

Se a instância do Commerce for implantada na infraestrutura em nuvem, atualize a extensão do diretório do projeto em nuvem. Consulte [Atualizar uma extensão](https://experienceleague.adobe.com/pt-br/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) no _Guia de Infraestrutura do Adobe Commerce on Cloud_.
