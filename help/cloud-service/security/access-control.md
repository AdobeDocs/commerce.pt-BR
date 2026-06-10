---
title: Gerenciamento de identidade e acesso
description: Saiba mais sobre os recursos de gerenciamento de identidade e acesso do Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---


# Gerenciamento de identidade e acesso

O [!DNL Adobe Commerce as a Cloud Service] aproveita a infraestrutura de identidade corporativa da Adobe para garantir controle de acesso seguro, escalável e centralizado em todos os ambientes. O IAM (gerenciamento de identidade e acesso) no [!DNL Adobe Commerce as a Cloud Service] foi projetado para simplificar o provisionamento de usuários, impor acesso de privilégios mínimos e dar suporte à conformidade com padrões de segurança globais.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service] usa o [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) para autenticar usuários e gerenciar direitos. Isso inclui suporte para provedores de identidade federada e [controle de acesso baseado em função](../user-management.md).

- **Governança do Admin Console**: os administradores gerenciam o acesso à loja e ao back-end por meio do [!DNL Adobe Admin Console]. As permissões podem ser enviadas para recursos e funções específicos, garantindo acesso de privilégio mínimo.

## Adobe Identity Management Services (IMS)

[!DNL Adobe Commerce as a Cloud Service] usa [!DNL Adobe Identity Management Services (IMS)] para autenticar usuários e gerenciar direitos na plataforma. O IMS fornece:

- **Suporte à identidade federada**: integre-se a provedores de identidade corporativa, como Azure AD e Okta, usando SAML ou OIDC.
- **Logon Único (SSO)**: acesso fácil a [!DNL Adobe Commerce] e outros produtos do [!DNL Adobe Experience Cloud].
- **Autenticação Multifator (MFA)**: imposta no nível da organização para segurança aprimorada.
- **Redundância global**: os dados de identidade são armazenados em uma infraestrutura de nuvem com várias regiões e balanceamento de carga.

## Controle de acesso do Admin Console

O [!DNL Adobe Admin Console] é o hub central para gerenciar o acesso do usuário a [!DNL Adobe Commerce as a Cloud Service]:

- **Controle de Acesso Baseado em Função (RBAC)**: atribua permissões granulares aos usuários com base em suas funções, como Desenvolvedor, Administrador e Analista.
- **Perfis de produto**: defina escopos de acesso para ambientes diferentes, como preparo e produção.
- **Administração delegada**: administradores do sistema e administradores de produtos podem gerenciar o acesso de usuários sem envolvimento de TI.

Consulte [gerenciamento de usuários](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management) para obter mais informações.

## Segurança de autenticação e integração de API

A autenticação da API REST de [!DNL Adobe Commerce as a Cloud Service] é realizada por meio do [!DNL Adobe Identity Management Services (IMS)] da Adobe usando protocolos OAuth 2 padronizados. Esse sistema de autenticação oferece suporte a fluxos de trabalho interativos baseados no usuário e integrações automatizadas de servidor para servidor, garantindo acesso seguro e apropriado a diferentes casos de uso.

>[!NOTE]
>
>Os métodos de geração de token de integração e de administrador nas versões PaaS de [!DNL Adobe Commerce] não são suportados em ambientes SaaS. Em vez disso, você deve obter um token de administrador IMS por meio da autenticação OAuth.

- **Suporte ao OAuth 2.0**: autenticação segura baseada em token para integrações e serviços de terceiros.
- **Acesso à API com escopo**: limite o acesso à API a recursos e operações específicos.
- **Log de auditoria**: controle eventos de autenticação e acesse alterações para fins de conformidade e solução de problemas.

Consulte [Autenticação REST](https://developer.adobe.com/commerce/webapi/rest/authentication/) para obter mais informações.
