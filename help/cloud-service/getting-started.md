---
title: Introdução ao  [!DNL Adobe Commerce as a Cloud Service]
description: Saiba como começar a usar o  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: c608d9e82a892e40d362065c229b8d451ed3dbfb
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Introdução

[!DNL Adobe Commerce as a Cloud Service] fornece a maioria das configurações prontas para uso. Depois de concluir alguns processos de configuração básica, seu armazenamento entrará em funcionamento rapidamente. Este guia orienta você na criação e no trabalho com uma instância.

Clique nas guias abaixo para ver as visões gerais de alto nível do fluxo de trabalho para os seguintes tipos de usuário:

* Administradores
* Comerciantes
* Desenvolvedores

>[!BEGINTABS]

>[!TAB Fluxo de trabalho de administrador e comerciante]

Este diagrama fornece uma visão geral de alto nível de como administradores e comerciantes acessam e gerenciam instâncias do [!DNL Adobe Commerce as a Cloud Service]. Consulte o [Guia do Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html) para obter mais informações sobre fluxos de trabalho de administrador.

![[!DNL Adobe Commerce as a Cloud Service] diagrama de fluxo de comerciante](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Fluxo de trabalho do desenvolvedor]

Este diagrama fornece uma visão geral de alto nível de como os desenvolvedores criam integrações com o [!DNL Adobe Commerce as a Cloud Service] usando o App Builder. Consulte a [documentação da API](https://developer.adobe.com/commerce/webapi/rest/) para obter mais informações.

![[!DNL Adobe Commerce as a Cloud Service] diagrama do fluxo do desenvolvedor](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Criar uma instância

>[!NOTE]
>
>Antes de criar uma instância, o administrador de produto ou administrador de sistema da sua organização deve adicioná-lo como usuário do produto [!DNL Adobe Commerce as a Cloud Service]. Consulte [Adicionar usuários e administradores](./user-management.md#add-users-and-admins) para obter mais informações.

[!DNL Adobe Commerce as a Cloud Service] instâncias usam um sistema baseado em crédito. Você pode criar várias instâncias, mas cada instância requer uma quantidade relativa de créditos. A quantidade de créditos que você tem inicialmente depende de sua assinatura.

1. Faça logon em sua conta do [Adobe Experience Cloud](https://experience.adobe.com/).

1. Em [!UICONTROL Quick access], clique em [!UICONTROL **Commerce**] para abrir o [!UICONTROL Commerce Cloud Manager].

   O [!UICONTROL Commerce Cloud Manager] exibe uma lista de [!DNL Adobe Commerce as a Cloud Service] instâncias que estão disponíveis em sua organização do Adobe IMS.

1. Clique em [!UICONTROL **Adicionar instância**] no canto superior direito da tela.

   ![Criar Instância](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Selecione [!UICONTROL **Commerce as a Cloud Service**].

1. Insira um **Nome** e uma **Descrição** para sua instância.

1. Selecione a região onde deseja que sua instância seja hospedada.

   >[!NOTE]
   >
   >Depois de criar a instância, você não poderá modificar a região.

1. Escolha o [!UICONTROL **Tipo de Ambiente**] para sua instância. Você pode escolher entre as seguintes opções:

   * [!UICONTROL **Sandbox**] - Ideal para fins de design e teste. Você deve iniciar a jornada [!DNL Adobe Commerce as a Cloud Service] usando o ambiente de sandbox.
   * [!UICONTROL **Produção**] - Para lojas online e sites voltados para o cliente.

   >[!NOTE]
   >
   >Atualmente, as instâncias de sandbox estão limitadas à região da América do Norte.

1. _(Opcional)_ Se desejar incluir dados de produtos de exemplo para fins de teste e aprendizado, selecione [!UICONTROL **Adobe Store**] na lista suspensa [!UICONTROL **Dados de teste**].

   Você pode ignorar essa opção, mas sua loja não terá nenhum produto se você tiver. Será necessário [importar seu catálogo](#import-your-catalog) para ver a experiência completa da vitrine.

1. Clique em [!UICONTROL **Adicionar instância**].

## Acessar uma instância

Após criar uma instância, você pode acessá-la pelo [!UICONTROL Commerce Cloud Manager].

1. Faça logon em sua conta do [Adobe Experience Cloud](https://experience.adobe.com/).

1. Em [!UICONTROL Quick access], clique em [!UICONTROL **Commerce**] para abrir o [!UICONTROL Commerce Cloud Manager].

   O [!UICONTROL Commerce Cloud Manager] exibe uma lista de instâncias que estão disponíveis em sua organização do Adobe IMS.

1. Para abrir o [!UICONTROL Commerce Admin] para uma instância, clique no nome da instância.

>[!TIP]
>
>Para ver informações sobre sua instância, incluindo os endpoints REST e GraphQL e o URL Admin, clique no ícone de informações ao lado do nome da instância.

## Importar seu catálogo

Por padrão, [!DNL Adobe Commerce as a Cloud Service] instâncias não incluem dados de produtos. Você tem a opção de incluir dados de amostra do produto ao criar uma instância para fins de teste e aprendizado antes de importar seu próprio catálogo.

Há duas maneiras de importar seu catálogo para o [!DNL Adobe Commerce as a Cloud Service]:

* [**Administrador do Commerce**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Uma interface amigável que permite importar os dados do catálogo com apenas alguns cliques.
* [**Importar API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - Uma API REST que permite importar os dados do catálogo de forma programática.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Configurar a loja

Agora que você criou uma instância, você está pronto para prosseguir [configurando](storefront.md) sua Commerce Storefront com a Edge Delivery Services.
