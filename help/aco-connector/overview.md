---
title: Adobe Commerce Optimizer Connector
description: Saiba como conectar seus dados da nuvem do Commerce ou do projeto local à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: c9cce4766ef3f30390d50f53237328be1cfeefdf
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# Adobe Commerce Optimizer Connector

O Adobe Commerce Optimizer Connector é uma integração nativa e própria entre o Adobe Commerce (nuvem ou no local) e a Adobe Commerce Optimizer. Ele sincroniza os dados de catálogo e preço das lojas do Adobe Commerce na Commerce Optimizer para que você possa:

- **Descoberta e recomendações de produtos orientadas por IA**
- Execute **fronts de loja headless de alto desempenho** (incluindo vitrines para Commerce alimentadas pela Edge Delivery)
- Analisar **antes e depois de** KPIs e integridade da sincronização de dados em um único local

O Commerce permanece como seu sistema de registro de produtos, preços e estrutura de catálogo. O Commerce Optimizer se torna sua experiência e camada de merchandising, apresentando resultados rápidos e relevantes para qualquer loja ou canal conectado.

## Principais benefícios {#key-benefits}

| Benefício | O que isso significa para você |
| --- | --- |
| **Nenhum conector personalizado a ser compilado** | Use uma integração própria compatível em vez de escrever e manter feeds e scripts personalizados. |
| **Retorno do valor mais rápido com o Commerce Optimizer** | Ative Pesquisas com IA, recomendações e lojas headless na implantação existente do Adobe Commerce. |
| **Alinhado aos escopos do Commerce** | Mapeia automaticamente sites, visualizações da loja e grupos de clientes em construções de catálogo do Commerce Optimizer (origens de catálogo e catálogos de preços). |
| **Visibilidade operacional** | Monitore a integridade do feed, os últimos horários de sincronização e o status por SKU a partir de uma exibição dedicada do Status de sincronização do feed de dados. |
| **Caminho pronto para o futuro em direção a SaaS** | Fornece um caminho de modernização de baixo risco do PaaS em direção ao Adobe Commerce as a Cloud Service + Otimizer, sem uma replataforma. |

## Arquitetura do conector {#connector-architecture}

O diagrama a seguir ilustra a arquitetura completa do conector, desde o Adobe Commerce, passando pelo Commerce Optimizer, até as lojas e os sistemas de finalização.

![Diagrama completo de arquitetura do Commerce Optimizer Connector Commerce](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

Nesta arquitetura:

- O Adobe Commerce (na nuvem ou no local) é o sistema de produtores de registros e feeds
- O conector exporta feeds de catálogo, preço e categoria
- O Commerce Optimizer assimila e normaliza os dados do feed em Origens de Catálogo, Catálogos de preços e Exibições de catálogo
- As vitrines (vitrines do Commerce no Edge Delivery ou compilações headless personalizadas) chamam APIs do Commerce Optimizer GraphQL para detecção e recomendações e chamam a Commerce ou outra plataforma de terceiros conectada para operações de carrinho e finalização

## Como o conector funciona com o Adobe Commerce {#how-it-works}

- O Commerce Optimizer assimila e normaliza os dados do feed em Origens de Catálogo, Catálogos de preços e Exibições de catálogo.

- As vitrines (vitrines do Commerce no Edge Delivery ou builds headless personalizados) chamam as APIs do Commerce Optimizer GraphQL para detecção e recomendações e chamam a Commerce ou outra plataforma de terceiros conectada para operações de carrinho e finalização.

## Como o conector funciona com o Adobe Commerce

O Adobe Commerce Optimizer Connector opera usando seus escopos existentes do Commerce (sites e visualizações de loja) e a segmentação de clientes para preencher o modelo de catálogo do Commerce Optimizer:

![Mapeando dados do Commerce para o Adobe Commerce Optimizer](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Exibições da loja → Fontes de catálogo** — Cada exibição da loja se torna uma Source de catálogo separada na Commerce Optimizer. Essa origem inclui atributos localizados do produto e quaisquer dados específicos da visualização da loja
- **Sites → Catálogos de preços** — Cada site do Commerce mapeia para um ou mais Catálogos de preços no Commerce Optimizer. Preços do site e exportação de preços do grupo de clientes como catálogos de preços e entradas de preços
- **Grupos de clientes → Variantes de preços** — os preços de grupos de clientes da Commerce aparecem como entradas adicionais nos Catálogos de preços relevantes

Depois que o Commerce Optimizer assimilar os dados, você pode configurar:

- **Modos de Exibição e Políticas do Catálogo** no Commerce Optimizer (para região de compilação, marca ou subconjuntos específicos do cliente)
- **Descoberta de Produto** (pesquisa, aspectos, regras de merchandising)
- **Recomendações de produto**

Ao ativar o conector, a instância do Adobe Commerce permanece o sistema de registro para dados de catálogo e preço. Ao atualizar dados no Commerce, o conector sincroniza essas atualizações para a instância [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Para obter detalhes sobre como configurar o Commerce Optimizer, consulte [[!DNL Adobe Commerce Optimizer] Ferramentas de merchandising](../optimizer/overview.md#quick-tour).

## Fluxos de trabalho típicos {#typical-workflows}

Esses fluxos de trabalho descrevem como as equipes configuram e usam o Adobe Commerce Optimizer Connector. Para obter detalhes sobre como configurar a integração e habilitar esses fluxos de trabalho, consulte [Introdução](get-started.md).

### Instalação e configuração iniciais {#initial-setup}

1. **Instale o pacote de conectores no Adobe Commerce** usando o Composer:

   `composer require adobe-commerce/commerce-data-export-aco-adapter`

1. **Configurar detalhes de autenticação e ambiente** no Commerce Admin ou via CLI:

   ```terminal
   bin/magento aco:config:init \
     --org_id=<your-org> \
     --tenant_id=<your-tenant> \
     --client_id=<your-client-id> \
     --client_secret=<your-secret> \
     --region=na1 \
     --type=production
   ```

1. **Mapear escopos do Commerce para o Commerce Optimizer:**

   - Confirmar quais Sites e Exibições de Loja devem estar no escopo
   - Garantir que os grupos de clientes e as regras de preço sejam modelados conforme esperado

1. **Verificar conectividade:**

   - Execute uma sincronização de teste e confirme se Origens do catálogo, Catálogos de preços e produtos iniciais aparecem no Commerce Optimizer
   - Use a página Status da sincronização do feed de dados no Commerce e os painéis de Sincronização de dados no Commerce Optimizer para validação

### Sincronização de dados em andamento {#ongoing-sync}

Após a configuração inicial, o conector suporta:

- **Sincronização completa do catálogo** para migração inicial ou grandes alterações estruturais
- **Sincronizações delta** para atualizações contínuas quando produtos ou preços mudam
- **Ressincronizar comandos** para feeds direcionados (incluindo categorias a partir de v1.0.12):

   - `bin/magento saas:resync --feed=products`
   - `bin/magento saas:resync --feed=prices`
   - `bin/magento saas:resync --feed=categories`

### Configurar merchandising e lojas {#merchandising-storefronts}

Depois que os dados do Commerce estiverem disponíveis no Commerce Optimizer, use o Commerce Optimizer Studio para conectar as experiências de merchandising e de loja ao catálogo sincronizado.

**Para configurar merchandising e vitrines:**

1. **Criar Modos de Exibição e Políticas do Catálogo** no Commerce Optimizer Studio:

   - Filtrar o catálogo por marca, região, segmento de cliente ou canal
   - Aplicar regras de acesso a dados por loja ou parceiro

1. **Configurar a Descoberta de Produtos e as Recomendações** na Interface do Otimizador:

   - Criar regras de merchandising, facetas, sinônimos e unidades de recomendação
   - O conector descarrega toda a pesquisa e configuração de recomendação no Commerce Optimizer (as regras do Live Search e as Recomendações de produto no Commerce Admin não se aplicam mais a esses fluxos)

1. **Conectar vitrines** à Commerce Optimizer:

   - Para uma Loja do Commerce habilitada pela Edge Delivery Services, configure a loja para usar o locatário do Otimizer e a Exibição do catálogo corretos e para chamar endpoints de pesquisa e recomendação por meio da API de merchandising
   - Para vitrines de terceiros, use APIs públicas ou SDKs do Otimizer para chamadas de pesquisa e recomendação

   >[!NOTE]
   >
   >Para obter um exemplo de integração de terceiros, consulte o [Salesforce Commerce Connector for Commerce Optimizer](../optimizer/developer/salesforce-connector.md).

1. **Manter check-out** na plataforma existente:

   - Manter o carrinho, o checkout, o gerenciamento de pedidos e as contas do cliente na Adobe Commerce ou em uma plataforma de terceiros
   - Use o App Builder e a API Mesh para entrega do carrinho ao integrar com sistemas de check-out externos

## Cenários compatíveis {#supported-scenarios}

O conector é projetado para comerciantes B2C com Adobe Commerce em implantações na nuvem e no local que desejam adotar o Commerce Optimizer sem reconstruir seu back-end.

**Casos de uso comuns:**

- **Modernizar somente a loja**
Mantenha seu back-end existente do Commerce, mova o PLP/Search/PDP para vitrines do Edge Delivery alimentadas pela Commerce Optimizer

- **Dimensionando desempenho de catálogo e pesquisa**
Descarregue a indexação e a pesquisa de catálogos pesados para os serviços SaaS da Commerce Optimizer, mantendo a propriedade do produto e do preço no Commerce

- **Adoção incremental de SaaS**
Use o conector como uma etapa na direção do Adobe Commerce as a Cloud Service + Otimizer, com um catálogo Commerce combinável

## Responsabilidades e pré-requisitos de implementação {#responsibilities-prerequisites}

A Commerce é a fonte da verdade para produtos, preços e grupos de clientes. Fazer alterações no Commerce; o conector as sincroniza com o Commerce Optimizer.

**A Commerce Optimizer é responsável por:**

- Modelagem de catálogo (Origens de catálogo, Catálogos de preços, Exibições de catálogo, Políticas)
- Detecção e recomendações de produtos
- Métricas de vitrine, painéis de sincronização de dados e relatórios de Métricas de sucesso

**O conector não:**

- Modificar o carrinho do Commerce, o check-out ou os fluxos do pedido
- Provisionar projetos da loja automaticamente (a loja Commerce/ferramenta Edge Delivery lida com isso)

**Antes de começar:**

- Verifique se o Commerce atende aos requisitos mínimos de versão e conector de serviços. Consulte [Introdução](get-started.md#prerequisites) para obter detalhes.
- Verifique se você tem acesso à Organização IMS, uma instância [!DNL Adobe Commerce Optimizer] e as credenciais e os detalhes de região necessários.

## Documentação relacionada {#related-documentation}

- Configure a integração e habilite os fluxos de trabalho principais: [Introdução ao Adobe Commerce Optimizer Connector](get-started.md)
- Saiba mais sobre os conceitos e a arquitetura do Commerce Optimizer: [O que é o Adobe Commerce Optimizer?](../optimizer/overview.md)
