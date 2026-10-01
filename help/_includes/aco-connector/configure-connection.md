---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# Obter detalhes da instância [!DNL Commerce Optimizer]

Obtenha a _ID do locatário_ do campo _[!DNL Instance Id]_na [[!DNL Instance details] página](/help/optimizer/get-started.md#manage-instances) da instância [!DNL Commerce Optimizer] ou da URL usada para acessar a instância. Por exemplo, em `https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`.

1. No Administrador do Commerce, selecione **[!UICONTROL Adobe Commerce Optimizer]** para exibir a página de configuração com instruções.

   ![[!DNL Commerce Optimizer] página de configuração](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Na linha de comando, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para se conectar ao ambiente de preparo [!DNL Adobe Commerce].

1. Para configurar a integração, execute o seguinte comando da CLI do [!DNL Adobe Commerce], substituindo os valores de espaço reservado pelos valores do seu projeto [!DNL Commerce Optimizer]:

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Verifique a conexão retornando ao Administrador do Commerce e selecionando a opção [!UICONTROL Adobe Commerce Optimizer].

   Ao selecionar a opção, ela abrirá a interface do usuário do [!DNL Commerce Optimizer] em uma nova guia.
