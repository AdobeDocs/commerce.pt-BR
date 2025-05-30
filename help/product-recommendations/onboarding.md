---
title: Integração
description: Learn the requirements and supported platforms in [!DNL Product Recommendations].
exl-id: 7b8a1117-b6d5-4e5d-bb97-09f76a024cbd
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Integração

O processo de integração do [!DNL Product Recommendations] requer acesso à linha de comando do servidor e consiste nas seguintes etapas. Se você não estiver familiarizado com o trabalho a partir da linha de comando, peça ajuda a um desenvolvedor ou integrador de sistemas.

- [Fluxo de trabalho de implementação](implementation-workflow.md)
- [Instalar e configurar](install-configure.md)
- [Configurações](settings.md)
- [Verify](verify.md)
- [Staging Environment](staging-environment.md)

## Requisitos

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2
- Compositor 2

### Plataformas compatíveis

- Adobe Commerce no local (EE): 2.4.4+
- Adobe Commerce na nuvem (ECE): 2.4.4+

## Endpoint

[!DNL Product Recommendations] se comunica através do ponto de extremidade em `https://catalog-service.adobe.io/graphql`.

### Page Builder support

[!DNL Product Recommendations] can be added to a page as a Page Builder content type. To add Page Builder support to Product Recommendations, refer to [Install and Configure](install-configure.md).

Consulte [[!DNL Page Builder] Integração](page-builder.md) para obter instruções sobre como adicionar [!DNL Product Recommendations] ao conteúdo [!DNL Page Builder].

### Indexação de preços SaaS

Os clientes da Recomendação de produto podem usar a [indexação de preço do SaaS](../price-index/price-indexing.md), que oferece atualizações de alterações de preço e tempo de sincronização mais rápidos.

### Suporte B2B {#b2bsupport}

As vitrines B2B geralmente exigem uma lógica complexa que determina a visibilidade e os preços do produto para cada comprador ou grupo de clientes. [!DNL Product Recommendations] agora [oferece suporte](release-notes.md) a essa funcionalidade ao honrar [permissões de categoria](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=pt-BR), [catálogos compartilhados](https://experienceleague.adobe.com/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html?lang=pt-BR) e [preços específicos de grupo de clientes](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=pt-BR). Por exemplo, se você tiver ocultado determinadas categorias do segmento de cliente de varejo, um comprador nesse segmento não receberia recomendações para produtos nessas categorias. Além disso, ao definir um catálogo compartilhado para grupos de clientes e empresas específicos, esses compradores veem recomendações somente para produtos que podem acessar. Todos os produtos recomendados refletem o preço correto específico do grupo de clientes com base no grupo de clientes de cada comprador.

>[!NOTE]
>
>Merchants may customize and extend widgets or storefront elements by using the [Catalog Service](../catalog-service/overview.md) Storefront API but any customization is out of scope for Adobe&#39;s support team.
