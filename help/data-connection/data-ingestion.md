---
title: Tipos de dados do Commerce
description: Saiba mais sobre os tipos de dados que você pode coletar e enviar para a Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 6354963c-f27f-4e69-9ecb-acb4befb7c2a
TQID: https://experienceleague.adobe.com/LXMqOhHAZpUHaCeeU5ioKKXVrkLftospQEPDd9H-MD8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c09c161ca293b14918bd1ea3248978c12190584c
workflow-type: tm+mt
source-wordcount: 342
ht-degree: 0%

---

# Tipos de dados do Commerce

A [extensão de Conexão de Dados](overview.md) conecta seus dados do Commerce à Experience Platform. Os dados destinados ao uso na Experience Platform estão agrupados em dois tipos de comportamento: dados de série temporal, que pertencem à classe **Evento de experiência**, e dados de registro, que pertencem à classe **Perfil individual**.

Saiba mais sobre [comportamento dos dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition#data-behaviors) e [classes](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/composition#class) no Experience Platform.

## Dados de série temporal

Os dados de série temporal fornecem um instantâneo do sistema no momento em que uma ação foi tomada direta ou indiretamente por um titular de registro. Por exemplo, quando um comprador navega por um produto em seu site, o adiciona um produto ao carrinho, faz um pedido e assim por diante. Os dados de série temporal são assimilados na Experience Platform usando um esquema que tem a classe definida como **Evento de experiência**.

### Dados de série temporal capturados

Consulte [eventos comportamentais](events.md) e [eventos de back office](events-backoffice.md) para saber quais dados são capturados quando um evento de série temporal é gerado.

### Esquema necessário para assimilar dados do evento de série temporal

Saiba como [criar um esquema](update-xdm.md) que possa assimilar dados de evento de série temporal comportamental e de back office.

## Registrar dados

Os dados do registro fornecem informações sobre os atributos de um assunto. Um assunto pode ser uma organização ou um indivíduo. Por exemplo, um comprador em seu site cria uma conta e gera dados de registro. Estes dados são assimilados na Experience Platform usando um esquema que tem a classe definida como **Perfil Individual**. Você pode enviar esses dados de registro para o serviço de gerenciamento e segmentação de perfis da Adobe: [Real-Time CDP](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview).

### Dados de registro de perfil capturados

Consulte [dados de registro de perfil do cliente](events-profilerecord.md) para saber quais dados são capturados quando um registro de perfil é gerado.

### Esquema necessário para assimilar dados de registro de perfil

Saiba como [criar um esquema](profile-data.md) que possa assimilar dados de registro de perfil.
