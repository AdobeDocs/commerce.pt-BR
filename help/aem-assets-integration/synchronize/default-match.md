---
title: Correspondência automática padrão
description: Saiba como a regra de correspondência automática padrão permite a sincronização perfeita entre o Adobe Commerce e a integração do AEM Assets, garantindo que os ativos sejam vinculados automaticamente às entidades de merchandising corretas.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
TQID: 'https://experienceleague.adobe.com/z7vpuhsVJnKohiU-bKNrcGnoIQ5WAwcwiccYlvawN0U'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%
---
# Correspondência automática padrão

A integração do AEM Assets para Commerce fornece um mecanismo de correspondência automática padrão (**[!UICONTROL Match by product SKU]**) com base na configuração de metadados **AEM Assets**. Esta regra habilita a sincronização perfeita entre o **Adobe Commerce** e o **AEM Assets**, garantindo que os ativos sejam vinculados automaticamente às entidades de merchandising corretas.

## Configurar o mecanismo de correspondência automática

1. No Administrador do Commerce, navegue até **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Especifique **[!UICONTROL Match by product SKU]** como a regra de correspondência.

   ![Corresponder por regra SKU de produto e nome de propriedade de metadados](../assets/ootb-matching-rule.png){width="700" zoomable="yes"}

1. Em **[!UICONTROL Match by product SKU attribute name]**, insira o [nome da propriedade de metadados](../metadata.md) que armazena SKUs do produto no AEM Assets, não um valor de SKU real.

   >[!NOTE]
   >
   > Se o processo padrão de integração tiver sido seguido, esse valor deverá ser definido como `commerce:skus`.

## Como funciona o mecanismo de correspondência automática

Quando a regra de correspondência do **[!UICONTROL Match by product SKU]** é configurada no Administrador do Commerce, os arquivos de ativos do Commerce são sincronizados automaticamente do AEM Assets para o projeto do Commerce com base nos metadados de ativos configurados para cada arquivo. Você configura os metadados na guia **Commerce** do AEM no ambiente **autor do AEM Assets**:

1. Abra a instância do autor do AEM Assets (o URL é provisionado para o projeto na mesma organização IMS que o Adobe Commerce).

1. Na tela de navegação principal, clique em **Assets** para acessar a interface do Gerenciamento de Ativos Digitais (DAM).

1. No AEM Assets, atualize os metadados da imagem para adicionar a associação do Adobe Commerce definindo o campo `Eligible for Commerce` como `Yes`.

   ![Exemplo de metadados](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. Configure os metadados ([!UICONTROL SKU], [!UICONTROL position] e [!UICONTROL role]) que vinculam o ativo à SKU do produto associado.

   As quatro funções padrão são `image`, `small_image`, `thumbnail` e `swatch_image`. Com a extensão de Integração do AEM Assets versão 1.4.6 e posterior, você também pode inserir uma função de imagem personalizada, como `hero` ou `custom_role_1`. Consulte [Correspondência automática personalizada](custom-match.md) para obter detalhes.

   >[!NOTE]
   >
   > Se um ativo for usado para vários produtos, configure os metadados para cada SKU associada.

1. Na guia `Basic`, defina o valor padrão do campo _[!UICONTROL Review Status]_como `approved`.

   ![Exemplo de metadados](../assets/metadata-review-status.png){width="600" zoomable="yes"}

Após a aprovação do ativo, [verifique a associação do produto, o resultado da sincronização e a exibição da vitrine](../get-started/setup-synchronization.md#verify-the-integration). Se o ativo não aparecer, revise [Status de sincronização](../get-started/sync-status.md). Para o Adobe Commerce Optimizer, use o [Fluxo de trabalho de verificação do otimizador](../get-started/configure-aco.md#match-by-sku-workflow-example); o Status de Sincronização não está disponível.

[!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} Para obter uma solução de problemas de sincronização adicional, examine os [logs de integração](../get-started/logs.md).
