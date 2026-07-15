---
title: Visuais de produto com o AEM Assets
description: Saiba como usar o AEM Assets para imagens de produtos no [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# Visuais de produto com o AEM Assets

As Visualizações de produto permitem que os comerciantes do [!DNL Adobe Commerce Optimizer] gerenciem imagens de produtos por meio do Adobe Experience Manager (AEM) Assets. Essa integração fornece um fluxo de trabalho contínuo para sincronizar imagens de produto de alta qualidade do AEM Assets com o catálogo do [!DNL Commerce Optimizer] usando camadas de catálogo.

>[!NOTE]
>
>**Visuais de Produto** é o nome do conjunto fornecido com [!DNL Adobe Commerce as a Cloud Service] e [!DNL Adobe Commerce Optimizer]. Ele combina o [Dynamic Media com recursos OpenAPI](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview) e o [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime).
>
>Clientes com uma licença diferente do AEM Assets (por exemplo, **AEM Assets Ultimate**) podem usar a mesma integração; somente a versão do AEM afeta as etapas de integração, não o tipo de licença.

## Principais benefícios

* **Gerenciamento centralizado de ativos**: gerencie todas as imagens de produtos na AEM Assets, a solução de gerenciamento de ativos digitais de nível empresarial.
* **Sincronização automática**: as imagens do produto são sincronizadas automaticamente quando os ativos são aprovados ou atualizados no AEM Assets.
* **Entrega do Dynamic Media**: aproveite o Dynamic Media com recursos OpenAPI para entrega otimizada de imagens.
* **Camadas do catálogo**: as imagens do produto são aplicadas como uma camada do catálogo, permitindo que você sobreponha imagens do AEM Assets no catálogo base.

## Como funciona

A integração tem dois fluxos de evento independentes. Ambos usam o [Adobe I/O Events](https://developer.adobe.com/events/docs/) para transferir eventos para o serviço de integração do Assets, mas cada direção usa seu próprio provedor de eventos:

* **Do AEM Assets para o serviço de integração do Assets**: quando um ativo é aprovado, rejeitado ou removido, o evento é entregue ao serviço de integração do Assets. O serviço corresponde ativos a produtos usando uma `match-by-SKU` ou uma estratégia de correspondência personalizada e, em seguida, envia os mapeamentos de `product-asset` para [!DNL Commerce Optimizer], onde eles são armazenados como camadas de produto.

* **De [!DNL Commerce Optimizer] para o Serviço de Integração da Assets**: quando um produto é atualizado em [!DNL Commerce Optimizer], o evento é entregue ao Serviço de Integração da Assets. O serviço sincroniza todos os mapeamentos de ativos correspondentes de volta para [!DNL Commerce Optimizer].

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

Para habilitar a integração, [crie um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket) com o [!DNL Commerce Optimizer] e os detalhes do AEM Assets. O Suporte da Adobe configura a integração e registra seu locatário no Serviço de integração da Assets.

Consulte [Configurar AEM Assets para Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md) para obter informações sobre integração.

### Configurar metadados do AEM Assets

Para habilitar a correspondência automática de produtos, configure seus ativos no AEM Assets com metadados do Commerce.

Consulte [Configurar AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first) para obter os campos de metadados e etapas necessários.

## Limitação

Antes de usar Visuais de produto, revise as [limitações de integração](../../aem-assets-integration/get-started/configure-aco.md#limitations) — as restrições relacionadas à camada que afetam como os dados do AEM Assets se mesclam com o catálogo base.

Para alocações de capacidade e uso (armazenamento de ativos, operações do Dynamic Media, licenças de usuário), consulte [Limites de elementos visuais de produto](../boundaries-limits.md#product-visuals-limits) no _guia de Limites_.

## Uso de visuais de produto

Após a configuração da integração, gerencie as imagens do produto por meio do AEM Assets.

### Adicionar imagens aos produtos

1. Faça upload de imagens no repositório do AEM Assets.

1. Adicionar metadados do Commerce ao ativo.

   Consulte [Correspondência automática padrão](../../aem-assets-integration/synchronize/default-match.md) e [Correspondência automática personalizada](../../aem-assets-integration/synchronize/custom-match.md).

1. Aprovar o ativo para entrega. O ativo deve estar com o status **aprovado** para acionar a sincronização.

1. A imagem sincroniza automaticamente com [!DNL Commerce Optimizer].

### Aplicar a camada AEM-Assets

Para exibir imagens do AEM Assets em sua vitrine eletrônica, [atribua a camada `AEM-Assets` à exibição do catálogo](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view).

## Veja mais aqui

* [Camadas do catálogo](catalog-layer.md)
* [Exibições de catálogo](catalog-view.md)
* [Guia de integração do AEM Assets](../../aem-assets-integration/overview.md)
