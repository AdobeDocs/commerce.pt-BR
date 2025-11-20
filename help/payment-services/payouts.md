---
title: Relatório de pagamentos
description: Use o relatório de Pagamentos para obter total transparência no valor do pagamento, no volume processado e em relatórios detalhados no nível da transação para reconciliação financeira.
role: User
level: Intermediate
exl-id: f3f99474-cd28-4c8f-b0ea-dca8e014b108
feature: Payments, Checkout, Paas, Saas
source-git-commit: a0f9ddbf3d0f291855cb51fd70a782c48b8efc6c
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# Relatório de pagamentos

O [!DNL Payment Services] for [!DNL Adobe Commerce] e [!DNL Magento Open Source] oferece relatórios abrangentes para você ter uma visão clara das transações, ordens e pagamentos da sua loja.

Há duas visualizações de relatórios de Pagamentos disponíveis para permitir que você veja informações detalhadas sobre todos os seus pagamentos:

* **[Visualização de dados de pagamentos](#payouts-data-visualization-view)** — Gráfico disponível na Página Inicial dos Serviços de Pagamento que é uma representação visual dos valores agregados por dia da visualização de relatório de Pagamentos
* **[Exibição do relatório de pagamentos](#payouts-report-view)** — Relatório disponível em Pagamentos que mostra informações detalhadas sobre o pagamento de todas as transações

As visualizações de Pagamentos mostram rapidamente informações abrangentes sobre o pagamento, permitindo total transparência sobre o valor do pagamento, o volume processado e relatórios detalhados sobre o nível da transação para reconciliação financeira.

Você pode [baixar transações de pagamento](#download-transactions) em um formato de arquivo .csv para uso em software de contabilidade ou gerenciamento de pedidos existente.

>[!NOTE]
>
>Os relatórios de pagamentos mostram apenas pedidos capturados (a ação de pagamento está definida como [`Authorize and Capture`](https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/get-started/production.html?lang=pt-BR#set-payment-services-as-payment-method)) ou [marcados como `Invoiced`](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice).

## Visualização de visualização de dados de pagamentos

A visualização de dados de Pagamentos está disponível na Página inicial dos Serviços de pagamento. É uma representação visual dos valores agregados por dia da [exibição detalhada do relatório de Pagamentos](#payouts-report-view).

Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** para ver o gráfico de visualização de dados de créditos vs. débitos e as médias móveis ao longo do tempo.

![Visualização de dados de pagamento no Administrador](assets/payouts-report.png){width="800" zoomable="yes"}

Clique em **[!UICONTROL View Report]** para navegar até a [exibição detalhada do relatório de Pagamentos](#payouts-report-view).

### Personalizar período de transações

Por padrão, 30 dias de transações são exibidos.

Na visualização de dados de Pagamentos, é possível personalizar o período das transações de pagamento que deseja exibir, selecionando um intervalo de datas:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**. A visualização de dados dos Pagamentos está visível na seção Pagamentos.
1. Clique no filtro seletor **[!UICONTROL Range]**.
1. Escolha o intervalo de datas aplicável: 30 dias, 15 dias ou 7 dias.
1. Exibir as informações de transações para as datas especificadas.

### Informações de transações

Os valores de transação para um intervalo de datas selecionado são mostrados à esquerda da visualização de dados de Pagamentos. As datas do intervalo de datas selecionado são mostradas na parte inferior da exibição. Se não houver pagamentos em uma data específica, essa data não será exibida.

A visualização de visualização de dados dos Pagamentos inclui as seguintes informações.

| Dados | Descrição |
| ------------ | -------------------- |
| [!UICONTROL Transaction amount] | Intervalo de valores para transações no intervalo de tempo especificado; dados no eixo Y (à esquerda) |
| Intervalo de datas | Intervalo de datas para o intervalo de tempo especificado; dados no eixo X (inferior) |
| Crédito | Pagamentos no prazo especificado |
| Débito | Débitos (reembolsos) para o período de tempo especificado |
| Média móvel | Representação do pagamento médio para cada data no período especificado |
| Líquido para intervalo | Valor líquido de pagamento para o período de tempo especificado (intervalo) |

## Exibição do relatório de pagamentos

A visualização de relatório Pagamentos está disponível na visualização Pagamentos dos Serviços de pagamento. Ele inclui todas as informações disponíveis sobre pagamentos para sua(s) loja(s).

Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**&#x200B;para ver a exibição detalhada do relatório de Pagamentos em tabelas.

![Transações de pagamento no Administrador](assets/payouts-report-new.png){width="800" zoomable="yes"}

É possível configurar essa visualização, de acordo com as seções neste tópico, para apresentar melhor os dados que você deseja ver.

Consulte IDs de ordem e transação vinculadas do Commerce, valores da transação, método de pagamento por transação e muito mais, tudo nesse relatório.

Você pode [baixar transações de pagamento](#download-transactions) em um formato de arquivo .csv para uso em software de contabilidade ou gerenciamento de pedidos existente.

>[!NOTE]
>
>Os dados mostrados nesta tabela são classificados em ordem decrescente (`DESC`) por padrão usando o `TRANS DATE`. O `TRANS DATE` é a data e a hora em que a transação foi iniciada.

### Selecionar fonte de dados

Na exibição de relatório de Pagamentos, você pode selecionar a fonte de dados—**[!UICONTROL Live]** ou **[!UICONTROL Sandbox]**—para a qual deseja ver os resultados do relatório.

![Seleção de fontes de dados](assets/datasource.png){width="300" zoomable="yes"}

Se _[!UICONTROL Live]_&#x200B;for a fonte de dados selecionada, você poderá ver informações do relatório de armazenamentos no modo de produção. Se&#x200B;_[!UICONTROL Sandbox]_ for a fonte de dados selecionada, você poderá ver os armazenamentos de informações do relatório no modo sandbox.

As seleções de fonte de dados funcionam da seguinte maneira:

* Se você não tiver armazenamentos que estejam no modo Online, a seleção da fonte de dados assumirá _[!UICONTROL Sandbox]_&#x200B;como padrão.
* Se você tiver armazenamentos (um ou vários) no modo Online, a seleção da fonte de dados assumirá _[!UICONTROL Live]_&#x200B;como padrão.
* As exportações de relatórios sempre seguem a seleção da fonte de dados.

Para selecionar a origem de dados para o relatório de Status de Pagamento da Ordem:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. Clique em **[!UICONTROL Data source]** e selecione **[!UICONTROL Live]** ou **[!UICONTROL Sandbox]**.

   Os resultados do relatório são gerados novamente com base na fonte de dados selecionada.

### Exibir transações

Por padrão, 30 dias de transações são exibidos.

O número de linhas retornado em uma pesquisa, ou mostrado no padrão de 30 dias de transações, é mostrado acima da grade de exibição Pagamentos ao lado do filtro seletor de calendário de datas da transação.

Role para a esquerda e para a direita para exibir [informações de cada transação de pagamento](#column-descriptions) no relatório diário, incluindo a data da transação, a ID de referência, o número da fatura e os detalhes do método de pagamento.

#### Personalizar período de transações

Na exibição do relatório de Pagamentos, é possível personalizar o período das transações de pagamento que deseja exibir, informando datas específicas ou selecionando um intervalo de datas no seletor de datas:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. Clique no filtro seletor de calendário _[!UICONTROL Transaction dates]_.
1. Escolha o intervalo de datas aplicável.
1. Exiba os status de pagamentos na grade para as datas especificadas.

### Mostrar e ocultar colunas

A visualização de relatório de Pagamentos mostra a maioria das colunas de informações disponíveis por padrão. No entanto, você pode personalizar quais colunas verá no relatório.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. Clique no ícone _Configurações de coluna_ (![ícone de configurações de coluna](assets/column-settings.png){width="20" zoomable="yes"}).
1. Para personalizar quais colunas você vê no relatório, marque ou desmarque as colunas na lista.

   A visualização de relatório de Pagamentos mostrará imediatamente quaisquer alterações feitas no menu Configurações de coluna. As preferências de coluna serão salvas e permanecerão em vigor se você sair da exibição de relatório.

### Baixar transações

É possível baixar um arquivo .csv contendo todas as transações visíveis na grade de exibição de Pagamentos.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Payouts]_>**[!UICONTROL View Report]**.
1. [Personalize o período do intervalo de datas para suas transações](#customize-transactions-timeframe).
1. Clique no ícone _Download_ ( ![Ícone de download](assets/icon-download.png){width="20" zoomable="yes"} ).

Suas transações de pagamento são baixadas em um formato .csv.

### Descrições da coluna

Os relatórios de pagamento incluem as seguintes informações.

| Coluna | Descrição |
| ------------ | -------------------- |
| [!UICONTROL Provider] | Provedor de pagamento |
| [!UICONTROL Provider trans] | ID da transação |
| [!UICONTROL Trans date] | Data e hora em que a transação foi iniciada |
| [!UICONTROL Type] | Tipo de transação—*[!UICONTROL PAYMENT]*, *[!UICONTROL BONUS]*, *[!UICONTROL CHARGEBACK]*, *[!UICONTROL CORRECTION]*, *[!UICONTROL CURRENCY_CONVERSATION]*, *[!UICONTROL DEPOSIT]*, *[!UICONTROL DISBURSEMENT]*, *[!UICONTROL DISPUTE]*, *[!UICONTROL FEES]*, *[!UICONTROL HOLD]*, *[!UICONTROL HOLD_RELEASE]*, *[!UICONTROL INCENTIVES]*, *[!UICONTROL OTHERS]*, *[!UICONTROL RECOUP]*, *[!UICONTROL REFUND]*, *[!UICONTROL REVERSAL]*, *[!UICONTROL WITHDRAWAL]* <br> <br>Consulte [Tipos de transação](#transaction-types) para obter mais informações. |
| [!UICONTROL Status] | Status atual da transação—*[!UICONTROL SUCCESS]*, *[!UICONTROL DENIED]*, *[!UICONTROL PENDING]* |
| [!UICONTROL Code] | Código de transação que indica Crédito (*CR*) ou Débito (*DR*) |
| [!UICONTROL Reference ID] | ID da transação original para a qual este evento está relacionado |
| [!UICONTROL Invoice] | ID da fatura (uma por pedido) da transação |
| [!UICONTROL Commerce order] | ID do pedido Commerce <br> <br>Para ver as [informações do pedido](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/order-management/orders/orders) relacionadas, clique na ID. |
| [!UICONTROL Commerce trans] | ID de transação do Commerce |
| [!UICONTROL Pay method] | Tipo de cartão de crédito—*[!UICONTROL BANK]*, *[!UICONTROL PAYPAL]*, *[!UICONTROL CREDIT_CARD]*—e provedor de cartão associado (como *Visa* ou *MasterCard*) |
| [!UICONTROL TRANS AMT] | Valor da transação |
| [!UICONTROL CUR] | Unidade monetária para valor da transação |
| [!UICONTROL PENDING] | Valor a ser desembolsado |
| [!UICONTROL CUR] | Unidade monetária para o valor pendente |
| [!UICONTROL SELLER AMT] | Quantidade de fundos transferidos de ou para um cliente <br> <br>Os fundos que saem da conta do vendedor mostram um prefixo de traço (-). |
| [!UICONTROL CUR] | Unidade monetária para o valor do vendedor |
| [!UICONTROL PARTNER FEE] | Taxas de parceiro associadas à transação <br> <br>Os fundos que saírem da conta de taxas do parceiro mostram um prefixo de traço (-). |
| [!UICONTROL CUR] | Unidade monetária da taxa do parceiro |
| [!UICONTROL PROV FEES] | Taxas associadas à transação <br> <br>Os fundos que saírem da conta de tarifas do provedor mostrarão um prefixo de traço (-). |
| [!UICONTROL CUR] | Unidade monetária para a taxa do provedor |
| [!UICONTROL FEE %] | Porcentagem do valor da transação cobrado como uma taxa |
| [!UICONTROL FIXED FEE] | Valor da taxa fixa do provedor |
| [!UICONTROL CHBK FEE] | Taxa de cobrança retroativa associada à transação <br> <br>Um prefixo de traço (-) indica que a taxa de cobrança retroativa foi revertida. |
| [!UICONTROL CUR] | Unidade monetária para a taxa de substituição de débito |
| [!UICONTROL HOLD AMT] | Valor suspenso ou liberado da suspensão <br> <br>Um prefixo de traço (-) indica que os fundos em espera estão sendo liberados. |
| [!UICONTROL CUR] | Unidade monetária para o valor de retenção |
| [!UICONTROL RECOUP AMT] | Valor recuperado da conta de recuperação <br> <br>Os fundos transferidos da conta de recuperação mostram um prefixo de traço (-). |
| [!UICONTROL CUR] | Unidade monetária para o valor de recuperação |

### Tipos de transação

Esses tipos de transação podem ser observados nas transações de pagamento.

| Relatório | Descrição |
| ------------ | -------------------- |
| [!UICONTROL PAYMENT] | Dinheiro movido entre um comprador e um vendedor para um pedido |
| [!UICONTROL AUTH] | Transações de anulação de autorização e autorização |
| [!UICONTROL BONUS] | — |
| [!UICONTROL CHARGEBACK] | Transações de estorno de taxa de substituição de débito e de taxa de substituição de débito |
| [!UICONTROL CORRECTION] | — |
| [!UICONTROL CURRENCY_CONVERSION] | — |
| [!UICONTROL DEPOSIT] | — |
| [!UICONTROL DISBURSEMENT] | — |
| [!UICONTROL DISPUTE] | — |
| [!UICONTROL FEES] | Transações de reversão de taxas, taxas de pagamento e tarifas do parceiro |
| [!UICONTROL HOLD] | — |
| [!UICONTROL HOLD_RELEASE] | — |
| [!UICONTROL INCENTIVES] | — |
| [!UICONTROL OTHERS] | — |
| [!UICONTROL RECOUP] | Recuperações de contas bancárias ou de perdas |
| [!UICONTROL REFUND] | — |
| [!UICONTROL REVERSAL] | — |
| [!UICONTROL WITHDRAWAL] | — |
