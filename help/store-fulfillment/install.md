---
title: Instalação
description: Instale o  [!DNL Store Fulfillment solution] para uma loja da Adobe Commerce usando o Composer para PHP.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Instalação

Conclua a instalação inicial da extensão [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] em um ambiente de não produção com o gerenciador de filas em execução e o armazenamento em cache configurado para permitir o tratamento de exceções. Certifique-se de que seu ambiente de desenvolvimento inclua ferramentas de desenvolvimento para garantir as práticas recomendadas para operar e manter sua instância do Adobe Commerce.

>[!TIP]
>
>Atualize a extensão Store Fulfillment para Adobe Commerce local seguindo as [instruções de atualização](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html?lang=pt-BR) no _Guia de Atualização do Adobe Commerce_. Para o Adobe Commerce na infraestrutura em nuvem, consulte [Atualizar uma extensão](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html?lang=pt-BR#upgrade-an-extension) no *Guia do Commerce na Infraestrutura em Nuvem*.

## Pré-requisitos

Revise os [requisitos](solution-requirements.md) para a solução de Atendimento da Loja e colete as informações necessárias antes de instalar ou atualizar a extensão [!DNL Store Fulfillment] para o Adobe Commerce.

Se você tiver instalado uma versão de pré-lançamento ou beta da extensão Store Fulfillment for Adobe Commerce, use o seguinte comando para removê-la antes de instalar a versão atual.

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## Requisitos de instalação

- **Acesso ao Atendimento da Loja pelo arquivo de software Walmart Commerce Technologies (arquivo .zip)**—Durante o processo de integração e habilitação, trabalhe com seu Gerente de Conta para obter acesso ao arquivo de instalação da extensão de Atendimento da Loja.

- **Informações da conta da Adobe Commerce**-A instalação da solução [!DNL Store Fulfillment] requer uma [[!DNL Commerce] conta](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"}. Você precisa de uma ID de conta e credenciais com acesso de Proprietário ou Administrador ao projeto [!DNL Adobe Commerce].

- Para [!DNL Adobe Commerce] em projetos de infraestrutura em nuvem, os instaladores de software devem ter acesso de administrador ao projeto em nuvem. Consulte [Gerenciar acesso do usuário](https://experienceleague.adobe.com/pt-br/docs/commerce-cloud-service/user-guide/project/user-access).

- **Experiência usando o Composer e o[!DNL Commerce CLI]**—Consulte [Instalação geral da CLI](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"} para obter informações sobre como usar essas ferramentas para instalar e gerenciar extensões na plataforma [!DNL Adobe Commerce].

- **Experiência na instalação de extensões de terceiros no Adobe Commerce**. Para obter referência, consulte a documentação do Adobe Commerce.

   - [Instalar uma extensão para uma Adobe Commerce na instância da infraestrutura em nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension).

   - [Instale uma extensão para uma instância local do Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/extensions).

### Etapa 1: baixar o pacote de extensão

Siga as instruções fornecidas pelos representantes da sua conta para baixar o arquivo que contém os pacotes do Composer para instalar a extensão Store Fulfillment Services.

### Etapa 2: Extrair artefatos de extensão para seu aplicativo

Extraia o arquivo que contém o pacote de integração para instalar a extensão Store Fulfillment Services.

1. Crie um diretório de destino para os arquivos extraídos.

   - Na linha de comando, vá para o diretório raiz do documento do servidor Web.

   - Crie um diretório `artifacts`.

1. Extraia o arquivo morto para o novo diretório.

1. Verifique se os arquivos foram extraídos revisando a lista de arquivos.

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### Etapa 3: configurar seu aplicativo usando o Composer

Use o Composer para configurar o diretório de origem para a instalação e instalar a extensão Store Fulfillment Services.

1. Configure o repositório de origem para a instalação do Composer.

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. Adicione a extensão Store Fulfillment Services a `composer.json`.

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>Para obter melhor desempenho em instâncias locais do Adobe Commerce, você pode [atualizar a configuração de carregamento automático](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html?lang=pt-BR#update-the-autoloader): `composer dump-autoload --optimize`

### Etapa 4: Atualizar o esquema de banco de dados e os dados

Conclua a instalação usando o `bin/magento setup:upgrade` para atualizar o esquema de banco de dados e os dados com as alterações para dar suporte à solução Store Fulfillment.

>[!NOTE]
>
>Para projetos de infraestrutura em nuvem do Adobe Commerce, não é necessário registrar a extensão. Em vez disso, confirme as alterações de código da etapa anterior e envie-as para a ramificação do ambiente. Os comandos para atualizar o esquema do banco de dados e os dados são executados automaticamente durante o processo de criação e implantação da nuvem.

### Etapa 5: concluir a instalação

1. Registre a extensão com o Adobe Commerce usando o comando da CLI do Magento `setup:upgrade`.

   ```bash
   bin/magento setup:upgrade
   ```

1. Se solicitado, recompile o projeto [!DNL Commerce].

   ```bash
   bin/magento setup:di:compile
   ```

1. Limpe o cache.

   ```bash
   bin/magento cache:clean
   ```

1. Desabilitar modo de manutenção.

   ```bash
   bin/magento maintenance:disable
   ```

### Etapa 6: verificar a instalação

No servidor do Adobe Commerce, verifique se os módulos da extensão Store Fulfillment Services estão instalados e habilitados.

1. Faça logon no servidor.

   Para instalações no Adobe Commerce na infraestrutura em nuvem, [use o SSH para fazer logon no ambiente remoto](https://experienceleague.adobe.com/pt-br/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh).

1. Verifique se os módulos Store Fulfillment Services estão habilitados.

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   A saída deve incluir os seguintes módulos:

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### Etapas adicionais

Se necessário, use o comando CLI [setup:static-content:deploy](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} para implantar arquivos de exibição estáticos no ambiente de produção.

```bash
php bin/magento setup:static-content:deploy -f
```

A opção `-f` é necessária se você estiver usando um tema em branco.

>[!NOTE]
>
>Para obter mais informações, consulte o artigo [Práticas recomendadas de implantação de conteúdo estático no Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html?lang=pt-BR) na Central de Ajuda do Adobe Commerce.


