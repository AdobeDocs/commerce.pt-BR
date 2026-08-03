---
title: Visão geral das [!DNL Adobe Commerce as a Cloud Service]
description: Saiba mais sobre os principais recursos e benefícios do  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
autotag-review: '2026-06-18T16:02:31.185Z'
TQID: 'https://experienceleague.adobe.com/D1Aq9qlw2HprQUy-g5KcIH2Ky2XUDawZIrAbe2Jz6ZI'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c18ed297-2187-4aec-affb-9d9654eca6fcid: c32adafa-ed01-4b31-997e-2413013911b0id: cc250cf1-34eb-4863-80d0-d170d45ea067id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: a743e5dc-8f37-4b5d-a848-03c32ca30598id: e91a50b1-0b31-436e-9033-00e4776e94cbid: f236e2a1-90d4-477d-92e1-5996b5e92bffid: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: d095671a-1355-40aa-8b5f-06c33c68080bid: da3860b0-d637-47df-bef0-273751180266
source-git-commit: c5b10a715f64a220fc965328a7c913951d44dedc
workflow-type: tm+mt
source-wordcount: 1461
ht-degree: 0%

---

# Visão geral das [!DNL Adobe Commerce as a Cloud Service]

O [!DNL Adobe Commerce as a Cloud Service] oferece flexibilidade, escalabilidade e eficiência, permitindo que as empresas forneçam e dimensionem rapidamente operações digitais enquanto aceleram a inovação. A infraestrutura nativa em nuvem da Adobe ajusta automaticamente os recursos para atender às demandas de pico de tráfego, pedidos e gerenciamento de catálogos.

A tabela a seguir destaca os produtos que alimentam o [!DNL Adobe Commerce as a Cloud Service]:

<table style="table-layout:auto">
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de seleção" align="center"> <strong>Commerce Storefront</strong>
    </td>
    <td align="left">
      Interface voltada para o cliente, onde os compradores navegam e compram produtos
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de seleção" align="center"> <strong>Serviços de merchandising</strong>
    </td>
    <td align="left">
      Serviços de back-end que gerenciam catálogos de produtos, preços e inventário
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de seleção" align="center"> <strong>Visuais do Produto</strong>
    </td>
    <td align="left">
      Gerenciamento de ativos digitais para imagens e mídia de produtos
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="marca de seleção" align="center"> <strong>Plataforma de desenvolvedor</strong>
    </td>
    <td align="left">
      Ferramentas e APIs de desenvolvimento principais para a criação de funcionalidade personalizada
    </td>
  </tr>
</table>

## Arquitetura

Assista ao vídeo a seguir para obter uma breve introdução à arquitetura [!DNL Adobe Commerce as a Cloud Service]. Diagramas que ilustram a arquitetura são fornecidos abaixo do vídeo.

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

Este diagrama ilustra o fluxo de dados entre o [!DNL Adobe Commerce as a Cloud Service] e todas as soluções da Adobe Experience Cloud.

![Diagrama de fluxo de dados mostrando a integração do [!DNL Adobe Commerce as a Cloud Service] com as soluções do [!DNL Adobe Experience Cloud]](./assets/data-flow.png){zoomable="yes"}

## Commerce Storefront

Para criar experiências ricas em minutos com criação simples baseada em documentos ou edição visual com [!DNL Storefront Builder], use o [[!DNL Commerce Storefront]](https://experienceleague.adobe.com/developer/commerce/storefront/) da Adobe viabilizado por [!DNL Edge Delivery Services].

O [!DNL Commerce Storefront] é totalmente headless com uma arquitetura dissociada que fornece todos os serviços e dados de merchandising por meio de uma camada de API do GraphQL. Essa arquitetura permite que as equipes desenvolvam seus front-ends independentemente da Commerce Foundation, fornecendo agilidade para criar e testar novos pontos de contato com tecnologias emergentes.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] não dá suporte a vitrines Luma. Se você estiver migrando do Adobe Commerce na Nuvem ou no local, consulte [vitrines existentes](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) para obter orientações sobre a transição.

## Serviços de merchandising e serviços de pagamento

A Adobe fornece um conjunto avançado de serviços de merchandising inteligentes e combináveis para ajudá-lo a apoiar suas principais metas comerciais. Esses serviços também fornecem APIs essenciais para otimizar o desempenho em escala.

- [[!DNL Live Search]](../live-search/overview.md)—Forneça resultados mais inteligentes, mais rápidos e relevantes aos compradores com esta ferramenta de pesquisa alimentada por IA. Para obter instruções de configuração, consulte [Configurando [!DNL Live Search]](../live-search/workspace.md).
- [[!DNL Product Recommendations]](../product-recommendations/overview.md)—Adicione recomendações alimentadas por IA com base no comportamento do comprador, tendências populares, similaridade de produtos e muito mais. Para obter instruções de configuração, consulte [[!DNL Product Recommendations] Workspace](../product-recommendations/workspace.md).
- [Serviço de Catálogo](../catalog-service/guide-overview.md)—Dê aos seus clientes uma experiência otimizada de produto enquanto aumenta o desempenho, melhora a escalabilidade e aumenta as conversões.

  >[!NOTE]
  >
  >O Serviço de Catálogo é incluído automaticamente com [!DNL Live Search] e [!DNL Product Recommendations].

- [Serviços de Pagamento](../payment-services/guide-overview.md)—Impulsione a satisfação do cliente oferecendo vários métodos de pagamento, incluindo prestações de pagamento sem juros, e uma única visão do processamento de pagamento, ordens e faturas. Para obter instruções de configuração, consulte [Página Inicial dos Serviços de Pagamento](../payment-services/payments-home.md).

## [!DNL Product Visuals powered by AEM Assets]

As Visualizações de produto ajudam a simplificar o gerenciamento de ativos usando um sistema de gerenciamento de ativos digitais (DAM) que se integra ao Adobe Experience Manager para gerenciar conteúdo de mídia avançada.

A integração garante que ativos digitais, como imagens de produtos ou conteúdo de marketing, sejam vinculados dinamicamente às entidades de merchandising apropriadas, incluindo produtos e categorias no Adobe Commerce, com base na SKU ou outros atributos principais.

O [!DNL Product Visuals] está disponível nativamente com o [!DNL Adobe Commerce as a Cloud Service], fornecendo alguns dos recursos do [!DNL AEM Assets].

Como alternativa, os recursos nativos no [!DNL Adobe Commerce as a Cloud Service] fornecem ferramentas básicas de gerenciamento de ativos para armazenar e gerenciar ativos digitais.

Consulte o guia da [integração com o AEM Assets](../aem-assets-integration/overview.md) para saber mais sobre como integrar o [!DNL Product Visuals powered by AEM Assets] com o [!DNL Adobe Commerce as a Cloud Service].

### [!DNL Product Visuals] ou [!DNL AEM Assets]

A comparação a seguir ajuda a selecionar a melhor opção para o conteúdo de que o supply chain precisa:

<table>
  <tr>
    <td align="left">
      <strong>[!DNL Product Visuals powered by AEM Assets]</strong>
      <ul>
        <li>Gerente de ativos digitais (DAM) de vídeo e imagem de produto integrados e automatizados</li>
        <li>Redimensionar, cortar e converter imagens</li>
        <li>Entrega de vídeo e imagem em alta velocidade</li>
        <li>Otimizar formatos, tamanhos e qualidade de imagem com base nos recursos do navegador do cliente</li>
        <li>Acesso ao Adobe Express e ao Adobe Firefly</li>
        <li>Limites de uso para capacidade de entrega de imagens/vídeos e acesso do usuário</li>
        <li>Seletor de ativos integrado</li>
      </ul>
    </td>
    <td align="center">
      <br><br><br><br><br><br><br><br><br><br><br>
      <img src="../assets/icon-double-chevron-right.svg" alt="divisa" width="100">
    </td>
    <td align="left">
      <strong>AEM Assets</strong>
      <ul>
        <li>Todos os recursos dos Visuais do produto</li>
        <li>Gerenciador de ativos digitais de marketing completo (DAM)</li>
        <li>Usuários ilimitados (pagamento por usuário)</li>
        <li>Entrega ilimitada de imagens e vídeos</li>
        <li>Funcionalidade avançada de gerenciamento de ativos:</li>
        <ul>
          <li>Conjuntos de rotação de 360° e visualizadores interativos</li>
          <li>Suporte a modelo 3D e conteúdo imersivo</li>
          <li>Suporte ao PDF</li>
          <li>Corte inteligente alimentado por IA</li>
          <li>Modelos dinâmicos de imagem</li>
          <li>Marcação inteligente</li>
          <li>Rastreamento e análise do desempenho dos ativos</li>
        </ul>
      </ul>
    </td>
  </tr>
    <tr>
    <td align="center" colspan="3">
      <strong>A integração com a marca Adobe está disponível para facilitar a migração entre as ofertas.</strong>
    </td>
  </tr>
</table>

## Plataforma do desenvolvedor

A Adobe fornece aos desenvolvedores pontos de extensão e ferramentas abrangentes para criar aplicativos que ampliam os recursos do Commerce Foundation e integram-se a sistemas de terceiros (como CRMs, ERPs e PIMs). Essas ferramentas reduzem o custo total de propriedade da plataforma das seguintes maneiras:

- **Escalabilidade** — Os aplicativos podem ser dimensionados separadamente do software principal, permitindo maior eficiência e atualizações simplificadas.
- **Isolamento** — Um ambiente isolado significa que os desenvolvedores podem atualizar ou modificar suas extensões a seu critério, sem depender de uma versão principal.
- **Independência tecnológica** - Os desenvolvedores podem escolher qualquer pilha de tecnologia e linguagem de codificação que atenda às suas necessidades.

>[!TIP]
>
>Aplicativos criados pelo fornecedor também estão disponíveis para instalação no [Adobe Exchange](https://exchange.adobe.com/).

A Adobe fornece as seguintes ferramentas de desenvolvedor para criar integrações e personalizações:

- [**Malha de API para Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/)—Coordene e combine várias APIs, GraphQL, REST e outras fontes em um único ponto de extremidade de GraphQL consultável.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/intro_and_overview/)—Crie e implante aplicativos Web seguros e escalonáveis que estendam a funcionalidade do Commerce e se integrem a soluções de terceiros.
- [**Eventos**](https://developer.adobe.com/commerce/extensibility/events/) — Use disparadores de eventos personalizados para interagir com outras ferramentas de desenvolvimento extensíveis.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) — Use webhooks para acionar automaticamente interações entre o Commerce e sistemas de terceiros.
- [**Interface do Administrador SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/)—Personalize e aprimore o Administrador do Commerce com novas páginas e recursos para seus comerciantes.
- [**Integration Starter Kit**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) — acelere suas integrações back-office com integrações de referência, scripts de integração e uma arquitetura padronizada.

## Commerce Foundation

O [!DNL Commerce Foundation] fornece uma plataforma de hospedagem automatizada segura e recursos de autoatendimento para gerenciar seu aplicativo Commerce em um ambiente nativo em nuvem.

Os principais recursos incluem:

- Integração simplificada
- Atualizações ininterruptas
- Integrações de terceiros

### Integração simplificada

Inicie instâncias de sandbox e produção em minutos com o portal de provisionamento de autoatendimento do [!UICONTROL Commerce Cloud Manager]. Tudo o que você precisa, incluindo serviços de merchandising, uma instância do Commerce headless e o [!DNL App Builder], é automaticamente configurado e integrado às suas instâncias.

Consulte [Introdução](getting-started.md) para saber como criar e gerenciar instâncias do Commerce.

### Atualizações ininterruptas

Acesse os recursos e aprimoramentos mais recentes sem precisar de atualizações manuais. A entrega contínua de novos recursos e atualizações elimina a necessidade de patch manual, garantindo que você sempre tenha acesso aos recursos mais recentes com baixo custo total de propriedade.

O processo típico de atualização do Adobe Commerce na nuvem envolvia a criação de backups, a clonagem de instâncias, a execução de ferramentas de compatibilidade e a correção de conflitos de código. Isso não é mais necessário com [!DNL Adobe Commerce as a Cloud Service]. O Adobe envia notificações no aplicativo quando novos recursos e atualizações de segurança são lançados. Você tem um período de 30 dias para avaliar os novos recursos nas instâncias da sandbox antes que as atualizações sejam aplicadas automaticamente aos ambientes de produção.

>[!NOTE]
>
>O Adobe garante compatibilidade com versões anteriores para todas as atualizações. Isso significa que, quando as atualizações forem aplicadas, elas não interromperão a funcionalidade existente ou as personalizações que aderem ao modelo [API-first extensibility](https://developer.adobe.com/commerce/extensibility/).

### Integrações de terceiros

Os desenvolvedores podem usar o [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) e as [REST APIs](https://developer.adobe.com/commerce/webapi/rest/) abrangentes para integrar o [!DNL Commerce Foundation] a sistemas de terceiros e estender os recursos do Commerce.

<!-- 
## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. 
-->

## Benefícios

As seções a seguir fornecem informações sobre os benefícios que o [!DNL Adobe Commerce as a Cloud Service] oferece aos líderes de negócios e de TI.

### Líderes empresariais

- **Aumente a receita**: direcione o tráfego orgânico com uma vitrine de alto desempenho que aumenta a SEO. Crie experiências personalizadas que impulsionam a conversão usando dados avançados.
- **Operações de dimensionamento**: os serviços de dimensionamento automático atendem às demandas de pico da sua empresa com 99,9% de disponibilidade. Implante várias marcas e regiões e ofereça suporte a B2B e B2C a partir de uma única instância. Suporte a catálogos de produtos grandes e complexos com modelagem de dados flexível.
- **Aumente a produtividade do merchandiser**: use serviços de merchandising alimentados por IA para melhorar a conversão. Faça um experimento nativo, diretamente na loja. Gerencie a experiência da loja para criar experiências avançadas em minutos com a criação simples baseada em documentos ou um editor visual.
- **Diminua o custo total de propriedade (TCO) e acelere a inovação**: serviços sempre atualizados fornecem acesso imediato a novos recursos. Ative novos recursos instalando facilmente os aplicativos do marketplace. Libere recursos da manutenção tediosa para se concentrar na criação de novos recursos.

### Líderes em tecnologia da informação (TI)

- **Provisionamento rápido**: comece rapidamente com o provisionamento de autoatendimento em minutos. Todos os serviços são pré-configurados para trabalhar em conjunto de maneira simples e rápida. Provisione sandboxes para experimentação de desenvolvedores, conforme necessário.
- **Baixo custo de propriedade**: não há mais atualizações com serviços sempre atualizados. Mantenha-se seguro e em conformidade com os patches de segurança mais recentes aplicados automaticamente para você. Dimensione automaticamente para atender às cargas de trabalho mais exigentes.
- **Loja de alto desempenho**: crie experiências ricas em minutos com criação simples baseada em documento ou um editor visual. Use serviços de merchandising alimentados por IA para melhorar a conversão. Experimentação nativa incorporada à loja.
- **Inovação mais rápida**: libere recursos de uma manutenção tediosa para se concentrar na criação de novos recursos que agregam valor aos negócios. Use extensibilidade abrangente e tecnologias baseadas em padrões (JavaScript, HTML, CSS e ferramentas de baixo código) para criar experiências diferenciadas. Instale aplicativos de terceiros com um clique para adicionar novos recursos à sua plataforma de comércio.
