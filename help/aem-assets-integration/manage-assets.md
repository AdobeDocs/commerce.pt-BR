---
title: Gerenciar ativos
description: Use a integração do AEM Assets para Commerce a fim de gerenciar ativos de mídia para sua loja.
feature: CMS, Media
exl-id: 40ca36e0-d617-4814-852d-bc60ff53b2b3
source-git-commit: 394a958250fcc9b0d9f672c1daf46a6d7c16a71d
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Gerenciar ativos de mídia do Commerce

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

Você poderá gerenciar os seguintes tipos de mídia depois que a integração do AEM Assets para Commerce for ativada:

* Imagens do produto
* Imagens de conteúdo
* Vídeos de produtos
* Imagens de categoria

## Imagens do produto

Quando a integração é ativada, o gerenciamento de imagens é centralizado no sistema de gerenciamento de ativos digitais (DAM). Em seguida, o Adobe Commerce funciona como um canal principal de envolvimento, garantindo que somente imagens aprovadas e de alta qualidade sejam usadas nas vitrines. Essa configuração melhora a consistência da marca, minimiza o esforço manual e simplifica as atualizações de conteúdo — eliminando a necessidade de os comerciantes fazerem upload ou gerenciarem imagens manualmente no Adobe Commerce.

### Visualizar imagens do produto no Adobe Commerce

As imagens do produto são extraídas automaticamente do AEM Assets com base nas regras de correspondência pré-configuradas:

1. Na barra lateral _Admin_, navegue até **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Selecione um produto.

1. Abra a seção **Imagens e Vídeos**.

   ![Imagem do produto](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Uma mensagem indica que a integração está habilitada, tornando-a uma seção **somente leitura**, pois o gerenciamento de imagens é centralizado no DAM.

### Gerenciar imagens do produto no AEM Assets

Para gerenciar imagens relacionadas ao produto, todas as alterações devem ser feitas diretamente no **AEM Assets**. Esse processo é totalmente automatizado, garantindo que todas as alterações sejam sincronizadas com o Adobe Commerce sem a necessidade de intervenção manual.

### SLAs de sincronização

Verifique o [SLA de Sincronização](get-started/setup-synchronization.md#synchronization-sla)para obter mais informações sobre este tópico.

## Imagens de conteúdo

A Adobe Commerce fornece o Page Builder como um **sistema de gerenciamento de conteúdo (CMS)** para comerciantes que não estão usando o conjunto de ferramentas do Adobe Experience Manager (AEM). Para aprimorar a criação de conteúdo, nossa integração utiliza o [Seletor de ativos do AEM](synchronize/asset-selector-integration.md), permitindo que os profissionais de marketing acessem e incorporem imagens diretamente do **DAM**. Isso garante que somente imagens aprovadas e de alta qualidade sejam usadas na criação de conteúdo, eliminando a necessidade de armazenamento redundante no Adobe Commerce.

### Utilização do Seletor de ativos AEM no Page Builder

[!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} Para usar o **Seletor de ativos do AEM** para imagens incorporadas:

1. Navegue até qualquer seção no **Administrador do Adobe Commerce** que ofereça suporte ao `content enrichment` usando o **Page Builder**.

1. Abra o [Page Builder](https://developer.adobe.com/commerce/frontend-core/page-builder/){target=_blank}.

   Um novo Tipo de Mídia chamado **Ativo do AEM** estará disponível.

1. Arraste e solte o tipo de mídia AEM Asset em um bloco de conteúdo.

1. Quando solicitado, forneça as credenciais para acessar o DAM.

1. Selecione uma imagem do DAM e insira-a diretamente no conteúdo.

A associação com a imagem selecionada será armazenada no Adobe Commerce como uma URL direta apontando para **Dynamic Media**, garantindo que:

* Os arquivos de imagem não precisam ser armazenados no Adobe Commerce.

* Os comerciantes trabalham exclusivamente com ativos aprovados do DAM.

* O conteúdo permanece consistente e atualizado em todos os pontos de contato do cliente.

>[!TIP]
>
> [DA.live (Criação de Documentos)](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/#dalive-document-authoring){target=_blank} também fornece um seletor de Ativos para enriquecer dados.

## Vídeos de produtos

O Adobe Commerce serve como um canal principal de envolvimento para ativos digitais. Depois que a integração do AEM Assets é habilitada, o gerenciamento de vídeo é centralizado no **DAM**, garantindo consistência, conformidade e entrega otimizada nas vitrines de comércio.

### Gerenciar vídeos de produtos

1. Na barra lateral _Admin_, navegue até **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Selecione um produto.

1. Abra a seção **Imagens e Vídeos**.

   ![Imagem do produto](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Uma mensagem indica que a integração está habilitada, tornando esta seção **somente leitura**, pois os vídeos são controlados no AEM Assets.

### Associar vídeos no AEM Assets

1. No AEM Assets, navegue até o vídeo que deseja associar a um produto.

1. Vincule o vídeo a um ou mais produtos no Adobe Commerce.

1. A integração sincroniza automaticamente a associação, exibindo o reprodutor de vídeo do Dynamic Media diretamente na loja. Isso elimina a necessidade de os comerciantes gerenciarem as configurações de reprodução de vídeo.

### Somente suporte a API-First video

Atualmente, a integração é compatível com vídeos por meio da API, permitindo que os parceiros recuperem vídeos de forma programática.

>[!WARNING]
>
> Por padrão, os vídeos ainda não estão integrados às soluções da vitrine da Adobe Commerce.

Essa integração garante que os comerciantes possam gerenciar facilmente os vídeos de produtos de maneira escalável e otimizada, aproveitando o AEM Assets e o Dynamic Media para uma entrega perfeita.

### SLAs de sincronização

Verifique o [SLA de Sincronização](get-started/setup-synchronization.md#synchronization-sla)para obter mais informações sobre este tópico.

## Imagens de categoria

O Adobe Commerce permite que os comerciantes associem imagens a categorias de produtos, ajudando a criar uma loja visualmente envolvente. A integração do AEM Assets aproveita o Seletor de ativos da AEM, permitindo que os profissionais de marketing selecionem ativos diretamente do **Sistema de gerenciamento de ativos digitais (DAM)**. Isso garante que somente imagens aprovadas sejam usadas e elimina a necessidade de armazená-las no Adobe Commerce, mantendo a consistência e a eficiência em todos os canais de envolvimento.

### Usar o Seletor de ativos AEM para imagens de categoria

Após configurar o [Seletor de ativos do AEM](synchronize/asset-selector-integration.md), você pode usá-lo para adicionar ativos ao conteúdo de categorias do catálogo.

1. Na barra lateral _Admin_, navegue até **[!UICONTROL Catalog]** > **[!UICONTROL Categories]**.

1. Selecione uma categoria que deseja atualizar.

1. Expanda o ![Seletor de expansão](../assets/icon-display-expand.png) na seção **[!UICONTROL Content]**.

1. Na seção **[!UICONTROL Content]**, localize o *campo de imagem* associado à categoria.

   ![Conteúdo da categoria](assets/category-asset.png){width="600" zoomable="yes"}

1. Clique em **[!UICONTROL Select from Assets]** para alterar a imagem da categoria.

   ![Conteúdo da categoria](assets/asset-view.png){width="600" zoomable="yes"}

1. Escolha uma imagem no Seletor de ativos do AEM.

   ![Conteúdo da categoria](assets/select-image.png){width="600" zoomable="yes"}

1. Clique em **[!UICONTROL Save]** e continue.

   Para obter mais informações sobre como criar uma categoria, consulte [Concluir o conteúdo da categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content) no **Guia de Gerenciamento do Catálogo do Commerce**.

## Atualizar um ativo

Depois de atualizar e aprovar um ativo no AEM Assets, as atualizações são automaticamente enviadas para a Adobe Commerce usando o recurso de correspondência automatizada. Esse processo é acionado mediante aprovação de ativos. Para garantir que todas as alterações finais e atualizações de metadados sejam incluídas, reprocesse o ativo antes de aprová-lo.

Para obter detalhes, consulte a seguinte documentação do AEM Assets.

* [Reprocessando ativos digitais](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

* [Aprovar um ativo](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)
