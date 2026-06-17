---
title: Módulos de exportação de dados SaaS
description: Saiba mais sobre os pacotes do módulo Magento incluídos no  [!DNL SaaS Data Export]  e suas funções na coleta, transformação e envio de dados para os serviços SaaS da Adobe.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

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
