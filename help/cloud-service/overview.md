---
title: Visão geral das [!DNL Adobe Commerce as a Cloud Service]
description: Saiba mais sobre os principais recursos e benefícios do  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 0e3820eab0fded58a1a99d8a805b2774968380fd
workflow-type: tm+mt
source-wordcount: '1452'
ht-degree: 0%

---

# Visão geral das [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

O [!DNL Adobe Commerce as a Cloud Service] oferece flexibilidade, escalabilidade e eficiência, permitindo que as empresas forneçam e dimensionem rapidamente operações digitais e acelerem a inovação. A infraestrutura nativa em nuvem da Adobe ajusta automaticamente os recursos para atender às demandas de pico de tráfego, pedidos e gerenciamento de catálogos.

O gráfico a seguir destaca os produtos que alimentam o [!DNL Adobe Commerce as a Cloud Service]:

![[!DNL Adobe Commerce as a Cloud Service] pilha de produtos](./assets/product-stack.svg){align="center" zoomable="yes"}

>[!BEGINSHADEBOX]

![informações](assets/Smock_InfoOutline_18_N.svg) Se você deseja participar do programa de acesso antecipado [!DNL Adobe Commerce as a Cloud Service], preencha [este formulário](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4WOxhjY2doZPikS2hIbfmL5URFZXTE5TUk9PMUw0OFdOWTBNNlI3UTlNMS4u&amp;route=shorturl).

>[!ENDSHADEBOX]

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
- [Recomendações de Produto](../product-recommendations/overview.md)—Adicione recomendações alimentadas por IA com base no comportamento do comprador, tendências populares, similaridade de produto e muito mais.
- [Serviços de merchandising fornecidos por canais e políticas](../optimizer/catalog/overview.md)—Gerencie catálogos de produtos grandes e complexos com modelagem de dados flexível para fornecer catálogos comerciais flexíveis e de alto desempenho alinhados à estrutura dos negócios e às estratégias de entrada no mercado. Use com o [Commerce Optimizer](../optimizer/overview.md) para otimizar o desempenho do catálogo e melhorar as taxas de conversão.
- [Serviços de Pagamento](../payment-services/guide-overview.md)—Impulsione a satisfação do cliente oferecendo vários métodos de pagamento, incluindo prestações de pagamento sem juros, e uma única visão do processamento de pagamento, ordens e faturas.

## Visuais do produto

Simplifique o gerenciamento de ativos usando um sistema robusto de gerenciamento de ativos digitais (DAM) que se integra ao Adobe Experience Manager para gerenciar conteúdo de mídia avançada. Como alternativa, o miniDAM nativo fornece ferramentas básicas de gerenciamento de ativos para armazenar e gerenciar ativos digitais.

Consulte [gerenciamento de ativos](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration) para saber mais.

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

Os desenvolvedores podem usar as abrangentes [APIs do GraphQL e REST](https://developer.adobe.com/commerce/services/cloud/guides/) para integrar o Commerce Foundation a sistemas de terceiros e estender os recursos do Commerce.

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

## Novas soluções de recursos

A [Interface do Administrador](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/guide-overview) é a principal interface para acessar recursos para gerenciar operações de armazenamento de back-end, inventário, preços, promoções e interações com o cliente. No entanto, o [!DNL Adobe Commerce as a Cloud Service] oferece soluções exclusivas que substituem alguns dos recursos conhecidos disponíveis no Adobe Commerce em nuvem e em projetos locais. A tabela a seguir descreve os recursos e as soluções de substituição disponíveis no [!DNL Adobe Commerce as a Cloud Service]:

| Recurso | Solução | Disponibilidade | Detalhes |
|---------|----------|--------------|--------|
| [Gerenciamento de ativos digitais](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management) | [Visuais de Produto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration) ou miniDAM | Disponível | Um sistema robusto de gerenciamento de ativos digitais (DAM) que se integra ao Adobe Experience Manager para gerenciar conteúdo de mídia avançada. Como alternativa, o miniDAM fornece ferramentas básicas de gerenciamento de ativos para armazenar e gerenciar ativos digitais. |
| [Sistema de gerenciamento de conteúdo (CMS)](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/guide-overview) | [Commerce Storefront](https://www.aem.live/) | Disponível | Um CMS básico que permite que os usuários criem e gerenciem documentos e conteúdo de sites facilmente usando a criação baseada em documentos. Como alternativa, um Editor universal que permite um gerenciamento de conteúdo e personalização mais avançados em várias plataformas. |
| [Preparo de conteúdo](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/staging/content-staging) | [Serviço de catálogo](../catalog-service/overview.md) | Roteiro | Uma ferramenta de gerenciamento de catálogos que se vincula ao Adobe Experience Platform, permitindo o gerenciamento de catálogos grandes. |
| [Construtor de páginas](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/page-builder/guide-overview) | [Commerce Storefront](https://www.aem.live/) | Disponível | Um CMS básico que permite que os usuários criem e gerenciem documentos e conteúdo de sites facilmente usando a criação baseada em documentos. Como alternativa, um Editor universal que permite um gerenciamento de conteúdo e personalização mais avançados em várias plataformas. |
| [Pagamentos](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/payments/payments) | [Serviços de pagamento para o Adobe Commerce](../payment-services/guide-overview.md) | Disponível | Um serviço de pagamento integrado que facilita transações seguras e eficientes. |
| [substituições de URL](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite) | [Commerce Storefront](https://www.aem.live/) | Disponível | Um CMS básico que permite que os usuários criem e gerenciem documentos e conteúdo de sites facilmente usando a criação baseada em documentos. Como alternativa, um Editor universal que permite um gerenciamento de conteúdo e personalização mais avançados em várias plataformas. |
| [Merchandiser visual](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser) | [Serviço de catálogo](../catalog-service/overview.md) | Roteiro | Uma ferramenta de gerenciamento de catálogos que se vincula ao Adobe Experience Platform, permitindo o gerenciamento de catálogos grandes. |
