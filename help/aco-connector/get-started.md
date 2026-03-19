---
title: Introdução ao Adobe Commerce Optimizer Connector
description: Saiba como instalar e configurar o conector, personalizar a configuração de exportação, conectar ao Adobe Commerce Optimizer e monitorar o status de sincronização de dados.
feature: Personalization, Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: f302efcb6c08d5a3c695a47ae16fdac790a8bc24
workflow-type: tm+mt
source-wordcount: '1108'
ht-degree: 0%

---


# Introdução

Instale e configure o Commerce Optimizer Connector para sincronizar os dados do catálogo do Adobe Commerce com o [!DNL Adobe Commerce Optimizer] e, em seguida, monitore o status de sincronização de dados para garantir que sua loja esteja atualizada.

## Requisitos para usar a integração

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 ou 8.4
   * Composer 2.x

* [!DNL Adobe Commerce Optimizer] licença com uma instância de sandbox provisionada.

* Acesse o [repo.magento.com](https://repo.magento.com) para baixar o metapackage do Conector Commerce usando o Composer.

* Acesso de administrador a uma [instância da sandbox do Adobe Commerce Optimizer](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

O usuário do Adobe Commerce que configura a integração deve ter:

* Acesso de administrador ao Administrador do Adobe Commerce.

* [Acesso de linha de comando ao servidor de aplicativos do Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/project/user-access).

* Acesso de desenvolvedor à [Organização de IMS](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/administration/organizations?) onde o projeto [!DNL Adobe Commerce Optimizer] é provisionado.

>[!BEGINSHADEBOX]

## Pré-requisitos

Se você tiver uma das seguintes extensões instaladas, desinstale-as antes de instalar o Commerce Optimizer Connector:

* Adobe Commerce Live Search (`magento/live-search`)
* Recomendações de produto do Adobe Commerce (`magento/product-recommendations`)
* Serviço de Catálogo da Adobe Commerce (`magento/catalog-service`, `magento/catalog-service-installer`)
* Painel de Gerenciamento de Dados (`magento-catalog-sync-admin`)

Os dados associados a essas extensões ainda estão disponíveis no banco de dados do Commerce. No entanto, ele não é exportado para [!DNL Adobe Commerce Optimizer] quando o Conector está habilitado. Para implementar os recursos de pesquisa e merchandising fornecidos por essas extensões após habilitar o Conector, configure-os na [[!DNL Adobe Commerce Optimizer] Interface do usuário do administrador](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview#quick-tour).

>[!ENDSHADEBOX]

## Etapas de configuração

Siga estas etapas para habilitar o conector e começar a sincronizar dados do Commerce com a sua instância do Adobe Commerce Optimizer.

1. **[Instale o pacote Commerce Optimizer Connector](#install-the-commerce-connector-package)** usando o Composer para conectar sua instância do Commerce ao [!DNL Adobe Commerce Optimizer].

1. **[Revise e personalize a configuração da exportação de dados](#customize-commerce-data-export-configuration)** do Administrador.

1. **[Obtenha as credenciais de API necessárias para estabelecer a conexão entre o Commerce e o Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)**.

1. **[Habilitar a [!DNL Adobe Commerce Optimizer] integração](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verifique se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working)**.


## Instale o pacote Commerce Optimizer Connector

O Adobe Commerce Optimizer Connector é fornecido como um metappackage do Composer disponível para todos os comerciantes do Commerce com uma licença ativa para [!DNL Adobe Commerce Optimizer].

### Etapas de instalação

1. Adicionar o módulo `adobe-commerce/commerce-data-export-aco-adapter` usando o Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Implante as alterações no ambiente de preparo do Adobe Commerce.

Após a conclusão da implantação, a opção Commerce Optimizer fica disponível no menu Admin do Commerce. Clique em **[!UICONTROL Commerce Optimizer]** para abrir a instância do Commerce Optimizer diretamente do Administrador do Commerce.

>[!NOTE]
>
>Para obter instruções detalhadas sobre a instalação de extensões, consulte os guias a seguir:
>
>[Instalar extensão no Adobe Commerce na Infraestrutura em Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Instalar extensão no Adobe Commerce local](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/extensions)

### Obter detalhes de conexão necessários

Na Adobe Developer Console, crie um projeto de desenvolvedor habilitado para o serviço de Assimilação do [!DNL Adobe Commerce Optimizer] e gere credenciais OAuth de servidor para servidor. Para obter instruções detalhadas, consulte [Obter credenciais IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) no *Guia do Desenvolvedor de Merchandising*.

>[!TIP]
>
>Se você já tiver um projeto de desenvolvedor configurado com a API de assimilação de dados na mesma organização IMS que a instância do Commerce Optimizer, será possível reutilizar as credenciais OAuth de servidor para servidor existentes.

Salve os seguintes valores da página de credenciais:

* **ID da Organização** (`org_id`)
* **ID do Cliente** (`client_id`)
* **Segredo do cliente** (`client_secret`)

### Obter detalhes da instância [!DNL Adobe Commerce Optimizer]

Salve a ID da instância (também chamada de ID do locatário) da instância [!DNL Adobe Commerce Optimizer]. Você pode encontrá-los no URL usado para acessar a instância. Por exemplo, em `https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`, a ID da instância é `TToyu73daQRn66KAYaq8YZ`.

## Personalizar a configuração da exportação de dados do Commerce

Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites e exibições de loja). Você pode personalizar as configurações de exportação para sincronizar dados apenas para escopos específicos com base nas necessidades comerciais. Por exemplo, se você tiver várias exibições de loja, mas quiser exportar apenas os dados de uma delas, poderá desativar o exportador para as outras exibições de loja.

>[!IMPORTANT]
>
>A alteração das configurações de exportação aciona uma reindexação completa, que pode levar um tempo significativo, dependendo do tamanho do catálogo. Planeje essas alterações durante períodos de tráfego baixo para minimizar o impacto no desempenho.

### Exportação de dados por escopo

A tabela a seguir descreve quais dados são exportados em cada nível de escopo:

| Escopo | Dados exportados | Notas |
| ------- | --------------- | ------- |
| Site | Preços e catálogos de preços | Cada conjunto de preços é exportado como um [catálogo de preços](../optimizer/setup/pricebooks.md) usando a convenção de nomenclatura `website::customergroupcode`. Todos os grupos de clientes do site estão incluídos. |
| Exibição de loja | Produtos e atributos do produto | Cada exibição de armazenamento cria uma origem de catálogo separada em [!DNL Adobe Commerce Optimizer]. |

### Ativar e desativar comportamento

| Ação | Resultado |
| -------- | -------- |
| Desabilitar uma exibição de loja | A origem do catálogo permanece em [!DNL Adobe Commerce Optimizer], mas todos os dados são removidos. |
| Desabilitar e depois habilitar novamente uma exibição de loja | A mesma origem de catálogo é preenchida novamente com uma ressincronização de dados completa. |

### Atualizar a configuração de exportação

Após instalar o pacote de conectores, a grade Loja no Admin agora mostra as configurações de exportação do Commerce Optimizer.

![Armazenar grade com configurações de sincronização do Commerce Optimizer](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**Para alterar as configurações de um modo de exibição de site ou loja:**

1. No Administrador do Commerce, navegue até **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**.

1. Selecione o site ou a exibição de loja que deseja configurar.

1. Nas **[!DNL Adobe Commerce Optimizer]configurações do exportador**, use a caixa de seleção para habilitar ou desabilitar a sincronização de dados conforme necessário.

   ![Atualizar configuração de sincronização de dados](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. Salve as alterações.

## Habilitar a integração do [!DNL Adobe Commerce Optimizer]

>[!IMPORTANT]
>
>O processamento da sincronização de dados é iniciado assim que você executa o comando de configuração. Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites e exibições de loja). Dependendo do tamanho do catálogo, o processo de sincronização de dados pode levar de alguns minutos a várias horas.

Usando as credenciais de API e os detalhes de instância coletados nas etapas anteriores, agora é possível configurar a integração entre as instâncias do Commerce e do [!DNL Adobe Commerce Optimizer].

1. No Administrador do Commerce, selecione **[!UICONTROL Adobe Commerce Optimizer]** para exibir a página de configuração com instruções.

   ![[!DNL Adobe Commerce Optimizer] página de configuração](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Na linha de comando, [use SSH](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/secure-connections) para se conectar ao ambiente de preparo do Commerce.

1. Execute o seguinte comando da CLI do Commerce para configurar a integração, substituindo os valores de espaço reservado pelos valores do seu projeto do Commerce Optimizer:

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Verifique a conexão retornando ao Administrador do Commerce e selecionando a opção [!UICONTROL Adobe Commerce Optimizer].

   Quando você clica na opção, ela abre a interface do usuário do [!DNL Adobe Commerce Optimizer] em uma nova guia.

## Verifique se a sincronização de dados está funcionando

Após habilitar a integração, a sincronização de dados é iniciada automaticamente. Dependendo do tamanho do catálogo, a sincronização inicial pode levar de alguns minutos a várias horas.

1. **Verifique o status de sincronização no Administrador do Commerce:**

   Vá para **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.

   ![Página Status da sincronização do feed de dados com relatórios de status do item de feed](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Quando a sincronização está em execução, os dados do feed mostram registros enviados com êxito. Selecione um feed para ver detalhes ou solucionar problemas de sincronização.

1. **Confirmar dados recebidos no Commerce Optimizer:**

   No menu [!DNL Adobe Commerce Optimizer], selecione **[!UICONTROL Data Sync]**.

   ![Sincronização de Dados](./assets/data-sync.png){width="500" zoomable="yes"}

   Verifique se os produtos, preços e atributos esperados aparecem.

>[!TIP]
>
>Se você tiver algum problema com a sincronização de dados, consulte a seção [Solução de problemas](/help/data-export/troubleshooting-logging.md) na documentação de *Exportação de dados SaaS*.

## Próximas etapas

1. **[Configurar [!DNL Adobe Commerce Optimizer] exibições e políticas de catálogo](#configure-adobe-commerce-optimizer-stores)**

   Crie políticas e exibições de catálogo no Guia do [!DNL Adobe Commerce Optimizer]. Observe que os catálogos de preços são criados automaticamente a partir dos grupos de clientes do Adobe Commerce.

1. **[Configurar uma Commerce Storefront no Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   Siga a [documentação de configuração da loja](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=pt-BR) para conectar sua loja à instância do [!DNL Adobe Commerce Optimizer] e começar a fornecer experiências de comércio personalizadas.


