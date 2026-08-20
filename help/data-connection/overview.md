---
title: Introdução ao [!DNL Data Connection]
description: Saiba como integrar dados do Adobe Commerce com o Adobe Experience Platform usando a extensão  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
TQID: https://experienceleague.adobe.com/-wfkGM2isTVmAaJokndxVy0-UtZ4pM9msYXmh2IE-Hc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 494033dc2367b0e2914494ee44cec7c6b45209f1
workflow-type: tm+mt
source-wordcount: 1399
ht-degree: 0%

---

# Introdução ao [!DNL Data Connection]

>[!IMPORTANT]
>
>O conector do Experience Platform foi renomeado para [!DNL Data Connection].

A extensão [!DNL Data Connection] conecta a instância da Web do Adobe Commerce à Adobe Experience Platform e à Edge Network. Para desenvolvedores de aplicativos móveis, você usa o Adobe Experience Platform Mobile SDK com Commerce para capturar e enviar dados do Commerce para o Experience Platform. [Saiba mais](./mobile-sdk-epc.md).

Os comerciantes de vários sites podem definir as configurações aplicáveis do [!DNL Data Connection] por site, incluindo a seleção da sandbox do Experience Platform. Consulte [Conectar dados do Commerce ao Adobe Experience Platform](connect-data.md#configuration-scope) para campos globais versus de escopo de site.

Sua loja Commerce contém uma grande quantidade de dados. As informações sobre como seus compradores navegam, visualizam e compram os produtos em seu site podem revelar oportunidades para criar uma experiência de compra mais personalizada. Embora esses dados possam informar recursos nativos do Commerce, como regras de preço do carrinho e blocos dinâmicos, os dados permanecem em silos na instância do Commerce.

A Adobe Experience Platform fornece um conjunto de tecnologias que, quando hidratadas com os dados da sua loja Commerce, podem distribuir esses dados por meio da Edge Network para outros produtos Adobe DX, a fim de desbloquear insights sobre o comportamento de compra do seu comprador. Com esses insights profundos, você pode criar uma experiência de compras mais personalizada em todos os canais.

A imagem a seguir mostra como os dados do Commerce fluem de sua loja para outros produtos Adobe DX quando a extensão [!DNL Data Connection] é instalada e configurada.

![Como os dados fluem para a borda do Experience Platform](assets/commerce-edge.png)

Na imagem acima, seus dados comportamentais, de back office e de perfil do cliente são enviados para a borda do Experience Platform usando uma SDK, uma API e um conector de origem. Não é necessário entender totalmente como essas partes funcionam, pois a extensão lida com a complexidade do compartilhamento de dados para você. Quando os dados do evento estiverem na borda, você poderá usá-los em produtos Adobe DX downstream, como o [Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview), [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2c-overview/cja-overview), [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/analyze/admin-overview/analytics-overview) e [Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/get-started/essentials/get-started). Para obter exemplos guiados, consulte [Usar o Adobe Journey Optimizer para enviar um email de carrinho abandonado](using-ajo.md) e [Criar um público no Real-Time CDP usando os dados de evento do Commerce](create-audience.md).

## Enviar dados do Experience Platform de volta para o Commerce

Enviar os dados do Commerce para a Experience Platform usando a extensão [!DNL Data Connection] é um lado dos recursos de compartilhamento de dados da Commerce. O outro lado, que é uma extensão opcional, é chamado [Audience Activation](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/audience-activation). Essa extensão permite criar públicos-alvo no Real-Time CDP e implantá-los na Commerce Store para informar as regras de preço do carrinho, as regras de produto relacionadas e os blocos dinâmicos.

Em um alto nível, o fluxo de dados do armazenamento do Commerce para a Experience Platform e de volta pela extensão do Audience Activation é semelhante ao seguinte:

![[!DNL Data Connection] fluxo](assets/data-connection.png)

Após configurar a conexão entre o Commerce e o Experience Platform e entre o Experience Platform e o Commerce, os dados continuam a fluir. Você não precisa se reconectar, a menos que isso seja exigido por uma atualização.

## Conceitos

O compartilhamento de dados entre esses dois sistemas requer a compreensão de vários conceitos.

- **Tipos de dados** — [!DNL Data Connection] coleta dados **comportamentais (vitrine)** do navegador, dados do **back office** de servidores da Commerce e dados do **perfil**. A coleção de vitrines de rótulos de administrador **Eventos de vitrines**. Consulte [Tipos de dados do Commerce](data-ingestion.md) para obter a taxonomia completa.

- **Dados comportamentais (vitrine)** — Capturados das interações do comprador no site, como `addToCart`, `pageView`, `startCheckout` e `completeCheckout`. Consulte [eventos de vitrine](events.md#storefront-events).

- **Dados do back office** — capturados em servidores Commerce, incluindo [status do pedido](events-backoffice.md#order-status) eventos como [`orderPlaced`](events-backoffice.md#orderplaced) e [`orderShipped`](events-backoffice.md#ordershipmentcompleted). Consulte [eventos de back office](events-backoffice.md).

- **Registros de perfil** — Dados de instantâneo enviados quando um perfil de comprador é criado no Commerce. Consulte [registros de perfil](events-profilerecord.md) e [Atualizar esquema de registro de perfil](profile-data.md).

- **Eventos de perfil** — Eventos de série temporal para alterações de ciclo de vida de perfil no servidor. Consulte [eventos de perfil do cliente](events-backoffice.md#customer-profile-events).

- **Experience Platform e Edge Network** - O data warehouse da maioria dos produtos Adobe DX. Os dados enviados para a Experience Platform são propagados para os produtos Adobe DX por meio da Experience Platform Edge Network. Por exemplo, você pode iniciar o Journey Optimizer, recuperar seus dados de evento específicos do Commerce da borda e criar um email de carrinho abandonado no Journey Optimizer. O Journey Optimizer pode enviar esse email se houver carrinhos abandonados na loja do Commerce. Saiba mais sobre o [Experience Platform e o Edge Network](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/web-sdk/overview).

- **Esquema** - O esquema descreve a estrutura dos dados que estão sendo enviados. Antes que o Experience Platform possa assimilar seus dados do Commerce, você deve compor um esquema para descrever a estrutura dos dados e fornecer restrições para o tipo de dados que pode estar contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema. O esquema usa a estrutura XDM, que todos os produtos Adobe DX podem ler. O esquema garante que os dados enviados para a Experience Platform sejam compreendidos em todos os produtos DX. Saiba mais sobre [esquemas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home).

- **Conjunto de dados** - Uma construção de armazenamento e gerenciamento para uma coleção de dados, geralmente uma tabela que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados. Todos os dados assimilados com sucesso na Adobe Experience Platform estão contidos em conjuntos de dados. Saiba mais sobre [conjuntos de dados](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/overview).

- **Sequência de dados** - ID que permite que os dados fluam do Adobe Experience Platform para outros produtos Adobe DX. Essa ID deve ser associada a um site específico em sua instância específica do Adobe Commerce. Ao criar esse fluxo de dados, especifique o esquema XDM criado acima. Saiba mais sobre [datastreams](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview).

## Arquitetura com suporte

A extensão [!DNL Data Connection] está disponível nas seguintes arquiteturas:

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/cif-storefront/integrations/aep)

>[!BEGINSHADEBOX]

## Pré-requisitos

Para usar a extensão [!DNL Data Connection], você deve ter o seguinte:

- Adobe Commerce 2.4.4 ou mais recente
- Adobe ID e ID da organização
- [ACDL (Adobe Client Data Layer)](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/client-data-layer/overview), que é necessária para coletar dados do evento de vitrine
- Qualificações para outros produtos Adobe DX.

>[!ENDSHADEBOX]

## Ativar a extensão {#enable-extension}

Em um nível superior, habilitar a extensão [!DNL Data Connection] envolve as seguintes etapas:

1. [Instalar](install.md) a extensão [!DNL Data Connection].
1. [Entre](https://helpx.adobe.com/manage-account/using/access-adobe-id-account.html) com sua conta da Adobe e [exiba para confirmar](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) sua ID da organização. A ID da organização é a ID associada à empresa provisionada pela Experience Cloud. A ID é uma sequência de 24 caracteres alfanuméricos seguidos por (e deve incluir) `@AdobeOrg`.
1. Verifique se você tem [permissão para a coleta de dados no Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/collection/permissions).
1. Revise os [tipos de dados](data-ingestion.md) que você pode coletar e enviar.
1. Crie ou atualize seu [esquema de evento de série temporal](update-xdm.md) ou [esquema de dados de registro de perfil](profile-data.md) com grupos de campos específicos do Commerce.
1. [Crie um conjunto de dados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform#create-a-dataset) com base no esquema que você criou ou atualizou. Esse conjunto de dados contém os dados do Commerce enviados para o Experience Platform Edge.
1. [Crie uma sequência de dados](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview) e selecione o esquema XDM que contém os grupos de campos específicos do Commerce.
1. [Conecte-se aos Serviços Commerce](../landing/saas.md).
1. [Conectar-se ao Adobe Experience Platform](connect-data.md).

O restante deste guia o guiará por todas essas etapas com mais detalhes para que você possa se atualizar e começar a usar o poder dos produtos Adobe DX na sua loja Commerce.

>[!NOTE]
>
>Para desenvolvedores móveis, saiba como [integrar](./mobile-sdk-epc.md) o Adobe Experience Platform Mobile SDK ao Commerce.

## Disponibilidade para HIPAA

A extensão [!DNL Data Connection] permite compartilhar dados de back office do [!DNL Commerce] com a Experience Platform e manter a conformidade com a HIPAA. [Saiba mais](hipaa-readiness.md).

## Público-alvo

Este guia foi projetado para o comerciante do Adobe Commerce que deseja enriquecer e personalizar sua loja da Commerce para aprimorar a experiência de compras dos clientes.

## Suporte

Se você precisar de informações ou tiver dúvidas que não são abordadas neste guia, use os seguintes recursos:

- [Central de ajuda](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview){target="_blank"}
- [Tíquetes de suporte](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case){target="_blank"} — Envie um tíquete para receber ajuda adicional.
