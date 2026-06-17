---
title: Mecanismo de bloqueio de feed para exportação de dados SaaS
description: Saiba como o [!DNL SaaS Data Export] usa bloqueios de feed para evitar operações de sincronização conflitantes e proteger a integridade de dados durante atualizações de feed simultâneas.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# Mecanismo de bloqueio de feed para exportação de dados SaaS

A extensão [!DNL SaaS Data Export] usa um mecanismo de bloqueio de feed para evitar condições de corrida quando vários processos tentam sincronizar o mesmo feed simultaneamente. Isso pode acontecer, por exemplo, quando uma ressincronização acionada pelo cron se sobrepõe a uma chamada manual da CLI `saas:resync`.

## Como funciona o bloqueio de feed

Cada operação de sincronização de feed — seja acionada por um trabalho cron ou por uma chamada CLI `saas:resync` manual — segue a mesma sequência:

1. O processo tenta adquirir o bloqueio de feed. A tentativa de bloqueio não é bloqueada e retorna imediatamente se o bloqueio já estiver sendo mantido por outro processo.
1. Se o bloqueio for **não disponível**, a operação será ignorada e registrada.

   Nenhum dado é perdido. A próxima execução do cron seleciona as alterações pendentes após a conclusão do processo atual.
1. Se o bloqueio for **adquirido**, o processo registrará seu nome e PID para fins de diagnóstico e, em seguida, executará a sincronização.
1. Quando a sincronização for concluída ou falhar, o bloqueio será liberado incondicionalmente para que o próximo trabalho cron agendado possa continuar normalmente.

Somente uma operação de sincronização pode manter o bloqueio de feed por vez, independentemente de ele ter sido iniciado pelo cron ou pela CLI. O bloqueio de feed é implementado através de `LockManagerInterface` de [!DNL Adobe Commerce]. O back-end padrão é o MySQL, que usa as funções `GET_LOCK` e `RELEASE_LOCK`. Para configurar um provedor de bloqueio diferente, consulte [Configurar o provedor de bloqueio](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}.

## Mensagens de log esperadas

A seguinte mensagem em `commerce-data-export.log` é normal e não indica um problema:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

Esta mensagem aparece quando uma sincronização parcial acionada pelo cron tenta ser executada enquanto uma reindexação completa ou `saas:resync` já está em andamento. A operação ignorada não é perdida. Quando o processo em execução for concluído e liberar o bloqueio, a próxima execução do cron selecionará e sincronizará todas as alterações pendentes.

>[!NOTE]
>
>Para obter informações gerais sobre o formato de log e os tipos de operação registrados em `commerce-data-export.log`, consulte [Revisar logs e solucionar problemas](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Sincronizar dados com a Exportação de dados SaaS](sync-overview.md)
> - [Sincronizar feeds usando a CLI do Commerce](data-export-cli-commands.md)
> - [Pipeline de sincronização do conector](../aco-connector/connector-sync-pipeline.md)
> - [Configurar o provedor de bloqueio](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
