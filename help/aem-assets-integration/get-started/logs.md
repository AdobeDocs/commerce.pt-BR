---
title: Exibir e gerenciar logs
description: Saiba onde encontrar e gerenciar logs para a Integração do AEM Assets para o Commerce.
feature: CMS, Media, Integration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# Exibir e gerenciar logs

A integração do AEM Assets fornece os seguintes arquivos de log na instância do Commerce:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Para obter uma exibição centrada em ativos de ativos sincronizados no Administrador, incluindo pesquisa, filtros e resumos de erros de sincronização, consulte [Exibir status de sincronização do AEM Assets](sync-status.md).

Solicite ao administrador do sistema que verifique a programação de rotação dos arquivos de registro para esses registros, a fim de evitar que eles fiquem muito grandes. Em alguns ambientes, os logs giram automaticamente; em outros, você deve configurar a rotação de logs manualmente.  Para obter detalhes, consulte os seguintes tópicos:

- Para instalações locais do Adobe Commerce, peça ao Administrador do Sistema para configurar a [rotação de log](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/next-steps/configuration#server-settings).
- Para projetos de infraestrutura em nuvem do Adobe Commerce, consulte [Exibir e gerenciar logs](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/test/log-locations).
