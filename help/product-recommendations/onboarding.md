---
title: Integração
description: Saiba mais sobre os requisitos e as plataformas compatíveis do  [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
TQID: https://experienceleague.adobe.com/FLrOFe-Lwe7i3dOwCISflVGEv2MIkXmmE-NqTvpaY-0
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: c09c161ca293b14918bd1ea3248978c12190584c
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 0%

---

# Integração

>[!IMPORTANT]
>
>**O Product Recommendations não é um serviço pronto para HIPAA.** Não ative ou use as Recomendações de produto em nenhuma implementação do Adobe Commerce que use a oferta pronta para HIPAA ou que processe de outra forma as PHIs (Protected Health Information, informações protegidas de saúde). O Product Recommendations faz parte dos serviços SaaS da Commerce, atualmente classificados como prontos para não-HIPAA.
>
>Para obter detalhes sobre quais recursos do Adobe Commerce estão prontos para HIPAA e quais serviços não devem ser usados com PHI, consulte [Preparação para HIPAA no Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) e [Operações](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

O processo de integração do [!DNL Product Recommendations] requer acesso à linha de comando do servidor e consiste nas seguintes etapas. Se você não estiver familiarizado com o trabalho a partir da linha de comando, peça ajuda a um desenvolvedor ou integrador de sistemas.

- [Fluxo de trabalho de implementação](implementation-workflow.md)
- [Instalar e configurar](install-configure.md)
- [Configurações](settings.md)
- [Verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify)
- [Ambiente de preparo](staging-environment.md)

## Requisitos

[Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+. Para obter detalhes, consulte [Requisitos do sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements){target="_blank"}.

### Plataformas compatíveis

- Adobe Commerce no local (EE): 2.4.4+
- Adobe Commerce na nuvem (ECE): 2.4.4+

Para obter requisitos detalhados, consulte [Requisitos do sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements).

## Endpoint

[!DNL Product Recommendations] se comunica através do ponto de extremidade em `https://catalog-service.adobe.io/graphql`.

### Suporte ao Page Builder

[!DNL Product Recommendations] pode ser adicionado a uma página como um tipo de conteúdo do Page Builder. Para adicionar suporte do Page Builder às Recomendações de Produto, consulte [Instalar e Configurar](install-configure.md).

Consulte [[!DNL Page Builder] Integração](page-builder.md) para obter instruções sobre como adicionar [!DNL Product Recommendations] ao conteúdo [!DNL Page Builder].

### Indexação de preços SaaS

Os clientes da Recomendação de produto podem usar a [indexação de preço do SaaS](../price-index/price-indexing.md), que oferece atualizações de alterações de preço e tempo de sincronização mais rápidos.

### Suporte B2B {#b2bsupport}

As vitrines B2B geralmente exigem uma lógica complexa que determina a visibilidade e os preços do produto para cada comprador ou grupo de clientes. [!DNL Product Recommendations] agora [oferece suporte](release-notes.md) a essa funcionalidade ao honrar [permissões de categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions), [catálogos compartilhados](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared) e [preços específicos de grupo de clientes](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/pricing-advanced). Por exemplo, se você tiver ocultado determinadas categorias do segmento de cliente de varejo, um comprador nesse segmento não receberá recomendações para os produtos nessas categorias. Além disso, ao definir um catálogo compartilhado para grupos de clientes e empresas específicos, esses compradores veem recomendações somente para produtos que podem acessar. Todos os produtos recomendados refletem o preço correto específico do grupo de clientes com base no grupo de clientes de cada comprador.

>[!NOTE]
>
>Os comerciantes podem personalizar e estender widgets ou elementos de vitrine usando a API de vitrine do [Serviço de catálogo](../catalog-service/overview.md), mas qualquer personalização está fora do escopo da equipe de suporte da Adobe.
