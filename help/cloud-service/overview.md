---
title: Visão geral das [!DNL Adobe Commerce as a Cloud Service]
description: Saiba mais sobre os principais recursos e benefícios do  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---


# Visão geral das [!DNL Adobe Commerce as a Cloud Service]

O [!DNL Adobe Commerce as a Cloud Service] oferece flexibilidade, escalabilidade e eficiência, permitindo que as empresas forneçam e dimensionem rapidamente operações digitais e acelerem a inovação. A infraestrutura nativa em nuvem da Adobe ajusta automaticamente os recursos para atender às demandas de pico de tráfego, pedidos e gerenciamento de catálogos.

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

![[!DNL Adobe Commerce as a Cloud Service] diagrama de arquitetura](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Use a [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=pt-BR) da Adobe alimentada pela Edge Delivery Services para criar experiências ricas em minutos com criação simples baseada em documentos ou edição visual com o Storefront Builder.

A Commerce Storefront é totalmente headless com uma arquitetura dissociada que fornece todos os serviços e dados de merchandising por meio de uma camada de API do GraphQL. Essa arquitetura permite que as equipes desenvolvam seus front-ends independentemente da Commerce Foundation, fornecendo agilidade para criar e testar novos pontos de contato com tecnologias emergentes.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] não dá suporte a vitrines Luma. Se você estiver migrando do Adobe Commerce na Nuvem ou no local, consulte [vitrines existentes](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=pt-BR#existing-storefronts) para obter orientação sobre a transição.

## Serviços de merchandising e serviços de pagamento

A Adobe fornece um conjunto avançado de serviços de merchandising inteligentes e combináveis para ajudá-lo a apoiar suas principais metas comerciais. Esses serviços também fornecem APIs essenciais para otimizar o desempenho em escala.

- [Live Search](../live-search/overview.md)—Forneça resultados mais inteligentes, mais rápidos e relevantes aos compradores com esta ferramenta de pesquisa habilitada por IA.
- [Recomendações de Produto](../optimizer/merchandising/recommendations/overview.md)—Adicione recomendações alimentadas por IA com base no comportamento do comprador, tendências populares, similaridade de produto e muito mais.
- [Serviço de Catálogo](../catalog-service/guide-overview.md)—Dê aos seus clientes uma experiência otimizada de produto enquanto aumenta o desempenho, melhora a escalabilidade e aumenta as conversões.
- [Serviços de Pagamento](../payment-services/guide-overview.md)—Impulsione a satisfação do cliente oferecendo vários métodos de pagamento, incluindo prestações de pagamento sem juros, e uma única visão do processamento de pagamento, ordens e faturas.

## Visualizações de produto viabilizadas pelo AEM Assets

As Visualizações de produto ajudam a simplificar o gerenciamento de ativos usando um sistema de gerenciamento de ativos digitais (DAM) que se integra ao Adobe Experience Manager para gerenciar conteúdo de mídia avançada.

A integração garante que ativos digitais, como imagens de produtos ou conteúdo de marketing, sejam vinculados dinamicamente às entidades de merchandising apropriadas, incluindo produtos e categorias no Adobe Commerce, com base na SKU ou outros atributos principais.

As Visualizações do produto estão disponíveis prontas para uso com o [!DNL Adobe Commerce as a Cloud Service], fornecendo alguns dos recursos do AEM Assets.

Como alternativa, os recursos nativos no [!DNL Adobe Commerce as a Cloud Service] fornecem ferramentas básicas de gerenciamento de ativos para armazenar e gerenciar ativos digitais.

### Visuais de produto ou AEM Assets

A comparação a seguir ajuda a selecionar a melhor opção para as necessidades da cadeia de suprimento de conteúdo:

<table>
  <tr>
    <td align="left">
      <strong>Visualizações de produto fornecidas pelo AEM Assets</strong>
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

Consulte o guia [Integração com o AEM Assets](../aem-assets-integration/overview.md) para saber mais sobre como integrar Visuais de Produtos fornecidos pelo AEM Assets com o [!DNL Adobe Commerce as a Cloud Service].

## Plataforma do desenvolvedor

O Adobe fornece aos desenvolvedores pontos de extensão e ferramentas abrangentes para criar aplicativos que ampliam os recursos do Commerce Foundation e integram-se a sistemas de terceiros (como CRMs, ERPS e PIMS). Essas ferramentas reduzem o custo total de propriedade da plataforma das seguintes maneiras:

- **Escalabilidade** — Os aplicativos podem ser dimensionados separadamente do software principal, permitindo maior eficiência e atualizações simplificadas.
- **Isolamento**-Um ambiente isolado significa que os desenvolvedores podem atualizar ou modificar suas extensões a seu critério, sem depender de uma versão principal.
- **Independência tecnológica** - Os desenvolvedores podem escolher qualquer pilha de tecnologia e linguagem de codificação que atenda às suas necessidades.

>[!TIP]
>
>Aplicativos criados pelo fornecedor também estão disponíveis para instalação no [Adobe Exchange](https://exchange.adobe.com/).

A Adobe fornece as seguintes ferramentas de desenvolvedor para criar integrações e personalizações:

- [**Malha de API para Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/)—Coordene e combine várias APIs, GraphQL, REST e outras fontes em um único ponto de extremidade de GraphQL consultável.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/)—Crie e implante aplicativos Web seguros e escalonáveis que estendam a funcionalidade do Commerce e se integrem a soluções de terceiros.
- [**Eventos**](https://developer.adobe.com/commerce/extensibility/events/) — Use disparadores de eventos personalizados para interagir com outras ferramentas de desenvolvimento extensíveis.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) — Use webhooks para acionar automaticamente interações entre o Commerce e sistemas de terceiros.
- [**Interface do Administrador SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/)—Personalize e aprimore o Administrador do Commerce com novas páginas e recursos para seus comerciantes.
- [**Integration Starter Kit**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) — acelere suas integrações back-office com integrações de referência, scripts de integração e uma arquitetura padronizada.

## Commerce Foundation

O Commerce Foundation fornece uma plataforma de hospedagem automatizada segura e recursos de autoatendimento para gerenciar seu aplicativo Commerce em um ambiente nativo em nuvem.

Os principais recursos incluem:

- Integração simplificada
- Atualizações ininterruptas
- Integrações de terceiros

### Integração simplificada

Inicie instâncias de sandbox e produção em minutos com o portal de provisionamento de autoatendimento do [!UICONTROL Commerce Cloud Manager]. Tudo o que você precisa, incluindo Serviços de merchandising, uma instância do Commerce headless e o App Builder, é configurado automaticamente e integrado às suas instâncias.

Consulte [Introdução](getting-started.md) para saber como criar e gerenciar instâncias do Commerce.

### Atualizações ininterruptas

Acesse os recursos e aprimoramentos mais recentes sem precisar de atualizações manuais. A entrega contínua de novos recursos e atualizações elimina a necessidade de patch manual, garantindo que você sempre tenha acesso aos recursos mais recentes com baixo custo total de propriedade.

O processo típico de atualização do Adobe Commerce na nuvem envolvia a criação de backups, a clonagem de instâncias, a execução de ferramentas de compatibilidade e a correção de conflitos de código. Isso não é mais necessário com [!DNL Adobe Commerce as a Cloud Service]. O Adobe envia notificações no aplicativo quando novos recursos e atualizações de segurança são lançados. Você tem um período de 30 dias para avaliar os novos recursos nas instâncias da sandbox antes que as atualizações sejam aplicadas automaticamente aos ambientes de produção.

>[!NOTE]
>
>O Adobe garante compatibilidade com versões anteriores para todas as atualizações. Isso significa que, quando as atualizações forem aplicadas, elas não interromperão a funcionalidade existente ou as personalizações que aderem ao modelo [API-first extensibility](https://developer.adobe.com/commerce/extensibility/).

### Integrações de terceiros

Os desenvolvedores podem usar as abrangentes [APIs do GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) e [REST](https://developer.adobe.com/commerce/webapi/rest/) para integrar o Commerce Foundation a sistemas de terceiros e estender os recursos do Commerce.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

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
