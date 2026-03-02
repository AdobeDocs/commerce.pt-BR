---
title: Visuais de produto com o AEM Assets
description: Saiba como usar o AEM Assets para imagens de produtos no [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: bf1d88ef7daec25872678bb27bce0bb7c97fd296
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---


# Visuais de produto com o AEM Assets

As Visualizações de produto permitem que os comerciantes do [!DNL Adobe Commerce Optimizer] gerenciem imagens de produtos por meio do Adobe Experience Manager (AEM) Assets. Essa integração fornece um fluxo de trabalho contínuo para sincronizar imagens de produto de alta qualidade do AEM Assets com o catálogo do [!DNL Commerce Optimizer] usando camadas de catálogo.

## Principais benefícios

* **Gerenciamento centralizado de ativos**: gerencie todas as imagens de produtos na AEM Assets, a solução de gerenciamento de ativos digitais de nível empresarial.
* **Sincronização automática**: as imagens do produto são sincronizadas automaticamente quando os ativos são aprovados ou atualizados no AEM Assets.
* **Entrega do Dynamic Media**: aproveite o Dynamic Media com recursos OpenAPI para entrega otimizada de imagens.
* **Camadas do catálogo**: as imagens do produto são aplicadas como uma camada do catálogo, permitindo que você sobreponha imagens do AEM Assets no catálogo base.

## Como funciona

A integração tem dois fluxos principais:

* **Do AEM Assets**: quando um ativo é aprovado, rejeitado ou removido, o evento flui pelo Pipeline do Adobe para o Serviço de Integração do Assets. O serviço corresponde ativos a produtos usando um `match-by-SKU` ou uma estratégia de correspondência personalizada e, em seguida, envia os mapeamentos de `product-asset` para o [!DNL Commerce Optimizer], onde eles são armazenados como camadas de produto.

* **Do ACO**: quando um produto é atualizado no [!DNL Commerce Optimizer], o evento flui pelo Pipeline do Adobe para o Serviço de Integração da Assets. O serviço sincroniza todos os mapeamentos de ativos correspondentes ao ACO.

As imagens atualizadas estão disponíveis por meio das APIs da loja (Serviço de catálogo, Live Search, Recomendações de produto).

### Source e configuração de camadas

As imagens do AEM Assets são assimiladas como uma camada de catálogo com a seguinte configuração de origem:

> Exemplo de uma configuração de origem

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

Essa configuração garante que as imagens do AEM Assets sejam aplicadas como uma sobreposição em seu catálogo de produtos base.

## Pré-requisitos

Antes de habilitar Visualizações de Produto, verifique se você atende aos [pré-requisitos para o Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md#prerequisites).

## Configuração

Para habilitar a integração, [crie um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) com o [!DNL Commerce Optimizer] e os detalhes do AEM Assets. O Suporte da Adobe configura a integração e registra seu locatário no Serviço de integração da Assets.

Consulte [Configurar AEM Assets para Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) para obter informações sobre integração.

### Configurar metadados do AEM Assets

Para habilitar a correspondência automática de produtos, configure seus ativos no AEM Assets com metadados do Commerce.

Consulte [Configurar AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets) para obter os campos de metadados e etapas necessários.

## Uso de visuais de produto

Após a configuração da integração, gerencie as imagens do produto por meio do AEM Assets.

### Adicionar imagens aos produtos

1. Faça upload de imagens no repositório do AEM Assets.

1. Adicionar metadados do Commerce ao ativo. Consulte [Aplicar metadados aos ativos](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets).

1. Aprovar o ativo para entrega. O ativo deve estar com o status **aprovado** para acionar a sincronização.

1. A imagem sincroniza automaticamente com [!DNL Commerce Optimizer].

### Aplicar a camada AEM-Assets

Para exibir imagens do AEM Assets em sua vitrine eletrônica, [atribua a camada `AEM-Assets` à exibição do catálogo](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Veja mais aqui

* [Camadas do catálogo](catalog-layer.md)
* [Exibições de catálogo](catalog-view.md)
* [Guia de integração do AEM Assets](../../aem-assets-integration/overview.md)
