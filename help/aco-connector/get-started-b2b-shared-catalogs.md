---
title: Configurar o conector para o Commerce B2B
description: Saiba como instalar o conector B2B, selecionar escopos do Commerce, sincronizar dados de catálogo compartilhados, verificar exibições de catálogo e monitorar a integridade da projeção.
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
last-update: 2026-10-01
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
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
source-git-commit: c76e776250d9f996daf61d3cf62e2070803e998c
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%
---

# Configurar o conector para o Commerce B2B

Os comerciantes que usam [!DNL Adobe Commerce] catálogos compartilhados B2B podem usar [!DNL Adobe Commerce Optimizer Connector for B2B] para sincronizar dados e configurações personalizados de catálogo compartilhado com [!DNL Adobe Commerce Optimizer].

{{aco-integration-environment-alignment}}

## Requisitos para usar a integração {#requirements-to-use-the-integration}

* Adobe Commerce 2.4.8+ com [Commerce B2B versão 1.5.3+](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/b2b/install) instalado e habilitado.

* [!DNL Commerce Optimizer] licença com instância de sandbox provisionada.

* [Chaves de autenticação](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) para baixar o metapacote do conector usando o Composer.

* Acesso de administrador a uma [[!DNL Commerce Optimizer] instância da sandbox](../optimizer/get-started.md).

O usuário [!DNL Adobe Commerce] que está configurando a integração deve ter:

* Acesso de administrador ao Administrador do Commerce.

* [Acesso de linha de comando ao [!DNL Adobe Commerce] servidor de aplicativos](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/project/user-access).

* Acesso de desenvolvedor à [Organização de IMS](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/administration/organizations?) onde o projeto [!DNL Commerce Optimizer] é provisionado.

### Requisitos do aplicativo

* cron e indexadores do Commerce funcionando normalmente.
* Os sites e as exibições de loja necessários identificados para exportação.
* Catálogos compartilhados, atribuições da empresa, sortimento e preços B2B configurados ou prontos para configuração no Adobe Commerce.

>[!BEGINSHADEBOX]

## Remover extensões conflitantes {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Etapas de configuração {#configuration-steps}

Para habilitar o [!DNL Adobe Commerce Optimizer Connector for B2B] e começar a sincronizar a configuração personalizada do catálogo compartilhado de [!DNL Adobe Commerce] para sua instância do [!DNL Commerce Optimizer], siga estas etapas.

1. **[Instale o [!DNL Adobe Commerce Optimizer Connector for B2B] pacote](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)** usando o Composer para conectar sua instância do [!DNL Adobe Commerce] ao [!DNL Commerce Optimizer].

1. **[Personalize a configuração de exportação de escopos do Commerce](#data-export-and-scope-mapping)** do Administrador.

1. **[Habilitar a [!DNL Commerce Optimizer] integração](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Verifique se a sincronização de dados está funcionando](#verify-that-the-data-sync-is-working)**.

## Instalar o pacote [!DNL Adobe Commerce Optimizer Connector for B2B] {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

O [!DNL Adobe Commerce Optimizer Connector for B2B] é entregue como um meta pacote do Composer disponível a todos os comerciantes do Commerce com uma licença ativa para [!DNL Commerce Optimizer].

### Etapas de instalação

1. Adicionar o módulo `adobe-commerce/commerce-data-export-aco-adapter-b2b` usando o Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. Implante as alterações no ambiente de preparo do [!DNL Adobe Commerce].

   Após a conclusão da implantação, a opção [!DNL Commerce Optimizer] fica disponível no menu Admin do Commerce. Selecione **[!UICONTROL Commerce Optimizer]** para abrir a instância do [!DNL Commerce Optimizer] diretamente do Administrador do Commerce.

{{install-extension-links}}

### Exportação de dados e mapeamento de escopo

Selecione os sites e as exibições de armazenamento a serem sincronizados e verifique os feeds iniciais. Para B2B, o conector usa os escopos habilitados quando projeta dados de catálogo compartilhados para [!DNL Commerce Optimizer].

* **Exibição da loja** → fonte do catálogo com conteúdo de produto localizado
* **Site e grupo de clientes** → catálogo de preços para site e grupo de clientes
* **Catálogo compartilhado** → exibição de catálogo privado protegido e política imposta

O catálogo compartilhado define a classificação do produto e cada exibição de loja habilitada fornece a origem do catálogo localizada. O site e o grupo de clientes determinam o catálogo de preços aplicável. O conector projeta cada catálogo compartilhado personalizado para cada exibição de armazenamento ativada, de modo que você não precisa de uma configuração de escopo separada para a projeção B2B.

Um catálogo compartilhado personalizado pode gerar várias exibições de catálogo privado protegidas, uma para cada exibição de armazenamento ativada. O catálogo público compartilhado padrão não é projetado como uma visualização de catálogo privado B2B. Para obter o mapeamento de objeto detalhado e o fluxo de autorização de tempo de execução, consulte [Projeção de catálogo compartilhado B2B](b2b-shared-catalog-projection.md).

>[!IMPORTANT]
>
>Alterar as configurações de exportação aciona uma reindexação completa, que pode levar um tempo significativo, dependendo do tamanho do catálogo. Configure os escopos do Commerce antes de habilitar a integração e iniciar a sincronização de dados inicial.

### Para alterar as configurações de exportação do escopo

1. No Administrador do Commerce, vá para **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Selecione o site ou a exibição de loja que deseja configurar.

1. Nas **[!DNL Commerce Optimizer]configurações do exportador**, use a caixa de seleção para habilitar ou desabilitar a sincronização de dados conforme necessário.

   ![Atualizar configuração de sincronização de dados](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. Salve as alterações.

### Ativar e desativar comportamento

| Ação | Resultado |
| -------- | -------- |
| Desabilitar uma exibição de loja | **A desabilitação da sincronização remove os dados do catálogo da loja B2B.** A origem do catálogo permanece em [!DNL Adobe Commerce Optimizer], mas todos os dados sincronizados são removidos na próxima execução de cron. |
| Desabilitar e depois habilitar novamente uma exibição de loja | A mesma origem de catálogo é preenchida novamente com uma ressincronização de dados completa. |

### Monitorar alterações no catálogo compartilhado B2B

O conector observa as alterações nos catálogos compartilhados e atribuições da empresa. Ao remover um catálogo compartilhado no Commerce Admin, o conector remove o acesso à visualização do catálogo privado após um período de carência configurável.

>[!NOTE]
>
>O período de carência de exclusão é padronizado como sete dias. Você pode alterá-lo atualizando a configuração de configurações de sincronização da exibição do catálogo. Consulte [configuração de status de sincronização de exibição de catálogo](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings).

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

1. **Monitorar a projeção da exibição do catálogo B2B**

Após a sincronização inicial do feed, use o [Status de Sincronização de Exibição de Catálogo](catalog-view-sync-status.md) para verificar exibições de catálogo privado projetadas, políticas, referências de catálogo de preços e configuração de chave de acesso restrito. Para o modelo de projeção e o fluxo de autorização de tempo de execução, consulte [Projeção do catálogo compartilhado B2B](b2b-shared-catalog-projection.md).

1. **Configurar uma Commerce Storefront em[!DNL Edge Delivery Services]**

   Para conectar sua loja à instância do [!DNL Commerce Optimizer] e começar a fornecer experiências de comércio personalizadas, siga a [documentação de configuração da loja](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
