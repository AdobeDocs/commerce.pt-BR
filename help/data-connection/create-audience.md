---
title: Criar um público no Real-Time CDP usando  [!DNL Commerce] dados do evento
description: Saiba como usar os dados do evento  [!DNL Commerce]  para criar um público-alvo no Real-Time CDP
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# Criar públicos no Real-Time CDP usando dados do evento [!DNL Commerce]

Use os dados do evento capturados do seu armazenamento [!DNL Commerce] para criar públicos no Real-Time CDP. Os dados capturados são baseados no comportamento de navegação, compras anteriores, atributos de perfil, tendências de conversão ou churn, status de fidelidade, valor alto e baixo do cliente e muito mais.

## Quais dados devo considerar usar?

Crie públicos-alvo no Real-Time CDP usando dados de eventos da loja, do back office e do perfil.

| Tipos de dados | Dados da vitrine (Eventos comportamentais) | Dados de back office (eventos do lado do servidor) | Perfil do cliente e dados do segmento |
|---|---|---|---|
| **Definição** | Cliques ou ações que os clientes realizam no site. | Informações sobre o ciclo de vida e detalhes de cada pedido (passado e atual). | Quem são seus compradores e para quais segmentos eles se qualificam. |
| **Eventos capturados pelo Adobe Commerce** | [productPageView](events.md#productpageview)<br>[addToCart](events.md#addtocart) | [placeOrder](events.md#completecheckout)<br>[orderplacement](events-backoffice.md#orderplaced)<br>[orderLineItemRefund](events-backoffice.md#orderlineitemrefunded)<br>[Pedido cancelado](events-backoffice.md#ordercancelled)<br>[histórico de pedidos](connect-data.md#send-historical-order-data) | [createAccount](events.md#createaccount)<br>[editAccount](events.md#editaccount)<br>[Registro de perfil](events-profilerecord.md) |

## O que outros clientes conquistaram?

Os clientes do Adobe [!DNL Commerce] obtiveram impactos comerciais significativos ao ativar públicos-alvo incorporados no Real-Time CDP e implantá-los na instância [!DNL Commerce].

Um varejista global de vestuário de várias marcas obteve:

- Uma fonte da verdade com dezenas de milhões de perfis unificados de clientes
- Foram criados mais de 40 públicos-alvo exclusivos de &quot;clientes de alta intenção&quot; para se envolver em vários canais

Uma empresa global de bebidas coletou:

- 98 milhões de perfis de clientes de mais de 100 países

## Vamos começar

Neste artigo, você aprenderá a:

- Crie um público no Real-Time CDP com base nos dados [!DNL Commerce] que os eventos coletam
- Ative esse público para sua loja [!DNL Commerce]
- Usar o público em [!DNL Commerce] para informar uma regra de preço de carrinho

>[!IMPORTANT]
>
>Conclua as tarefas descritas neste artigo usando seu ambiente de sandbox do [!DNL Commerce]. Isso garante que os dados de eventos da loja e do back office enviados à Experience Platform não diluam seus dados de eventos de produção.

### Pré-requisitos

Antes de começar, verifique se:

- Você foi provisionado para usar o Real-Time CDP. Se não tiver certeza, consulte o integrador de sistemas ou a equipe de desenvolvimento que gerencia projetos e ambientes.
- Você [instalou](install.md) e [configurou](connect-data.md) a extensão [!DNL Data Connection] em [!DNL Commerce].
- Você [confirmou](connect-data.md#confirm-that-event-data-is-collected) que os dados do evento [!DNL Commerce] estão chegando à borda do Experience Platform.

### 1. Criar um público-alvo

Um público-alvo é um conjunto de clientes que compartilham comportamento ou características semelhantes. Neste exercício, você cria um público-alvo que qualifica as pessoas interessadas em um produto específico da sua loja.

Para simplificar este exercício, use os dados do evento [productPageView](events.md#productpageview). Este evento captura detalhes sobre o produto visualizado, como nome do produto, SKU, preço, etc.

Use esses dados do evento para especificar que o público-alvo inclui indivíduos que têm pelo menos um evento &quot;Exibições do produto&quot;, no qual o SKU (identificador do produto) é igual a um produto específico do site e o evento ocorre no último dia. &#x200B;

1. Abra o Experience Platform e selecione **[!UICONTROL Audiences]** no menu de navegação esquerdo.

   ![Painel de público-alvo](assets/audience-left-rail.png)

1. Clique em **[!UICONTROL Create Audience]**.

   ![Criar público-alvo](assets/browse-create-audience.png)

   O espaço de trabalho **Construtor de segmentos** é exibido.

1. No espaço de trabalho **Construtor de segmentos**, selecione o método de criação **Regra de compilação**.

   ![Regra de Compilação](assets/build-rule.png)

   O espaço de trabalho do **Construtor de segmentos** é onde você define as regras e condições do seu público-alvo.&#x200B; Essas regras e condições se baseiam nos dados de evento e perfil da loja da Commerce e definem os critérios que determinam se um usuário se qualifica para o público-alvo. Por exemplo, você pode criar uma regra que inclua usuários que visualizaram um produto específico ou usuários que fizeram uma compra em um determinado período. Saiba mais sobre o [Construtor de segmentos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder) e as regras e condições.

1. Selecione a guia [Eventos](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/segment-builder#events).

   ![Guia Eventos](assets/audience-events-tab.png)

1. Procure o tipo de evento &quot;Exibições de produto&quot;. Em seguida, arraste e solte-o no espaço de trabalho **Construtor de segmentos**.

1. Retorne à guia **Eventos** e procure por &quot;SKU&quot;, que é o campo de dados sob o campo `productListItems`. Arraste e solte-o no espaço de trabalho do **Construtor de segmentos** sobre o evento **Exibição do produto**.

   A seção **Regras de evento** exibe onde você pode especificar o produto específico do qual deseja criar seu público-alvo.

   ![Selecionar SKU](assets/audience-addsku.png)

1. Defina o intervalo de tempo como um dia, clicando em **A Qualquer Momento** e selecionando *Em último* com um valor de *1*.

   Ao criar um público-alvo, você pode especificar um intervalo de tempo para capturar a atividade recente. Definir um intervalo de tempo permite direcionar os usuários com base em suas interações ou comportamentos recentes em um período específico.

1. Na seção **Propriedades do público-alvo** no lado direito do espaço de trabalho, defina as propriedades do público-alvo fornecendo um nome, uma descrição e um método de avaliação para o público-alvo.

1. Para salvar o público, clique em **[!UICONTROL Save and Close]**.

   Os detalhes do seu público são exibidos no painel **Público**.

### 2. Ativar o público para o destino [!DNL Commerce]

Você disponibiliza um público-alvo no [!DNL Commerce] ativando-o para o destino [!DNL Commerce].

>[!IMPORTANT]
>
>Se você ainda não definiu [!DNL Commerce] como um destino disponível para receber dados, consulte o tópico [Adobe [!DNL Commerce] Conexão](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/personalization/adobe-commerce).

1. Na guia **Detalhes** do público-alvo, clique em **Ativar para destino**.

1. Selecione o destino [!DNL Commerce]. Em seguida, clique em **Avançar**.

1. Conclua o processo de ativação clicando em **[!UICONTROL Finish]**.

## 3. Exibir o público-alvo no Painel de públicos-alvo

No [!DNL Commerce], você pode exibir todos os [públicos-alvo ativos](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) que podem ser personalizados para sua instância do [!DNL Commerce] usando o painel **Públicos-alvo do Real-Time CDP**.

Para acessar o painel **Públicos-alvo do Real-Time CDP**, vá para a barra lateral _Admin_ e, em seguida, vá para **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**.

No painel, procure pelo público-alvo criado. Observe que ela não está sendo usada em uma regra de preço do carrinho ou em um bloco dinâmico. Na próxima seção, vincule o público-alvo a uma regra de preço do carrinho.

![Painel de Públicos-Alvo do Real-Time CDP](assets/real-time-cdp-dashboard.png)

### 4. Criar uma regra de preço do carrinho com base no público-alvo

Esta seção mostra como criar uma regra de preço de carrinho com base no novo público-alvo.

1. Confirme se o novo público-alvo é exibido no painel **Públicos-alvo da Real-Time CDP**.
1. [Criar uma regra de preço de carrinho](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create).
1. [Defina a condição](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition) da regra de preço do carrinho usando seu novo público-alvo.
1. [Defina a ação](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions) que você deseja que ocorra quando o produto for adicionado ao carrinho.
1. Continue a configurar a regra de preço do carrinho.
1. Acesse a visualização do cliente da instância da sandbox.
1. Adicione o produto no qual você baseou o público-alvo do ao carrinho. Observe que a regra de preço do carrinho está ativada.

## Encerrar

Neste exercício, você criou um público no Real-Time CDP e o ativou para o destino [!DNL Commerce]. Em seguida, no administrador [!DNL Commerce], você criou uma regra de preço do carrinho com base nesse público-alvo e habilitou a regra no ambiente de sandbox.
