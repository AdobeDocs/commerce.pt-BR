---
title: Relatório de Status do Pagamento do Pedido
description: Use o relatório de status de pagamento de Pedido para obter visibilidade sobre o status de pagamento de seus pedidos e identificar possíveis problemas.
role: User
level: Intermediate
exl-id: 192e47b9-d52b-4dcf-a720-38459156fda4
feature: Payments, Checkout, Orders, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '2045'
ht-degree: 0%

---

# Relatório de Status do Pagamento do Pedido

O [!DNL Payment Services] for [!DNL Adobe Commerce] e [!DNL Magento Open Source] oferece relatórios abrangentes para você ter uma visão clara das [transações](reporting.md), pedidos e pagamentos da sua loja.

Há duas exibições disponíveis do relatório de status do pagamento da ordem para permitir que você exiba rapidamente o status do pagamento de suas ordens:

* **[Exibição da visualização do status do pagamento da ordem](#order-payment-status-data-visualization-view)** — Gráfico disponível na Página Inicial dos Serviços de Pagamento que é uma representação visual dos status de pagamento agregados por dia da exibição do relatório de status do pagamento da ordem
* **[Exibição do relatório de status do pagamento da ordem](#order-payment-status-report-view)** — Relatório disponível no status do pagamento da ordem que mostra os status detalhado de pagamento, faturado, remetido, reembolso e contestação de todas as transações

As exibições de status do Pedido de pagamento ajudam você a entender facilmente onde uma ordem específica está dentro do fluxo do processo da ordem para caixa. Esses relatórios permitem visualizar rapidamente os pedidos, com base no status do pagamento e na data do pagamento, e identificar possíveis problemas.

Você pode [baixar os status de pagamento de Pedidos](#download-order-payment-statuses) em um formato de arquivo .csv para uso em software de contabilidade ou gerenciamento de pedidos existente.

>[!NOTE]
>
>Você não pode exibir relatórios financeiros se não tiver [o modo Online integrado e ativado](production.md#enable-live-payments) para [!DNL Payment Services].

## Exibição da visualização de dados do status do pagamento da ordem

A visualização de dados do status do pagamento do pedido está disponível na Página inicial dos Serviços de pagamento. É uma representação visual dos status de pagamento agregados por dia da [exibição detalhada do relatório de status de pagamento da ordem](#order-payment-status-report-view).

Na barra lateral _Admin_, vá para **Vendas** > **Serviços de Pagamento** > _Pedidos_ para ver o [gráfico de status de pagamento](#statuses-information) da visualização de dados.

![Visualização de dados de pagamento no Administrador](assets/orderpayment-dataviz.png){width="800" zoomable="yes"}

Clique em **[!UICONTROL View Report]** para navegar até a [exibição detalhada do relatório de status do pagamento da ordem](#order-payment-status-report-view).

### Personalizar período de status

Por padrão, são exibidos 30 dias de status de pagamento.

Na exibição de visualização do status do pagamento da Ordem, é possível personalizar o período dos status de pagamento que você deseja exibir, selecionando um intervalo de datas:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**. A visualização de dados do status do pagamento do pedido está visível na seção _Pedidos_.
1. Clique no filtro seletor **[!UICONTROL Range]**.
1. Escolha o intervalo de datas aplicável: 30 dias, 15 dias ou 7 dias.
1. Exiba as informações de status das datas especificadas.

### Informações de status

Os status de pagamento de um intervalo de datas selecionado são mostrados à esquerda da visualização de dados Status do pagamento do pedido. As datas do intervalo de datas selecionado são mostradas na parte inferior da exibição. Se não houver pedidos em uma data específica, essa data não aparecerá.

A visualização de dados do status do pagamento do pedido inclui as seguintes informações.

| Dados | Descrição |
| ------------ | -------------------- |
| [!UICONTROL Orders] | Intervalo de valores para ordens no intervalo de tempo especificado; dados no eixo Y (à esquerda) |
| Intervalo de datas | Intervalo de datas para o intervalo de tempo especificado; dados no eixo X (inferior) |
| Autorizado | Pedido autorizado |
| Captura solicitada | Captura solicitada para o pedido |
| Captura confirmada | Captura de pedido concluída |
| Captura parcial | Pedido parcialmente capturado |
| Falha na captura | Falha na captura do pedido |
| Anulado | Pedido anulado |

## Exibição do relatório de status do pagamento da ordem

A visualização do relatório Status do pagamento do pedido está disponível na visualização Início dos Serviços de pagamento. Ele inclui status detalhados — pagamento, faturado, enviado, reembolso, contestação e muito mais — para todas as transações.

Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**para ver a exibição detalhada do relatório de status de pagamento de pedido.

![Transações de status de pagamento de pedido no Administrador](assets/orders-report-data.png){width="800" zoomable="yes"}

É possível configurar essa visualização, de acordo com as seções neste tópico, para apresentar melhor os dados que você deseja ver.

Você pode [baixar transações de pagamento](#download-order-payment-statuses) em um formato de arquivo .csv para uso em software de contabilidade ou gerenciamento de pedidos existente.

>[!NOTE]
>
>Os dados mostrados nesta tabela são classificados em ordem decrescente (`DESC`) por padrão usando o `TRANS DATE`. O `TRANS DATE` é a data e a hora em que a transação foi iniciada.

### Atualizações do status de pagamento

Determinados métodos de pagamento exigem um período para capturar o pagamento. [!DNL Payment Services] agora detecta os status pendentes de uma transação de pagamento em um pedido por:

* Detectando `pending capture` transações de forma síncrona
* Monitorando `pending capture` transações de forma assíncrona

>[!NOTE]
>
>A detecção dos status pendentes das transações de pagamento em uma ordem impede a entrega acidental de ordens se o pagamento ainda não tiver sido recebido. Isso pode ocorrer para transações de Cheque eletrônico e PayPal.

#### Detecção síncrona de transações de captura pendentes

Detectar automaticamente as transações de captura em um status `Pending` e impedir que os pedidos insiram um status `Processing` quando essa transação for detectada.

Durante o check-out do cliente ou quando um administrador cria uma fatura para um pagamento autorizado anteriormente, o [!DNL Payment Services] detecta automaticamente as transações de captura em um status `Pending` e muda as ordens correspondentes para o status `Payment Review`.

#### Monitoramento assíncrono de transações de captura pendentes

Detectar quando uma transação de captura pendente entra em um status `Completed` para que os comerciantes possam retomar o processamento do pedido afetado.

Para garantir que esse processo funcione conforme o esperado, os comerciantes devem configurar um novo trabalho cron. Quando o job estiver configurado para ser executado automaticamente, nenhuma outra intervenção será esperada do comerciante.

Consulte [Configurar trabalhos cron](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs.html). Depois de configurado, o novo trabalho é executado a cada 30 minutos para buscar atualizações para pedidos com status `Payment Review`.

Os comerciantes podem verificar o status de pagamento atualizado por meio da exibição do relatório Status de pagamento da ordem.

### Dados usados no relatório

[!DNL Payment Services] usa dados de pedidos e os combina com dados de pagamentos agregados de outras fontes (incluindo o PayPal) para fornecer relatórios significativos e altamente úteis.

Os dados do pedido são exportados e mantidos no serviço de pagamento. Quando você [altera ou adiciona status de pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-status#custom-order-status) ou [edita uma exibição de loja](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-views#edit-a-store-view), [loja](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/store-details#store-information) ou o nome do site, esses dados são combinados com dados de pagamento e o relatório de status de pagamento de Pedido é preenchido com as informações combinadas.

Há duas etapas neste processo:

1. O índice foi alterado nos dados de `ON SAVE` (sempre que as informações de pedido ou de armazenamento são alteradas) ou `BY SCHEDULE` (em um cronograma cron pré-configurado), dependendo de como ele está configurado no [Gerenciamento de Índice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) no Administrador.

   Por padrão, a indexação de dados ocorre `ON SAVE`, o que significa que sempre que algo for alterado na ordem, no status do pedido, na exibição do armazenamento, no armazenamento ou no site, o processo de reindexação ocorrerá imediatamente.

1. Os dados indexados são enviados para o serviço de pagamento, que é preenchido no relatório Order payment status.

Os únicos dados exportados e agrupados para fins de relatório são os dados usados pelo relatório de status do Pedido de pagamento.

>[!NOTE]
>
>Os dados mostrados nesta tabela são classificados em ordem decrescente (`DESC`) por padrão usando o `ORDER DATE`. O `ORDER DATE` é o carimbo de data e hora de quando o pedido foi criado.

#### Configurar exportação de dados

Embora a reindexação ocorra por padrão no modo `ON SAVE`, é recomendável indexar no modo `BY SCHEDULE`. O índice `BY SCHEDULE` é executado em um cronograma cron de um minuto, e quaisquer dados alterados são exibidos no relatório de status do pedido dentro de dois minutos após qualquer alteração de dados. Essa reindexação programada ajuda a reduzir qualquer esforço na loja, especialmente se você tiver um grande volume de pedidos recebidos, pois isso acontece em um cronograma (não conforme cada pedido é feito).

Você pode alterar o modo do índice—`ON SAVE` ou `BY SCHEDULE`—[no Administrador](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode).

Para saber como configurar a exportação de dados, consulte [Configuração da linha de comando](configure-cli.md#configure-data-export).

### Selecionar fonte de dados

Na exibição do relatório Status de pagamento de pedido, é possível selecionar a fonte de dados—**[!UICONTROL Live]** _ ou **[!UICONTROL Sandbox]**—para a qual você deseja ver os resultados do relatório.

![Seleção de fontes de dados](assets/datasource.png){width="300" zoomable="yes"}

Se _[!UICONTROL Live]_for a fonte de dados selecionada, você poderá ver as informações do relatório de suas lojas que usam [!DNL Payment Services] no modo de produção. Se_[!UICONTROL Sandbox]_ for a fonte de dados selecionada, você poderá ver informações do relatório para o modo sandbox.

As seleções de fonte de dados funcionam da seguinte maneira:

* Se você não tiver armazenamentos que usem [!DNL Payment Services] no modo Online, a seleção da fonte de dados assumirá _[!UICONTROL Sandbox]_como padrão.
* Se você tiver armazenamentos (um ou vários) que usam [!DNL Payment Services] no modo Online, a seleção da fonte de dados assumirá _[!UICONTROL Live]_como padrão.
* As exportações de relatórios sempre seguem a seleção da fonte de dados.

Para selecionar a fonte de dados para seu relatório [!UICONTROL Order Payment Status]:

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Orders]** > **[!UICONTROL View Report]**.
1. Clique no filtro seletor _[!UICONTROL Data source]_e selecione **[!UICONTROL Live]**ou **[!UICONTROL Sandbox]**.

   Os resultados do relatório são gerados novamente com base na fonte de dados selecionada.

### Personalizar período de datas do pedido

Na exibição do relatório Status de pagamento da ordem, você pode personalizar o período dos resultados do status que deseja exibir selecionando datas específicas. Por padrão, 30 dias de status de pedidos de pagamento são mostrados na grade.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Clique no filtro seletor de calendário _[!UICONTROL Order dates]_.
1. Escolha o intervalo de datas aplicável.
1. Exiba os status de pagamento da ordem para as datas especificadas na grade.

### Filtrar informações do relatório

Na exibição do relatório Status de pagamento da ordem, você pode filtrar os resultados dos status que deseja exibir selecionando critérios de filtro.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Clique no seletor **[!UICONTROL Filter]**.
1. Alterne as opções de _Status de Pagamento_ para ver os resultados do relatório somente para os status de pagamento de ordem selecionados.
1. Exibir resultados do relatório dentro de um intervalo de valores de ordem inserindo um _[!UICONTROL Min Order Amount]_ou _[!UICONTROL Max Order Amount_].
1. Clique em **[!UICONTROL Hide filters]** para ocultar o filtro.

### Mostrar e ocultar colunas

O relatório Status do Pagamento da Ordem mostra todas as colunas de informações disponíveis por padrão. No entanto, você pode personalizar quais colunas verá no relatório.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Clique no ícone _Configurações de coluna_ (![ícone de configurações de coluna](assets/column-settings.png){width="20" zoomable="yes"}).
1. Para personalizar quais colunas você vê no relatório, marque ou desmarque as colunas na lista.

   O relatório de status do pagamento da Ordem mostra imediatamente quaisquer alterações feitas no menu de configurações Coluna. As preferências de coluna são salvas e permanecem em vigor se você sair da exibição de relatório.

### Exibir status

A exibição do relatório Status de pagamento da ordem mostra informações abrangentes de status de pagamento para cada ordem.

Por padrão, 30 dias de status de pedidos de pagamento são mostrados na grade.

Role para a esquerda e para a direita para exibir [informações sobre o status do pagamento do pedido](#column-descriptions), incluindo data do pedido, data de autorização, faturado, remetido, status do pagamento e muito mais.

O número de linhas retornadas em uma pesquisa, ou mostradas nos 30 dias padrão de status de pagamento da ordem, é mostrado acima da grade de exibição Status de pagamento da ordem, ao lado do filtro Seletor de calendário de datas da ordem.

#### Status de pagamento

A coluna Status do pagamento mostra o status atual de qualquer pagamento. Um pagamento `Capture failed` mostra um status de alerta vermelho e um pagamento `Voided` mostra um status de alerta cinza.

#### Status do reembolso

A coluna Status da restituição mostra o status atual de qualquer restituição. Um pagamento `Capture failed` mostra um status de alerta vermelho e um pagamento `Voided` mostra um status de alerta cinza.

### Atualizar dados do relatório

A exibição do relatório Status do pagamento da ordem mostra um carimbo de data/hora de _[!UICONTROL Last updated]_que mostra a última vez que as informações do relatório foram atualizadas. Por padrão, os dados do relatório de status de pagamento da ordem são atualizados automaticamente a cada três horas.

Você também pode forçar manualmente uma atualização dos dados do relatório Status de pagamento da ordem para ver as informações mais atualizadas do relatório.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Clique no ícone _Atualizar_ (![ícone de atualização](assets/refresh-button-med.png){width="20" zoomable="yes"}).

   Os dados do relatório Status de pagamento da ordem foram atualizados, uma confirmação *[!UICONTROL Update complete]* é exibida e as informações mais recentes estão presentes na grade.

### Exibir contestações

Você pode visualizar todas as contestações nos pedidos da sua loja e navegar até o Centro de Resolução do PayPal para tomar medidas sobre elas, a partir do relatório Order payment status.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Navegue até **[!UICONTROL Disputes column]**.
1. Exiba todas as contestações de uma ordem específica e consulte [o status da contestação](#order-payment-status-information).
1. Revise os detalhes da contestação no [Centro de Resolução do PayPal](https://www.paypal.com/us/cshelp/article/what-is-the-resolution-center-help246) clicando no link da ID de contestação que começa com _PP-D-_.
1. Tomar as medidas apropriadas para a disputa, conforme necessário.

   Para classificar contestações de ordem por status, clique no cabeçalho da coluna [!UICONTROL Disputes].

### Baixar status de pagamento da ordem

É possível baixar um arquivo .csv com todos os status visíveis na grade de exibição do status do Order payment, seja visualizando os status padrão de 30 dias ou um período personalizado.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Orders]_>**[!UICONTROL View Report]**.
1. Se você quiser ver os status de um período diferente dos últimos 30 dias, [personalize o período de intervalo de datas para seus status](#customize-dates-timeframe).
1. Clique no ícone _Download_ (![ícone de download](assets/icon-download.png){width="20" zoomable="yes"}).

Os status do seu pedido de pagamento são baixados em um formato .csv.

### Descrições da coluna

Os relatórios de status do pagamento da ordem incluem as informações a seguir.

| Coluna | Descrição |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | ID do pedido Commerce<br> <br>Para ver as [informações do pedido](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"} relacionadas, clique na ID. |
| [!UICONTROL Order Date] | Carimbo de data e hora do pedido |
| [!UICONTROL Authorized Date] | Data/carimbo de data/hora da autorização de pagamento |
| [!UICONTROL Order Status] | Status atual do pedido [Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-status){target="_blank"} |
| [!UICONTROL Invoiced] | Status da fatura do pedido—*[!UICONTROL No]*, *[!UICONTROL Partial]* ou *[!UICONTROL Yes]* |
| [!UICONTROL Shipped] | Status de remessa do pedido—*[!UICONTROL No]*, *[!UICONTROL Partial]* ou *[!UICONTROL Yes]* |
| [!UICONTROL Order Amt] | Valor total geral do pedido |
| [!UICONTROL Cur] | Tipo de moeda do pedido |
| [!UICONTROL Pay Status] | Status do pagamento de um pedido específico |
| [!UICONTROL Paid Amt] | Valor pago em um pedido |
| [!UICONTROL Cur] | Tipo de moeda do valor pago em um pedido |
| [!UICONTROL Refund Status] | Status de uma restituição em uma ordem (como informações de devoluções, RMAs e avisos de crédito)—   *[!UICONTROL Requires refund]*, *[!UICONTROL Refund requested]*, *[!UICONTROL Refunded]*, *[!UICONTROL Refund failed]* ou *[!UICONTROL Voided]* |
| [!UICONTROL Refund Amount] | Total do valor reembolsado de um pedido |
| [!UICONTROL Cur] | Tipo de moeda do valor reembolsado de um pedido |
| [!UICONTROL Disputes] | Status de qualquer contestação em um pedido (informações de contestações e substituições de débito)—*[!UICONTROL Open]*, *[!UICONTROL Waiting for buyer response]*, *[!UICONTROL Waiting for seller response]*, *[!UICONTROL Under review]*, *[!UICONTROL Resolved]* ou *[!UICONTROL Other]* |
| [!UICONTROL Payment Method] | Método de pagamento usado na transação do Commerce para uma ordem |
| [!UICONTROL Website] | Site do qual o pedido foi feito |
| [!UICONTROL Store] | Armazenamento no qual o pedido foi feito |
| [!UICONTROL Store View] | Exibição de armazenamento da qual o pedido foi feito |
