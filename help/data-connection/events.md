---
title: Eventos comportamentais
description: Saiba quais dados cada evento comportamental captura.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection] Eventos comportamentais

Veja a seguir uma lista dos eventos comportamentais do Commerce disponíveis ao instalar a extensão [!DNL Data Connection]. Os dados que esses eventos coletam são enviados para a Adobe Experience Platform. Você também pode criar [eventos personalizados](custom-events.md) para coletar dados adicionais não fornecidos imediatamente.

Além dos dados coletados pelos eventos a seguir, você também obtém [outros dados](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=pt-BR) fornecidos pelo Adobe Experience Platform Web SDK.

Os eventos comportamentais coletam dados comportamentais anônimos dos compradores enquanto eles navegam pelo site. Você pode usar os dados que esses eventos coletam para criar promoções e campanhas direcionadas a um conjunto específico de compradores.

>[!NOTE]
>
>Todos os eventos comportamentais incluem o campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=pt-BR), que inclui o endereço de email do comprador, quando disponível, e a ECID.

## Eventos da loja

Os eventos da vitrine eletrônica capturam dados das interações dos compradores no site e incluem eventos como `addToCart`, `pageView`, `createAccount`, `editAccount`, `startCheckout`, `completeCheckout`, `signIn`, `signOut`, e assim por diante. Os eventos da vitrine eletrônica se aplicam apenas a produtos simples e configuráveis.

Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para saber mais sobre os eventos da loja.

## Eventos de perfil do cliente

Os eventos de perfil capturados da loja incluem informações da conta, como `signIn`, `signOut`, `createAccount` e `editAccount`. Esses dados são usados para ajudar a preencher os principais detalhes do cliente necessários para definir melhor os segmentos ou executar campanhas de marketing, como enviar ofertas de desconto de inscrição, confirmações de alterações de conta etc.

Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para saber mais sobre os eventos de perfil do cliente.

## Pesquisar eventos

Os eventos de pesquisa fornecem dados relevantes para a intenção do comprador. O insight tem a intenção de ajudar os comerciantes a ver como eles estão procurando por itens, em que clicam e, por fim, compram ou abandonam os produtos. Um exemplo de como você pode usar esses dados é se quiser direcionar os compradores existentes que pesquisam pelo seu produto principal, mas nunca compram o produto. Você deve instalar a extensão [[!DNL Live Search]](../live-search/install.md) para acessar esses eventos.

Use os campos `searchRequest.id` e `searchResponse.id` encontrados nos eventos `searchRequestSent` e `searchResponseReceived` para fazer referência cruzada de uma solicitação de pesquisa para a resposta de pesquisa correspondente.

Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para saber mais sobre eventos de pesquisa.

## Eventos B2B

![B2B para Adobe Commerce](../assets/b2b.svg) Para comerciantes B2B, você deve [instalar](install.md#install-the-b2b-extension) a extensão `experience-platform-connector-b2b` para acessar esses eventos.

Os eventos B2B contêm informações de [lista de requisições](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html?lang=pt-BR), como se uma lista de requisições tivesse sido criada, adicionada ou excluída de. Ao rastrear eventos específicos para listas de requisição, você pode ver quais produtos seus clientes compram frequentemente e criar campanhas com base nesses dados.

Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) para saber mais sobre eventos B2B.
