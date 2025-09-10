---
title: Integração
description: Saiba mais sobre os requisitos e as plataformas compatíveis do  [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Integração

O processo de integração do [!DNL Product Recommendations] requer acesso à linha de comando do servidor e consiste nas seguintes etapas. Se você não estiver familiarizado com o trabalho a partir da linha de comando, peça ajuda a um desenvolvedor ou integrador de sistemas.

- [Fluxo de trabalho de implementação](implementation-workflow.md)
- [Instalar e configurar](install-configure.md)
- [Configurações](settings.md)
- [Verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/)
- [Ambiente de preparo](staging-environment.md)

## Requisitos

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Compositor 2

### Plataformas compatíveis

- Adobe Commerce no local (EE): 2.4.4+
- Adobe Commerce na nuvem (ECE): 2.4.4+

## Endpoint

[!DNL Product Recommendations] se comunica através do ponto de extremidade em `https://catalog-service.adobe.io/graphql`.

### Suporte ao Page Builder

[!DNL Product Recommendations] pode ser adicionado a uma página como um tipo de conteúdo do Page Builder. Para adicionar suporte do Page Builder às Recomendações de Produto, consulte [Instalar e Configurar](install-configure.md).

Consulte [[!DNL Page Builder] Integração](page-builder.md) para obter instruções sobre como adicionar [!DNL Product Recommendations] ao conteúdo [!DNL Page Builder].

### Indexação de preços SaaS

Os clientes da Recomendação de produto podem usar a [indexação de preço do SaaS](../price-index/price-indexing.md), que oferece atualizações de alterações de preço e tempo de sincronização mais rápidos.

### Suporte B2B {#b2bsupport}

As vitrines B2B geralmente exigem uma lógica complexa que determina a visibilidade e os preços do produto para cada comprador ou grupo de clientes. [!DNL Product Recommendations] agora [oferece suporte](release-notes.md) a essa funcionalidade ao honrar [permissões de categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=pt-BR), [catálogos compartilhados](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html?lang=pt-BR) e [preços específicos de grupo de clientes](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=pt-BR). Por exemplo, se você tiver ocultado determinadas categorias do segmento de cliente de varejo, um comprador nesse segmento não receberia recomendações para produtos nessas categorias. Além disso, ao definir um catálogo compartilhado para grupos de clientes e empresas específicos, esses compradores veem recomendações somente para produtos que podem acessar. Todos os produtos recomendados refletem o preço correto específico do grupo de clientes com base no grupo de clientes de cada comprador.

>[!NOTE]
>
>Os comerciantes podem personalizar e estender widgets ou elementos de vitrine usando a API de vitrine do [Serviço de catálogo](../catalog-service/overview.md), mas qualquer personalização está fora do escopo da equipe de suporte da Adobe.
