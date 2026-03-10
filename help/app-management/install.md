---
title: Instalar e acessar [!DNL App Management]
description: Pré-requisitos e requisitos de acesso para usar o Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

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
