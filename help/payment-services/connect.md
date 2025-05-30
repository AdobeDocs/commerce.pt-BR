---
title: Conectar sua instância
description: Conecte sua instância do Commerce usando uma chave de API e uma chave privada e especifique o espaço de dados na configuração.
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: 0f2e9c3a7d990a46bafc5f3b8a083436d42643b5
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Conectar sua instância

Conecte sua instância do Commerce usando uma chave de API e uma chave privada e especifique o espaço de dados na configuração usando o [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=pt-BR). **Você configurou esta conexão apenas uma vez.**

>[!VIDEO](https://video.tv.adobe.com/v/3448022?captions=por_br)

>[!INFO]
>
> Consulte o vídeo do [[!DNL Adobe Commerce] Conector de serviços](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=pt-BR) para obter mais informações.

* Se você já *conectou sua instância*, obtendo e usando suas credenciais de API e configurando os Serviços Commerce, prossiga para [configurando sua sandbox de teste](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/sandbox.html?lang=pt-BR).
* Se você ainda *precisa conectar sua instância*, consulte as informações neste tópico sobre [obtenção de credenciais de API](#obtain-api-credentials) e [configuração dos Serviços Commerce](#configure-commerce-services).
* Se você estiver *sem certeza se sua instância está conectada*, navegue até **Sistema** > Serviços > **Commerce Services Connector** e exiba os valores de chave de API pública e privada nas seções [!UICONTROL Sandbox Keys] e [!UICONTROL Production Keys] e os campos *Projeto* e *Espaço de Dados* na seção [!UICONTROL SaaS Identifier]. Se esses valores estiverem presentes, sua instância será conectada.

>[!NOTE]
>
>Todos os comerciantes habilitados para Serviços de Pagamento podem usar um espaço de dados de produção e dois espaços de dados de teste.

## Obter credenciais de API

Para consumir um serviço SaaS do Commerce, você deve usar as chaves de API da sua instância (chave de API pública do Commerce e uma chave privada) para sandbox e produção, que são criadas e gerenciadas no [Painel da Minha Conta](https://account.magento.com/customer/account/login). [O par de chaves](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/config/services/saas) pode ser criado para uma conta da Commerce, um para sandbox e um para produção, embora apenas um par possa ser usado ativamente de cada vez.

>[!NOTE]
>
>Precisa de ajuda para acessar seu painel [!UICONTROL My Account]? Consulte [Criar uma conta do Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/start/commerce-account/commerce-account-create).

Uma chave de API pública, uma vez criada, está sempre disponível no Painel Minha conta. Ela pode ser copiada ou excluída, conforme necessário. A chave de API privada torna-se visível quando você cria uma chave de API pública para sandbox ou produção; ela só está disponível para copiar ou salvar da caixa de diálogo subsequente e não pode ser acessada posteriormente.

Um determinado par de chaves de API é válido para todos os serviços da Commerce em um ambiente. Portanto, se você já tiver o Commerce Services configurado para sua instância, seu par de chaves de API já estará presente no Commerce Services Connector.

Se sua chave de API for perdida, um novo par de chaves de API deverá ser [gerado](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html?lang=pt-BR#generate-an-api-key-and-private-key) e [aplicado](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/connect.html?lang=pt-BR#configure-saas-project) à configuração do Commerce Services Connector no Administrador. Se as chaves incorretas estiverem configuradas ou não houver nenhuma na configuração, uma caixa de diálogo de erro de verificação de conta será exibida nos Serviços de pagamento, notificando-o de que a conta não foi verificada.

Consulte uma [lista de Serviços Commerce disponíveis que usam a API](https://experienceleague.adobe.com/pt-br/docs/commerce-merchant-services/user-guides/integration-services/saas#availableservices).

Para saber como gerar uma chave de API para ambientes de sandbox ou produção, consulte [Credenciais](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=pt-BR#apikey).

>[!IMPORTANT]
>
>É recomendável não regenerar um par de chaves de API *e*. Altere o identificador SaaS e/ou o espaço de dados em uma instância de produção ativa. Você perderá os dados da sua instância se eles forem modificados.

## Configurar os serviços da Commerce

A mesma chave de API pode ser usada em várias instâncias, mas cada instância deve ter seu próprio [Espaço de dados SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=pt-BR#saasenv).

>[!NOTE]
>
>Os comerciantes devem usar as mesmas chaves geradas para a MageID em seus direitos de Pagamento.

Agora que obteve as credenciais, é possível configurar o projeto SaaS e o Espaço de dados Saas.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**.
1. Clique em **[!UICONTROL Configure Commerce Services]**.

   Essa opção estará visível se você ainda não tiver configurado os Serviços da Commerce para sua conta.

   Você é direcionado para a área de configuração no Administrador, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, para configurar o Commerce Services Connector.

1. Para configurar os Serviços da Commerce, siga as etapas descritas em [Configuração do SaaS](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html?lang=pt-BR#saasenv).

   >[!INFO]
   >
   > Consulte o vídeo do [[!DNL Adobe Commerce] Conector de serviços](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=pt-BR#configuration-faqs) para obter mais informações.

## Endpoint

[!DNL Payment Services] usa o [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/saas.html?lang=pt-BR) para se conectar aos Serviços Commerce e implantar como SaaS. Este [!DNL Commerce Services Connector] se comunica através do ponto de extremidade em:

* `commerce-beta.adobe.io` para ambientes de sandbox.
* `commerce.adobe.io for` para ambientes dinâmicos.
