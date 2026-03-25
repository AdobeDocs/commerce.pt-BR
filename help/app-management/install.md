---
title: Instalar e acessar [!DNL App Management]
description: Pré-requisitos e requisitos de acesso para usar o Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: 86c0945bbb0a562de1b66d420dec2a05d4d81e5f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Instalar e acessar [!DNL App Management]

[!DNL App Management] está disponível no Administrador do Commerce para instâncias do Commerce qualificadas. A disponibilidade depende do tipo de implantação.

## Disponibilidade

Depois de atender aos seguintes requisitos, selecione a guia correspondente ao seu tipo de implantação abaixo, para ver se o [!DNL App Management] requer instalação ou se já está disponível na sua instância.

## Pré-requisitos

Antes de associar um aplicativo, verifique se você tem o seguinte:

| Requisito | Descrição |
|-------------|-------------|
| **Acesso de administrador** | Administrador do Commerce com [!DNL App Management] permissões |
| **Aplicativo implantado** | aplicativo App Builder implantado em sua organização e pronto para se conectar |
| **Acesso à organização** | Acesso à organização da Adobe em que o aplicativo é implantado |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management] está disponível automaticamente em [!DNL Adobe Commerce as a Cloud Service]. Nenhuma instalação é necessária. [Habilite-o no Administrador](#access-app-management) e comece a associar aplicativos.

>[!TAB Adobe Commerce na nuvem (PaaS) e no local]

* O **Adobe Commerce 2.4.8 e posterior**—[!DNL App Management] é incluído automaticamente. Nenhuma instalação é necessária.

* **Adobe Commerce 2.4.5 a 2.4.7**—Instale o [!DNL Admin UI SDK] (que inclui [!DNL App Management]) usando o Composer:

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  Em seguida, execute:

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

Consulte [Instalar ou atualizar o Adobe Commerce Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"} para obter mais informações.

>[!ENDTABS]

## Acessar [!DNL App Management]

1. Faça logon no Administrador do Commerce.

1. Navegue até **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

A visualização [!DNL App Management] é exibida. Aqui, você pode associar, configurar e gerenciar aplicativos do App Builder.

## Instalação de aplicativos do App Builder

Se você precisar instalar um aplicativo do App Builder da Adobe Exchange (por exemplo, um aplicativo de integração ou marketplace pré-criado), consulte [Instalar aplicativos do App Builder da Adobe Exchange](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} para obter instruções passo a passo.

Depois que um aplicativo for instalado e implantado, use o [!DNL App Management] para [associá-lo à sua instância do Commerce](manage-app.md#associate-an-app) e definir suas configurações.

## webhooks e aplicativos do Commerce

Alguns aplicativos do App Builder usam [webhooks do Adobe Commerce](https://developer.adobe.com/commerce/extensibility/webhooks/) para que o Commerce possa chamar seu aplicativo por HTTP quando determinados eventos ocorrerem (por exemplo, depois que um produto for salvo). Os pontos de extremidade e a lógica de assinatura do Webhook são definidos pelo **desenvolvedor de aplicativos** quando o aplicativo é criado e implantado; os administradores de loja não configuram webhooks separadamente no Gerenciamento de Aplicativos.

Depois de [associar o aplicativo](https://experienceleague.adobe.com/pt-br/docs/commerce/app-management/manage-app/manage-app) à sua instância do Commerce e concluir as instruções de configuração do aplicativo, o comportamento de webhook segue a implementação do aplicativo.

Se [!DNL App Management] não puder acionar o ponto de extremidade de validação do aplicativo (por exemplo, a URL está inacessível ou a resposta não atende aos requisitos), você poderá ver um erro semelhante ao seguinte no painel [!DNL App Management]:

![Erro de validação do Webhook](assets/webhook-validation-error.png){width="600" zoomable="yes"}

Trabalhe com o **desenvolvedor de aplicativos** para corrigir a configuração ou implantação do webhook, para que a validação obtenha êxito.

**Desenvolvedores de aplicativos**. Para implementar assinaturas de webhook e respostas de manipulador do App Builder, consulte [Webhooks](https://developer.adobe.com/commerce/extensibility/app-management/installation/webhooks/) na documentação do desenvolvedor de Extensibilidade do Commerce e o pacote [`@adobe/aio-commerce-lib-webhooks`](https://github.com/adobe/aio-commerce-sdk/tree/main/packages/aio-commerce-lib-webhooks) no GitHub.
