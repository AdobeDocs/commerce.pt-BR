---
title: Configurar a integração
description: Saiba como conectar seu projeto do Adobe Commerce e projetos do Experience Manager Assets para habilitar a sincronização de ativos entre esses dois sistemas.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# Configurar a integração

Configure a integração conectando o Commerce à instância do AEM Assets e selecionando a estratégia correspondente para a sincronização de ativos.

Depois de identificar o projeto do AEM Assets, selecione a regra de correspondência para sincronizar ativos entre o Adobe Commerce e o AEM Assets.

* **[!UICONTROL Match by product SKU]** — Regra padrão que corresponde ao SKU nos metadados do ativo com o [SKU do produto Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/implementation-playbook/glossary#sku) para garantir que os ativos estejam associados aos produtos corretos.

* **[!UICONTROL Custom match]** — Regra de correspondência para cenários mais complexos ou requisitos de negócios específicos que exigem lógica de correspondência personalizada. A implementação da correspondência personalizada requer o desenvolvimento de código personalizado no Adobe Developer App Builder para definir como os ativos são correspondidos aos produtos. Mais detalhes em breve...

Para a configuração inicial, use a regra padrão *Corresponder por SKU de produto*.

## Pré-requisitos

* [Instalar pacote do AEM Assets](configure-aem.md)

* [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} [Instale pacotes do Adobe Commerce](configure-commerce.md) para adicionar a extensão e gerar as credenciais e conexões necessárias para usar a extensão.

* Siga as etapas descritas no tópico [habilitar API aberta do Dynamic Media](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis). Inclua as seguintes informações para a equipe de suporte:

   * **[!UICONTROL AEM Program ID]**
   * **[!UICONTROL Adobe Commerce URL]**
   * **[!UICONTROL AEM Environment ID]**,
   * **[!UICONTROL IMS Org ID]** para o ambiente de criação do AEM Assets que você deseja conectar ao Commerce.

## Configurar a conexão

1. Obtenha o [Ambiente de Criação do AEM Assets](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/sites/authoring/quick-start) e a ID do ambiente.

   1. Abra o AEM Cloud Manager e selecione **[!UICONTROL Assets]**.

   1. Copie e salve as IDs de projeto e ambiente da URL:<br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

1. No Administrador do Commerce, abra a configuração da Integração do AEM Assets.

   1. Vá para **[!UICONTROL Store]** > Configuração > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

      ![A Integração do AEM Assets habilita a integração](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. Entre no ambiente AEM Assets **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]**.

   Edite os valores de configuração removendo a seleção de *[!UICONTROL Use system value]*.

1. Insira o **[!UICONTROL Asset Selector IMS Client ID]**.

   Para obter detalhes sobre o Seletor de ativos, consulte [Selecionar ativos manualmente](../synchronize/asset-selector-integration.md)

1. [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} Selecione o [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) para solicitações de autenticação entre o Commerce e o serviço de correspondência de ativos.

1. Defina o **[!UICONTROL Commerce integration]** como `assets-integration` para selecionar a Integração do Commerce a ser usada com o AEM Assets.

1. Defina **[!UICONTROL Synchronization enabled]** como `Yes` para permitir que o Commerce aceite atualizações de entrada do AEM Assets.

   Depois de habilitar a integração, opções de configuração adicionais estão disponíveis para especificar os critérios de correspondência de ativos.

1. Selecione uma das regras de correspondência de ativos para sincronização de ativos na lista suspensa **[!UICONTROL Asset matching rule]**.

   * Selecione **[!UICONTROL Match by SKU]** para [correspondência automática padrão](../synchronize/default-match.md),
   * Selecione **[!UICONTROL Custom match]** para [correspondência automática personalizada](../synchronize/custom-match.md) (requer [Adobe Developer App Builder](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder).)

1. Adicione o [nome do campo de metadados do AEM Assets](configure-aem.md#configure-metadata) definido para SKUs de produtos Commerce no campo **[!UICONTROL Match by product SKU attribute name]**, `commerce:skus` por padrão.

1. Selecione **[!UICONTROL Save Config]** para aplicar atualizações e iniciar a sincronização de ativos.

   A atualização de configuração aciona o processo de sincronização inicial, permitindo que o Commerce aceite atualizações recebidas do AEM Assets. O tempo necessário para a sincronização depende do volume de ativos e de configurações específicas. A integração utiliza processos automatizados para minimizar o tempo necessário para a sincronização.

### SLA de sincronização

A integração garante os seguintes níveis de desempenho de sincronização:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

Isso garante que as páginas de produtos sempre exibam as imagens mais atualizadas, mantendo o conteúdo da vitrine eletrônica preciso e visualmente atraente.

### Configurar o proprietário da visualização

A configuração **Proprietário da visualização** determina qual sistema fornece imagens de produto na integração:

* Adobe Commerce - Usa imagens hospedadas no Commerce.
* AEM Assets - Usa imagens sincronizadas do AEM.

O Administrador exibe as imagens disponíveis para esse proprietário, enquanto o restante das imagens é esmaecido e exibido com um rótulo **oculto**.

Consulte o tópico [definir detalhes da imagem](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} para obter detalhes sobre o comportamento de exibição da imagem.

>[!TIP]
>
> Durante a migração do Commerce para o AEM Assets, defina o **Proprietário da visualização** como Commerce para evitar links de imagens quebradas. Depois que todos os produtos forem sincronizados com o AEM Assets, alterne para o proprietário do AEM Assets para concluir a transição. Isso garante a disponibilidade contínua da imagem em todo o processo.

1. Navegue até **[!UICONTROL Store]** > Configuração > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![Recurso do proprietário da visualização de Integração do AEM Assets](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. Selecione a origem **Proprietário da Visualização** para exibir as imagens.

1. Clique em **[!UICONTROL Save Config]** para aplicar atualizações e iniciar a sincronização de ativos.

### Opcional. Configurar o URL do domínio personalizado

Se o projeto AEM Assets as a Cloud Service tiver sido configurado com um [Nome de domínio personalizado](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, adicione o nome de domínio à configuração de armazenamento do Commerce para que a integração do AEM Assets para Commerce possa usá-lo.

1. Navegue até **[!UICONTROL Store]** > Configuração > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![A Integração do AEM Assets habilita a integração](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. Adicione a **URL de Domínio Personalizado** ao campo **[!UICONTROL Asset Custom Domain]**.

1. Clique em **[!UICONTROL Save Config]** para aplicar atualizações e iniciar a sincronização de ativos.

## Próxima etapa

[Gerenciar ativos do Commerce](../manage-assets.md)
