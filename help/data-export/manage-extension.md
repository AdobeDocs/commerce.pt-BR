---
title: '[!DNL Manage the Data Export extension]'
description: Saiba como atualizar a extensão  [!DNL Data Export]  e remover ou desabilitar serviços de exportação de dados que não são necessários.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: c09c161ca293b14918bd1ea3248978c12190584c
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# Gerenciar a extensão de exportação de dados SaaS

A [[!DNL data export] extensão](https://github.com/magento/commerce-data-export) para serviços SaaS é uma coleção de módulos que permitem a coleta e a sincronização de dados entre o Adobe Commerce e os Commerce Services conectados.

Módulos específicos são incluídos nos metapackages para extensões dos Serviços da Adobe Commerce, como
como [Live Search](/help/live-search/overview.md), [Recomendações de Produto](/help/product-recommendations/overview.md), [Serviço de Catálogo](/help/catalog-service/overview.md) e [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md). Se você estiver usando esses serviços, nenhuma instalação separada será necessária para habilitar a extensão Exportação de dados.

## Remova ou desative os recursos de exportação de dados do Commerce

Se você não precisar de um dos módulos de exportação de dados de comércio instalados, use o comando da CLI `magento:module:disable` para desabilitá-lo.

Por exemplo, há uma [API de Categorias](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) que usa os dados de feed de permissões de categorias internamente. Se você não estiver usando essa API, poderá desativar a exportação de dados para o feed de permissões de categorias.

```shell
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Atualizar um módulo para uma versão específica

Você pode atualizar qualquer um dos módulos de exportação de dados de comércio instalados usando o Composer. Revise as [notas de versão](release-notes.md) para determinar se uma correção necessária está disponível e atualize para essa versão específica e para quaisquer dependências necessárias.

>[!NOTE]
>
>Se você atualizar para a versão mais recente do [Live Search](/help/live-search/overview.md), do [Serviço de Catálogo](/help/catalog-service/overview.md), do [Product Recommendations](/help/product-recommendations/overview.md) ou do [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md), também receberá a versão mais recente da extensão de exportação de dados. O metappackage de exportação de dados é uma dependência dos pacotes do Composer para esses serviços.

1. Faça logon no servidor de aplicativos do Commerce.

1. Na linha de comando, atualize o módulo usando o Composer:

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Se a instância do Commerce for implantada na infraestrutura em nuvem, atualize a extensão do diretório do projeto em nuvem. Consulte [Atualizar uma extensão](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure-store/extensions#upgrade-an-extension) no _Guia de Infraestrutura do Adobe Commerce on Cloud_.

>[!MORELIKETHIS]
>
> - [Notas de versão](release-notes.md)
> - [Módulos de exportação de dados SaaS](reference/data-export-modules.md)
> - [Visão geral do guia](overview.md)
