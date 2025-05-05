---
title: Atualizar esquemas de evento de série de tempo para assimilação de dados do Commerce
description: Saiba como criar um esquema, conjunto de dados e sequência de dados para coletar e enviar dados do evento de série de tempo para assimilação de dados do Commerce.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Atualizar esquemas de evento de série de tempo para assimilação de dados do Commerce

Uma das [etapas de integração](overview.md#onboarding-steps) para usar a extensão [!DNL Data Connection] é acessar o espaço de trabalho da sequência de dados e [criar uma sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR) específica para o Adobe Commerce. Ao criar esse fluxo de dados, você também deve selecionar um esquema que descreva os dados que planeja assimilar. Esse esquema deve incluir grupos de campos específicos do comércio.

Este artigo fornece os grupos de campos que seu esquema deve incluir para coletar com êxito os seguintes dados de série temporal fornecidos pelos eventos do Adobe Commerce:

- [Comportamento](events.md) - Inclui eventos da loja, do perfil, da pesquisa e B2B.
- [Back office](events-backoffice.md) - Inclui status de pedido e eventos de perfil.

Saiba mais sobre [dados de série temporal](data-ingestion.md).

Saiba mais sobre as [noções básicas da composição de esquema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR).

## Atualizar esquema com dados comportamentais de série temporal e de evento de back office

Nesta seção, você aprenderá a atualizar seu esquema existente ou criar um esquema para incluir dados de evento comportamentais e de back office.

>[!NOTE]
>
>Consulte [dados do evento de perfil de série temporal](#time-series-profile-event-data) para saber como adicionar campos específicos de perfil.

1. Se você ainda não tiver um esquema, [crie](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#create) um com a classe definida como **Evento de experiência**.

1. [Adicione](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#add-field-groups) os seguintes grupos de campos específicos da Commerce (ou edite o esquema existente e adicione esses grupos de campos):

   - Pesquisa no site
   - Visitar página da Web
   - Processo de logon do usuário
   - Chaves de referência
   - Detalhes de contato pessoal
   - Detalhes do canal
   - Detalhes do Commerce
   - Adobe Analytics ExperienceEvent Commerce (se desejar enviar dados para o Adobe Analytics)

   >[!NOTE]
   >
   > Não defina grupos de campos específicos do Commerce como `Primary identity`. Isso identifica o campo como obrigatório e o Experience Platform espera esse campo em cada evento. Se esse campo estiver ausente, a assimilação de dados falhará.

   Seu esquema agora contém grupos de campos específicos do Commerce para que os dados de série temporal coletados dos eventos [comportamentais](events.md) e [back office](events-backoffice.md) do Commerce sejam representados no esquema.

1. [Habilitar](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#profile) o esquema para o Perfil.

   Quando um esquema é ativado para o Perfil, qualquer conjunto de dados criado a partir desse esquema participa do Real-Time CDP, que mescla dados de fontes diferentes para criar uma visualização completa de cada cliente.

1. [Crie um conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=pt-BR#create-a-dataset) com base no esquema que você criou ou atualizou.

   Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

1. [Crie uma sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR) e selecione o esquema que contém os grupos de campos específicos do Commerce e o conjunto de dados correspondente.

   O fluxo de dados encaminha os dados coletados para o conjunto de dados. Os dados são representados no conjunto de dados com base no esquema selecionado.

Com os esquemas, conjuntos de dados e sequências de dados configurados para dados comportamentais e de back office, você pode [configurar](connect-data.md#data-collection) sua instância do Commerce para coletar e enviar esses dados para a Experience Platform.

Para incluir as informações do perfil do comprador, consulte [dados do evento de perfil de série temporal](#time-series-profile-event-data).

## Dados do evento de perfil de série temporal

Os dados do evento de perfil de série temporal são gerados a partir dos seguintes eventos:

- [&quot;accountCreated&quot;](events-backoffice.md#accountcreated)
- [&quot;accountUpdated&quot;](events-backoffice.md#accountupdated)
- [&quot;accountDeleted&quot;](events-backoffice.md#accountdeleted)

Se quiser assimilar os dados do evento de perfil do cliente na Experience Platform, atualize o esquema existente do Commerce e use o mesmo fluxo de dados já configurado, ou crie um fluxo de dados e um esquema específicos do perfil. Essa decisão se baseia na governança de dados da sua empresa. As próximas duas seções o guiarão em ambos os casos.

### Enviar dados do evento de perfil de série temporal para a Experience Platform usando sua sequência de dados existente

Se quiser adicionar [dados do evento de perfil do lado do servidor](events-backoffice.md#customer-profile-events-server-side) à sequência de dados existente do Commerce, adicione o grupo de campos `Demographic Details` ao esquema. Seu esquema agora contém os seguintes grupos de campos específicos do Commerce:

- Pesquisa no site
- Visitar página da Web
- Processo de logon do usuário
- Chaves de referência
- Detalhes de contato pessoal
- Detalhes do canal
- Detalhes do Commerce
- Adobe Analytics ExperienceEvent Commerce (se desejar enviar dados para o Adobe Analytics)
- Novo: **Detalhes demográficos**

Com a adição do grupo de campos `Demographic Details` ao esquema existente do Commerce, o conjunto de dados e a sequência de dados já associados ao esquema do Commerce são usados para os dados do perfil desta série temporal.

### Enviar dados do evento de perfil de série temporal para a Experience Platform em um fluxo de dados separado

Se você quiser adicionar [dados do evento de perfil do lado do servidor](events-backoffice.md#customer-profile-events-server-side) a um novo esquema e sequência de dados específicos do perfil, conclua as etapas a seguir.

1. [Crie](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#create) um esquema e defina a classe como **Evento de Experiência**.

1. [Adicione](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#add-field-groups) os seguintes grupos de campos específicos de perfil:

   - Detalhes demográficos
   - Detalhes de contato pessoal
   - Detalhes do canal
   - Detalhes do Commerce

1. [Habilitar](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=pt-BR#profile) o esquema para o Perfil.

   Quando um esquema é ativado para o Perfil, qualquer conjunto de dados criado a partir desse esquema participa do Real-Time CDP, que mescla dados de fontes diferentes para criar uma visualização completa de cada cliente.

1. [Crie um conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=pt-BR#create-a-dataset) com base no esquema criado.

   Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

1. [Crie uma sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR) e selecione o esquema XDM que contém os grupos de campos específicos do Commerce e o conjunto de dados correspondente.

   O fluxo de dados encaminha os dados coletados para o conjunto de dados. Os dados são representados no conjunto de dados com base no esquema selecionado.

Com os esquemas, conjuntos de dados e sequências de dados configurados para dados de perfil do cliente, você pode [configurar](connect-data.md#data-collection) sua instância do Commerce para coletar e enviar esses dados para a Experience Platform.

Para criar um esquema, conjunto de dados e sequência de dados para dados de registro de perfil, consulte [enviar dados de registro de perfil à Experience Platform](profile-data.md).
