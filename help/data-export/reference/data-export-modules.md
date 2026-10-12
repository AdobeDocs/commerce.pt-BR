---
title: Módulos de exportação de dados SaaS
description: Saiba mais sobre os pacotes do módulo Magento incluídos no [!DNL SaaS Data Export] e suas funções na coleta, transformação e envio de dados para os serviços SaaS da Adobe.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 8%
---

# Módulos de exportação de dados SaaS

[!DNL SaaS Data Export] consiste em dois grupos de módulo: o primeiro para coleta e indexação de dados e o segundo para transporte e envio HTTP.

Esses módulos lidam com detecção de alteração de entidade, indexação de feed, extração de dados e definição de esquema.
A tabela a seguir fornece apenas módulos de nível de estrutura; a lista completa de módulos disponíveis depende dos pacotes instalados.

| Módulo | Finalidade | Classes de chave |
| --- | --- |--- |
| `DataExporter` | Estrutura principal: indexador, tabela de feed, hash, tentar novamente, bloqueio | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | DSL de consulta baseada em XML para coleta de dados | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | Transporte HTTP compartilhado, tentativa, CLI (`saas:resync`), orquestração de ressincronização | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

Para saber como esses módulos funcionam juntos durante a sincronização, consulte [Pipeline de exportação de dados SaaS](../sync-overview.md).

>[!MORELIKETHIS]
>
>- [Como a sincronização funciona](../sync-overview.md)
>- [Esquema da tabela de feeds](feed-table-reference.md)
>- [Gerenciar a extensão de exportação de dados SaaS](../manage-extension.md)
