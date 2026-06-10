---
title: Introdução ao  [!DNL Adobe Commerce Optimizer Connector]
description: Saiba como instalar o  [!DNL Adobe Commerce Optimizer Connector], definir configurações de exportação de escopo, habilitar a autenticação IMS e verificar a sincronização do catálogo.
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7a5ca0f5e76be50481447e6a17fc327562f7c3bf
workflow-type: tm+mt
source-wordcount: 1184
ht-degree: 0%

---


# Introdução

Instale e configure o [!DNL Adobe Commerce Optimizer Connector] para sincronizar seus dados de catálogo do [!DNL Adobe Commerce] com o [!DNL Adobe Commerce Optimizer] e, em seguida, monitore o status de sincronização de dados para garantir que sua vitrine eletrônica esteja atualizada.

{{aco-integration-environment-alignment}}

## Requisitos para usar a integração {#requirements-to-use-the-integration}

* [!DNL Adobe Commerce] 2.4.7+

   * PHP 8.2, 8.3 ou 8.4
   * Composer 2.x

* [!DNL Adobe Commerce Optimizer] licença com uma instância de sandbox provisionada.

* [Chaves de autenticação](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) para baixar o metapackage do conector usando o Composer.

* Acesso de administrador a uma [[!DNL Adobe Commerce Optimizer] instância da sandbox](../optimizer/get-started.md).

O usuário [!DNL Adobe Commerce] que está configurando a integração deve ter:

* Acesso de administrador ao Administrador do Commerce.

* [Acesso de linha de comando ao [!DNL Adobe Commerce] servidor de aplicativos](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/project/user-access).

* Acesso de desenvolvedor à [Organização de IMS](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/administration/organizations?) onde o projeto [!DNL Adobe Commerce Optimizer] é provisionado.

>[!BEGINSHADEBOX]

## Pré-requisitos

Se você tiver uma das seguintes extensões instaladas, desinstale-as antes de instalar o [!DNL Adobe Commerce Optimizer Connector]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* Painel de Gerenciamento de Dados (`magento-catalog-sync-admin`)

Os dados associados a essas extensões ainda estão disponíveis no banco de dados do Commerce. No entanto, ele não é exportado para [!DNL Adobe Commerce Optimizer] quando o conector está habilitado. Para implementar os recursos de pesquisa e merchandising fornecidos por essas extensões após habilitar o conector, configure-os na [[!DNL Adobe Commerce Optimizer] Interface do usuário do administrador](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Se essas extensões não forem removidas antes da habilitação do conector, você poderá ver telas de configuração com falha, dados duplicados em [!DNL Adobe Commerce Optimizer] porque os mesmos dados são exportados do conector e das extensões existentes e erros 401 ou 403 nos logs devido a conflitos na maneira como as extensões e o conector são autenticados com os serviços conectados.

>[!ENDSHADEBOX]

## Etapas de configuração

Siga estas etapas para habilitar o [!DNL Commerce Optimizer Connector] e começar a sincronizar dados de [!DNL Adobe Commerce] com sua instância do [!DNL Commerce Optimizer].

1. **[Instale o [!DNL Commerce Optimizer Connector] pacote](#install-the-adobe-commerce-optimizer-connector-package)** usando o Composer para conectar sua instância do [!DNL Adobe Commerce] ao [!DNL Adobe Commerce Optimizer].

1. **[Personalize a configuração da exportação de dados](#customize-the-commerce-scopes-export-configuration)** do Administrador.

1. **[Habilitar a [!DNL Adobe Commerce Optimizer] integração](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verifique se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working)**.

## Instalar o pacote [!DNL Commerce Optimizer Connector] {#install-the-adobe-commerce-optimizer-connector-package}

O [!DNL Commerce Optimizer Connector] é fornecido como um metapackage do Composer disponível a todos os comerciantes do Commerce com uma licença ativa para [!DNL Adobe Commerce Optimizer].

### Etapas de instalação

1. Adicionar o módulo `adobe-commerce/commerce-data-export-aco-adapter` usando o Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Implante as alterações no ambiente de preparo do [!DNL Adobe Commerce].

   Após a conclusão da implantação, a opção [!DNL Commerce Optimizer] fica disponível no menu Admin do Commerce. Selecione **[!UICONTROL Commerce Optimizer]** para abrir a instância do [!DNL Adobe Commerce Optimizer] diretamente do Administrador do Commerce.

>[!NOTE]
>
>Para obter instruções detalhadas sobre a instalação de extensões, consulte os guias a seguir:
>
>[Instalar extensão em [!DNL Adobe Commerce] na Infraestrutura em Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Instalar extensão em [!DNL Adobe Commerce] no local](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/extensions)

## Personalizar a configuração de exportação de escopos do Commerce {#customize-the-commerce-scopes-export-configuration}

Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites, grupos de clientes e visualizações de loja). Você pode personalizar as configurações de exportação para sincronizar dados apenas para escopos específicos com base nas necessidades comerciais. Por exemplo, se você tiver várias exibições de armazenamento que compartilham o mesmo idioma, poderá optar por exportar dados para apenas uma das exibições de armazenamento e usá-los como a [origem do catálogo](../optimizer/setup/catalog-source.md) para várias exibições de catálogo em [!DNL Adobe Commerce Optimizer].

>[!IMPORTANT]
>
>A alteração das configurações de exportação aciona uma reindexação completa, que pode levar um tempo significativo, dependendo do tamanho do catálogo. A Adobe recomenda configurar os escopos do Commerce para sincronização com o [!DNL Adobe Commerce Optimizer] antes de habilitar a integração e iniciar a sincronização de dados inicial.

A tabela a seguir descreve quais dados são exportados em cada nível de escopo:

| Escopo | Dados exportados | Notas |
| ----- | ------------- | ----- |
| Site e grupo de clientes | Preços e catálogos de preços | Cada conjunto de preços é exportado como um [catálogo de preços](../optimizer/setup/pricebooks.md) usando a convenção de nomenclatura `<website>::<SHA1 of customer group ID>`. Todos os grupos de clientes do site estão incluídos. |
| Exibição de loja | Produtos e atributos do produto | Cada exibição de armazenamento cria uma [origem do catálogo](../optimizer/setup/catalog-source.md) separada em [!DNL Adobe Commerce Optimizer]. |

![Armazenar grade com configurações de sincronização do Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

**Para alterar as configurações de um modo de exibição de site ou loja:**

1. No Administrador do Commerce, navegue até **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Selecione o site ou a exibição de loja que deseja configurar.

1. Nas **[!DNL Adobe Commerce Optimizer]configurações do exportador**, use a caixa de seleção para habilitar ou desabilitar a sincronização de dados conforme necessário.

   ![Atualizar configuração de sincronização de dados](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Salve as alterações.

### Ativar e desativar comportamento

| Ação | Resultado |
| -------- | -------- |
| Desabilitar uma exibição de loja | A origem do catálogo permanece em [!DNL Adobe Commerce Optimizer], mas todos os dados são removidos. |
| Desabilitar e depois habilitar novamente uma exibição de loja | A mesma origem de catálogo é preenchida novamente com uma ressincronização de dados completa. |

## Habilitar a integração do [!DNL Adobe Commerce Optimizer]

Você habilita a integração e inicia a sincronização de dados executando o comando da CLI do `aco:config:init`. Esse comando conclui as seguintes etapas:

1. Obtém um token de acesso IMS usando credenciais fornecidas como argumentos de linha de comando.
1. Chama o serviço Commerce Cloud Manager (CCM) em `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` para validar o locatário e extrair a URL de assimilação e a URL de Estúdio [!DNL Adobe Commerce Optimizer].
1. Salva toda a configuração (segredo do cliente criptografado) em `core_config_data`.
1. Agenda a sincronização completa inicial, invalidando todos os [!DNL Commerce Optimizer] indexadores de feed.

>[!IMPORTANT]
>
>O processamento da sincronização de dados é iniciado em segundo plano assim que você conclui a configuração. Dependendo do tamanho do catálogo, o processo de sincronização de dados pode levar de alguns minutos a várias horas.

### Obter detalhes de conexão necessários

No [Adobe Developer Console](https://developer.adobe.com/console), crie um novo projeto habilitado para o serviço de Assimilação do [!DNL Adobe Commerce Optimizer] e gere credenciais OAuth de servidor para servidor. Para obter instruções detalhadas, consulte [Obter credenciais IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) no *Guia do Desenvolvedor de Merchandising*.

Salve os seguintes valores da página de credenciais:

* **ID da Organização** (`org_id`)
* **ID do Cliente** (`client_id`)
* **Segredo do Cliente** (`client_secret`)

![Obter detalhes da credencial da página de projeto do Adobe Developer Console](./assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### Obter detalhes da instância [!DNL Adobe Commerce Optimizer]

Obtenha a _ID do locatário_ do campo _[!DNL Instance Id]_&#x200B;na [[!DNL Instance details] página](../optimizer/get-started.md#manage-instances) da instância [!DNL Adobe Commerce Optimizer] ou da URL usada para acessar a instância. Por exemplo, em `https://experience.adobe.com/#/@<your organization>/in:<tenant ID>/commerce-optimizer-studio/home`.

1. No Administrador do Commerce, selecione **[!UICONTROL Adobe Commerce Optimizer]** para exibir a página de configuração com instruções.

   ![[!DNL Adobe Commerce Optimizer] página de configuração](./assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Na linha de comando, [use SSH](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/secure-connections) para se conectar ao ambiente de preparo [!DNL Adobe Commerce].

1. Execute o seguinte comando da CLI do [!DNL Adobe Commerce] para configurar a integração, substituindo os valores de espaço reservado pelos valores do seu projeto [!DNL Commerce Optimizer]:

   ```terminal
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Verifique a conexão retornando ao Administrador do Commerce e selecionando a opção [!UICONTROL Adobe Commerce Optimizer].

   Ao selecionar a opção, ela abrirá a interface do usuário do [!DNL Adobe Commerce Optimizer] em uma nova guia.

## Verifique se a sincronização de dados está funcionando

Você pode monitorar e verificar se a sincronização está funcionando a partir da página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) disponível no Administrador.

1. **Verifique o status de sincronização no Administrador do Commerce:**

   Vá para **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Página Status da sincronização do feed de dados com relatórios de status do item de feed](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Quando a sincronização está em execução, os dados do feed mostram registros enviados com êxito. Selecione um feed para ver detalhes ou solucionar problemas de sincronização.

1. **Confirmar dados recebidos em [!DNL Commerce Optimizer]:**

   No menu [!DNL Adobe Commerce Optimizer], selecione **[!UICONTROL Data Sync]**.

   ![Página de Sincronização de Dados no Adobe Commerce Optimizer mostrando os dados de catálogo sincronizados](./assets/data-sync.png){width="500" zoomable="yes"}

   Verifique se os produtos, preços e atributos esperados aparecem.

>[!TIP]
>
>Se você tiver algum problema com a sincronização de dados, consulte o guia de [Solução de problemas](troubleshooting.md).

## Próximas etapas

1. **Configurar [!DNL Adobe Commerce Optimizer] exibições e políticas de catálogo**

   Crie políticas e exibições de catálogo na interface do usuário do [!DNL Adobe Commerce Optimizer]. Observe que os catálogos de preços são criados automaticamente de [!DNL Adobe Commerce] grupos de clientes. Para obter instruções, consulte a documentação das [Exibições de catálogo](../optimizer/setup/catalog-view.md) e [Políticas](../optimizer/setup/policies.md) no *[!DNL Adobe Commerce Optimizer]Guia do Usuário*.

1. **Configurar uma Commerce Storefront em[!DNL Edge Delivery Services]**

   Siga a [documentação de configuração da loja](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=pt-BR){target="_blank"} para conectar sua loja à instância do [!DNL Adobe Commerce Optimizer] e começar a fornecer experiências de comércio personalizadas.
