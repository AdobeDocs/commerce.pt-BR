---
title: Gerenciar chaves de acesso restrito para catálogos compartilhados B2B
description: Saiba como gerenciar as chaves de acesso restrito que o Adobe Commerce Optimizer Connector usa para proteger projeções de catálogo compartilhado B2B.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
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
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%
---

# Gerenciar chaves de acesso restrito para catálogos compartilhados B2B

[!BADGE Private Beta]{type=Caution tooltip="Requer a extensão B2B do Adobe Commerce Optimizer Connector, que atualmente está em beta privado."}

Se você usar [!DNL Adobe Commerce] catálogos compartilhados B2B com o [!DNL Adobe Commerce Optimizer Connector B2B extension], a extensão automaticamente gerará e atribuirá a primeira chave de acesso restrito quando uma exibição de catálogo for criada. Use a página [!UICONTROL Restricted Access Keys] no Administrador do Commerce para exibir essa chave e criar, atribuir ou excluir chaves adicionais.

![Chaves de Acesso Restrito para exibições de catálogo compartilhado B2B](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>Para gerenciar chaves criadas manualmente para casos de uso que não são B2B, como portais de parceiros, consulte [Chaves de acesso restrito](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key).

## Acessar a página {#access-the-page}

No Administrador do Commerce, vá para **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**.

Você pode atribuir uma chave à exibição de catálogo na grade Catálogo Compartilhado ou na grade Empresa. Consulte [Atribuir chaves a uma exibição de catálogo compartilhado B2B](#assign-keys-to-a-shared-catalog-view).

>[!NOTE]
>
>Para obter uma referência dos campos desta página, [Gerenciamento de Chaves de Acesso Restrito](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} no *Guia de Administração do Commerce*.—>

## Quando você precisar de mais do que a chave automática {#when-you-need-more-than-the-automatic-key}

A chave automática gerada pelo [!DNL Adobe Commerce Optimizer Connector B2B extension] abrange a maioria dos catálogos compartilhados B2B sem exigir nenhuma ação sua. Gerencie você mesmo as chaves nestes casos:

- **Girando uma chave** — Crie uma nova chave, atribua-a à exibição de catálogo junto com a existente, confirme se está funcionando e exclua a chave antiga. A rotação automática ainda não está disponível.
- **Falha ao vincular uma chave** — Se o [Status de Sincronização de Exibição de Catálogo](catalog-view-sync-status.md) mostrar um desvio relacionado à chave, tente salvar a atribuição de exibição de catálogo novamente para repetir o link com falha. Se a chave ainda falhar, execute [!UICONTROL Reconcile & Repair] para recuperar a chave ou o status antes de criar uma substituição. Crie uma chave de substituição somente se a chave tiver expirado ou se a falha for irrecuperável de forma persistente.
- **Localizar uma chave pública** — Na página Chaves de Acesso Restrito, selecione **[!UICONTROL View Public Key]** para exibir e copiar a chave pública de uma chave.

Uma visualização de catálogo pode ter até três chaves atribuídas de uma só vez. Durante a rotação de chaves, [!DNL Adobe Commerce Optimizer] aceita tokens assinados por qualquer chave atribuída não expirada; não há etapa manual para definir uma chave &quot;ativa&quot;.

## Criar uma chave

Na página [!UICONTROL Restricted Access Keys], crie uma chave selecionando **[!UICONTROL Create Key]**.

O Commerce gera um novo par de chaves e contém a chave privada. A tabela Chaves de acesso restrito é atualizada com uma nova entrada de chave que mostra a ID de chave exclusiva. Use este [!UICONTROL Key ID] quando atribuir a chave a uma exibição de catálogo.

A chave pública não é registrada com [!DNL Adobe Commerce Optimizer] até que você atribua a chave a uma exibição de catálogo. Após o registro, a entrada da tabela Chave de acesso restrito é atualizada para mostrar a atribuição do catálogo e a data de expiração.

## Atribuir chaves a uma exibição de catálogo projetada de catálogo compartilhado B2B {#assign-keys-to-a-shared-catalog-view}

Atribuir ou cancelar atribuição de chaves da exibição de catálogo da conta da empresa ou da página de catálogo compartilhado, não da grade [!UICONTROL Restricted Access Keys] principal.

Uma exibição de catálogo deve ter pelo menos uma chave e pode ter no máximo três.

- Se você tentar atribuir uma quarta chave, você receberá uma mensagem de erro quando tentar salvar o valor: `A Catalog View can have at most 3 access keys.`
- Se uma exibição de catálogo tiver apenas uma chave, essa chave não poderá ser excluída ou desatribuída.

Para atualizar a configuração da chave de visualização do catálogo, você pode acessá-la na página de conta da empresa ou na página de catálogo compartilhado.

>[!BEGINTABS]

>[!TAB Gerenciar chaves de uma conta de empresa]

1. No Administrador do Commerce, abra a página da empresa (**[!UICONTROL Customers]** > **[!UICONTROL Companies]**).

1. Na coluna [!UICONTROL Action] da empresa, selecione [!UICONTROL Edit].

1. Para exibir a lista de exibições de catálogo projetadas do catálogo compartilhado atribuído à Empresa, expanda a seção _[!UICONTROL Catalog Views]_.

A guia lista as exibições de catálogo projetadas no catálogo compartilhado, incluindo suas chaves atribuídas.

1. Na coluna [!UICONTROL Actions] da exibição do catálogo a ser atualizada, selecione **[!UICONTROL Edit Restricted Access Keys]**.

   ![Lista suspensa Editar Chaves de Acesso Restrito mostrando as chaves atribuídas a uma exibição de catálogo](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. Para atribuir uma chave, selecione a lista suspensa **[!UICONTROL Access Keys]**. Em seguida, selecione uma chave não atribuída pelo [!UICONTROL key ID], por exemplo `#42`. Em seguida, clique em [!UICONTROL Done] para atribuí-lo à exibição do catálogo.

   As chaves já atribuídas a uma exibição de catálogo diferente são rotuladas de acordo.

1. Para remover um token de acesso, remova-o do campo [!UICONTROL Access Tokens] selecionando o controle `x` no rótulo da chave.

1. Para salvar e aplicar as atualizações de configuração, selecione **[!UICONTROL Save]**.

>[!TAB Gerenciar chaves de um catálogo compartilhado]

1. No Administrador do Commerce, abra a página de catálogo compartilhado (**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**).

1. Na coluna [!UICONTROL Action] para o compartilhado, escolha **[!UICONTROL General Settings]** no menu [!UICONTROL Select].

1. Para exibir a lista de exibições de catálogo projetadas no catálogo compartilhado, selecione **[!UICONTROL Catalog Views]** no menu [!UICONTROL Shared Catalog Information].

A página [!UICONTROL Catalog Views] lista a ID de exibição do catálogo, a exibição de armazenamento associada e a chave de acesso para cada exibição de catálogo.

1. Na coluna [!UICONTROL Actions] da exibição do catálogo a ser atualizada, selecione **[!UICONTROL Edit Restricted Access Keys]**.

   ![Lista suspensa Editar Chaves de Acesso Restrito mostrando as chaves atribuídas a uma exibição de catálogo](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. Para atribuir uma chave, selecione a lista suspensa **[!UICONTROL Access Keys]**. Em seguida, selecione uma chave não atribuída pelo título de chave padrão, por exemplo `#42`. Em seguida, clique em [!UICONTROL Done] para atribuí-lo à exibição do catálogo.

   As chaves já atribuídas a uma exibição de catálogo diferente são rotuladas de acordo.

1. Para remover um token de acesso, remova-o do campo [!UICONTROL Access Tokens] selecionando o controle `x` no rótulo da chave.

1. Para salvar e aplicar as atualizações de configuração, selecione **[!UICONTROL Save]**.

>[!ENDTABS]

## Gerenciar expiração e renovação de chave

Você pode configurar o tempo de vida padrão da chave para chaves de acesso restrito. O valor determina a data de expiração definida quando a extensão [!DNL Adobe Commerce Optimizer Connector B2B] gera a chave inicial, ou quando você cria uma nova chave manualmente.

A data de expiração é mostrada na coluna [!UICONTROL Expires At] na página [!UICONTROL Restricted Access Keys].

Para alterar a duração, vá para **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**. Na página [!UICONTROL Provisioning], atualize o campo **[!UICONTROL Default Key Expiry (days)]**. O tempo de vida padrão da chave do sistema é definido inicialmente por um período estendido (~100 anos). Certifique-se de atualizá-lo para um valor que corresponda às suas políticas de segurança.

### Renovação da chave

Quando uma chave estiver dentro de 10 dias da expiração, a página [!UICONTROL Restricted Access Keys] mostrará um ícone de aviso ao lado de sua entrada. Se você não renovar a chave antes de expirar, a exibição do catálogo ficará inacessível até que você atribua uma nova chave.

Você pode criar e atribuir uma nova chave a qualquer momento e remover a antiga depois de confirmar que a nova chave está funcionando.

## Limitações conhecidas

A rotação de chaves automática ainda não está disponível.

>[!MORELIKETHIS]
>
> - [Gerenciar chaves de acesso restrito](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} — Referência de campo completa para esta página, no *Guia de Administração do Commerce* —>
> - [Monitorar sincronização de exibição de catálogo](catalog-view-sync-status.md) — Monitore as exibições de catálogo que essas chaves protegem
> - [Exibições de catálogo privado](/help/optimizer/setup/private-catalog-view.md) — Saiba o que é uma exibição de catálogo privado gerenciada por conector
> - [Chaves de acesso restrito](/help/optimizer/setup/restricted-access-keys.md) — Saiba como funciona o fluxo de chaves manual baseado no ACO Studio para casos de uso que não são B2B
