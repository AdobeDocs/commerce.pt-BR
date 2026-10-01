---
title: Monitorar sincronização de exibição de catálogo para catálogos compartilhados B2B
last-update: 2026-09-03
description: Use a página Status de Sincronização da View de Catálogo para monitorar e reconciliar a view de catálogo, a política, a referência de catálogo de preços e os dados-chave de configuração sincronizados com o Adobe Commerce Optimizer.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
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
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: 1fd5e3d84d5249ce96014cae46e045528d2790d0
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 0%
---

# Monitorar sincronização de exibição de catálogo para catálogos compartilhados B2B

Rastreie a sincronização da exibição do catálogo B2B de [!DNL Adobe Commerce] para [!DNL Adobe Commerce Optimizer] usando o painel [!UICONTROL Catalog View Sync Status] no Administrador do Commerce.

[!UICONTROL Catalog View Sync Status] verifica se a exibição de catálogo, a política, a referência de catálogo de preços e as configurações de chave de acesso restrito para cada catálogo compartilhado B2B existem em [!DNL Adobe Commerce Optimizer] e correspondem à sua configuração [!DNL Adobe Commerce]. Para acompanhar a sincronização de produtos, preços e feed de categorias, consulte [Gerenciar sincronização de dados](data-sync-status.md#verify-that-the-data-sync-is-working).

## Acessar a página de status de sincronização {#access-the-sync-status-page}

No Administrador do Commerce, vá para **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Catalog View Sync Status]**.

![Página Status de Sincronização da Exibição de Catálogo para monitorar o status de sincronização das configurações de exibição de catálogo, política, catálogo de preços e chave de acesso no Adobe Commerce Optimizer](assets/catalog-view-sync-status.png){width="600" zoomable="yes"}

A página tem três guias: [!UICONTROL Catalog Views], [!UICONTROL Orphaned in ACO] e [!UICONTROL Deleted].

## Interpretar o status de sincronização dos catálogos compartilhados {#interpret-sync-status}

Na guia [!UICONTROL Catalog View], cada linha representa uma exibição de catálogo compartilhado personalizada projetada de uma combinação de exibição de catálogo e repositório compartilhados. A projeção são os dados de configuração de exibição de catálogo, política, referência de catálogo de preços e chave de acesso restrito que [!DNL Commerce Optimizer Connector] exporta para [!DNL Adobe Commerce Optimizer] para o catálogo compartilhado. Use as informações de status para determinar se os dados entregues à experiência de loja da empresa estão completos e corretos. A tabela a seguir resume os valores de status mais comuns e o que eles significam para o catálogo compartilhado:

| Status | O que significa para o catálogo compartilhado |
| --- | --- |
| **Degradado** | Algo foi alterado diretamente no [!DNL Adobe Commerce Optimizer], por exemplo, a política ou o catálogo de preços vinculado. A empresa pode ver o sortimento ou o preço incorretos até que você resolva o problema. Isso também pode acontecer se a chave de acesso, o nome da exibição ou a fonte forem alterados no Commerce Optimizer. |
| **Falha** | A exibição de catálogo não existe em [!DNL Adobe Commerce Optimizer] ou se o período de carência expira antes da realização da primeira projeção. (Consulte [Definir configurações de sincronização de exibição de catálogo do ACO](#configure-aco-catalog-view-sync-settings)). Se o status de sincronização de um catálogo for `Failed`, a empresa não poderá acessar a experiência de vitrine desse catálogo compartilhado. |
| **Retirando** | Você excluiu o catálogo compartilhado em [!DNL Adobe Commerce]. A visualização do catálogo ainda pode ser acessada até que o período de carência de exclusão expire. O período de carência padrão é de sete dias. Você pode modificar o padrão atualizando as [configurações de sincronização de exibição de catálogo](#configure-aco-catalog-view-sync-settings). |
| **Órfão** | A exibição ou chave do catálogo foi criada diretamente no [!DNL Adobe Commerce Optimizer] Studio, não pelo conector. Consulte [Revisar entradas órfãs e excluídas](#review-orphaned-and-deleted-entries). |

[!UICONTROL Healthy], [!UICONTROL Pending] e [!UICONTROL Deleted] são estados informativos que não exigem ação. Consulte [Valores de status de sincronização](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/catalog-view-sync-status#sync-status-values){target="_blank"} no *Guia de Administração do Commerce* para obter a lista completa.

### Definir configurações de sincronização de exibição de catálogo ACO {#configure-aco-catalog-view-sync-settings}

Do Administrador [!DNL Adobe Commerce] (não do [!DNL Adobe Commerce Optimizer] Studio), vá para **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Catalog View Sync]** para controlar como o conector cronometra exclusões e criações e se ele repara a deriva automaticamente.

![Página de configuração de Sincronização de Exibição do Catálogo ACO mostrando as seções de Exclusão, Criação e Reconciliador de Descompasso](assets/aco-catalog-view-sync-configuration.png){width="600" zoomable="yes"}

- **[!UICONTROL Deletion Grace Period (days)]** — Número de dias que uma exibição de catálogo, política e metadados excluídos do catálogo compartilhado ficam retidos em [!DNL Adobe Commerce Optimizer] antes de serem removidos. O padrão é sete dias. Defina como `0` para remover a projeção imediatamente, sem período de carência.

- **[!UICONTROL Creation Grace Period (days)]** — Número de dias que uma exibição de catálogo recém-registrada pode aguardar sua primeira projeção para [!DNL Adobe Commerce Optimizer] enquanto relatada como [!UICONTROL Pending]. Se o período de carência terminar sem uma projeção, o status se tornará [!UICONTROL Failed]. O padrão é 1.

- **[!UICONTROL Enabled]** (Reconciliador de Descompasso) — Executa o reconciliador de descompasso agendado que compara [!DNL Adobe Commerce Optimizer] com o estado de projeção [!DNL Adobe Commerce] e repara ou relata divergência.

- **[!UICONTROL Automatically Repair Drift]** — Quando definido como **[!UICONTROL Yes]**, a execução agendada converge [!DNL Adobe Commerce Optimizer] de volta para [!DNL Adobe Commerce] para descompasso reparável. Quando definido como **[!UICONTROL No]**, a execução agendada detecta e registra somente o desvio; as entradas órfãs são sempre relatadas, nunca removidas automaticamente. Essa configuração afeta apenas o reconciliador agendado. A ação **[!UICONTROL Reconcile & Repair]** nesta página sempre repara o descompasso. Consulte [Escolher monitoramento ou reparo](#choose-monitoring-or-repair).

Consulte [Configuração de Sincronização de Exibição de Catálogo do ACO](https://experienceleague.adobe.com/en/docs/commerce-admin/configuration-reference/services/aco-catalog-view-sync.md) no *[!DNL Commerce Admin]Guia* para obter detalhes sobre cada configuração.

## Escolher monitoramento ou reparo {#choose-monitoring-or-repair}

[!DNL Adobe Commerce] é sempre a fonte da verdade para a exibição de catálogo, política, catálogo de preços e configurações-chave para catálogos compartilhados B2B. Se você ou outro administrador tiver alterado uma política, catálogo de preços ou definição de chave diretamente no [!DNL Adobe Commerce Optimizer] Studio, a reconciliação relatará as diferenças de configuração como descompasso.

- Selecione **[!UICONTROL Reconcile]** para verificar se há descompasso sem alterar nada, para que você possa examinar as diferenças antes de agir.
- Selecione **[!UICONTROL Reconcile & Repair]** para restaurar a configuração esperada para qualquer desvio reparável.

Para revisar o que foi alterado e o porquê, abra a página de detalhes de uma exibição de catálogo e verifique seu histórico de descompasso.

## Revisar entradas órfãs e excluídas {#review-orphaned-and-deleted-entries}

As guias **[!UICONTROL Orphaned in ACO]** e **[!UICONTROL Deleted]** abrangem dois casos que o conector não pode reparar automaticamente porque não há nenhum catálogo compartilhado [!DNL Adobe Commerce] para reconciliar:

- **[!UICONTROL Orphaned in ACO]** — O conector relata entidades órfãs no status de sincronização e durante a reconciliação de desvio. Ele não os adota ou exclui automaticamente, mesmo se a reconciliação for executada com o reparo ativado.

  Uma entidade é órfã quando existe em [!DNL Adobe Commerce Optimizer], mas o conector não a rastreia ou a associa a uma exibição de catálogo rastreada. Isso pode acontecer quando uma entidade é criada manualmente, por outra integração ou deixada para trás após uma operação de conector interrompida.

  - **Exibições de catálogo** — O conector não rastreia a exibição. Selecione o link de exibição de catálogo para abrir a página Detalhes de Exibição de Catálogo no [!DNL Adobe Commerce Optimizer] Studio. Se a exibição do catálogo não for mais necessária, remova-a.

  - **Chaves de acesso restrito**—Nenhuma exibição de catálogo ao vivo faz referência à chave. Selecione o link de exibição de catálogo para abrir a página Detalhes de Exibição de Catálogo no [!DNL Adobe Commerce Optimizer] Studio. Revise a chave de acesso configurada e remova-a se não for mais necessária.

  - **Políticas** — O conector não rastreia a política e nenhuma exibição de catálogo em tempo real faz referência a ela. Selecione o link da política para abri-la no [!DNL Adobe Commerce Optimizer] Studio.  Revise-a e remova-a se não for mais necessária.

- **[!UICONTROL Deleted]** — Você excluiu um catálogo compartilhado em [!DNL Adobe Commerce] e sua projeção de exibição de catálogo foi removida posteriormente. Essas linhas são mantidas por 90 dias como um registro do que foi removido.

>[!MORELIKETHIS]
>
> - [Monitoramento do Status de Sincronização da Exibição de Catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/catalog-view-sync-status.md){target="_blank"} — Referência de documentação completa para a página Status de Sincronização da Exibição de Catálogo, no *Guia de Administração do Commerce* —>
> - [Gerenciar sincronização de dados](data-sync-status.md) — Verifique a sincronização de feed de produto, preço e categoria
> - [Exibições de catálogo privado](/help/optimizer/setup/private-catalog-view.md) — Saiba o que é uma exibição de catálogo privado gerenciada por conector
> - [Chaves de acesso restrito](/help/optimizer/setup/restricted-access-keys.md) — Saiba como as chaves gerenciadas por conector funcionam
> - [Monitorar alterações no catálogo compartilhado B2B](get-started-b2b-shared-catalogs.md#monitor-b2b-shared-catalog-changes) — Saiba o que o conector automatiza para catálogos compartilhados B2B
