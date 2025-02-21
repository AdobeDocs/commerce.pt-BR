---
title: Integrar o Adobe Experience Platform Mobile SDK ao Commerce
description: Saiba como usar o Adobe Experience Platform Mobile SDK com sua loja headless ou personalizada do Commerce.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Integrar o Adobe Experience Platform Mobile SDK ao Commerce

>[!IMPORTANT]
>
>O Adobe Experience Platform Mobile SDK para iOS é compatível com o iOS 11 ou posterior.

Integrar a [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) com o aplicativo móvel do Commerce permite que os comerciantes enviem os [dados do evento](events.md) do Commerce para a borda do Experience Platform.

Quando os dados do evento do Commerce estiverem disponíveis na borda, eles poderão ser acessados por outros aplicativos da Adobe Experience Cloud. Por exemplo, você pode usar os dados para criar públicos no Real-Time CDP e [usar esses públicos](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html) para personalizar seu aplicativo móvel do Commerce.

## Configuração

Para começar a usar o Adobe Experience Platform Mobile SDK com o Commerce, instale e configure o SDK no Experience Platform. Em seguida, finalize a configuração no Commerce.

### Experience Platform

1. Saiba mais sobre os recursos do aplicativo móvel consultando o [tutorial sobre Adobe Experience Cloud em aplicativos móveis](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html).

1. [Instalar e configurar](https://developer.adobe.com/client-sdks/documentation/getting-started/) o SDK no Experience Platform.

   >[!NOTE]
   >
   >O esquema criado e configurado na Experience Platform é o mesmo esquema usado no código do aplicativo no aplicativo móvel do Commerce.

### Commerce

Após concluir a configuração do SDK para a Experience Platform, adicione a configuração do SDK ao Commerce.

1. Para enviar dados do evento do Commerce para o Experience Platform por meio da SDK, você deve fornecer um esquema XDM no código do aplicativo. Este esquema deve corresponder ao esquema [configurado](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) para a SDK na Experience Platform.

   O exemplo a seguir mostra como rastrear o evento `web.webpagedetails.pageViews` e definir o `identityMap` usando o campo de email.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Conecte-se ao ambiente do Commerce Cloud.

   Nas configurações de build do seu projeto, adicione o URL ao endpoint do Commerce GraphQL. Tais como:

   - Depuração: http://_debug_.commerce.cloud/graphql/
   - Versão: http://_release_.commerce.cloud/graphql/

1. Para recuperar dados dos pontos de extremidade do Commerce GraphQL, gere primeiro os arquivos e diretórios necessários em seu projeto usando o [Gerador de código Apollo](https://www.apollographql.com/docs/ios/).

   1. No diretório do projeto, [instale](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) o Apollo iOS.

   1. [Inicialize](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) a CLI do Codegen Apollo.

      Isso cria um arquivo `apollo-codegen-configuration.json`.

   1. Gere os arquivos e diretórios necessários do GraphQL em seu projeto substituindo o conteúdo do arquivo `apollo-codegen-configuration.json` pelo seguinte:

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [Buscar](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) o esquema do Commerce GraphQL.

      Verifique se o caminho é para o arquivo `./apollo-codegen-config.json`, que contém a referência ao esquema do Commerce GraphQL.

   1. [Gerar](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) o código-fonte.

      Verifique se o caminho é para o arquivo `./apollo-codegen-config.json`, que contém as informações de configuração para gerar os arquivos e diretórios necessários.

   1. Na pasta **GraphQLGenerated** recém-criada, adicione ou edite tipos de GraphQL. Por exemplo, você pode adicionar um tipo `DynamicBlocks.graphql` com o seguinte conteúdo:

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   Agora você integrou o Adobe Experience Platform Mobile SDK ao seu aplicativo móvel do Commerce. Os dados do evento fluem do seu aplicativo para a borda do Experience Platform.

## Como distinguir eventos Commerce gerados de aplicativos móveis

Todos os [eventos](events.md) contêm um campo chamado `channel`. O campo `channel` contém `channel._id` e `channel._type`, que para uma loja Luma têm valores de namespace de `"https://ns.adobe.com/xdm/channels/web"` e `"https://ns.adobe.com/xdm/channel-types/web"`, respectivamente. No entanto, para uma vitrine móvel, os valores de namespace são `"https://ns.adobe.com/xdm/channels/mobile-app"` e `"https://ns.adobe.com/xdm/channel-types/mobile"`, respectivamente.

## Próximas etapas

Para saber como recuperar públicos-alvo da Real-Time CDP de seu aplicativo para dispositivos móveis Commerce para informar regras de preço de carrinho, blocos dinâmicos e regras de produto relacionadas, consulte [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk).
