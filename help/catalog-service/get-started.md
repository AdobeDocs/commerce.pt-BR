---
title: Introdução ao  [!DNL Catalog Service]
description: Saiba como acessar o [!DNL Catalog Service] e integrar a aplicativos de front-end e serviços de terceiros.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: null
workflow-type: tm+mt
source-wordcount: 586
ht-degree: 0%

---

# Introdução ao [!DNL Catalog Service]

Depois que o [!DNL Catalog Service] for habilitado, você poderá acessar o serviço e usá-lo para recuperar dados de catálogo, como informações de produto e categoria, da sua instância do Adobe Commerce. O serviço está disponível como uma API do GraphQL que pode ser acessada pelo administrador do Commerce ou por qualquer aplicativo de front-end que ofereça suporte a consultas do GraphQL.

{{aco-merchandising-services}}

## Acessar o serviço

O [!DNL Catalog Service] está disponível como uma API do GraphQL que você pode acessar do Administrador do Commerce ou de qualquer aplicativo de front-end que ofereça suporte a consultas do GraphQL. O serviço está disponível em ambientes SaaS e PaaS.

[!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."}

| Ambiente | Endpoint |
| ------------ | ----------: |
| **Testando** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Produção** | `https://catalog-service.adobe.io/graphql` |

[!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."}

| Ambiente | Endpoint |
| ----------- | --------:|
| Testes | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| Produção (ainda não disponível) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**Estrutura de URL para pontos de extremidade SaaS**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` é a região da nuvem em que sua instância está implantada.
- `<environment>` é o tipo de ambiente, como `sandbox`. Se o ambiente for de produção, esse valor será omitido.
- `<tenantId>` é o identificador exclusivo da instância específica da sua organização na Adobe Experience Cloud.

Para obter detalhes sobre como usar a API do GraphQL do Serviço de Catálogo, consulte o [Guia do Catalog Service for Adobe Commerce](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) na documentação do *Adobe Commerce Developer*.

## Integrar a uma loja headless ou a serviços de terceiros

Para integrar com uma loja headless, você deve atualizar a configuração da loja para habilitar a comunicação entre a loja e a [!DNL Catalog Service] para recuperar dados de produto e categoria.

Se você estiver usando a loja do Adobe Commerce no Edge Delivery Services, adicione o ponto de extremidade do Serviço de catálogo à configuração da loja. Para obter detalhes, consulte a [documentação do Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration).

Para outras integrações, consulte a documentação de configuração do projeto para obter detalhes sobre como configurar integrações entre o serviço e as fontes de dados de back-end.

### Configuração do firewall

Para permitir [!DNL Catalog Service] por meio de um firewall, adicione `commerce.adobe.io` ao incluo na lista de permissões.

## Serviço de catálogo e API Mesh

A [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permite que os desenvolvedores integrem APIs privadas ou de terceiros e outras interfaces com produtos da Adobe usando o Adobe IO.

Consulte o tópico [[!DNL Catalog Service] e Malha de API](mesh.md) para obter detalhes sobre instalação e configuração.

## Monitorar e solucionar problemas de exportação de dados

O administrador do Commerce fornece ferramentas para monitorar e solucionar problemas na exportação de dados do Commerce para os serviços conectados:

- **[Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** — Monitore a sincronização de dados entre o [!DNL Catalog Service] e sua instância do Adobe Commerce. O painel mostra o status geral de sincronização e lista todos os produtos sincronizados.

- **[Página Status da Sincronização do Feed de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** — Rastreie o status da exportação de todos os feeds de dados para garantir a consistência dos dados. Essa página alerta sobre problemas que ocorrem durante o processo de exportação para que você possa resolvê-los rapidamente. Um status &quot;Sucesso&quot; indica que os dados foram exportados e estarão disponíveis nos serviços conectados da Commerce quando o processo de sincronização de dados for concluído.

>[!NOTE]
>
>Se a página Status da sincronização do feed de dados não estiver disponível no Commerce Admin for Commerce em implantações na nuvem ou locais, siga as [instruções de instalação da extensão](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status#install-the-extension) para habilitá-la.
