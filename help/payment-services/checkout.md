---
title: Check-out em  [!DNL Payment Services]
description: Personalize o check-out do  [!DNL Payment Services]  de acordo com as necessidades do cliente.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---


# Check-out em [!DNL Payment Services]

Você pode configurar o check-out para o Adobe Commerce [!DNL Payment Services] para melhor atender aos seus compradores. Uma funcionalidade como a [anulação automática de pedido](#order-auto-voided-if-error) e a [compartimentalização de cartão de crédito](#credit-card-vaulting) garante que seus compradores tenham uma experiência perfeita para o usuário.

## Pedido anulado automaticamente em caso de erro

Se ocorrer um erro durante o check-out, [!DNL Payment Services] anulará/cancelará automaticamente a ordem.

Uma mensagem de erro é exibida na página de check-out do comprador. A mensagem pode variar.

![Erro ao verificar](assets/user-checkout-error.png "Erro ao fazer check-out"){width="600" zoomable="yes"}

Um comentário sobre o pedido cancelado também é exibido no Admin para um [pedido](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/orders.html?lang=en) específico.

![Comentário de pedido cancelado no Administrador para pedido](assets/admin-checkout-error.png "Comentário de pedido cancelado no Administrador para pedido"){width="600" zoomable="yes"}

Se um comprador obtiver autorização para um pedido, mas o pedido não tiver sido criado e convertido em um `Capture`, o pedido será anulado automaticamente. Esse processo garante que nenhum crédito seja reservado no cartão de crédito do comprador e evita a taxa do provedor de pagamento que ocorre quando a autorização é anulada no final do período padrão de 29 dias.

>[!NOTE]
>
>A anulação automática da ordem só ocorre quando o cliente usa um método de pagamento definido como modo `Authorize`, não modo `Authorize and Capture`.

## Check-out da página do produto

Quando um cliente faz o check-out diretamente da página do produto, usando os botões PayPal ou [!DNL Pay Later], somente o item representado na página do produto atual é comprado. Os itens que já residem no carrinho do cliente não são adicionados ao fluxo de check-out e não são comprados.

Essa função permite que o cliente compre rapidamente o item que está visualizando no momento, enquanto retém os itens adicionados anteriormente ao carrinho.
Se o cliente cancelar o pedido, o item na página do produto atual será adicionado ao carrinho do cliente.

Quando um cliente entra no fluxo de check-out da página do produto, a página de check-out é simplificada — a visualização mostra apenas os dados e as opções relacionados ao pedido.

## Compartimentalização de cartão de crédito

Os compradores podem arquivar (ou &quot;salvar&quot;) suas informações de cartão de crédito para compras futuras no nível do site (qualquer loja na conta do mesmo comerciante).

Consulte [Compartimentalização de cartão de crédito](vaulting.md) para obter mais informações
