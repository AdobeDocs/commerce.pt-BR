---
title: Mecanismo de bloqueio de feed para exportação de dados SaaS
description: Saiba como o [!DNL SaaS Data Export] usa bloqueios de feed para evitar operações de sincronização conflitantes e proteger a integridade de dados durante atualizações de feed simultâneas.
role: Admin, Developer
feature: Services
source-git-commit: cfa1002653bf66afd3f6b8484b33076adcd1b7d4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Mecanismo de bloqueio de feed para exportação de dados SaaS

A extensão [!DNL SaaS Data Export] usa um mecanismo de bloqueio de feed para evitar condições de corrida quando vários processos tentam sincronizar o mesmo feed simultaneamente. Isso pode acontecer, por exemplo, quando uma ressincronização acionada pelo cron se sobrepõe a uma chamada manual da CLI `saas:resync`.

## Como funciona o bloqueio de feed

Cada operação de sincronização de feed — seja acionada por um trabalho cron ou por uma chamada CLI `saas:resync` manual — segue a mesma sequência:

1. O processo tenta adquirir o bloqueio de feed. A tentativa de bloqueio não é bloqueada e retorna imediatamente se o bloqueio já estiver sendo mantido por outro processo.
1. Se o bloqueio for **não disponível**, a [operação será ignorada e registrada].

   Nenhum dado é perdido. A próxima execução do cron seleciona as alterações pendentes após a conclusão do processo atual.
1. Se o bloqueio for **adquirido**, o processo registrará seu nome e PID para fins de diagnóstico e, em seguida, executará a sincronização.
1. Quando a sincronização for concluída ou falhar, o bloqueio será liberado incondicionalmente para que o próximo trabalho cron agendado possa continuar normalmente.

Somente uma operação de sincronização pode manter o bloqueio de feed por vez, independentemente de ele ter sido iniciado pelo cron ou pela CLI. O bloqueio de feed é implementado através de `LockManagerInterface` de [!DNL Adobe Commerce]. O back-end padrão é o MySQL, que usa as funções `GET_LOCK` e `RELEASE_LOCK`. Para configurar um provedor de bloqueio diferente, consulte [Configurar o provedor de bloqueio](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}.

## Mensagens de log esperadas

A seguinte mensagem em `commerce-data-export.log` é normal e não indica um problema:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

Esta mensagem aparece quando uma sincronização parcial acionada pelo cron tenta ser executada enquanto uma reindexação completa ou `saas:resync` já está em andamento. A operação ignorada não é perdida. Quando o processo em execução for concluído e liberar o bloqueio, a próxima execução do cron selecionará e sincronizará todas as alterações pendentes.

>[!NOTE]
>
>Para obter informações gerais sobre o formato de log e os tipos de operação registrados em `commerce-data-export.log`, consulte [Revisar logs e solucionar problemas](troubleshooting-logging.md).

## Mais ajuda sobre este tópico

- [Sincronizar dados com a exportação de dados SaaS](data-synchronization.md)
- [Sincronizar feeds usando a CLI do Commerce](data-export-cli-commands.md)
- [Configurar o provedor de bloqueio](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
