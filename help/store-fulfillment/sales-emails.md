---
title: Modelos de e-mail de vendas
description: Configure os modelos de email transacional para se comunicar com os clientes e administradores de loja durante o processo de preenchimento de pedidos de Retirada de loja.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# Modelos de e-mail de vendas

O Atendimento da loja oferece um conjunto estendido de modelos de email transacional para suportar workflows de pedidos e atendimento. Eles oferecem comunicação e mensagens consistentes e automatizadas entre canais, notificando os administradores de clientes e lojas sobre alterações no status dos pedidos, instruções para pedidos de coleta na loja e muito mais.

Os modelos de email de Atendimento da loja são configurados com as mensagens e configurações padrão. Os administradores de comerciantes no Adobe Commerce podem gerenciar e modificar configurações e selecionar os modelos de email para se comunicar com os clientes em diferentes cenários. Os administradores também podem configurar e personalizar modelos.

Configure os modelos de Email de Vendas do Administrador: **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**.

## Emails - Configurações gerais

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Envio assíncrono</strong></td>
<td>Determina se os emails de vendas são enviados de forma assíncrona. Opções: <br/>**`Desabilitar`** - (Padrão) Os emails de vendas são enviados quando acionados por um evento. Para obter a comunicação e o tempo de resposta mais rápidos para a Retirada da loja, use a configuração padrão. <br/>**`Habilitar`** - habilitar essa opção move os processos que manipulam o check-out e as notificações por email de processamento de pedidos para o plano de fundo a serem enviados em intervalos regulares predeterminados.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>

## Pedido pronto para retirada na loja

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Ativado</strong></td>
<td>Este email é enviado ao cliente quando o associado da loja conclui a separação da ordem. Defina como "Não" para desativar a notificação por email. Se o template de email estiver desabilitado, isso não impedirá que um pedido seja escolhido pelo associado da loja.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Pedido Pronto Para Remetente De Email De Retirada</strong></td>
<td>A identidade do remetente usada ao enviar a notificação por email.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Modelo De Email De Pedido Pronto Para Retirada</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes registrados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<td><strong>Modelo de email de pedido pronto para retirada para convidado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes convidados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Modelo de Email Pronto para Retirada para Contato de Retirada Alternativo</strong></td>
<td>O modelo de mensagem de email usado para notificar contatos adicionais nomeados na ordem. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Enviar Pedido Pronto Para Retirada E-Mail Copiar Para</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email para enviar uma cópia de cada notificação.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Método De Cópia De Email De Enviar Pedido Pronto Para Retirada</strong></td>
<td>O método de cópia de email (cópia carbono) a ser usado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>


## A ordem foi retirada na Loja

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Ativado</strong></td>
<td>Esse email é enviado ao cliente quando ele confirmar que selecionou seu pedido da loja. Defina como "Não" para desativar a notificação por email. Se o template de email estiver desativado, isso não impede que um pedido seja coletado pelo cliente.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>O Pedido Foi Retirado Do Remetente De Email</strong></td>
<td>A identidade do remetente usada ao enviar a notificação por email.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>O pedido foi retirado do modelo de e-mail</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes registrados. Um template padrão é fornecido com a integração</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<td><strong>O pedido foi retirado do modelo de e-mail do convidado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes convidados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Envio Foi Retirado Cópia De E-Mail Para</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email para enviar uma cópia de cada notificação.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Método De Cópia De Email De Envio Selecionado</strong></td>
<td>O método de cópia de email (cópia carbono) a ser usado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>

## Pedido Atrasado

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Ativado</strong></td>
<td>Esse email é enviado ao cliente para notificá-lo sobre um atraso no processamento ou na separação do pedido na loja do comerciante. Defina como "Não" para desativar a notificação por email. Se o template de email estiver desativado, o recurso não impede que um pedido seja atrasado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Ordenar Remetente de Email Atrasado
</strong></td>
<td>A identidade do remetente usada ao enviar a notificação por email.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Modelo de email de pedido atrasado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes registrados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<td><strong>Modelo de email de pedido atrasado para convidado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes convidados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Enviar cópia de email com atraso do pedido para</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email para enviar uma cópia de cada notificação.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Método de Cópia Atrasada da Ordem de Envio</strong></td>
<td>O método de cópia de email (cópia carbono) a ser usado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>



## Pedido cancelado

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Ativado</strong></td>
<td>Esse email é enviado ao cliente para notificá-lo de que seu pedido foi cancelado na loja do comerciante. Defina como <code>No</code> para desabilitar a notificação por email. Se o template de email estiver desativado, esse recurso não impedirá que um pedido seja cancelado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Remetente de email de pedido cancelado
</strong></td>
<td>A identidade do remetente usada ao enviar a notificação por email.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Modelo de e-mail de pedido cancelado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes registrados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<td><strong>Pedido cancelado para convidado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes convidados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Enviar cópia do e-mail de pedido cancelado para</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email para enviar uma cópia de cada notificação.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Método de Cópia de Ordem de Envio Cancelada</strong></td>
<td>O método de cópia de email (cópia carbono) a ser usado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>


## Pedido parcialmente cancelado

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Ativado</strong></td>
<td>Esse email é enviado ao cliente para notificá-lo de que parte de seu pedido foi cancelada na loja do comerciante. Defina como <code>No</code> para desabilitar a notificação por email. Se o template de email estiver desativado, isso não impede que um pedido seja parcialmente cancelado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Remetente do e-mail do pedido parcialmente cancelado
</strong></td>
<td>A identidade do remetente usada ao enviar a notificação por email.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Modelo de e-mail do pedido parcialmente cancelado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes registrados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<td><strong>Modelo de email do pedido parcialmente cancelado para contato de retirada alternativo</strong></td>
<td>O modelo de mensagem de email usado para notificar contatos adicionais nomeados na ordem. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Pedido parcialmente cancelado para convidado</strong></td>
<td>O modelo de mensagem de email usado para notificar clientes convidados. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Enviar cópia de email do pedido parcialmente cancelado para</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email para enviar uma cópia de cada notificação.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Método de cópia Enviar pedido parcialmente cancelado</strong></td>
<td>O método de cópia de email (cópia carbono) a ser usado.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>

## Enviar para loja

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descrição</strong></th>
<th><strong>Escopo</strong></th>
<th><strong>Obrigatório</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>O Pedido Tem Remetente De Email De Produtos De Entrega Para Armazenamento</strong></td>
<td>Email enviado à equipe de comerciante especificada como um relatório agregado de todas as ordens em aberto que não podem ser separadas em um armazenamento de comerciante até que o estoque esteja disponível. </br></br> Comerciantes podem usar este relatório para iniciar e gerenciar transferências de estoque de loja para loja ou reabastecimento. </br></br>Esta notificação só se aplica quando os recursos [!DNL Ship-to-Store] estão habilitados.
</br></br>Este rótulo não afeta a transportadora selecionada nem seus rótulos de método de envio disponíveis.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Destinatários de Email da Loja de Destino</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email para enviar uma cópia de cada notificação.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Modelo de e-mail</strong></td>
<td>O modelo de mensagem de email usado para notificar os destinatários. Um template padrão é fornecido com a integração.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>

>[!NOTE]
>
>Se você permitir pedidos pendentes, deverá fornecer um endereço de email de administrador para receber notificações sobre esses pedidos. Adicione o endereço às seguintes configurações: **[!UICONTROL Send Order Delayed Email Copy To]** no modelo [Atraso do Pedido](#order-delayed) e [!UICONTROL Ship To Store Email Recipients] no modelo [Enviar para Loja](#ship-to-store).



