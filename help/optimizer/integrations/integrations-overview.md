---
title: Integrações do Commerce Optimizer
description: Saiba mais sobre as integrações do Adobe Commerce Optimizer para sincronização de catálogo, gerenciamento de ativos, otimização de vitrine e conectividade do Salesforce Commerce Cloud.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a  [!DNL Adobe Commerce Optimizer] projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: d8cd6f543353e1b11f3aa14b3b97b02155d23809
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer] integrações

O [!DNL Adobe Commerce Optimizer] inclui integrações que permitem sincronizar dados do Adobe Commerce na nuvem ou no local, gerenciar ativos, melhorar as experiências da loja e conectar sistemas externos. As seções abaixo descrevem como cada integração funciona com o [!DNL Adobe Commerce Optimizer]. Siga os links para instalação, configuração e uso diário.

## Adobe Commerce Optimizer Connector {#aco-connector}

O Adobe Commerce Optimizer Connector é a ponte que sincroniza os dados de catálogo e preço entre o Adobe Commerce (nuvem ou local) e o [!DNL Adobe Commerce Optimizer]. Ao habilitar o conector, o Commerce permanece o sistema de registro de dados de produtos enquanto o [!DNL Adobe Commerce Optimizer] habilita a descoberta de produtos, as recomendações, as regras de merchandising, a análise e as experiências de frente de loja headless.

- [Visão geral do Adobe Commerce Optimizer Connector](../../aco-connector/overview.md){target="_blank"}
- [Introdução ao conector](../../aco-connector/get-started.md){target="_blank"}

## Visuais de produto com o AEM Assets {#product-visuals}

As Visualizações de produto permitem gerenciar imagens de produtos por meio do Adobe Experience Manager (AEM) Assets. Configure o AEM Assets para Commerce Optimizer para ativar Visualizações de produto. Após concluir a configuração, você usa o AEM Assets como a solução centralizada de gerenciamento de ativos digitais para as imagens de seus produtos, com fluxos de trabalho automatizados de revisão e gerenciamento de ativos que mantêm as imagens sincronizadas com seu catálogo Commerce Optimizer. A integração corresponde ativos a produtos por SKU. As atualizações fluem pelos serviços de integração da Adobe, para que as vitrines reflitam a mídia mais recente sem recarregamentos manuais.

- [Visuais de produto com o AEM Assets](../setup/product-visuals.md)
- [Configurar AEM Assets para Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

O Adobe Experience Manager Sites Optimizer analisa sites da Commerce e melhora o desempenho ao encontrar o **[!UICONTROL Opportunities]** orientado por IA — recomendações que ajudam a melhorar a descoberta, o engajamento e as conversões.

>[!AVAILABILITY]
>
>Este recurso requer a licença **Ultima** do Adobe Sites Optimizer. Você pode solicitar uma licença por meio do Adobe Customer Technical Advisor. Depois que sua conta é provisionada, o recurso Oportunidades fica disponível na interface do [!DNL Adobe Commerce Optimizer] e você pode começar a usar insights orientados por IA para otimizar suas estratégias de vitrine e merchandising.

- [Oportunidades](../manage-results/opportunities.md)

## Commerce Salesforce Connector {#commerce-salesforce-connector}

O Commerce Salesforce Connector (integrado no Adobe App Builder) sincroniza dados de catálogo e preço do Salesforce Commerce Cloud B2C com o [!DNL Adobe Commerce Optimizer] para que você possa usar os recursos de merchandising e vitrine da Adobe sem reformatar a sua infraestrutura de comércio do Salesforce. Você pode agendar sincronizações, executar atualizações sob demanda e estender a integração usando as APIs do Salesforce Commerce.

- [Salesforce Commerce Connector](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Documentação técnica do Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Introdução ao Adobe Commerce Optimizer](../get-started.md)
