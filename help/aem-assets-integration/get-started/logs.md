---
title: Exibir e gerenciar logs
description: Saiba onde encontrar e gerenciar logs para a Integração do AEM Assets para o Commerce.
feature: CMS, Media, Integration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
source-git-commit: d425bad4d3314aa0e14b639ffb8d89dd8b6b0f74
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Exibir e gerenciar logs

A integração do AEM Assets fornece os seguintes arquivos de log na instância do Commerce:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Para obter uma exibição centrada em ativos de ativos sincronizados no Administrador, incluindo pesquisa, filtros e resumos de erros de sincronização, consulte [Exibir status de sincronização do AEM Assets](sync-status.md).

Solicite ao administrador do sistema que verifique a programação de rotação dos arquivos de registro para esses registros, a fim de evitar que eles fiquem muito grandes. Em alguns ambientes, os logs giram automaticamente; em outros, você deve configurar a rotação de logs manualmente.  Para obter detalhes, consulte os seguintes tópicos:

- Para instalações locais do Adobe Commerce, peça ao Administrador do Sistema para configurar a [rotação de log](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings).
- Para projetos de infraestrutura em nuvem do Adobe Commerce, consulte [Exibir e gerenciar logs](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html).
