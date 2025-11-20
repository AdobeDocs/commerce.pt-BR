---
title: Instalar e configurar
description: Saiba como instalar, atualizar e desinstalar o  [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Instalar e configurar

A implantação do [!DNL Product Recommendations] na vitrine e no Administrador requer a instalação do módulo e a configuração do [Commerce Services Connector](../landing/saas.md). À medida que as atualizações forem lançadas, você poderá atualizar facilmente a instalação com a versão mais recente.

- [Instalar](#install)
- [Configurar &#x200B;](#configure)
- [Atualizar](#update)
- [Desinstalar](#uninstall)

## Instalar [!DNL Product Recommendations] {#install}

Como o módulo [!DNL Product Recommendations] é um metapackage independente, as atualizações são lançadas com mais frequência do que o Adobe Commerce. Para verificar se você está atualizado com os recursos e correções de erros mais recentes, consulte as [notas de versão](release-notes.md).

>[!IMPORTANT]
>
>Verifique se você tem os [direitos](../landing/saas.md#credentials) corretos para usar as Recomendações de Produto.

Instalar o módulo `magento/product-recommendations` com o Composer:

```bash
composer require magento/product-recommendations
```

### Adicionar suporte ao Page Builder {#pbsupport}

O [!DNL Product Recommendations] for Page Builder é um módulo opcional e é instalado separadamente. Para usar o [!DNL Product Recommendations] com o Page Builder, instale o módulo executando o seguinte comando:

```bash
composer require magento/module-page-builder-product-recommendations
```

Ao habilitar [!DNL Product Recommendations] no Page Builder, você pode adicionar uma [unidade de recomendação](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) existente e ativa a qualquer conteúdo criado no Page Builder, como páginas, blocos e blocos dinâmicos.

Consulte [Usar [!DNL Product Recommendations] com conteúdo do Page Builder](page-builder.md) para obter mais instruções.

### Adicionar tipo de recomendação de similaridade visual {#vissimsupport}

O tipo de recomendação _Semelhança visual_ permite implantar uma unidade de recomendação na página de detalhes do produto que exibe produtos que são [visualmente semelhantes](type.md#visualsim) ao produto que está sendo visualizado. Esse tipo de recomendação é mais útil quando imagens e aspectos visuais dos produtos são partes importantes da experiência de compra. Instale o tipo de recomendação _Similaridade visual_ executando o seguinte comando:

```bash
composer require magento/module-visual-product-recommendations
```

## Configurar [!DNL Product Recommendations] {#configure}

1. Após instalar o módulo `magento/product-recommendations`, configure o [Commerce Services Connector](../landing/saas.md) especificando as Chaves de API e selecionando um Espaço de Dados SaaS.

   A configuração dessa conexão permite a sincronização de dados e a comunicação entre a instância do Commerce, o Serviço de catálogo e outros serviços de suporte. A sincronização de dados é realizada pela [extensão de Exportação de Dados SaaS](../data-export/overview.md).

1. Para garantir que a exportação de catálogo possa ser executada corretamente, confirme se os trabalhos [cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e os [indexadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) estão em execução e se o indexador `Product Feed` está definido como `Update by Schedule`.

Depois de vincular com êxito o aplicativo do Commerce aos Serviços da Commerce e especificar o [Espaço de Dados SaaS](../landing/saas.md#saas-configuration), a sincronização do catálogo será iniciada. Em seguida, você pode [verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) se os dados comportamentais estão sendo enviados para a loja.

## Monitorar e solucionar problemas de sincronização de dados

Com o Administrador do Commerce, é possível monitorar o processo de sincronização usando o [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Use a [CLI do Commerce](../data-export/data-export-cli-commands.md#troubleshooting) e os logs para gerenciar e solucionar problemas do processo.

Em seguida, você pode [verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) se os dados comportamentais estão sendo enviados para a loja.

## Atualize sua instalação do [!DNL Product Recommendations] {#update}

Como todo o Adobe Commerce, o [!DNL Product Recommendations] usa o Composer para instalação e atualizações. Para atualizar o módulo `magento/product-recommendations`, execute o seguinte:

```bash
composer update magento/product-recommendations --with-dependencies
```

Para atualizar para uma versão principal, como de 5.0 para 6.0, você deve editar o arquivo raiz `composer.json` do seu projeto. (Consulte as [notas de versão](release-notes.md) para obter informações sobre a versão mais recente.) Por exemplo, vamos abrir o arquivo `composer.json` principal e pesquisar pelo módulo `magento/product-recommendations`:

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Vamos aumentar a versão principal de `5.0` para `6.0`:

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

Salve o arquivo `composer.json` e execute:

```bash
composer update magento/product-recommendations --with-dependencies
```

Ou se você instalou os módulos `magento/module-visual-product-recommendations` e `magento/module-page-builder-product-recommendations`:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> Nas versões 3.x.x do Product Recommendations, você só precisava de uma única chave de API. Nas versões 4.x.x e superior, você deve fornecer chaves de API públicas e privadas para os ambientes de sandbox e produção. Se você não fornecer ambos os pares de chaves de API, não poderá acessar o recurso Recomendações de produto no Admin. No entanto, a coleta de dados continua em sua loja e as recomendações existentes continuam a ser mostradas aos seus compradores.

## Firewalls

Para permitir que as Recomendações de Produto passem por um firewall, adicione `commerce.adobe.io` à lista de permissões.

## Desinstalar [!DNL Product Recommendations] {#uninstall}

Se necessário, você pode [desinstalar](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) o módulo product-recommendations.
