---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# Remover extensões conflitantes

Se você tiver uma das seguintes extensões instaladas, desinstale-as antes de instalar o [!DNL Adobe Commerce Optimizer Connector for B2B]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

Os dados associados a essas extensões ainda estão disponíveis no banco de dados do Commerce. No entanto, ele não é exportado para [!DNL Commerce Optimizer] quando o conector está habilitado. Para implementar os recursos de pesquisa e merchandising do Adobe Commerce fornecidos por essas extensões após habilitar o conector, configure-os na [[!DNL Commerce Optimizer] Interface do usuário do administrador](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Falha ao remover essas extensões antes de habilitar o conector causa telas de configuração com falha, dados duplicados no [!DNL Commerce Optimizer] e erros de autenticação 401 ou 403.