---
title: Testar e Implantar Atendimento de Armazenamento
description: Teste um plano para verificar a funcionalidade de Atendimento da Loja. Os testes abrangem a API de sincronização de inventário, o fluxo de trabalho de atendimento completo para pedidos cancelados, o gerenciamento de usuários do aplicativo Store Fulfillment e a experiência de check-in do cliente.
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Testar e Implantar Abastecimento de Armazenamento para Adobe Commerce

Após concluir o processo de integração no ambiente de desenvolvimento, você pode iniciar o processo para testar e implantar a solução Store Fulfillment no ambiente de produção.

**Pré-requisitos**

Antes de testar ou sincronizar quaisquer informações, lojas ou pedidos, verifique se você concluiu as seguintes tarefas:

- Concluída a [Configuração Geral](enable-general.md) para os serviços de Atendimento de Loja.

- [Adicione e valide as credenciais da conta e os detalhes da conexão para seus ambientes de sandbox e produção](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- Confirme se a [Integração do Adobe Commerce](connect-set-up-service.md#configure-store-fulfillment-account-credentials) para a solução de Atendimento da Loja está disponível e autorizada.

## Preparar para teste

A configuração da conexão deve ser concluída antes de criar qualquer pedido de teste ou executar o teste de integração. Antes de testar, você também deve verificar se os dados do armazenamento estão sincronizados.

1. Sincronizar fontes de Abastecimento da Loja.

   - Ir para **[!UICONTROL Stores > Sources]**.

   - Selecione **[!UICONTROL Synchronize Store Fulfillment Sources]**.

1. Na grade de armazenamento, verifique se os armazenamentos foram marcados como `Synced` antes de criar ordens de teste.

## Exemplo de plano de teste

Os varejistas validam a funcionalidade básica da solução Store Fulfillment durante as fases de configuração e teste de uma implantação. Este plano de teste de amostra fornece um ponto de partida para testes. Adicione outros cenários com base em suas necessidades.

>[!NOTE]
>
>Após concluir a integração inicial da solução Store Fulfillment ou atualizar uma instalação existente, sempre teste o aplicativo em um ambiente que não seja de produção antes de implantar na produção.

Este plano de teste de amostra abrange as seguintes áreas funcionais:

| Área funcional | Função | Função |
|-------------------------------------|------------------------------------------|----------------------------------|
| Sincronização de Inventário e Ordem | Sincronização da API de inventário | Administrador do Adobe Commerce |
| De ponta a ponta | Workflows de cancelamento de pedido | Cliente, Administrador, Associado da loja |
| Admin | Permissões do Aplicativo de Abastecimento da Loja | Admin |
| Front-end do Adobe Commerce | Tipos de produto | Cliente, Administrador |
| Check-out front-end</br>Formulário de Check-in | Experiência de check-in | Cliente, Administrador |
| Aplicativo de Assistência da Loja | Pedido</br>Escolher</br>Estágio</br>e Entrega | Armazenar associado |

### Sincronização da API do Inventory

Esta seção do plano de teste aborda a sincronização de estoque e pedido para verificar se as atualizações das fontes de retirada e estoques estão sincronizadas corretamente entre a Adobe Commerce e a solução Store Fulfillment.

**Área Funcional**: Sincronização de Inventário e Pedido</br>
**Função:** Administrador</br>
**Tipo de teste:** todos positivos

<table>
<thead>
<tr>
<th>Função</th>
<th>Cenário de teste</th>
<th>Resultados esperados</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Adicionar origem de estoque de retirada</strong></td>
<td>Salve uma nova origem de estoque de retirada.</td>
<td>A sincronização em tempo real envia os detalhes da origem ao serviço Walmart GIF em 5 minutos.</td>
</tr>
<tr>
<td><strong>Atualizar origem de estoque de retirada existente</strong></td>
<td>Salvar atualizações em uma origem de estoque de retirada existente.</td>
<td>A operação de sincronização em tempo real envia os detalhes para o Walmart GIF em 5 minutos</td>
</tr>
<tr>
<td><strong>Status da origem do estoque de retirada</br><code>Is Synced</code></strong></td>
<td>Salvar atualizações em uma origem de estoque de retirada existente.</td>
<td>Após uma operação bem-sucedida, a coluna <code>Is Synced</code> da página Gerenciar Source atualiza de <code>No</code> para <code>Yes</code>.</td>
</tr>
<tr>
<td><strong>Processo de reserva de estoque modificado</strong></td>
<td>Criar e enviar um novo pedido para um produto.</td>
<td>A quantidade comercializável do produto diminui de forma correspondente.</td>
</tr>
<tr>
<td><strong>Envio de novo pedido, Sincronização de API — Pedido do cliente</strong></td>
<td>O cliente envia uma ordem de retirada de loja.</td>
<td><ul><li>Na exibição do Pedido de administração, um <strong>usuário administrador do Adobe Commerce</strong> vê que o status da Sincronização de pedidos foi atualizado para <code>Sent</code></li><li>O log de detalhes do pedido inclui a mensagem <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Nova Ordem por Push, Sincronização de API — o administrador envia ordem</strong></td>
<td>Um <strong>Administrador</strong> da Adobe Commerce envia uma ordem de retirada.</td>
<td><ul><li>Na exibição Ordem do Administrador, o status da Sincronização de Pedidos é atualizado para <code>Sent</code>.</li><li>O log de detalhes do pedido inclui a mensagem <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Submissão de Novo Pedido, Fila de Exceções<strong></td>
<td>Identifique vários produtos virtuais e baixáveis no Adobe Commerce Admin que possam ser cumpridos por meio da Adobe Commerce sem a necessidade de interação com o Fulfillment service (FaaS).</td>
<td>Esses produtos são removidos ou sinalizados adequadamente na exportação para evitar um conflito downstream com os FaaS.</td>
</tr>
</tbody>
</table>

### Workflows de cancelamento de pedido

Esta seção do plano de teste inclui cenários para testar o workflow completo para pedidos que são cancelados por meio do Adobe Commerce.

**Área funcional:** Administrador do Adobe Commerce</br>
**Função:** Ponta a Ponta (Administrador, Associado da Loja, Cliente)</br>
**Tipo de resultado de teste:** positivo para todos os cenários

<table style="table-layout:fixed">
<tr>
<th>Função</th>
<th>Cenário</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Cancelamento completo do pedido</strong></td>
<td><ol>
<li>Fazer pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique a criação da fatura (se autorizar e capturar) do recebimento do email da fatura.</li>
<li>Criar Aviso de Crédito com todos os produtos solicitados da exibição NFF.</li>
</ol>
</td>
<td>
<ul>
<li>Histórico de pedidos atualizado com <code>We refunded $X online. Transaction ID: transactionID</code> e <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>O status do pedido é <code>Closed</code>. (Definimos agora a ANÁLISE DE PAGAMENTO.)</li>
<li>Memorando de crédito criado no Adobe Commerce. (Aguarde até que o cron funcione.)</li>
<li>Se todos os itens foram separados, o email pronto para retirada <code>DISPLAY COMMENT HISTORY</code> mostra <code>Order is ready for pickup</code> (<code>CUSTOMER NOTIFIED</code> o sinalizador é <code>true</code>.)</li>
<li>Se todos os itens não forem separados, o email de cancelamento e o HISTÓRICO DE COMENTÁRIOS DE EXIBIÇÃO serão exibidos <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> o sinalizador é <code>true</code>.)</li>
</ul>
</td>
</tr>
<tr><td><strong>Cancelamento de Pedido Parcial<strong></td>
<td>
<ol>
<li>Faça o pedido com pelo menos dois produtos.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Aguarde duas horas pela liquidação da transação.</li>
<li>Criar Aviso de Crédito com apenas parte dos produtos solicitados da exibição Fatura.</li>
</td>
<td>
<ul>
<li>Atualização do histórico do pedido: <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>Atualização do histórico do pedido: <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>Recibo de e-mail de reembolso do pedido: <code>$x amount was refunded</code></li>
<li>O status do pedido é <code>Processing</code>.</li>
<li>Memorando de crédito criado no Adobe Commerce (Aguarde até que o cron funcione).</li>
<li>Se alguns itens não foram separados, confirme se o email [!UICONTROL Ready for Pickup] com a seção de separação ou reembolso nulo é exibido. <code>DISPLAY COMMENT HISTORY</code> mostra <code>Order is ready for pickup, but some items not available.</code>.</li>
<li><code>CUSTOMER NOTIFIED</code> o sinalizador é <code>true</code>.</li>
</ul>
</td>
</tr>
<td><strong>Pronto para retirada</br></br>Cancelamento completo</br>(todos os produtos estão definidos como separados com 0 qtd.)</strong></td>
<td>
<ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Vá para a Postman e execute a solicitação Ready for Pickup com todos os produtos definidos como <code>picked</code> com <code>0 qty</code>.</li>
</ol>
</td>
<td>
<ul>
<li>Histórico de pedidos atualizado: <code>We refunded $X offline</code></li>
<li>O status do pedido é <code>CLOSED</code>.
<li>O Aviso de Crédito é criado. (Aguarde até que o cron funcione.)</li>
<li>Email de reembolso recebido: <code>$x amount was refunded</code></li>
<li>Email de cancelamento de pedido enviado.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Pronto para Retirada - Cancelamento parcial</strong></br></br><strong>(Alguns produtos foram separados, e alguns foram separados com <code>0 qty</code>)</strong>
</td>
<td>
<ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Acesse o Postman e execute a solicitação Ready for Pickup com parte dos produtos definidos como separados com 0 e o restante como separados.</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> com [!UICONTROL Ready for Pickup Items] e [!UICONTROL Canceled Items] tabelas. </li>
<li>O status do pedido é PRONTO PARA RETIRADA. </li>
<li>Histórico de pedidos atualizado: <code>We refunded $X offline.</code>
<li>Histórico de pedidos atualizado: <code>Order notified as partly canceled at: Date and hour</code>
<li>Email de reembolso recebido: <code>$x amount was refunded</code>
<li>O memorando de crédito é criado. (Aguarde até que o cron funcione.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Pronto para Retirada - Cancelamento Parcial</br></br>Alguns produtos foram selecionados, e outros com <code>0 qty</code>)</strong>
</td>
<td><ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Acesse o Postman e execute a solicitação Ready for Pickup com parte dos produtos definidos como separados com 0 e o restante como separados.</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> com [!UICONTROL Ready for Pickup Items] e [!UICONTROL Canceled Items] tabelas. </li>
<li>O status do pedido é PRONTO PARA RETIRADA. </li>
<li>Histórico de pedidos atualizado: <code>We refunded $X offline.</code>
<li>Histórico de pedidos atualizado: <code>Order notified as partly canceled at: Date and hour</code>
<li>Email de reembolso recebido: <code>$x amount was refunded</code>
<li>O memorando de crédito é criado. (Aguarde até que o cron funcione.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Dispensado (durante a dispensa) </br></br>Cancelamento completo (todos os produtos foram definidos como rejeitados)</strong>
</td>
<td>
<ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Vá para o Postman e execute a solicitação Ready for Pickup com todos os produtos definidos como selecionados.</li>
<li>Abra sua caixa de correio e localize o email Pronto para recebimento. Em seguida, clique em **[!UICONTROL Confirm Arrival]**.</li>
<li>Check-in.</li>
<li>Vá para o Postman e execute a solicitação Dispensed com todos os produtos definidos como rejeitados.</li>
</ol>
<td><ul>
<li>Histórico de pedidos atualizado: <code>We refunded $X offline.</code></li>
<li>Email de reembolso recebido: <code>$x amount was refunded</code></li>
<li>Status definido como <code>CLOSED</code>.</li>
<li>Aviso de Crédito criado. (Aguarde até que o cron funcione.)</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Dispensado (durante a dispensa)</br></br>Cancelamento Parcial</br>(Alguns produtos são dispensados; alguns são rejeitados.)</strong>
</td>
<td>
<ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Vá para o Postman e execute a solicitação Ready for Pickup com todos os produtos definidos como selecionados.</li>
<li>Abra sua caixa de correio. Localize o email Pronto para Retirada e selecione <code>Confirm Arrival</code>.</li>
<li>Check-in.</li>
<li>Vá para o Postman e execute a solicitação Dispensed com alguns produtos definidos como dispensados e outros como rejeitados</li>
</ol>
</td>
<td>
<li>Histórico de pedidos atualizado: <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>Email de reembolso recebido: <code>$x amount was refunded</code>
<li>Status do Pedido definido como <code>Ready for pickup Dispensed</code>
<li>Aviso de Crédito criado. (Aguarde até que o cron funcione.)</li>
</td>
</tr>
<tr>
<td> <strong>Novo RMA Após retorno (completo)</strong>
</td>
<td>
<ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Se a opção authorize and capture estiver configurada, verifique se a fatura foi criada e se o cliente recebeu o email da fatura.</li>
<li>Escolha todos os produtos com o Postman.</li>
<li>Check-in.</li>
<li>Faça uma dispensa.</li>
<li>Vá para a ordem e selecione<strong>[!UICONTROL Create returns]=
<li>Crie a RMA.</li>
</ol>
</td>
<td>
<ul>
<li>A ADM foi criada e é exibida abaixo da guia <strong>[!UICONTROL Returns]</b> na exibição Pedido.</li>
<li>O cliente recebeu um email de confirmação de RMA.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Novo RMA Após retorno — Parcial</strong>
</td>
<td>
<ol>
<li>Coloque o pedido.</li>
<li>Aguarde até que o pedido seja sincronizado.</li>
<li>Verifique se a fatura foi criada (se autorizar e capturar) e se o email da fatura foi recebido.</li>
<li>Escolha todos os produtos com o Postman.</li>
<li>Check-in.</li>
<li>Faça uma dispensa.</li>
<li>Acesse a ordem e selecione  <strong>[!UICONTROL Create returns]</strong></li>
<li>Crie a RMA com parte dos produtos solicitados.</li>
</ol>
<td>
<ul>
<li>O RMA foi criado e exibido abaixo da guia <strong>[!UICONTROL Returns]</strong> na exibição Pedido.</li>
<li>O cliente recebeu o email de confirmação RMA.</li>
<li>Após criar o RMA, obtenha a autorização do RMA: do Administrador, vá para <strong>[!UICONTROL Sales > Returns]</strong>. Selecione a RMA que você criou e autorize-a.</li>
<li>Verifique se o cliente recebeu o email de confirmação de autorização RMA.</li>
<li>Verifique se o reembolso foi adicionado ao histórico de transações e pedidos.</li>
</ul>
</td>
</tr>
</table>


### Permissões do Aplicativo de Abastecimento da Loja

Esta seção do plano de teste aborda o gerenciamento de conta para Usuários do Aplicativo de Atendimento da Loja.

- Confirme se um associado da loja pode ser autenticado em uma nova conta de usuário criada pelo administrador do Adobe Commerce.
- Confirme se as atualizações das contas existentes foram aplicadas com êxito.

**Área funcional:** Administrador do Adobe Commerce</br>
**Função:** Administrador, Associado da Loja</br>
**Tipo de teste:** Todos positivos

<table style="table-layout:auto">
<tr>
<th>Função</th>
<th>Cenário</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Gerenciamento de Conta de Usuário - Criar Conta</strong></br></br>
</td>
<td>
<ol>
<li><strong>Administrador</strong> — Faça logon no Adobe Commerce Admin</li>
<li>Vá para <strong>[!UICONTROL System] &gt; Permissões do Aplicativo de Atendimento da Loja &gt; Todos os Usuários do Aplicativo de Atendimento da Loja</strong></li>
<li><strong>Adicionar novo usuário.</strong></li>
</ol>
<td>
<ul>
<li>Conta criada com sucesso.</li>
<li>Nova conta de usuário exibida no painel [!UICONTROL Store Fulfillment Users].</li>
<li><strong>Associado da Loja</strong> faça logon no aplicativo de Assistência da Loja com a nova conta de usuário.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Gerenciamento de Conta de Usuário - Atualizar conta de usuário existente</strong>
</td>
<td>
<ol>
<li>Faça logon no Adobe Commerce Admin com a conta de usuário Admin.</li>
<li>Vá para <strong>[!UICONTROL System] &gt; Permissões do Aplicativo de Atendimento da Loja &gt; Todos os Usuários do Aplicativo de Atendimento da Loja</strong>.</li>
<li>Na lista de contas de usuário, abra uma conta de usuário ativa existente selecionando <strong>[!UICONTROL Edit]</strong>.
<li>Desabilite a conta alterando <strong>[!UICONTROL Is Active]</strong> para <strong>Não</strong>.</li>
</ol>
</td>
<td>
<ul>
<li>No painel <strong>[!UICONTROL Store Fulfillment App Users]</strong>, o status da conta atualizada mudou para <strong>[!UICONTROL Inactive]</strong>.</li>
<li>Store Associate não pode fazer logon no aplicativo Store Assist com as credenciais de conta inativas.</li>
</ul>
</td>
</tr>
</table>

## Tipos de produto do Adobe Commerce

Os cenários de teste para Tipos de produto do Adobe Commerce verificam se os clientes veem as informações corretas do produto, do estoque e do método de entrega para diferentes tipos de produto:

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- [!UICONTROL Bundle products] na loja do Adobe Commerce.

**Área funcional:** Front-end do Adobe Commerce</br>
**Função:** Usuário do Aplicativo de Assistência da Loja (Associado da Loja)</br>
**Tipo de teste:** Todos positivos

<table style="table-layout:auto">
<tr>
<th>Função</th>
<th>Cenário</th>
<th>Comentários</th>
</tr>
<tr>
<td><strong>Produtos configuráveis</strong>
</td>
<td>
<ul>
<li>Verifique se o usuário pode visualizar apenas as opções configuráveis, qual origem está ativada, se o estoque está atribuído e se há alguns itens no estoque - verifique os produtos secundários.</li>
<li>Verifique se, ao selecionar um armazenamento diferente, as opções que não estão disponíveis são mostradas riscadas.</li>
<li>Verifique se, se o usuário selecionar um armazenamento diferente, as opções configuráveis não serão selecionadas.</li>
<li>Verifique se um produto configurável já está no carrinho e um usuário seleciona uma loja diferente; o produto é exibido como esgotado.</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>Produtos agrupados</strong>
</td>
<td>
<ul>
<li>Verifique se os métodos de Entrega e o botão [!UICONTROL Add to cart] estão desabilitados para o cliente quando todos os produtos derivados tiverem
<code>qty</code> definido como <code>0</code>.</li>
<li>Verifique se os Métodos de entrega estão habilitados para o cliente quando pelo menos um dos produtos derivados tiver <code>qty</code> definido como <code>0.</code></li>
<li>Verifique se o método [!UICONTROL Store Pickup Delivery] está visível e ativo somente para os produtos que têm [!UICONTROL Available for Store Pickup] habilitado. (Verifique o produto secundário.)</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>Produtos virtuais</strong>
</td>
<td>
Verifique se os produtos virtuais não oferecem o método de entrega [!UICONTROL In-store Pickup].
<td></td>
</td>
</tr>
<tr>
<td><strong>Agrupar produtos</strong>
</td>
<td>
<ul>
<li>Verifique se, se pelo menos um produto derivado tiver [!UICONTROL Available for Store Pickup] desabilitado, a opção de entrega Coleta da Loja não estará disponível para o cliente.</li>
<li>Verifique se, se pelo menos um produto derivado tiver o [!UICONTROL Available for Home Delivery] desabilitado, a opção Entrega Doméstica não estará disponível para o cliente.</li>
<li>Verifique se pelo menos um dos produtos secundários em um pacote está indisponível, o pacote (produto principal) também é mostrado
como [!UICONTROL Out of stock].</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## Experiência de check-in

Esta seção do plano de teste aborda a Experiência de check-in para pedidos de retirada de loja para os seguintes recursos:

- Contato de retirada alternativo — Verifique o fluxo de trabalho para adicionar um [!UICONTROL Alternate Pickup Contact] e selecionar um [!UICONTROL Preferred Contact] em Pedidos de retirada de loja.

- Formulário de check-in — Verifique o fluxo de trabalho para enviar uma solicitação de check-in para ordens de retirada da Loja.

**Áreas funcionais:** Check-out do carrinho, Formulário de check-in para pedidos de retirada de armazenamento</br>
**Função:** Administrador, Cliente, Associado da Loja</br>
**Tipo de teste:** Todos positivos

### Contato de Retirada Alternativo


**Área funcional:** Check-out do carrinho</br>
**Função:** Cliente</br>
**Tipo de teste:** Todos positivos

<table style="table-layout:auto">
<tr>
<th>Função</th>
<th>Cenário</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Contato de Retirada Alternativo</br>
Check-in<strong>
</td>
<td>
Um cliente envia um pedido com a opção Coleta na loja.</td>
<td>Durante o processo de check-out, o cliente vê a opção [!UICONTROL Alternate Pickup Contact] na etapa de envio.
</td>
</tr>
<tr>
<td><strong>Contato Preferencial para Retirada Alternativa, Check-in</strong>
<td>
Um cliente envia um pedido com a opção Coleta na loja. Durante o check-out, o cliente adiciona um [!UICONTROL Alternate Pickup Contact].</td>
<td>Durante o processo de finalização, o cliente vê a opção [!UICONTROL Preferred Contact] na etapa de envio.</td>
</td>
</tr>
<tr>
<td><strong>Detalhes de Contato de Recebimento Alternativo, Check-in</strong>
</td>
<td>
Um cliente envia um pedido com a opção Coleta na loja. Durante o check-out, o cliente seleciona [!UICONTROL Alternate Pickup Contact] na etapa de remessa.
</td>
<td>O cliente vê opções de entrada para inserir detalhes de contato: [!UICONTROL First name], [!UICONTROL Last name], [!UICONTROL Phone] e [!UICONTROL Email].</td>
</tr>
<tr>
<td><strong>Seleção Alternativa, Fazer Check-in no Email</strong>
</td>
<td>Um cliente envia um pedido com a opção Coleta na loja. Durante o check-out, o cliente seleciona [!UICONTROL Alternate Pickup Contact] na etapa de envio, adiciona os detalhes do contato e envia o pedido.</td>
<td>O cliente e o contato alternativo recebem um email de check-in do pedido.</td>
</tr>
<td><strong>Retirada Alternativa, Detalhes do pedido</strong></td>
<td>Um cliente envia um pedido com a opção Coleta na loja. Durante o check-out, o cliente seleciona [!UICONTROL Alternate Pickup Contact] na etapa de envio, adiciona os detalhes do contato e envia o pedido.</td>
<td>O administrador vê as informações adicionais de contato no pedido salvo.</td>
</tr>
<tr>
<td><strong>Contato de Retirada Alternativo, exibição de pedido Associado à Loja</strong>
</td>
<td>Um cliente envia um pedido com a opção Coleta na loja. Durante o check-out, o cliente seleciona [!UICONTROL Alternate Pickup Contact] na etapa de envio, adiciona os detalhes do contato e envia o pedido.</td>
<td>O associado da loja pode ver as informações adicionais de contato do pedido em FaaS/ChaaS.</td>
</td>
</tr>
</tbody>
</table>

### Formulário de check-in


**Área funcional:** Formulário de check-in</br>
**Função:** Cliente</br>
**Tipo de teste:** Todos positivos

<table style="table-layout:auto">
<tr>
<th>Função</th>
<th>Cenário</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Ação de check-in—Enviar solicitação</strong>
</td>
<td>No formulário de check-in, um cliente preenche todos os campos obrigatórios e envia a solicitação.</td>
<td>O cliente recebe uma resposta bem-sucedida.</td>
</tr>
<tr>
<td><strong>Ação de Check-in — Exibir detalhes da solicitação</strong></td>
<td>Um cliente envia uma solicitação de check-in com êxito.</td>
<td>O status do pedido é atualizado no sistema FaaS, e o associado da loja pode ver os detalhes da solicitação de check-in nos FaaS.
</td>
</tr>
<tr>
<td><strong>Ação de Check-in — Enviar solicitação apenas uma vez</strong></td>
<td>Depois de enviar uma solicitação de check-in para um pedido, um cliente seleciona o link para check-in uma segunda vez.</td>
<td>No formulário de Check-in, o cliente não vê uma opção para editar ou reenviar o formulário.</td>
</tr>
<tr>
<td><strong>Check-in Action — Confirmar Chegada</strong></td>
<td>Uma ordem de retirada na loja está marcada como pronta para retirada no FaaS. O cliente recebe um email de Pronto para recebimento e seleciona [!UICONTROL Confirm Arrival].</td>
<td>O cliente vê o formulário de check-in do pedido.</td>
</tr>
</tbody>
</table>

## Aplicativo de assistência da loja

Esta seção do plano de teste aborda cenários para ordem de teste, separação e fluxos de trabalho de entrega no aplicativo Store Assist.

**Área funcional:** Aplicativo de Assistência da Loja</br>
**Função:** Associado do Repositório</br>
**Tipo de teste:** Todos positivos

<table style="table-layout:auto">
<tr>
<th>Função</th>
<th>Cenário</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td>
<strong>Separação de ordem única—caminho feliz, retirada na berma</strong></td>
<td>Separar itens de quantidade única e múltipla. Nenhuma separação nula e retirada na beira do leito (com preparo).
</td>
<td>
</td>
</tr>
<tr>
<td><strong>Separação de vários pedidos — caminho feliz, retirada na beira do passeio</strong></td>
<td>Itens de quantidade única e múltipla. Nenhuma separação nula e retirada na lateral (com preparo)</td>
<td></td>
</tr>
<tr>
<td><strong>Separação de pedido único — escolha de caminho feliz na loja</strong></td>
<td>Itens de quantidade única e múltipla. Nenhuma separação nula e retirada na loja (com preparo)</td>
<td>
</td>
</tr>
<tr>
<td><strong>Separação de vários pedidos — caminho feliz, coleta na loja</strong></td>
<td>Separar itens de quantidade única e múltipla. Nenhuma separação nula e retirada na beira do leito (com preparo).</td>
<td></td>
</tr>
<tr>
<td><strong>Separação de pedido único — caminho não feliz, coleta na loja</strong></td>
<td>Separar itens de quantidade única e múltipla com separação parcial e nula e retirada na loja (com preparo)</td>
</td>
<td></td>
</tr>
<td><strong>Separação de vários pedidos — não é uma escolha feliz na beira do caminho</strong></td>
<td>Separar itens de quantidade única e múltipla com separação parcial e nula e retirada na loja (com preparo)</td>
<td></td>
</tr>
<td><strong>Separação de pedido único — caminho não feliz, retirada na berma</strong></td>
<td>Separar itens de quantidade única e múltipla com separação parcial e nilpick e retirada na borda (com preparo)</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>Ordem feita - cancelada antes da separação</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Pedido feito - cancelado antes da entrega</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Pedido feito - pesquisar no módulo de pedido</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Pedido feito - pesquisa e check-in manual para entrega</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Pedido feito - todos os itens não separados ou não disponíveis marcados pelo seletor</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Pedido feito com itens de pacote - separação e entrega</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Pedido feito - Entregar com rejeição</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Pedido feito - Entrega com rejeição de todos os itens</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## Implantar

Depois de verificar se a solução foi configurada e testada de acordo com suas especificações, você estará pronto para implantar do armazenamento temporário à produção.

A implantação e o teste variam dependendo da infraestrutura e dos recursos.

>[!TIP]
>
>Para obter diretrizes de implantação, listas de verificação e práticas recomendadas para o Adobe Commerce em projetos de infraestrutura em nuvem, consulte [Implantar sua loja](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) na documentação para desenvolvedores do Adobe Commerce.
