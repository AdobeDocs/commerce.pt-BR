---
title: Introdução ao [!DNL Adobe Commerce Optimizer Connector]
description: Saiba como instalar o [!DNL Adobe Commerce Optimizer Connector], definir configurações de exportação de escopo, habilitar a autenticação IMS e verificar a sincronização do catálogo.
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
last-update: 2026-09-11
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 0%
---

# Introdução

Instale e configure o [!DNL Adobe Commerce Optimizer Connector] para sincronizar seus dados de catálogo do [!DNL Adobe Commerce] com o [!DNL Adobe Commerce Optimizer] e, em seguida, monitore o status de sincronização de dados para garantir que sua vitrine eletrônica esteja atualizada.

{{aco-integration-environment-alignment}}

>[!NOTE]
>
>Este tópico aborda o [!DNL Adobe Commerce Optimizer Connector]. Se você usa [!DNL Adobe Commerce] catálogos compartilhados B2B, siga as [Instruções de introdução [!DNL Adobe Commerce Optimizer Connector for B2B]](get-started-b2b-shared-catalogs.md). O conector B2B estende a sincronização de dados do catálogo base para oferecer suporte à sincronização de catálogos compartilhados personalizados.

## Requisitos para usar a integração {#requirements-to-use-the-integration}

* [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.7+. Para obter requisitos detalhados, consulte [Requisitos do sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/system-requirements).

* [!DNL Commerce Optimizer] licença com uma instância de sandbox provisionada.

* [Chaves de autenticação](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) para baixar o metapackage do conector usando o Composer.

* Acesso de administrador a uma [[!DNL Commerce Optimizer] instância da sandbox](../optimizer/get-started.md).

O usuário [!DNL Adobe Commerce] que está configurando a integração deve ter:

* Acesso de administrador ao Administrador do Commerce.

* [Acesso de linha de comando ao [!DNL Adobe Commerce] servidor de aplicativos](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Acesso de desenvolvedor à [Organização de IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) onde o projeto [!DNL Commerce Optimizer] é provisionado.

>[!BEGINSHADEBOX]

## Remover extensões conflitantes

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Etapas de configuração {#configuration-steps}

Para habilitar o [!DNL Adobe Commerce Optimizer Connector] e começar a sincronizar dados do [!DNL Adobe Commerce] com sua instância do [!DNL Commerce Optimizer], siga estas etapas.

1. **[Instale o [!DNL Adobe Commerce Optimizer Connector] pacote](#install-the-adobe-commerce-optimizer-connector-package)** usando o Composer para conectar sua instância do [!DNL Adobe Commerce] ao [!DNL Commerce Optimizer].

1. **[Personalize a configuração de exportação de escopos do Commerce](#customize-the-commerce-scopes-export-configuration)** do Administrador.

1. **[Habilitar a [!DNL Commerce Optimizer] integração](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verifique se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working)**.

## Instalar o pacote [!DNL Adobe Commerce Optimizer Connector] {#install-the-adobe-commerce-optimizer-connector-package}

O [!DNL Adobe Commerce Optimizer Connector] é fornecido como um metapackage do Composer disponível a todos os comerciantes do Commerce com uma licença ativa para [!DNL Commerce Optimizer].

### Etapas de instalação

1. Adicionar o módulo `adobe-commerce/commerce-data-export-aco-adapter` usando o Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Implante as alterações no ambiente de preparo do [!DNL Adobe Commerce].

   Após a conclusão da implantação, a opção [!DNL Commerce Optimizer] fica disponível no menu Admin do Commerce. Selecione **[!UICONTROL Commerce Optimizer]** para abrir a instância do [!DNL Commerce Optimizer] diretamente do Administrador do Commerce.

{{install-extension-links}}

## Personalizar a configuração de exportação de escopos do Commerce {#customize-the-commerce-scopes-export-configuration}

Por padrão, a sincronização de dados do catálogo é habilitada para todos os escopos do Commerce (sites, grupos de clientes e exibições de loja). Você pode personalizar as configurações de exportação para sincronizar dados apenas para escopos específicos com base nas necessidades comerciais. Por exemplo, se várias exibições de armazenamento compartilharem o mesmo idioma, você poderá exportar dados para uma exibição de armazenamento e usá-los como a [origem do catálogo](../optimizer/setup/catalog-sources.md) para várias exibições de catálogo em [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>A alteração das configurações de exportação aciona uma reindexação completa, que pode levar um tempo significativo, dependendo do tamanho do catálogo. A Adobe recomenda configurar os escopos do Commerce para sincronização com o [!DNL Commerce Optimizer] antes de habilitar a integração e iniciar a sincronização de dados inicial.

A tabela a seguir descreve quais dados são exportados em cada nível de escopo:

| Escopo | Dados exportados | Notas |
| ----- | ------------- | ----- |
| Site e grupo de clientes | Preços e catálogos de preços | Cada conjunto de preços é exportado como um [catálogo de preços](../optimizer/setup/pricebooks.md) usando a convenção de nomenclatura `&lt;website&gt;::&lt;SHA1 of customer group ID&gt;`. Todos os grupos de clientes do site estão incluídos. |
| Exibição de loja | Produtos e atributos do produto | Cada exibição de armazenamento cria uma [origem do catálogo](../optimizer/setup/catalog-sources.md) separada em [!DNL Commerce Optimizer]. |

![Armazenar grade com configurações de sincronização do Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

### Para alterar as configurações de exportação do escopo

1. No Administrador do Commerce, vá para **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Selecione o site ou a exibição de loja que deseja configurar.

1. Nas **[!DNL Commerce Optimizer]configurações do exportador**, use a caixa de seleção para habilitar ou desabilitar a sincronização de dados conforme necessário.

   ![Atualizar configuração de sincronização de dados](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Salve as alterações.

### Ativar e desativar comportamento

| Ação | Resultado |
| -------- | -------- |
| Desabilitar uma exibição de loja | **Desabilitar a sincronização remove os dados do catálogo da loja.** A origem do catálogo permanece em [!DNL Commerce Optimizer], mas todos os dados sincronizados são removidos na próxima execução de cron. |
| Desabilitar e depois habilitar novamente uma exibição de loja | A mesma origem de catálogo é preenchida novamente com uma ressincronização de dados completa. |

## Habilitar a integração do [!DNL Commerce Optimizer] {#enable-the-adobe-commerce-optimizer-integration}

Você habilita a integração e inicia a sincronização de dados executando o comando da CLI do `aco:config:init`. Esse comando conclui as seguintes etapas:

1. Obtém um token de acesso IMS usando credenciais fornecidas como argumentos de linha de comando.
1. Chama o serviço Commerce Cloud Manager (CCM) em `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` para validar o locatário e extrair a URL de assimilação e a URL de Estúdio [!DNL Commerce Optimizer].
1. Salva toda a configuração (segredo do cliente criptografado) em `core_config_data`.
1. Agenda a sincronização completa inicial, invalidando todos os [!DNL Commerce Optimizer] indexadores de feed.


{{aco-data-sync-processing-note}}

## Obter detalhes de conexão necessários

{{$include /help/_includes/aco-connector/connection-details.md}}

### Obter detalhes da instância [!DNL Commerce Optimizer]

{{$include /help/_includes/aco-connector/configure-connection.md}}

## Verifique se a sincronização de dados está funcionando {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Próximas etapas

1. **Configurar [!DNL Commerce Optimizer] exibições e políticas de catálogo**

   Crie políticas e exibições de catálogo na interface do usuário do [!DNL Commerce Optimizer]. Observe que os catálogos de preços são criados automaticamente de [!DNL Adobe Commerce] grupos de clientes. Para obter instruções, consulte a documentação das [Exibições de catálogo](../optimizer/setup/catalog-view.md) e [Políticas](../optimizer/setup/policies.md) no *[!DNL Commerce Optimizer]Guia do Usuário*. Para restringir o acesso a uma exibição de catálogo, consulte [Exibições de catálogo privado](../optimizer/setup/private-catalog-view.md).

1. **Configurar uma Commerce Storefront em[!DNL Edge Delivery Services]**

   Para conectar sua loja à instância do [!DNL Commerce Optimizer] e começar a fornecer experiências de comércio personalizadas, siga a [documentação de configuração da loja](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
