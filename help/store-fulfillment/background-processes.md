---
title: Configuração do processo de segundo plano
description: Configure os agendamentos para  [!DNL Store Fulfillment] processos em segundo plano usados na sincronização de dados com os serviços de preenchimento.
role: Admin, Developer
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configuração do processo de segundo plano

A integração Store Fulfillment usa processos em segundo plano e filas de mensagens para obter o desempenho e a escala ideais. Crie ambientes para seus armazenamentos Adobe Commerce usando [variáveis de implantação](https://experienceleague.adobe.com/pt-br/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#cron_consumers_runner) que iniciam automaticamente [executores de fila de mensagens](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework).

Os processos em segundo plano são gerenciados com a funcionalidade padrão do Adobe Commerce [Tarefas Agendadas](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/cron). Esses processos são responsáveis por sincronizar dados de configuração de ordem e armazenamento de comerciante com serviços da Web de preenchimento de loja.

## Gerenciar tarefas agendadas para Atendimento de Loja

No Administrador, vá para **[!UICONTROL Stores > Configuration > Advanced > System > Cron (Scheduled Tasks) > Cron configuration options for group:store_fulfillment]**.

Revise a configuração padrão para os serviços de Atendimento da Loja. Você pode personalizar essas configurações com base no volume de processamento do pedido e na disponibilidade de recursos.
