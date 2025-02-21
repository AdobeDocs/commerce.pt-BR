---
title: Extensão do Adaptador de Catálogo
description: Utilização do Adaptador de catálogo para renderizar preços dos Serviços Commerce
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Adaptador do catálogo

A extensão `[!DNL Catalog Adapter]` desabilita o indexador de preço de produto padrão incluído no aplicativo do Commerce e usa os preços fornecidos pelo [Serviço de Catálogo](../catalog-service/overview.md).

O adaptador foi projetado para funcionar com a [exportação de dados SaaS](../data-export/overview.md) e o Serviço Adobe Commerce. A exportação de dados SaaS é responsável pelo envio dos preços, e o [!DNL Catalog Adapter] recupera todos os preços do Serviço Adobe Commerce.

Ao habilitar o [!DNL Catalog Adapter], a indexação de preços e as operações são afetadas das seguintes maneiras:

- O indexador de preços incluído no aplicativo Adobe Commerce está desativado.
- Os preços são gerenciados com a exportação de dados SaaS e o [indexador de preços SaaS](price-indexing.md).
- Quando um cliente abre um produto, categoria ou outra página que mostra os preços do produto, os preços são recuperados do Serviço da Adobe Commerce.
- Os preços são enviados ao Serviço Adobe Commerce sincronizando dados da [exportação de dados SaaS](../data-export/overview.md).
- O check-out recalcula os preços dinamicamente.

Você pode reativar a indexação de preços no aplicativo do Commerce removendo ou desabilitando a extensão Adaptador de Catálogo.

## Requisitos

- Adobe Commerce 2.4.4+
- Tenha um dos seguintes serviços da Commerce instalado:

   - [Live Search](../live-search/install.md)
   - [Recomendações de produto](../product-recommendations/install-configure.md)
   - [Serviço de catálogo](../catalog-service/installation.md)

## Instalação

A extensão Adaptador do catálogo é um metapackage do Composer que instala os seguintes módulos:

- **Desabilitador do Indexador de Preços** - Este módulo desabilita o índice de preços no aplicativo Commerce para que os preços sejam entregues por meio da indexação de preços SaaS. O indexador de preços do produto no aplicativo Commerce não pode ser ativado quando a extensão de indexação de preços SaaS estiver instalada.
- **Provedor de Preços** - Este módulo fornece preços para produtos do Serviço Adobe Commerce. Ele forma o query de pesquisa e obtém os preços dos produtos no front-end.
- **Adaptador de Pesquisa do Serviço de Catálogo** - Este módulo transfere os preços do aplicativo Adobe Commerce para um Serviço Adobe Commerce em resposta a uma solicitação de pesquisa de produto.

## Etapas de instalação

>[!BEGINTABS]

>[!TAB Infraestrutura em nuvem]

Use este método para instalar o [!DNL Catalog Adapter] para uma instância do Commerce Cloud.

1. Na estação de trabalho local, altere para o diretório do projeto do Adobe Commerce na infraestrutura em nuvem.

   >[!NOTE]
   >
   >Para obter informações sobre o gerenciamento local de ambientes de projeto do Commerce, consulte [Gerenciamento de ramificações com a CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) no _Guia do Usuário do Adobe Commerce na Infraestrutura da Nuvem_.

1. Confira a ramificação de ambiente para atualizar usando a CLI da Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Adicione o módulo Adaptador do Catálogo.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Atualizar dependências de pacote.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. Confirmar e enviar alterações de código para os arquivos `composer.json` e `composer.lock`.

1. Adicione, confirme e envie por push as alterações de código dos arquivos `composer.json` e `composer.lock` para o ambiente de nuvem.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   A ação de enviar as atualizações para o ambiente de nuvem inicia o [processo de implantação da nuvem do Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) para aplicar as alterações. Verifique o status da implantação no [log de implantação](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB No local]

Use este método para instalar o [!DNL Catalog Adapter] para uma instância local.

1. Adicione o Adaptador de catálogo ao seu projeto usando o Composer:

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Atualize as dependências e instale a extensão:

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Atualizar o Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Limpe o cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >Em alguns casos, especialmente ao implantar na produção, você pode evitar a limpeza do código compilado, pois pode levar algum tempo. Certifique-se de fazer backup do sistema antes de fazer qualquer alteração.

>[!ENDTABS]


## Reativar o indexador de preço do produto Adobe Commerce

Se você tiver aplicativos de terceiros que dependem do indexador de preço de produto padrão do Adobe Commerce, será possível reativá-lo com os seguintes comandos:

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Desabilitar indexador de preços de produto para o cenário de frente de loja headless

Se você tiver uma instância do Commerce headless, talvez seja necessário desativar a indexação de preço do produto do Adobe Commerce para reduzir a carga na instância do Adobe Commerce. Você pode concluir esta tarefa instalando o módulo `magento/module-price-indexer-disabler`:

```bash
composer require magento/module-price-indexer-disabler
```

## Cenários de uso

Veja a seguir alguns cenários `[!DNL Catalog Adapter]` comuns.

### Nenhuma dependência no indexador de preço de produto do Adobe Commerce

- Você é um comerciante do Luma ou do Adobe Commerce Core GraphQL que tem um serviço necessário instalado (Live Search, Recomendações de produto, Serviço de catálogo)
- Nenhuma integração com extensões de terceiros que dependem do indexador de preço do produto da Adobe Commerce

1. Instale o [!DNL Catalog Adapter].

### Com dependências no indexador de preço de produto do Adobe Commerce

- Você é um comerciante do Luma ou do Adobe Commerce Core GraphQL que tem um serviço compatível instalado (Live Search, Recomendações de produto, Serviço de catálogo)
- Use uma extensão de terceiros que depende do indexador de preço do produto do Adobe Commerce

1. Instale o [!DNL Catalog Adapter].
1. Reative a indexação padrão de preço do produto Adobe Commerce.

### Instâncias headless do Commerce

- Um comerciante com uma instância do Commerce headless com os serviços necessários instalados (Live Search, Recomendações de produto, Serviço de catálogo)
- Nenhuma dependência do indexador de preço de produto padrão do Adobe Commerce

1. Instale o módulo `magento/module-price-indexer-disabler` do pacote [!DNL Catalog Adapter].

