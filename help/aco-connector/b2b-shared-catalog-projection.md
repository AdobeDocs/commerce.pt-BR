---
title: Projeção do catálogo compartilhado B2B
description: Saiba como o conector B2B projeta catálogos compartilhados B2B do Adobe Commerce em visualizações protegidas de catálogo do Commerce Optimizer e como as vitrines resolvem e autorizam o acesso do comprador.
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# Projeção do catálogo compartilhado B2B

O [!DNL Adobe Commerce Optimizer Connector for B2B] projeta [!DNL Adobe Commerce] catálogos compartilhados e atribuições da empresa em exibições de catálogo [!DNL Adobe Commerce Optimizer] protegidas.

## Sincronização base e projeção B2B

A base [!DNL Adobe Commerce Optimizer Connector] sincroniza feeds de catálogo e preço, mapeando exibições de repositório para fontes de catálogo, sites para catálogos de preços e grupos de clientes para catálogos de preços.

O [!DNL Adobe Commerce Optimizer Connector for B2B] projeta a variedade e os preços de cada catálogo compartilhado personalizado em uma exibição protegida. O Adobe Commerce seleciona a exibição usando a atribuição da empresa do comprador. A chave de acesso restrito verifica solicitações assinadas, mas não determina o acesso ao catálogo. O Adobe Commerce é o sistema de registro para catálogo gerenciado por conector, preços e dados de projeção B2B. Gerencie a descoberta de produtos e as recomendações na configuração [!DNL Adobe Commerce Optimizer].

## Mapeamento de dados

A projeção B2B combina conteúdo e preço de catálogo sincronizado com a classificação de Catálogo compartilhado e o contexto de atribuição da empresa.

![Mapeamento de diagrama [!DNL Adobe Commerce] exibições de armazenamento, preços, catálogos compartilhados e atribuições da empresa para exibições de catálogo privado projetadas em [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}

| Dados de [!DNL Adobe Commerce] | [!DNL Adobe Commerce Optimizer] resultado | Finalidade |
| --- | --- | --- |
| Exibição de loja e dados do produto habilitados | Origem do catálogo | Fornece conteúdo de produto localizado. |
| Preços do site e do grupo de clientes | Catálogo de preços | Fornece os preços aplicáveis mas não autoriza o acesso |
| Ordenação personalizada do catálogo compartilhado | Política | Filtra a exibição de catálogo para a classificação de catálogo compartilhado. |
| Catálogo compartilhado personalizado e exibição de armazenamento ativada | Exibição de catálogo privado | Cria uma exibição protegida para cada combinação, com a origem do catálogo, a política e o catálogo de preços aplicáveis. |
| Atribuição da empresa a um catálogo compartilhado | Contexto de comprador resolvido | Permite que o back-end autenticado resolva a exibição de catálogo associada à empresa do comprador. |
| Chave de acesso restrito atribuída a uma exibição protegida | Proteção de catálogo | Autoriza solicitações para a exibição do catálogo protegido, mas não seleciona preços. |

Cada exibição de catálogo privado pode fazer referência a apenas um catálogo de preços. Visualizações de loja com o mesmo site e contexto de preços de grupo de clientes podem compartilhar um catálogo de preços ao usar diferentes fontes de catálogo localizadas. O conector não cria um catálogo de preços por catálogo compartilhado.

O catálogo compartilhado padrão não é projetado como uma visualização de catálogo privado B2B.

## Autorização em tempo de execução

Depois que um comprador faz logon, o back-end do Commerce autentica a sessão e usa a atribuição da empresa do comprador e a exibição da loja para resolver a exibição de catálogo e o catálogo de preços apropriados.

A loja envia a ID de visualização do catálogo, a ID do catálogo de preços e o token assinado com cada solicitação de API de merchandising. [!DNL Adobe Commerce Optimizer] verifica a assinatura RS256 do JWT em relação às chaves de acesso restrito atribuídas à exibição de catálogo. Ele retorna dados de catálogo somente quando o token e a chave são válidos e não expiram.

![Fluxo de autorização em tempo de execução para solicitações de catálogo B2B de um comprador por meio de uma vitrine e do back-end do Commerce para [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}

Para solicitações de catálogo privado, envie estes cabeçalhos:

| Cabeçalho | Finalidade |
| --- | --- |
| `AC-View-ID` | Identifica a exibição do catálogo. |
| `AC-Price-Book-ID` | Identifica o catálogo de preços a ser usado. |
| `AC-Catalog-View-Access-Token` | Carrega o JWT assinado que autoriza o acesso à exibição de catálogo protegida. |

Para conhecer todos os requisitos de solicitação e token, consulte [Autenticação da API de merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication) e [Verificar acesso a uma exibição de catálogo privado](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced).

## Limite de proteção

A proteção de catálogo abrange somente solicitações de catálogo e pesquisa. Ele não protege o carrinho, o checkout ou as operações de pedidos. Imponha a qualificação de compra no Adobe Commerce ou no sistema de transações conectado.

## Configuração e monitoramento da projeção

O conector B2B projeta exibições de catálogo privado, políticas, referências de catálogo de preços e configuração de chave de acesso restrito de [!DNL Adobe Commerce]. Não é necessário criar manualmente esses objetos de projeção gerenciados pelo conector. Para obter instruções de configuração, consulte [Introdução ao conector B2B](get-started-b2b-shared-catalogs.md).

Para monitorar exibições de catálogo projetadas e reconciliar o desvio da configuração, consulte [Monitorar sincronização de exibição de catálogo](catalog-view-sync-status.md). Para gerenciar as chaves atribuídas, consulte [Gerenciar chaves de acesso restrito para catálogos compartilhados B2B](restricted-access-keys.md).
