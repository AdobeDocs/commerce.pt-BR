---
title: Configurar permissões de usuário do IMS para a integração com o AEM Assets
description: Saiba como a identidade do IMS e os perfis do Admin Console habilitam o acesso ao delivery do AEM Assets, o Seletor de ativos e os campos de configuração do Commerce preenchidos automaticamente.
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Permissões de usuário e IMS

**IMS** (Adobe Identity Management System) é a camada de autenticação. Para o Adobe Commerce as a Cloud Service, a autenticação IMS é habilitada por padrão no Administrador. Para o Adobe Commerce na nuvem ou no local, o IMS é opcional;[Habilitar o IMS para o Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} fornece uma interface de usuário de configuração avançada (Seletor de ativos, menus suspensos preenchidos automaticamente), mas você pode configurar a integração sem o IMS inserindo manualmente a **ID do Programa** e a **ID do Ambiente**.

A Integração do AEM Assets também requer **perfis de produto do Adobe Admin Console** específicos ao usar o IMS. Os usuários que configuram a integração no Commerce Admin precisam do **perfil de produto Usuários do AEM Assets DM OpenAPI - entrega** ou do perfil de produto **autor** como um fallback. Isso é controlado por meio de perfis de produto do Admin Console na organização IMS do usuário e permite:

* O **Seletor de ativos** permite selecionar imagens do AEM Assets ao gerenciar imagens de categoria ou conteúdo do Page Builder.
* **Campos de configuração preenchidos automaticamente**, como **ID do Programa**, **ID do Ambiente** e **Mapeamento de domínio** detalhados que extraem valores da sessão IMS do usuário com base nos perfis de produto do Admin Console (entrega ou autor).

Sem as permissões corretas, o Seletor de ativos não está disponível e esses campos aparecem vazios ou exigem entrada manual.
>[!BEGINSHADEBOX]

**Como o IMS e as permissões funcionam juntos**

O Adobe IMS fornece a identidade de usuário e o contexto da organização, enquanto o Adobe Admin Console define quais **perfis de produto**(permissões) ele tem. A Integração do AEM Assets usa os detalhes do IMS mais o perfil atribuído para determinar se pode preencher automaticamente campos de configuração e ativar o Seletor de ativos.

>[!ENDSHADEBOX]

## Por que os perfis de produto são necessários

A integração só pode carregar domínios mapeados para um perfil. Portanto, os usuários podem ter os seguintes perfis de produto:

* **Perfil de produto de entrega do AEM**. Obrigatório para o Seletor de ativos e a interface de configuração quando o usuário tem perfis de autor e de entrega. A integração usa o perfil de produto de delivery do AEM quando disponível.

* **Criar perfil de produto**. Necessário para acessar a interface do usuário do AEM Assets. Também serve como fallback para o Seletor de ativos e a Interface do usuário de configuração quando o usuário não tiver o perfil de produto do delivery do AEM no Admin Console.

Os domínios (incluindo ID de programa, ID de ambiente e Mapeamento de domínio) são atribuídos ao perfil de produto de delivery do AEM. A integração carrega domínios do **perfil de produto de entrega do AEM** quando disponível, ou retorna ao **perfil de produto do autor** quando o perfil de produto de entrega do AEM não está no Admin Console do usuário. Os usuários precisam de um desses perfis para:

* Preencha os menus suspensos **ID do programa**, **ID do ambiente** e **Mapeamento de domínio** na configuração de administrador do Commerce.
* Use o Seletor de ativos para procurar e selecionar ativos da AEM Assets.

Se nenhum dos perfis estiver configurado, os usuários poderão inserir manualmente a **ID do Programa** e a **ID do Ambiente**, mas o Seletor de Ativos não estará disponível.

## Conceder permissões por tipo de implantação

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE Somente SaaS]{type=Positive tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."}

A autenticação IMS é habilitada por padrão. Adicione o usuário ao **perfil de produto Usuários do AEM Assets DM OpenAPI - entrega** no [Adobe Admin Console](https://adminconsole.adobe.com/), ou ao perfil de produto **autor** (por exemplo, `<environment-name> - author - <program-id> - <environment-id>`) como um fallback quando o usuário não tiver o perfil de produto de entrega do AEM em seu Admin Console.

>[!NOTE]
>
> Os usuários também devem ser adicionados ao Commerce e ao AEM Assets. Consulte [Adicionar um usuário ao AEM Assets ou Visuais de Produto](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} no guia _Usuário e Identity Management_ para obter a configuração completa.

![Perfil de produto do Admin Console para entrega do AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB Adobe Commerce na nuvem ou no local]

[!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."}

A **ID do Cliente IMS** é necessária para que o PaaS habilite o Seletor de Ativos. Consulte [Configurar o projeto do AEM Assets](configure-aem.md#prerequisites) para obter os pré-requisitos, incluindo como obter a ID do cliente IMS ao habilitar o Dynamic Media com OpenAPI.

Para usar o Seletor de ativos e os campos de configuração preenchidos automaticamente (ID do programa, ID do ambiente, Mapeamento de domínio):

1. [Habilite o Adobe IMS para Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html){target=_blank} para que o Administrador do Commerce use a autenticação IMS e possa ler os perfis de produto do Admin Console do usuário.

1. [Abra um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) para solicitar uma ID de cliente IMS personalizada para o Seletor de ativos.

1. No [Adobe Admin Console](https://adminconsole.adobe.com/), adicione o usuário ao perfil de produto **Usuários do AEM Assets DM OpenAPI - entrega**, ou ao perfil de produto **autor** (por exemplo, `<environment-name> - author - <program-id> - <environment-id>`) como um fallback quando o usuário não tiver o perfil de produto de entrega do AEM em seu Admin Console.

Sem o IMS, ainda é possível configurar a integração inserindo manualmente a ID do programa e a ID do ambiente no Administrador do Commerce.

>[!ENDTABS]

## Documentação relacionada

* [Configurar permissões de usuário IMS para a Integração do AEM Assets](setup-synchronization.md)—Conecte o Commerce ao AEM Assets e configure regras correspondentes.
* [Seleção manual de ativos](../synchronize/asset-selector-integration.md) — Use o Seletor de ativos para imagens de categoria e Page Builder.
* [Adicionar um usuário ao AEM Assets ou Visuais de Produto](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} — Para ACCS, adicione usuários ao Commerce e ao AEM Cloud Manager (Proprietário da Empresa, Gerente de Implantação) primeiro. Os **Usuários do AEM Assets DM OpenAPI - entrega** perfil (ou perfil **autor** como fallback) são um requisito adicional para o Seletor de ativos e os recursos de preenchimento automático.
* [Atribuir membros da equipe à camada de entrega do AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}. Documentação do AEM para obter acesso à entrega.
