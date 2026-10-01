---
title: Adobe Commerce Optimizer Connector
description: Saiba mais sobre o [!DNL Adobe Commerce Optimizer Connector] para sincronização de catálogo, pesquisa e entrega de vitrine entre [!DNL Adobe Commerce] e [!DNL Adobe Commerce Optimizer].
feature: Integration, Storefront, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T19:00:00.000Z'
nudge: true
TQID: 'https://experienceleague.adobe.com/v769V06jl-9YfovpL3HOB-FxovIMZyHxOlHXHvkQmbc'
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
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%
---
# [!DNL Adobe Commerce Optimizer Connector]

O [!DNL Adobe Commerce Optimizer Connector] é uma integração nativa e própria entre o [!DNL Adobe Commerce] (nuvem ou local) e o [!DNL Adobe Commerce Optimizer]. Ele sincroniza os dados de catálogo e preço dos seus armazenamentos do [!DNL Adobe Commerce] no [!DNL Adobe Commerce Optimizer] para que você possa:

- **Descoberta e recomendações de produtos orientadas por IA**
- Executar **frente de loja headless de alto desempenho** (incluindo frente de loja da Commerce alimentadas por [!DNL Edge Delivery Services])
- Analisar **antes e depois de** KPIs e integridade da sincronização de dados em um único local

O [!DNL Adobe Commerce] permanece como seu sistema de registro de produtos, preços e estrutura de catálogo. O [!DNL Adobe Commerce Optimizer] se torna sua experiência e camada de merchandising, oferecendo resultados rápidos e relevantes a qualquer vitrine ou canal conectado.

## Principais benefícios {#key-benefits}

| Benefício | O que isso significa para você |
| --- | --- |
| **Nenhum conector personalizado a ser compilado** | Use uma integração própria compatível em vez de escrever e manter feeds e scripts personalizados. |
| **Retorno do valor mais rápido com[!DNL Adobe Commerce Optimizer]** | Ative Pesquisas com IA, recomendações e headless na sua implantação existente do [!DNL Adobe Commerce]. |
| **Alinhado aos escopos do Commerce** | Mapeia automaticamente sites, exibições de loja e grupos de clientes em [!DNL Adobe Commerce Optimizer] construções de catálogo (Origens de Catálogo e Catálogos de Preços). |
| **Visibilidade operacional** | Monitore a integridade do feed, os últimos horários de sincronização e o status por SKU a partir de uma exibição dedicada do [!UICONTROL Data Feed Sync Status]. |
| **Caminho pronto para o futuro em direção a SaaS** | Fornece um caminho de migração em fases do Commerce na nuvem ou no local para [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], sem replataforma. |

## Arquitetura do conector {#connector-architecture}

O diagrama a seguir ilustra a arquitetura completa do conector, de [!DNL Adobe Commerce] até [!DNL Adobe Commerce Optimizer] e até as vitrines e os sistemas de check-out.

![Diagrama completo de arquitetura do Adobe Commerce Optimizer Connector](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

Nesta arquitetura:

- [!DNL Adobe Commerce] (na nuvem ou no local) é o sistema de produtor de registro e feed
- O conector exporta feeds de catálogo, preço e categoria
- [!DNL Adobe Commerce Optimizer] assimila e normaliza os dados de feed em fontes de catálogo, catálogos de preços e exibições de catálogo
- As vitrines (vitrines do Commerce em [!DNL Edge Delivery Services] ou compilações headless personalizadas) chamam APIs do GraphQL [!DNL Adobe Commerce Optimizer] para descoberta e recomendações e chamam [!DNL Adobe Commerce] ou outra plataforma de terceiros conectada para operações de carrinho e check-out

Criado em [[!DNL SaaS Data Export]](/help/data-export/overview.md), o conector mapeia os feeds coletados para o formato [!DNL Catalog Data Ingestion API] e processa a autenticação e o envio. Consulte [Pipeline de sincronização do conector](/help/aco-connector/connector-sync-pipeline.md) para obter informações sobre comportamento de sincronização, controle de escopo e tratamento de erros.

## Como o conector funciona com o [!DNL Adobe Commerce] {#how-the-connector-works-with-adobe-commerce}

O [!DNL Adobe Commerce Optimizer Connector] dá suporte à sincronização do catálogo B2C. Ele sincroniza feeds de catálogo e preços de uma instância do [!DNL Adobe Commerce] e mapeia exibições de loja, sites e grupos de clientes para fontes de catálogo e catálogos de preços no [!DNL Adobe Commerce Optimizer]. Ele não sincroniza o catálogo compartilhado B2B ou a configuração de atribuição da empresa. Após a sincronização, configure as exibições e políticas do catálogo no [!DNL Adobe Commerce Optimizer] Studio.

![Mapeando dados de [!DNL Adobe Commerce] para [!DNL Adobe Commerce Optimizer]](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

### Mapeamento do catálogo base

O conector mapeia os dados do catálogo [!DNL Adobe Commerce] para o modelo de catálogo [!DNL Adobe Commerce Optimizer]:

- **Exibição de armazenamento → Fontes de Catálogo** — Cada exibição de armazenamento se torna uma fonte de catálogo separada em [!DNL Adobe Commerce Optimizer]. Essa fonte inclui atributos de produto localizados e quaisquer dados específicos da visualização da loja.
- **Site → Catálogos de Preços** — Cada site do [!DNL Adobe Commerce] mapeia para um ou mais catálogos de preços no [!DNL Adobe Commerce Optimizer]. Preços do site e exportação de preços do grupo de clientes como catálogos de preços e entradas de preços.
- **Grupo de clientes → Entradas do catálogo de preços** — [!DNL Adobe Commerce] o preço do grupo de clientes aparece como entradas adicionais nos catálogos de preços relevantes.

Depois que o conector sincroniza os dados do catálogo, configure o modelo de merchandising no [!DNL Adobe Commerce Optimizer] Studio. Por exemplo, configure:

- **Modos de Exibição e Políticas do Catálogo** para subconjuntos específicos de região, marca ou cliente
- **Descoberta de Produto** para pesquisa, aspectos e regras de comercialização
- **[!DNL Product Recommendations]**

### Comportamento do conector B2B {#b2b-shared-catalog-projection-specification}

O [!DNL Adobe Commerce Optimizer Connector for B2B] estende o conector base com uma projeção unidirecional do catálogo compartilhado B2B e da configuração de atribuição da empresa em experiências de catálogo protegidas. [!DNL Adobe Commerce] permanece a fonte da verdade para dados de catálogo e preço; o conector B2B se baseia no catálogo base e na sincronização de preços e gerencia suas projeções geradas pelo conector.

Para o mapeamento de projeção, fluxo de autorização de tempo de execução e limite de proteção, consulte [Projeção do catálogo compartilhado B2B](b2b-shared-catalog-projection.md). Para obter instruções de configuração, consulte [Introdução ao conector B2B](/help/aco-connector/get-started-b2b-shared-catalogs.md).

>[!NOTE]
>
>Para obter detalhes sobre a configuração de [!DNL Adobe Commerce Optimizer], consulte [[!DNL Adobe Commerce Optimizer] Ferramentas de merchandising](/help/optimizer/overview.md#quick-tour).

## Fluxos de trabalho típicos {#typical-workflows}

Estes fluxos de trabalho descrevem como as equipes configuram e usam o [!DNL Adobe Commerce Optimizer Connector]. Para obter detalhes sobre como configurar a integração e habilitar esses fluxos de trabalho, consulte [Introdução](/help/aco-connector/get-started.md).

### Instalação e configuração iniciais {#initial-setup}

Consulte [Etapas de configuração](/help/aco-connector/get-started.md#configuration-steps) no guia _Introdução_.

### Sincronização de dados em andamento {#ongoing-sync}

Após a configuração inicial, o conector suporta:

- **Sincronização completa do catálogo** para migração inicial ou grandes alterações estruturais
- **Sincronizações delta** para atualizações contínuas quando produtos ou preços mudam
- **Ressincronizar comandos** para sincronizar feeds direcionados

Para obter comportamento de sincronização automatizada, agendamentos de cron e manipulação de erros, consulte [Pipeline de sincronização do conector](/help/aco-connector/connector-sync-pipeline.md). Antes de uma sincronização completa de catálogo ou atualização extensa, use [Estimar volume de dados e tempo de sincronização](/help/aco-connector/reference/estimate-data-volume-sync-time.md) para planejar o tempo e evitar a interrupção do site.

Os seguintes feeds estão disponíveis para o [!DNL Adobe Commerce Optimizer Connector]:

- `products` - dados de produtos
- `productAttributes` - metadados para atributos de produto
- `priceBooks` - catálogos de preços
- `prices` - preços do produto
- `categories` - dados de categorias

Para obter detalhes adicionais, consulte os seguintes tópicos:

- Verifique a sincronização de dados do catálogo e ressincronize manualmente os feeds do conector: [Gerenciar sincronização](/help/aco-connector/data-sync-status.md)
- Para operações de ressincronização de CLI do [!DNL Adobe Commerce], consulte [Sincronizar feeds usando a CLI do Commerce](/help/data-export/data-export-cli-commands.md)
- [[!DNL Adobe Commerce Optimizer Connector] módulos e pontos de extremidade de feed](/help/aco-connector/reference/connector-reference.md)
- [Mapeamento de campos para feeds de conector](/help/aco-connector/reference/field-mapping.md)

### Configurar merchandising e lojas {#merchandising-storefronts}

Quando os dados do [!DNL Adobe Commerce] estiverem disponíveis no [!DNL Adobe Commerce Optimizer], use o [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) para conectar as experiências de merchandising e de vitrine ao catálogo sincronizado. As próximas etapas típicas incluem:

- **Modos de exibição e políticas de catálogo** — Para o conector básico, defina subconjuntos específicos de região, marca ou cliente e regras de acesso no menu [!UICONTROL Store setup]. Para restringir quem pode consultar uma exibição de catálogo, consulte [Exibições de catálogo privado](/help/optimizer/setup/private-catalog-view.md)
- **Descoberta de produtos e recomendações** — Configure pesquisa, aspectos, regras de merchandising, sinônimos e unidades de recomendação no menu [!UICONTROL Merchandising]. O comportamento de pesquisa e recomendação é gerenciado em [!DNL Adobe Commerce Optimizer]; as configurações [!DNL Live Search] e [!DNL Product Recommendations] no Administrador [!DNL Adobe Commerce] não se aplicam mais a esses fluxos
- **Conexões da loja** — lojas Point Commerce em [!DNL Edge Delivery Services] ou compilações headless de terceiros no [!DNL Adobe Commerce Optimizer] locatário correto, exibição de catálogo e pontos de extremidade de API de Merchandising. Para integrações headless personalizadas, consulte [Integração headless de vitrine](/help/aco-connector/headless-storefront.md). Para obter um exemplo de integração de terceiros, consulte o [Salesforce Commerce Connector for [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Check-out** — Mantenha o carrinho, o check-out, o gerenciamento de pedidos e as contas de clientes em [!DNL Adobe Commerce] ou em uma plataforma conectada de terceiros. Use [!DNL App Builder] e [!DNL API Mesh] para entrega do carrinho quando necessário

Para obter uma orientação de configuração passo a passo, consulte [Introdução](/help/aco-connector/get-started.md) e as [[!DNL Adobe Commerce Optimizer] ferramentas de Merchandising](/help/optimizer/overview.md#quick-tour).

## Cenários compatíveis {#supported-scenarios}

A base [!DNL Adobe Commerce Optimizer Connector] oferece suporte a comerciantes B2C com [!DNL Adobe Commerce] em nuvem e implantações locais que desejam adotar [!DNL Adobe Commerce Optimizer] sem reconstruir seu back-end.

O [!DNL Adobe Commerce Optimizer Connector for B2B] separado estende o conector base para sincronizar a configuração do catálogo compartilhado e projetar automaticamente catálogos compartilhados personalizados como exibições de catálogo privado. Para obter detalhes, consulte [Projeção do catálogo B2B](b2b-shared-catalog-projection.md).

**Casos de uso comuns:**

- **Migração da vitrine eletrônica para o Edge Delivery**
Mantenha seu back-end existente do [!DNL Adobe Commerce], mova o PLP/Search/PDP para [!DNL Edge Delivery Services] vitrines viabilizadas pelo [!DNL Adobe Commerce Optimizer].

- **Dimensionando desempenho de catálogo e pesquisa**
Descarregue a indexação e a pesquisa de catálogos pesados para os serviços SaaS (Software as a Service) do [!DNL Adobe Commerce Optimizer], mantendo a propriedade do produto e do preço no [!DNL Adobe Commerce].

## Responsabilidades e pré-requisitos de implementação {#responsibilities-prerequisites}

[!DNL Adobe Commerce] é o sistema de registro para produtos, preços e grupos de clientes. Faça alterações em [!DNL Adobe Commerce], e o conector as sincroniza com [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer]é responsável por:**

- Modelagem de catálogo (origens de catálogo, catálogos de preços, exibições de catálogo, políticas)
- Detecção e recomendações de produtos
- Métricas da loja, painéis de sincronização de dados e relatórios de métricas de sucesso

**O conector não:**

- Modificar fluxos de carrinho, check-out ou pedido de [!DNL Adobe Commerce]
- Provisionar automaticamente projetos da loja (a Commerce Storefront / [!DNL Edge Delivery Services] manipula isso)

**Antes de começar:**

- Verifique se [!DNL Adobe Commerce] atende à versão mínima e aos requisitos de [!DNL Adobe Commerce Optimizer Connector]. Consulte [Introdução](/help/aco-connector/get-started.md#requirements-to-use-the-integration) para obter detalhes.
- Verifique se você tem acesso à Organização IMS, uma instância [!DNL Adobe Commerce Optimizer] e as credenciais e os detalhes de região necessários.

>[!MORELIKETHIS]
>
> - [Introdução ao [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md) — Configure a integração e habilite os fluxos de trabalho principais.
> - [Pipeline de sincronização do conector](/help/aco-connector/connector-sync-pipeline.md) — Entenda o mecanismo de sincronização, a inicialização e a manipulação de erros.
> - [Gerenciar sincronização](/help/aco-connector/data-sync-status.md) — Verifique a sincronização de dados do catálogo e ressincronize os feeds manualmente.
> - [Mapeamento de campos para feeds de conector](/help/aco-connector/reference/field-mapping.md) — Revise o mapeamento de dados em nível de campo para todos os feeds.
> - [Cenários de solução de problemas](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md) — Resolva erros de configuração ou resultados de sincronização inesperados.
> - [Notas de versão](/help/aco-connector/release-notes.md) — Revise as atualizações de conectores e os problemas conhecidos.
