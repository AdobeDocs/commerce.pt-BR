---
title: Configuração geral
description: Defina as configurações gerais para habilitar [!DNL Store Fulfillment] para seu armazenamento. Defina as configurações de extensão global, as configurações do sistema para registro, sincronização de dados e segurança. Forneça os principais dados para habilitar a integração entre o Adobe Commerce e os serviços de Atendimento da loja.
role: Admin
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 0%

---

# Serviço de armazenamento e configuração de vendas

Habilite a extensão [!DNL Store Fulfillment] no Administrador [!DNL Commerce] definindo as configurações de extensão, as configurações de segurança para os usuários do aplicativo Store Assist e as opções de método de entrega.

>[!IMPORTANT]
>
>A configuração do serviço de Atendimento da Loja se aplica somente após a conexão da instância do Adobe Commerce e do aplicativo [!DNL Store Fulfillment]. Consulte [Atendimento do Connect Store](connect-set-up-service.md).

## Gerenciar configurações de Serviços de Atendimento da Loja

Gerencie as configurações dos serviços de Atendimento da Loja no menu [!DNL Commerce Admin Store Configuration].

- Habilite a extensão, defina as configurações globais e especifique as opções de segurança para conexões e contas de usuário do aplicativo Store Assist, selecionando **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**.

  ![Configuração de serviços do Admin Store para Atendimento do Repositório](assets/store-services-admin-sf-config.png)

- Configure os métodos de entrega selecionando **[!UICONTROL Store > Configuration > Sales > Delivery Methods > In-Store Pickup]**.

  ![Configuração de vendas da Loja do Administrador para Atendimento da Loja](assets/store-sales-admin-sf-deliver-config.png)

## Configurações básicas

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Price]</strong></td>
<td>O preço que você cobra do cliente pela coleta na loja. O padrão é zero.</td>
<td>Site</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Search Radius]</strong></td>
<td>O raio, em quilômetros, a ser usado quando um comprador procurar um local de coleta de loja na finalização da loja. Os resultados da pesquisa retornam apenas armazenamentos localizados no raio de pesquisa especificado.</td>
<td>Site</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Displayed error message]</strong></td>
<td>Mensagem que é exibida quando um cliente seleciona a retirada na loja para um item que não está disponível para a retirada na loja. Você pode personalizar o texto padrão, se necessário.
</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>A configuração [!UICONTROL Search Radius] será usada somente se você tiver configurado a [localização de repositório e a configuração de mapeamento](store-location-map-provider-setup.md) para o Adobe Commerce.

## Habilitar a solução Store Fulfillment

Habilite a solução [!DNL Store Fulfillment] para adicionar os recursos de retirada na loja e na beira da calçada às experiências de compra e check-out na loja da Adobe Commerce.

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enabled]</strong></td>
<td>Habilitar ou desabilitar a solução. Quando habilitado, configure e use os recursos de Atendimento da Loja e estabeleça a conexão entre sua loja da Adobe Commerce e os serviços do [!DNL Store Fulfillment]. Quando desabilitados, todos os recursos de Atendimento da Loja são desabilitados e não há comunicação entre o Adobe Commerce e os serviços de Atendimento da Loja. As informações da ordem não podem ser processadas ou recebidas.</td>
<td>Site</td>
<td>Sim</td>
</tr>
</tbody>
</table>

## Adicionar credenciais da conta

<table>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Environment]</strong></td>
<td>Selecione <i>[!UICONTROL Sandbox]</i> ou <i>[!UICONTROL Production]</i><br></br>Selecionar [!UICONTROL Sandbox] habilita a comunicação com serviços de preenchimento em um ambiente de teste.<br></br>Selecionar [!UICONTROL Production] habilita a comunicação com os serviços de preenchimento em um ambiente ativo.<br></br>Você recebeu um conjunto de credenciais para cada ambiente e pode gerenciar ambos os conjuntos na mesma instalação. <br></br>Salve as credenciais antes de validar a conexão.</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL API Server URL]</strong></td>
<td>O URL para o endpoint da API de Atendimento da Walmart Store. O valor deve ser o URL totalmente qualificado fornecido durante o processo de integração. Os clientes de Atendimento da loja recebem um URL de Sandbox e Produção. Ao adicionar os valores, copie e cole o URL completo, incluindo a barra à direita "/".</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Token Auth Server URL]</strong></td>
<td>O URL para o ponto de extremidade de Autenticação de Abastecimento de Loja Walmart. O valor deve ser o URL totalmente qualificado fornecido durante o processo de integração. Você recebe um URL de sandbox e produção. Ao adicionar os valores, copie e cole o URL completo, incluindo a barra à direita "/".</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Merchant Id]</strong></td>
<td>Sua ID de comerciante (locatário) exclusiva fornecida durante o processo de integração. Essa ID é usada para encaminhar pedidos para garantir que seus armazenamentos de comerciantes os recebam.</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Id]</strong></td>
<td>A ID de integração exclusiva fornecida durante o processo de integração. Essa ID é usada para autenticar toda a comunicação entre o Adobe Commerce e os serviços de preenchimento de loja</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Secret]</strong></td>
<td>A chave de integração exclusiva fornecida durante o processo de integração. Essa chave é usada para autenticar toda a comunicação entre o Adobe Commerce e o serviço de preenchimento de loja.</td>
<td>Global</td>
<td>Sim</td>
</tr>
</table>

Após configurar o [!UICONTROL Account Credentials], selecione <strong>[!UICONTROL Validate Credentials]</strong> para verificar e estabelecer uma conexão com o serviço de preenchimento de repositório pela primeira vez.

## Configurar registro

Os logs dos serviços de preenchimento de repositório estão disponíveis no arquivo de log `var/log/walmart-bopis.log`.

Solicite ao administrador do sistema que configure seus ambientes para permitir o tratamento de exceções para que as exceções relacionadas à API possam ser capturadas por meio do firewall ou do cache.

Como o arquivo de log do aplicativo pode crescer rapidamente, habilite o log do aplicativo somente por um curto período quando necessário - por exemplo, ao solucionar problemas de preenchimento de repositório para um pedido [!DNL Commerce]. Essa configuração evita problemas de tempo de resposta em ambientes de produção causados por arquivos de log grandes.

>[!TIP]
>
>Para instalações locais do Adobe Commerce, peça ao administrador do sistema para configurar a rotação de log para o arquivo `var/log/walmart-bopis.log` para minimizar o tamanho. Para instalações locais do Adobe Commerce, consulte [Rotação de logs](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html#server-settings) no _Guia de Instalação do Adobe Commerce_. Para projetos de infraestrutura em nuvem do Adobe Commerce, consulte [Exibir e gerenciar logs](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html).

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Debug Mode]</strong></td>
<td>O Modo de depuração é usado para aumentar a atividade registrada na integração. Quando desativado, nenhuma informação de depuração é registrada. Quando habilitado, todas as informações de depuração são registradas <br></br>Todos os dados registrados podem ser encontrados no arquivo: <pre>var/log/walmart-bopis.log</pre>
<td>Global</td>
<td>Não</td>
</tr>
</tbody>
</table>

## Gerenciar Sincronização de pedidos

Defina as configurações para gerenciar a manipulação de erros para a sincronização de ordens, os atributos do catálogo a serem usados para a verificação de código de barras durante a separação de ordens e configure os tamanhos do lote de ordens para a fila de atendimento de armazenamento.

Você pode exibir detalhes sobre operações de sincronização de ordens no painel Gerenciamento da Fila de Abastecimento de Loja no Admin (
<strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong>).

### Gerenciamento de Erros de Sincronização

<table>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Retry Critical Error]</strong></td>
<td>Especifica as tentativas de repetição para uma operação de sincronização de registros após a ocorrência de um erro crítico.<br></br>Erros críticos ocorrem sempre que a integração falha ao obter uma resposta positiva do serviço de preenchimento. Esses problemas ocorrem quando o serviço está inativo ou quando há um erro nos dados do pedido que está sendo enviado.<br></br>Quando o limite de novas tentativas é atingido, o item permanece em uma fila, mas não é processado novamente. Exibir todos os itens com erros do Gerenciamento <strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong> no Administrador. Para solucionar problemas de itens com falha consistente, entre em contato com o Gerente de conta.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Error Notification Email]</strong></td>
<td>Habilite as notificações de erro para receber um email quando o [!UICONTROL Retry Critical Error Threshold] for alcançado para um pedido. A notificação inclui todos os detalhes disponíveis sobre o erro.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Send Error Notification Email To]</strong></td>
<td>Uma lista delimitada por vírgulas de endereços de email de recipients para notificações de erro.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Order Sync Exception Email Template]</strong></td>
<td>Especifica o modelo de email usado para notificar os destinatários sobre erros de sincronização de pedidos. Um template padrão é fornecido. Ele não oferece suporte à personalização.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</table>

### Sincronização de pedidos

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Barcode Source]</strong></td>
<td>O atributo de catálogo que armazena o código digitalizável para itens correspondentes em seus locais de comerciante.<br></br>Se você tiver apenas uma localização de comerciante existente, é provável que use códigos UPC, enquanto o canal de comércio eletrônico identifica produtos por SKU. Nesse cenário, selecione o atributo de catálogo que contém o código UPC.<br></br>Essa configuração garante que as ordens enviadas para os itens da lista de lojas com o identificador correto, para que as associadas de loja possam verificar com precisão os itens durante o processo de separação.<br></br>Se não tiver certeza, consulte seus associados de preenchimento no departamento de Remessa e Separação para determinar qual atributo deve ser enviado. Se o atributo não estiver incluído no banco de dados, você poderá adicioná-lo ao conjunto de atributos do produto Adobe Commerce.</td>
<td>Site</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Barcode Type]</strong></td>
<td>O atributo de catálogo que armazena a origem do código de barras para itens correspondentes em seus locais de comerciante.<br></br>Essa configuração garante que as ordens enviadas para os itens da lista de lojas com o identificador correto, para que as associações de loja possam verificar com precisão os itens durante o processo de separação. As opções incluem - SKU, UPC, GTIN, UPCA, EAN13, UPCE0, DISA, UAB, CODABAR, Preço incorporado UPC.<br></br>Se não tiver certeza, selecione a opção mais parecida com os valores contidos no seu atributo [!UICONTROL Barcode Source]. Os associados da loja ainda podem corresponder itens manualmente em sua lista de separação.</td>
<td>Site</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Max Number of Items]</strong></td>
<td>O número máximo de itens a serem enviados da fila de atendimento de armazenamento de uma vez.<br></br>Os pedidos BOPIS são enviados ao serviço de atendimento em lotes, em intervalos regulares. Essa configuração permite controlar o tamanho do lote.<br></br>O valor padrão é 100 itens. Dependendo do volume e da capacidade do seu pedido, você pode ajustar o valor máximo para cima ou para baixo.</td>
<td>Global</td>
<td>Não</td>
</tr>
</tbody>
</table>

## Habilitar opções de remessa de Atendimento da Loja

Configure as opções de envio de Store Fulfillment que determinam a disponibilidade das opções de entrega na loja e em casa para suas lojas Adobe Commerce.

### Entregar para armazenamento

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship To Store]</strong></td>
<td>A configuração de entrega para armazenamento baseia-se nos recursos existentes de entrega para armazenamento. Se você usa o Inventory management, ou se você pode aceitar e atender ordens em locais de comerciantes sem inventário por meio de transferências de inventário de loja para loja, defina esta opção como "Sim".<br></br>Se você não puder oferecer suporte à opção entregar para armazenamento ou não quiser oferecê-la, defina como `Não`. Quando desabilitados, os itens do catálogo com estoque zero para uma loja de comerciantes, ou os itens que estão abaixo de [!DNL Out of Stock Threshold] para esse local, não são oferecidos com as opções de retirada na loja.<br></br>Você pode ajustar o valor dessa configuração por localização do comerciante.</td>
<td>Global</td>
<td>Não</td>
</tr>
</tbody>
</table>

### Entregar do armazenamento

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></td>
<td>Ativa ou desativa a opção Entrega em casa nas lojas do comerciante. Quando ativado, seus locais de loja de comerciantes são considerados em conjunto com outras fontes atribuídas no estoque associado ao seu site.<br></br>Nos serviços padrão do Inventory management, a opção [!DNL Ship from Store] é inerente e não pode ser desabilitada. Com a solução Store Fulfillment, você pode ativá-la ou desativá-la.<br></br>Você pode ajustar essa configuração por localização e produto do comerciante.</td>
<td>Global</td>
<td>Não</td>
</tr>
</tbody>
</table>


## Gerenciar contas e permissões de uso do Aplicativo de Atendimento da Loja

Defina as configurações da segurança de senha e conta de usuário do Aplicativo de Abastecimento da Loja e da autenticação de dois fatores.

### Segurança do aplicativo

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL User Session Lifetime]</strong></td>
<td>O período, em segundos, em que uma sessão de usuário associado de armazenamento permanece ativa antes do logout automático. Os valores válidos variam de 60 a 31536000.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Maximum Login Failures to Lockout Account]</strong></td>
<td>Especifica o número de tentativas de logon com falha permitidas antes que uma associada de armazenamento seja bloqueada de sua conta.<br></br>Para desabilitar o bloqueio de conta, defina o valor como 0.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Lockout Time (minutes)]</strong></td>
<td>Número de minutos para bloquear uma conta após uma falha de logon.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Force Password Change]</strong></td>
<td><em>[!UICONTROL Yes]</em>: Exigir que o usuário altere a senha após a configuração da conta.<br></br><em>[!UICONTROL No]</em>: recomenda que o usuário altere a senha após a configuração da conta.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Password Lifetime]</strong></td>
<td>O número de dias que uma senha permanece válida antes de uma alteração de senha necessária. Deixe em branco para desativar esta opção.</td>
<td>Global</td>
<td>Não</td>
</tr>
</tbody>
</table>

## Métodos de delivery

A Store Fulfillment funciona estendendo os recursos nativos do Adobe Commerce [!DNL In-Store Delivery]. Após instalar a extensão, é possível configurar métodos de entrega na loja usando as seguintes configurações estendidas que são adicionadas ao Administrador.

- **Coleta na loja** — Opções de oferta para entrega na loja durante o processo de check-out
Essas configurações definem os cenários de entrega mais comuns para pedidos BOPIS.

- **[!UICONTROL Curbside pick up]**-Ofereça opções para que os clientes estacionem em um local de loja e que seus pedidos sejam entregues a eles por um associado da loja.

Defina essas configurações no Administrador selecionando <strong>[!UICONTROL Stores > Configuration > Sales > Delivery Methods > In-Store Pickup]</strong>.

>[!NOTE]
>
>Para obter informações adicionais sobre a configuração das opções de entrega na loja, consulte [Entrega na loja](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/basic-methods/shipping-in-store-delivery) no _Guia do Usuário do Adobe Commerce_.


### Configuração de métodos de entrega

Com o método de entrega na loja, o cliente pode selecionar uma origem a ser usada como um local de retirada durante a finalização da compra.

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descrição</strong></td>
<td><strong>Escopo</strong></td>
<td><strong>Obrigatório</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enable In-Store Pickup]</strong></td>
<td>Habilite ou desabilite a opção de retirada na loja disponível durante o check-out para clientes que escolhem a retirada da loja. Quando a coleta na loja está desativada, a opção não é exibida.<br></br>Esta configuração global se aplica a todos os locais de lojas de varejo. Quando ativado, você pode desativá-lo seletivamente no local da loja de varejo.</td>
<td>Site</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Curbside Pickup]</strong></td>
<td>Habilite ou desabilite a opção de retirada à beira-mar durante o processo de finalização para clientes que escolhem a retirada da loja.<br></br>Esta configuração global se aplica a todos os locais de lojas de varejo. Quando ativado, você pode desativá-lo seletivamente no local da loja de varejo.</td>
<td>Site</td>
<td>Não</td>
</tr>
</tbody>
</table>

### Configuração de título do método de entrega

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
<td><strong>Título da entrega inicial</strong></td>
<td>Especifica o título a ser exibido para a opção Entrega inicial nas áreas do produto, carrinho e finalização. A entrega em casa refere-se aos recursos de entrega padrão do Adobe Commerce — de um depósito, por uma transportadora ou diretamente para o endereço de entrega fornecido pelo cliente. </br></br>Este rótulo não afeta os rótulos do método de envio da transportadora selecionada.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Descrição da entrega inicial</strong></td>
<td>Uma descrição opcional que é exibida sempre que o Título do delivery inicial é exibido aos clientes. Na maioria das vezes, a descrição é uma mensagem estática para comunicar suas promessas de delivery. Alguns exemplos:</br><code>Same-day shipping on orders by 4</code></br></br><code>Ships within 2 business days</code></td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Título da retirada da loja</strong></td>
<td>Quando uma opção de entrega é apresentada ao cliente e a retirada na loja está disponível, este rótulo é exibido. </br></br>Você pode personalizar este rótulo, que é exibido nas áreas do produto, carrinho e check-out.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<td><strong>Descrição da retirada da loja</strong></td>
<td>Sempre que o Título de retirada da loja for exibido, você poderá incluir uma descrição, se desejar. Esta mensagem estática ajuda a melhorar as comunicações do cliente relacionadas à experiência de retirada da loja. Alguns exemplos:</br></br><code>Get it today for free!</code></br></br><code>Ready for pickup in an hour!</code></td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Título de retirada na loja</strong></td>
<td>Quando a Coleta na loja está ativada, esse título é exibido aos clientes como a opção de entrega Coleta da loja. Você pode personalizar seu rótulo.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<tr>
<td><strong>Título de retirada da borda</strong></td>
<td>Quando a opção Seleção à beira da proibição está ativada, a opção é mostrada aos clientes como um tipo de opção de entrega de Seleção de loja. Você pode personalizar seu rótulo aqui.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Instruções de retirada na loja</strong></td>
<td>Quando um pedido estiver pronto para retirada em suas lojas de varejo, o cliente será notificado por e-mail. Se o cliente selecionou [!DNL In-Store Pickup] durante o check-out, você pode personalizar as instruções de retirada aqui. </br></br>Essas instruções são definidas globalmente e se aplicam a todos os locais de lojas de varejo. Você também pode personalizar as instruções no nível do local da loja de varejo.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Instruções de retirada da calçada</strong></td>
<td>Especifica instruções personalizadas de retirada de ordem a serem incluídas nas notificações por email do cliente para ordens de retirada na borda. </br></br>Essas instruções são definidas globalmente e se aplicam a todos os locais de lojas de varejo. Você também pode personalizar as instruções no nível do local da loja de varejo.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Lead Time de Retirada Estimado</strong></td>
<td>O número de minutos necessários antes de um pedido ser recebido, atendido e pronto para ser retirado. Essas informações são mostradas ao cliente ao selecionar um local de loja de varejo para a opção Entrega de retirada da loja. Essa configuração se aplica a todos os locais de loja de varejo. Você também pode personalizar o prazo de entrega no nível de localização da loja de varejo.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Rótulo de tempo estimado de retirada</strong></td>
<td>Exibe o tempo estimado até que um pedido esteja disponível para retirada do cliente. Essas informações são mostradas aos clientes quando eles selecionam um local de loja de varejo para a opção de entrega [!DNL In-Store Pickup]. </br></br>Ao personalizar este rótulo, você pode usar o código <code>%1</code> para inserir seu <strong>Prazo de Entrega Estimado</strong>. Por exemplo:</br></br><code>Ready for Pickup in %1 minutes.</code></br></br>Essa configuração se aplica a todos os locais de lojas de varejo. Você também pode personalizar o prazo de entrega no nível de localização da loja de varejo.</td>
<td>Exibição da loja</td>
<td>Não</td>
<tr>
<td><strong>Aviso de isenção de tempo de retirada</strong></td>
<td>O conteúdo exibido na página do produto na dica de ferramenta que lista horas de armazenamento, feriados, fechamentos inesperados e assim por diante</td>
<td>Exibição da loja
</td>
<td>Não
</td>
</tr>
</tbody></table>

### Configuração dos títulos de disponibilidade do Stock

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
<td><strong>Em Estoque</strong></td>
<td>Quando um cliente estiver usando o endereço da loja de varejo, a disponibilidade do inventário para os itens atuais é mostrada para cada local. </br></br>Você pode personalizar o rótulo de status <em>[!UICONTROL in-stock]</em> aqui.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Sem estoque</strong></td>
<td>Quando um cliente estiver usando o endereço da loja de varejo, a disponibilidade do inventário para qualquer item atual é mostrada para cada local.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
<tr>
<td><strong>Parcialmente em Estoque</strong></td>
<td>Quando um cliente estiver usando o endereço da loja de varejo, a disponibilidade do inventário para quaisquer itens atuais é mostrada para cada local. </br></br>Você pode personalizar o rótulo de status <em>[!UICONTROL partially in-stock]</em> aqui.</td>
<td>Exibição da loja</td>
<td>Não</td>
</tr>
</tbody></table>

