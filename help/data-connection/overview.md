---
title: Visão geral do Guia
description: Saiba como integrar dados do Adobe Commerce com o Adobe Experience Platform usando a extensão  [!DNL Data Connection] .
recommendations: noCatalog
exl-id: 660f9337-cad8-47fb-a959-0770f0fd813c
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 0%

---

# Introdução ao [!DNL Data Connection]

>[!IMPORTANT]
>
>O conector do Experience Platform foi renomeado para [!DNL Data Connection].

A extensão [!DNL Data Connection] conecta a instância da Web do Adobe Commerce à Adobe Experience Platform e à Edge Network. Para desenvolvedores de aplicativos móveis, você usa o Adobe Experience Platform Mobile SDK com Commerce para capturar e enviar dados do Commerce para o Experience Platform. [Saiba mais](./mobile-sdk-epc.md).

Sua loja Commerce contém uma grande quantidade de dados. As informações sobre como seus compradores navegam, visualizam e compram os produtos em seu site podem revelar oportunidades para criar uma experiência de compra mais personalizada. Embora esses dados possam informar recursos nativos do Commerce, como regras de preço do carrinho e blocos dinâmicos, os dados permanecem em silos na instância do Commerce.

A Adobe Experience Platform fornece um conjunto de tecnologias que, quando hidratadas com os dados da sua loja Commerce, podem distribuir esses dados por meio da Edge Network para outros produtos Adobe DX, a fim de desbloquear insights sobre o comportamento de compra do seu comprador. Com esses insights profundos, você pode criar uma experiência de compras mais personalizada em todos os canais.

A imagem a seguir mostra como os dados do Commerce fluem de sua loja para outros produtos Adobe DX quando a extensão [!DNL Data Connection] é instalada e configurada.

![Como os dados fluem para a borda do Experience Platform](assets/commerce-edge.png)

Na imagem acima, seus dados comportamentais, de back office e de perfil do cliente são enviados para a borda do Experience Platform usando uma SDK, uma API e um conector de origem. Não é necessário entender totalmente como essas partes funcionam, pois a extensão lida com a complexidade do compartilhamento de dados para você. Quando os dados do evento estiverem na borda, você poderá puxá-los para outros aplicativos da Experience Platform. Por exemplo:

| Aplicativo | Finalidade | Casos de uso |
|---|---|---|
| [Adobe [!DNL Real-Time CDP]](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR) | Serviço de gerenciamento e segmentação de perfil | **Segmentação do histórico de compras**: os comerciantes podem identificar clientes que compram um item com base em um período específico (mensal, trimestral, anual, etc.). Os comerciantes podem então criar segmentos para esses clientes e direcioná-los para promoções, campanhas e como _parte superior dos dados do funnel_ para clientes potenciais para serviços de assinatura.<br> **Segmentação baseada em categoria**: os comerciantes podem ver qual categoria de produtos foi comprada.<br> **Segmentação baseada em ofertas**: os comerciantes podem identificar clientes que retornam produtos de forma consistente. As ofertas e os descontos dados a eles agora podem ser mais inteligentes. Por exemplo, o frete grátis pode ser removido para um cliente que devolve produtos o tempo todo.<br> **Direcionamento por semelhança**: um _Público-alvo por semelhança_ é uma metodologia adotada por um comerciante para que suas promoções alcancem novas pessoas que possam estar interessadas em seus negócios, pois compartilham características semelhantes às de seus clientes existentes. Segmentos semelhantes podem ser criados com base em dados comportamentais e transacionais.<br> **Propensão do cliente**: as alterações no comportamento do cliente podem ser identificadas como resultado dos perfis mais profundos do cliente que podem ser criados a partir dos dados transacionais. Haverá uma maior confiança na pontuação de propensão, pois há mais dados fluindo para os cálculos, como retornos de produtos e configurações de produtos.<br> **Venda cruzada**: um comerciante pode identificar fortes oportunidades de venda cruzada e venda adicional com base nas informações granulares capturadas no Commerce. |
| [Cliente [!DNL Journey Analytics]](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=pt-BR) | Análise profunda da jornada completa do Commerce | **Tendências sazonais**: um comerciante pode identificar tendências sazonais, o que os ajuda a se preparar para a alteração periódica na demanda de determinados produtos. Além disso, os comerciantes podem identificar mudanças na popularidade geral de qualquer produto ao longo dos anos.<br> **Análise de conversão**: ao saber quando um produto foi comprado, juntamente com o acesso aos eventos de impressão da loja, os comerciantes podem gerar um perfil avançado do cliente para executar a análise de conversão. |
| [Adobe [!DNL Analytics]](https://experienceleague.adobe.com/docs/analytics/analyze/admin-overview/analytics-overview.html?lang=pt-BR) | Análise detalhada do comportamento do cliente e do desempenho da campanha | **Devoluções de pedidos**: os comerciantes podem identificar clientes e os maiores segmentos de clientes que têm um padrão de devolução de produtos. Isso ajuda os comerciantes a melhorarem sua estratégia comercial, à medida que compreendem a aparência do comportamento da base de clientes.<br> **Endereço do pedido**: com base no endereço de entrega, um comerciante pode entender se os pedidos estão sendo feitos pelos próprios clientes ou se é para outro indivíduo ou entidade.<br> **Tendências de sazonalidade**: um comerciante pode identificar tendências sazonais, o que os ajuda a se preparar para a alteração periódica na demanda de determinados produtos. Além disso, os comerciantes podem identificar mudanças na popularidade geral de qualquer produto ao longo dos anos.<br> **Análise de conversão**: ao saber quando um produto foi comprado, juntamente com o acesso aos eventos de impressão da loja, os comerciantes podem gerar um perfil avançado do cliente para executar a análise de conversão. **Observação** o Adobe Analytics dá suporte somente a dados de eventos comportamentais (vitrine). O Adobe Analytics não oferece suporte a dados de eventos transacionais (backoffice). |
| [Adobe [!DNL Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=pt-BR) | Orquestração de campanha entre canais | **jornadas baseadas em comportamento**: os comerciantes podem direcionar um cliente que comprou um celular há dois anos, sugerindo que comprem o novo modelo. Os comerciantes podem criar campanhas e promoções personalizadas para esses clientes e usar a funcionalidade de email e SMS para entrar em contato com o. Além disso, os comerciantes podem usar dados históricos de ordem e comportamento para identificar tendências. Por exemplo, um cliente que comprou um item com uma configuração específica no passado e agora está pensando em comprar o mesmo produto novamente, pode ter sua jornada de compra aprimorada dando visibilidade e acesso às mesmas configurações de produto.<br> **Personalization**: com acesso às informações de perfil do cliente, o [!DNL Journey Optimizer] pode desbloquear jornadas altamente personalizadas, permitindo que comerciantes entrem em contato com clientes em vários canais diferentes.<br> **Novo perfil criado**: emails de boas-vindas e atividades promocionais podem incentivar e influenciar novos clientes em suas jornadas de compras.<br> **Perfil excluído**: os comerciantes podem optar por parar de enviar emails promocionais aos clientes que fecharam suas contas. Como alternativa, os comerciantes também podem criar campanhas para recuperar clientes perdidos. |

## Enviar dados do Experience Platform de volta para o Commerce

Enviar os dados do Commerce para a Experience Platform usando a extensão [!DNL Data Connection] é um lado dos recursos de compartilhamento de dados da Commerce. O outro lado, que é uma extensão opcional, é chamado [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=pt-BR). Essa extensão permite criar públicos-alvo no Real-Time CDP e implantá-los na Commerce Store para informar as regras de preço do carrinho, as regras de produto relacionadas e os blocos dinâmicos.

Em um alto nível, o fluxo de dados do armazenamento do Commerce para a Experience Platform e de volta pela extensão do Audience Activation é semelhante ao seguinte:

![[!DNL Data Connection] fluxo](assets/data-connection.png)

Após configurar a conexão entre o Commerce e o Experience Platform e entre o Experience Platform e o Commerce, os dados continuam a fluir. Você não precisa se reconectar, a menos que isso seja exigido por uma atualização.

## Conceitos

O compartilhamento de dados entre esses dois sistemas requer a compreensão de vários conceitos.

- **Dados** - Os dados compartilhados com a Experience Platform são os dados coletados dos eventos do navegador na sua vitrine eletrônica, dos eventos do back office no servidor e dos dados de registro do perfil. Os eventos de vitrine são capturados das interações dos compradores no site e incluem eventos como `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut`, e assim por diante. Consulte [eventos de vitrine](events.md#storefront-events) para obter a lista completa de eventos de vitrine. Os eventos do lado do servidor ou de back office incluem informações de [status do pedido](events-backoffice.md#order-status), como [`orderPlaced`](events-backoffice.md#orderplaced), [`orderReturned`](events-backoffice.md#orderitemreturncompleted), [`orderShipped`](events-backoffice.md#ordershipmentcompleted), [`orderCancelled`](events-backoffice.md#ordercancelled) e assim por diante. Consulte [eventos de back office](events-backoffice.md) para obter a lista completa de eventos de back office. Os dados de registro do perfil contêm informações quando um novo perfil é criado, atualizado ou excluído. Consulte [dados de registro de perfil](events-profilerecord.md) para saber mais.

- **Experience Platform e Edge Network** - O data warehouse da maioria dos produtos Adobe DX. Os dados enviados para a Experience Platform são propagados para os produtos Adobe DX por meio da Experience Platform Edge Network. Por exemplo, você pode iniciar o Journey Optimizer, recuperar seus dados de evento específicos do Commerce da borda e criar um email de carrinho abandonado no Journey Optimizer. O Journey Optimizer pode enviar esse email se houver carrinhos abandonados na loja do Commerce. Saiba mais sobre o [Experience Platform e o Edge Network](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html?lang=pt-BR).

- **Esquema** - O esquema descreve a estrutura dos dados que estão sendo enviados. Antes que o Experience Platform possa assimilar seus dados do Commerce, você deve compor um esquema para descrever a estrutura dos dados e fornecer restrições para o tipo de dados que pode estar contido em cada campo. Os esquemas consistem em uma classe base e zero ou mais grupos de campos de esquema. O esquema usa a estrutura XDM, que todos os produtos Adobe DX podem ler. O esquema garante que os dados enviados para a Experience Platform sejam compreendidos em todos os produtos DX. Saiba mais sobre [esquemas](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=pt-BR).

- **Conjunto de dados** - Uma construção de armazenamento e gerenciamento para uma coleção de dados, geralmente uma tabela que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados. Todos os dados assimilados com sucesso na Adobe Experience Platform estão contidos em conjuntos de dados. Saiba mais sobre [conjuntos de dados](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=pt-BR).

- **Sequência de dados** - ID que permite que os dados fluam do Adobe Experience Platform para outros produtos Adobe DX. Essa ID deve ser associada a um site específico em sua instância específica do Adobe Commerce. Ao criar esse fluxo de dados, especifique o esquema XDM criado acima. Saiba mais sobre [datastreams](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR).

## Arquitetura com suporte

A extensão [!DNL Data Connection] está disponível nas seguintes arquiteturas:

- PHP/Luma
- [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)
- [AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/aep.html?lang=pt-BR)

>[!BEGINSHADEBOX]

## Pré-requisitos

Para usar a extensão [!DNL Data Connection], você deve ter o seguinte:

- Adobe Commerce 2.4.4 ou mais recente
- Adobe ID e ID da organização
- [ACDL (Adobe Client Data Layer)](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html?lang=pt-BR), que é necessária para coletar dados do evento de vitrine
- Qualificações para outros produtos Adobe DX.

>[!ENDSHADEBOX]

## Etapas de integração

Em um nível superior, habilitar a extensão [!DNL Data Connection] envolve as seguintes etapas:

1. [Instalar](install.md) a extensão [!DNL Data Connection].
1. [Entre](https://helpx.adobe.com/br/manage-account/using/access-adobe-id-account.html) com sua conta da Adobe e [exiba para confirmar](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=pt-BR#concept_EA8AEE5B02CF46ACBDAD6A8508646255) sua ID da organização. A ID da organização é a ID associada à empresa provisionada pela Experience Cloud. A ID é uma sequência de 24 caracteres alfanuméricos seguidos por (e deve incluir) `@AdobeOrg`.
1. Verifique se você tem [permissão para a coleta de dados no Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=pt-BR).
1. Revise os [tipos de dados](data-ingestion.md) que você pode coletar e enviar.
1. Crie ou atualize seu [esquema de evento de série temporal](update-xdm.md) ou [esquema de dados de registro de perfil](profile-data.md) com grupos de campos específicos do Commerce.
1. [Crie um conjunto de dados](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=pt-BR#create-a-dataset) com base no esquema que você criou ou atualizou. Esse conjunto de dados contém os dados do Commerce enviados para o Experience Platform Edge.
1. [Crie uma sequência de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR) e selecione o esquema XDM que contém os grupos de campos específicos do Commerce.
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

- [Central de ajuda](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/overview.html?lang=pt-BR){target="_blank"}
- [Tíquetes de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=pt-BR#submit-ticket){target="_blank"}—Envie um tíquete para receber ajuda adicional.
