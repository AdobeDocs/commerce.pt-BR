---
title: Adobe Commerce Optimizer Connector
description: Saiba como conectar seus dados da nuvem do Commerce ou do projeto local à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Adobe Commerce Optimizer Connector

O Adobe Commerce Optimizer Connector é a ponte de integração que sincroniza os dados de catálogo e preço entre uma Adobe Commerce na infraestrutura de nuvem ou implantação local e [!DNL Adobe Commerce Optimizer]. A sincronização de dados com o Adobe Commerce Optimizer habilita recursos como Pesquisas com IA dinâmicas, recomendações, otimização de site e frentes de loja headless de carregamento rápido, incluindo frentes de loja da Adobe Commerce no Edge Delivery Services e análise de desempenho em tempo real.

## Arquitetura e experiência

O Adobe Commerce Optimizer Connector opera mapeando sites da Commerce e visualizações de armazenamento para um projeto do Commerce Optimizer, como mostrado na figura a seguir:

![Mapeando dados do Commerce para o Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="700" zoomable="yes"}

Quando os dados são exportados do Commerce para o Commerce Optimizer:

* As exibições da loja da Commerce são mapeadas para fontes do catálogo
* Os sites são mapeados para catálogos de preços

Os dados de catálogo e preço associados são exportados e usados posteriormente para criar exibições de catálogo e, opcionalmente, definir políticas para filtrar os dados de catálogo e preço para casos de uso de negócios específicos.

Quando o conector está habilitado, você também pode configurar e gerenciar regras de merchandising para descoberta de produtos e regras para recomendações usando [[!DNL Adobe Commerce Optimizer] Ferramentas de merchandising](../optimizer/overview.md#quick-tour). A instância do Adobe Commerce torna-se a fonte de dados para dados de catálogo e preço. Quando os dados são atualizados no Commerce, as atualizações são sincronizadas com a instância [!DNL Adobe Commerce Optimizer].

## Fluxos de trabalhos

O Conector permite vários workflows principais:

* **Exportar dados do catálogo do Commerce para[!DNL Adobe Commerce Optimizer]**—os dados do catálogo de preços e preços são exportados no nível do site e do grupo de clientes. Os dados de atributos do produto e do produto são exportados no nível `store view`. Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites e exibições de loja).

  Para habilitar esse fluxo de trabalho, instale a extensão PHP `adobe-commerce/commerce-data-export-aco-adapter`, revise a configuração do exportador e habilite a integração entre o Commerce e o Commerce Optimizer com o Administrador do Commerce. Para obter instruções detalhadas, consulte [Introdução](get-started.md).

* **Mapear o site da Commerce e armazenar dados para exportação para[!DNL Adobe Commerce Optimizer]**

  Opcionalmente, personalize as configurações de exportação para sincronizar dados somente de sites ou exibições de loja específicas. Por exemplo, você pode optar por exportar dados de catálogo para apenas uma exibição de loja a ser usada para um caso de uso específico, como otimizar a experiência de pesquisa e descoberta para um mercado ou região específica.

* **Configuração e gerenciamento da regra de merchandising**

  Quando o Conector está habilitado, as regras de merchandising para descoberta de produtos e recomendações são definidas e gerenciadas na interface do usuário do [!DNL Adobe Commerce Optimizer], não nas páginas [!UICONTROL Live Search] e [!UICONTROL Product Recommendations] do Administrador do Commerce.

* **Implantar a Commerce Storefront no Edge Delivery Services**

  Depois de configurar a integração com o [!DNL Adobe Commerce Optimizer], você pode implantar uma Commerce Storefront no Edge Delivery Services. Isso proporciona desempenho ultrarrápido, escalabilidade, criação contínua de conteúdo e personalização integrada usando uma arquitetura combinável orientada por API.

Para obter detalhes sobre como configurar a integração e habilitar esses fluxos de trabalho, consulte [Introdução](get-started.md).
