---
title: Migrar para o Adobe Commerce as a Cloud Service
description: Saiba como migrar para o Adobe Commerce as a Cloud Service.
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---


# Migrar para o Adobe Commerce as a Cloud Service

O Adobe Commerce as a Cloud Service fornece a maioria das configurações prontas para uso. No entanto, se você estiver migrando de uma Adobe Commerce existente na nuvem ou instância local, será necessário executar ações de migração diferentes, dependendo da sua configuração específica.

## Caminhos de migração

O Adobe Commerce as a Cloud Service é compatível com vários caminhos de migração, dependendo da linha do tempo, da loja e das personalizações.

Como alternativa a uma migração completa, o Adobe Commerce as a Cloud Service oferece suporte a uma migração em fases, usando o Commerce Optimizer ou uma abordagem incremental.

* **Migração Incremental** — Essa abordagem envolve a migração de dados, personalizações e integrações em estágios. Essa abordagem é ideal para grandes comerciantes com muitas personalizações que desejam fazer a transição gradual de suas personalizações e dados complexos para o Adobe Commerce as a Cloud Service em seu próprio ritmo.

![migração incremental](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** — Essa abordagem permite migrar interativamente usando o Commerce Optimizer como uma fase de transição para mover personalizações e dados complexos para o Adobe Commerce as a Cloud Service no seu próprio ritmo. A Commerce Optimizer fornece acesso aos Serviços de merchandising fornecidos pelos Canais e políticas do catálogo, pela Commerce Storefront fornecida pela Edge Delivery e pelos Visuais de produto fornecidos pela AEM Assets.

![migração iterativa](./assets/optimizer.png){width="600" zoomable="yes"}

* **Migração Completa** — Essa abordagem envolve a migração de todos os dados, personalizações e integrações de uma só vez. Essa abordagem é ideal para comerciantes menores com poucas personalizações que desejam fazer a transição rápida para o Adobe Commerce as a Cloud Service.

A tabela a seguir fornece uma visão geral do processo de migração para diferentes vitrines e configurações:

|                    | Loja LUMA | PWA Storefront | Commerce Storefront ativado por Edge Delivery | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migração de dados | Obrigatório | Obrigatório | Obrigatório | Obrigatório |
| Loja | Migrar para a Commerce Storefront habilitada pela Edge Delivery | Migrar para a Commerce Storefront viabilizada pelo Edge Delivery ou Manter | Sem impacto | Sem impacto |
| API Mesh | Criar nova malha | Criar nova malha ou reconfigurar existente | Criar nova malha ou reconfigurar existente | Criar nova malha ou reconfigurar existente |
| Integrações | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração |
| Personalizações | Mover para App Builder e API Mesh | Mover para App Builder e API Mesh | Mover para App Builder e API Mesh | Mover para App Builder e API Mesh |
| Gerenciamento do Assets | Migração necessária se estiver usando o OOTB | Migração necessária se estiver usando o OOTB | Migração necessária se estiver usando o OOTB | Migração necessária se estiver usando o OOTB |
| Extensões | Migrar para o App Builder | Migrar para o App Builder | Migrar para o App Builder | Migrar para o App Builder |

Conforme indicado na tabela, as mitigações para cada migração consistirão em:

* **Migração de Dados**—Usando as ferramentas de migração fornecidas para migrar dados de sua instância existente para o Adobe Commerce as a Cloud Service.
* **Storefront** — o EDS existente e as lojas headless não exigem mitigação, mas as lojas LUMA exigem migração para a Commerce Storefront viabilizada pela Edge Delivery. As vitrines da PWA Studio podem ser migradas para a Commerce Storefront com a tecnologia da Edge Delivery ou mantidas em seu estado atual. A Adobe fornecerá aceleradores para auxiliar na migração da loja.
* **[Malha de API](https://developer.adobe.com/graphql-mesh-gateway)**—Crie uma nova malha ou modifique a existente. A Adobe fornecerá malhas pré-configuradas para auxiliar nesse processo.
* **Integrações** — Todas as integrações precisam aproveitar o [kit inicial de integração](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) ou a [API REST do Adobe Commerce as a Cloud Service](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/).
* **Personalizações** — Todas as personalizações devem ser movidas para o App Builder e para a API Mesh.
* **Gerenciamento do Assets**—Todo o gerenciamento de ativos requer migração. Se você já estiver usando o AEM Assets, não será necessário migrar.
* **Extensões** — Todas as extensões em andamento precisam ser recriadas como extensões fora do processo. Até o final de 2025, a Adobe fornecerá 100 de nossas extensões mais populares pré-carregadas e prontas para uso para minimizar os tempos de compilação.

## Fases de migração

A migração da instância atual do Adobe Commerce para uma nova instância do Adobe Commerce as a Cloud Service envolve principalmente as seguintes fases:

* **[Disponibilidade](#readiness-phase)** — comece determinando se a implantação está pronta para ser movida para o ACCS. Nesta fase, você também deve se familiarizar com as alterações introduzidas pelo ACCS.&#x200B;
* **[Implementação](#implementation-phase)** — Em seguida, prepare o código, a vitrine, as extensões e as integrações para migração. Para facilitar a transição, o Adobe permite [abordagens iterativas de curto e longo prazo](#migration-paths).&#x200B;
* **[Ativar](#go-live-phase)** — Teste e confirme se tudo está no lugar e execute a migração de dados.
* **[Pós-ativação](#post-go-live-phase)** — Em colaboração com a Adobe, monitore os problemas e melhore o desempenho conforme necessário após a conclusão da migração.

### Fase de preparação

1. Comece analisando a arquitetura do Adobe Commerce as a Cloud Service, a estrutura de extensibilidade e os recursos da loja:

   * [Arquitetura do Adobe Commerce no Cloud Services](./overview.md)—Revise a arquitetura da plataforma e como ela difere da sua instância atual do Adobe Commerce.
   * [Estrutura de Extensibilidade do Adobe Commerce](https://developer.adobe.com/commerce/extensibility/)—Identifique como você deseja fazer a transição das personalizações atuais.
   * [Commerce Storefront habilitada pela Edge Delivery](https://experienceleague.adobe.com/developer/commerce/storefront/)—Revise a solução de vitrine recomendada.

1. Auditoria de compatibilidade de personalização:

   * Identifique seus módulos personalizados atuais e integrações de terceiros.
   * Avaliar as personalizações que precisam de reimplementação usando o App Builder.
   * Mapeie suas personalizações atuais para seus equivalentes de extensões do App Builder.

1. Confirme os requisitos da vitrine eletrônica e certifique-se de que eles estejam alinhados aos recursos do Adobe Edge Delivery.

1. Analise suas integrações atuais de terceiros e confirme a compatibilidade da API com a plataforma Adobe Commerce as a Cloud Service.

### Fase de implementação

As etapas a seguir descrevem o processo de desenvolvimento e execução da migração:

1. Crie uma nova instância do Adobe Commerce as a Cloud Service no [Commerce Cloud Manager](./getting-started.md#create-an-instance).

1. Instale os aplicativos e as personalizações necessários. O Adobe Commerce as a Cloud Service é pré-carregado com 100 dos aplicativos mais populares. Se precisar de aplicativos ou personalizações adicionais, você poderá reimplementá-los usando o App Builder.

1. Configure uma das seguintes vitrines baseadas no GraphQL:

   * [Criar uma vitrine do Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [Use o PWA Studio para criar uma loja personalizada baseada no GraphQL](https://developer.adobe.com/commerce/pwa-studio/)

1. Migre seus dados da instância anterior do Commerce para o ACCS:

   * Migrar dados nativos do Adobe Commerce usando ferramentas de migração de dados.
   * Migrar extensões e personalizações de terceiros
   * Migrar dados de configuração e integração:
      * Transfira configurações da API Mesh, serviços de terceiros e integrações de sistema usando o [Adobe Commerce Integration Starter Kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/).

### Fase de ativação

Antes de iniciar, valide e teste sua nova instância do Adobe Commerce as a Cloud Service:

* **Teste Funcional** — Verifique se os dados migrados, a funcionalidade da loja e as personalizações funcionam perfeitamente.

* **Teste de desempenho**—Avalie a velocidade e a escalabilidade de suas lojas para garantir um desempenho ideal globalmente.

* **Auditoria de Segurança**—Revise as medidas de segurança, incluindo o controle de acesso à API e quaisquer vulnerabilidades em potencial.

### Pós-fase de ativação

Depois de validar e testar a nova instância da sandbox do Adobe Commerce as a Cloud Service, você pode iniciar a instância de produção:

1. Go live

   * Redirecione o tráfego para a nova plataforma e monitore o desempenho.
   * Desative a instância antiga do Adobe Commerce.

1. Monitoramento pós-lançamento

   * Use ferramentas de monitoramento para garantir operações estáveis e solucionar problemas após o lançamento.
