---
title: Conectar dados do Commerce ao Adobe Experience Platform
description: Saiba como conectar os dados do Commerce à Adobe Experience Platform.
feature: Personalization, Integration, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 0%

---

# Conectar dados do Commerce ao Adobe Experience Platform

Ao instalar a extensão [!DNL Data Connection], duas novas páginas de configuração aparecem no menu **Sistema** em **Serviços** no _Administrador_ do Commerce.

- Commerce Services Connector
- [!DNL Data Connection]

Para conectar sua instância do Adobe Commerce à Adobe Experience Platform, você deve configurar ambos os conectores, começando com o conector do Commerce Services e terminando com a extensão [!DNL Data Connection].

## Configurar o conector de serviços do Commerce

Se você tiver instalado anteriormente um serviço do Adobe Commerce, provavelmente já terá configurado o conector de Serviços do Commerce. Caso contrário, você deve concluir as seguintes tarefas na página [Conector de serviços do Commerce](../landing/saas.md):

1. Faça logon em sua conta da Commerce para [recuperar as chaves de API de produção e de sandbox](../landing/saas.md#credentials).
1. Selecione um [espaço de dados SaaS](../landing/saas.md#saas-configuration).
1. Faça logon em sua conta da Adobe para [recuperar a ID da organização](../landing/saas.md#ims-organization-optional).

Após configurar o conector de Serviços da Commerce, configure a extensão [!DNL Data Connection].

## Configurar a extensão [!DNL Data Connection]

Nesta seção, você aprenderá a configurar a extensão [!DNL Data Connection].

### Adicionar conta de serviço e detalhes da credencial

Se você planeja coletar e enviar [dados históricos de pedido](#send-historical-order-data) ou [dados de perfil do cliente](#send-customer-profile-data), é necessário adicionar a conta de serviço e os detalhes da credencial. Além disso, se você estiver configurando a extensão [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=pt-BR), conclua essas etapas.

Se você estiver coletando e enviando apenas dados da loja ou do back office, pule para a seção [geral](#general).

#### Etapa 1: criar um projeto no Adobe Developer Console

Crie um projeto na Adobe Developer Console que autentica o Commerce para que ele possa fazer chamadas de API do Experience Platform.

Para criar o projeto, siga as etapas descritas no tutorial [Autenticar e acessar APIs do Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=pt-BR).

À medida que você avança pelo tutorial, certifique-se de que seu projeto tenha o seguinte:

- Acesso aos [perfis de produto](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=pt-BR#select-product-profiles) a seguir: **Acesso total à produção padrão** e **Acesso total padrão à AEP**.
- As [funções e permissões corretas estão configuradas](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=pt-BR#assign-api-to-a-role).
- Se você decidir usar JSON Web Tokens (JWT) como método de autenticação de servidor para servidor, também deverá carregar uma chave privada.

O resultado dessa etapa cria um arquivo de configuração que você usa na próxima etapa.

#### Etapa 2: baixar arquivo de configuração

Baixe o [arquivo de configuração do espaço de trabalho](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file). Copie e cole o conteúdo desse arquivo na página **Detalhes da Conta de Serviço/Credencial** do Administrador do Commerce.

1. No Administrador do Commerce, navegue até **Lojas** > Configurações > **Configuração** > **Serviços** > **[!DNL Data Connection]**.

1. Selecione o método de autorização de servidor para servidor que você implementou no menu **Tipo de Autorização do Adobe Developer**. A Adobe recomenda usar o OAuth. O JWT foi descontinuado. [Saiba mais](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

1. (Somente JWT) Copie e cole o conteúdo do seu arquivo `private.key` no campo **Segredo do cliente**. Use o comando a seguir para copiar o conteúdo.

   ```bash
   cat config/private.key | pbcopy
   ```

   Consulte [Autenticação de Conta de Serviço (JWT)](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) para obter mais informações sobre o arquivo `private.key`.

1. Copie o conteúdo do arquivo `<workspace-name>.json` no campo **Detalhes da Conta/Credencial de Serviço**.

   ![[!DNL Data Connection] Configuração de administração](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. Clique em **Salvar configuração**.

1. Clique no botão **[!UICONTROL Test connection]** para verificar se a conta de serviço e as informações de credencial inseridas estão corretas.

### Geral

1. No Admin, vá para **Sistema** > Serviços > **[!DNL Data Connection]**.

   ![[!DNL Data Connection] Configurações](./assets/epc-settings.png){width="700" zoomable="yes"}

1. Na guia **Configurações** em **Geral**, verifique a ID associada à sua conta do Adobe Experience Platform, conforme configurado no [Commerce Services Connector](../landing/saas.md#organizationid). A ID da organização é global. Somente uma ID de organização pode ser associada por instância do Adobe Commerce.

1. No menu suspenso **Escopo**, defina o contexto como **Site**.

1. (Opcional) Se você já tiver um [AEP Web SDK (alloy)](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) implantado em seu site, habilite a caixa de seleção e adicione o nome de seu AEP Web SDK. Caso contrário, deixe esses campos em branco e a extensão [!DNL Data Connection] implantará um para você.

   >[!NOTE]
   >
   >Se você especificar seu próprio AEP Web SDK, a extensão [!DNL Data Connection] usará a ID de sequência de dados associada a esse SDK e não a ID de sequência de dados especificada nessa página (se houver).

### Coleção de dados

Nesta seção, especifique o tipo de dados que deseja coletar e enviar para a borda do Experience Platform. Há três tipos de dados:

- **Comportamental** (dados do lado do cliente) são dados capturados na loja. Isso inclui informações de interações do comprador, como `View Page`, `View Product`, `Add to Cart` e [lista de requisições](events.md#b2b-events) (para comerciantes B2B).

- **Back office** (dados do lado do servidor) são dados capturados nos servidores do Commerce. Isso inclui informações sobre o status de um pedido, como se um pedido tivesse sido feito, cancelado, reembolsado, remetido ou concluído. Também inclui [dados históricos de pedido](#send-historical-order-data).

- **Perfil** são dados relacionados às informações de perfil do seu comprador. Saiba [mais](#send-customer-profile-data).

Para garantir que sua instância do Adobe Commerce possa iniciar a coleta de dados, verifique os [pré-requisitos](overview.md#prerequisites).

Consulte o tópico de eventos para saber mais sobre [loja](events.md#storefront-events), [back office](events-backoffice.md) e [perfil](events-backoffice.md#customer-profile-events-server-side) eventos.

>[!NOTE]
>
>Todos os campos na seção **Coleção de dados** se aplicam ao escopo do **Site** ou superior.

1. Selecione **Eventos de vitrine** se desejar enviar dados comportamentais de vitrine.

1. Selecione **Eventos do back office** se desejar enviar informações sobre o status do pedido, como se um pedido foi feito, cancelado, reembolsado ou remetido.

   >[!NOTE]
   >
   >Se você selecionar **Eventos do back office**, todos os dados do back office serão enviados para a borda do Experience Platform. Se um comprador optar por recusar a coleta de dados, você deverá definir explicitamente a preferência de privacidade do comprador na Experience Platform. Isso é diferente dos eventos da loja em que o coletor já lida com o consentimento com base nas preferências do comprador. Saiba [mais](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html?lang=pt-BR) sobre como definir a preferência de privacidade de um comprador na Experience Platform.

1. (Ignore esta etapa se você estiver usando sua própria AEP Web SDK.) [Crie](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=pt-BR#create) uma sequência de dados na Adobe Experience Platform ou selecione uma sequência de dados existente que você deseja usar para a coleção. Insira essa ID de sequência de dados no campo **ID de sequência de dados**.

1. Insira a **ID do conjunto de dados** que você deseja que contenha seus dados do Commerce. Para localizar a ID do conjunto de dados:

   1. Abra a interface do Experience Platform e selecione **Conjuntos de dados** no menu de navegação esquerdo para abrir o painel **Conjuntos de dados**. O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo o nome, o esquema ao qual o conjunto de dados pertence e o status da execução de assimilação mais recente.
   1. Abra o conjunto de dados associado à sua sequência de dados.
   1. No painel direito, exiba os detalhes sobre o conjunto de dados. Copie a ID do conjunto de dados.

1. Para garantir atualizações de dados de eventos de back office com base em um agendamento de acordo com um trabalho [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=pt-BR), você deve alterar o índice `Sales Orders Feed` para `Update by Schedule`.

   1. Na barra lateral _Admin_, vá para **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Index Management]**.

   1. Marque a caixa de seleção do indexador `Sales Orders Feed`.

   1. Defina **[!UICONTROL Actions]** como `Update by Schedule`.

   1. Se você estiver ativando os dados de back office pela primeira vez, execute os seguintes comandos para reindexar e acionar uma ressincronização. Ressincronizações subsequentes ocorrem automaticamente desde que o trabalho [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=pt-BR) esteja configurado corretamente.

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### Descrições dos campos

| Campo | Descrição |
|--- |--- |
| Escopo | Site específico no qual você deseja aplicar as configurações. |
| ID da organização (global) | ID que pertence à organização que comprou o produto Adobe DX. Essa ID vincula sua instância do Adobe Commerce ao Adobe Experience Platform. |
| O AEP Web SDK já foi implantado no site? | Marque essa caixa de seleção se você implantou seu próprio AEP Web SDK no site |
| AEP Web SDK Name (global) | Se você já tiver um Experience Platform Web SDK implantado em seu site, especifique o nome desse SDK neste campo. Isso permite que o Coletor de Eventos da Storefront e o SDK de Eventos da Storefront usem seu Experience Platform Web SDK em vez da versão implantada pela extensão [!DNL Data Connection]. Se você não tiver um Experience Platform Web SDK implantado no site, deixe esse campo em branco e a extensão [!DNL Data Connection] implantará um para você. |
| Eventos da loja | É marcado por padrão, desde que a ID da organização e a ID do fluxo de dados sejam válidas. Os eventos da loja coletam dados comportamentais anônimos dos compradores enquanto eles navegam pelo site. |
| Eventos de back office | Se marcado, a carga do evento conterá informações anônimas sobre o status do pedido, como se um pedido tivesse sido feito, cancelado, reembolsado ou remetido. |
| ID da sequência de dados (site) | ID que permite que os dados fluam do Adobe Experience Platform para outros produtos Adobe DX. Essa ID deve ser associada a um site específico em sua instância específica do Adobe Commerce. Se você especificar seu próprio Experience Platform Web SDK, não especifique uma ID de fluxo de dados nesse campo. A extensão [!DNL Data Connection] usa a ID de sequência de dados associada a essa SDK e ignora qualquer ID de sequência de dados especificada nesse campo (se houver). |
| ID do conjunto de dados (site) | ID do conjunto de dados que contém seus dados do Commerce. Este campo é obrigatório, a menos que você tenha desmarcado as caixas de seleção **Eventos da vitrine** ou **Eventos do back office**. Além disso, se você estiver usando sua própria Experience Platform Web SDK e, portanto, não tiver especificado uma ID de sequência de dados, ainda será necessário adicionar a ID do conjunto de dados associada à sequência de dados. Caso contrário, você não poderá salvar este formulário. |

Após a integração, os dados da loja começam a fluir para a borda do Experience Platform. Os dados de back office levam cerca de cinco minutos para serem exibidos na borda do. As atualizações subsequentes ficam visíveis na borda com base na programação do cron.

### Enviar dados de perfil do cliente

Há dois tipos de dados de perfil que você pode enviar para a Experience Platform: registros de perfil e eventos de perfil de série temporal.

Um registro de perfil contém dados que são salvos quando um comprador cria um perfil na instância do Commerce, como o nome do comprador. Quando o esquema e o conjunto de dados estão [configurados corretamente](profile-data.md), um registro de perfil é enviado à Experience Platform e encaminhado ao serviço de gerenciamento e segmentação de perfis da Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR).

Os eventos de perfil de série temporal contêm dados sobre as informações de perfil do comprador, como se ele criasse, editasse ou excluísse uma conta no site. Quando os dados do evento de perfil são enviados para a Experience Platform, eles ficam em um conjunto de dados em que podem ser usados por outros produtos DX.

1. Verifique se você [forneceu](#add-service-account-and-credential-details) a conta de serviço e os detalhes da credencial.

1. Verifique se você tem um esquema e um conjunto de dados especificados para [assimilação de dados de registro de perfil](profile-data.md) e [assimilação de dados de evento de perfil de série temporal](update-xdm.md#time-series-profile-event-data).

1. Marque a caixa de seleção **Perfis de cliente** se desejar enviar dados de perfil para a Experience Platform.

1. Insira a **ID do Conjunto de Dados de Perfil**.

   Os dados do registro de perfil devem usar um conjunto de dados diferente do que você está usando atualmente para dados de evento comportamentais e de back office.

1. Se você não quiser transmitir eventos de perfil por meio da mesma ID de sequência de dados que está usando para dados comportamentais e de back office, remova a marca de seleção de **Transmitir perfis de clientes por meio da mesma ID de sequência de dados** e insira a ID de sequência de dados que deseja usar.

Pode levar cerca de 10 minutos para que um registro de perfil fique disponível no Real-Time CDP. Os eventos de perfil começam a ser transmitidos imediatamente.

>[!TIP]
>
>Se você não estiver vendo os dados do perfil na Experience Platform, consulte a [Base de Dados de Conhecimento Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) para obter sugestões de solução de problemas.

#### Descrições dos campos

| Campo | Descrição |
|--- |--- |
| Perfis de cliente | Marque essa caixa de seleção se desejar coletar e enviar registros de perfil do cliente. |
| ID do conjunto de dados do perfil | Um registro de perfil deve usar um conjunto de dados diferente do usado para eventos comportamentais e de back office. |
| Transmitir perfis de clientes por meio da mesma ID de sequência de dados | Decida se deseja usar o mesmo fluxo de dados usado atualmente para seus eventos comportamentais e de back office ou não. |
| Sequência de dados para perfis de clientes | Especifique a sequência de dados específica do registro de perfil do cliente. |

### Enviar dados históricos do pedido

A Adobe Commerce coleta até cinco anos de [dados históricos e status de pedidos](events-backoffice.md#back-office-events). Você pode usar a extensão [!DNL Data Connection] para enviar esses dados históricos para a Experience Platform a fim de enriquecer os perfis do cliente e personalizar as experiências do cliente com base nesses pedidos anteriores. Os dados são armazenados em um conjunto de dados na Experience Platform.

Embora o Commerce já colete os dados históricos do pedido, há várias etapas que você deve concluir para enviar esses dados para o Experience Platform.

Assista a este vídeo para saber mais sobre pedidos históricos e, em seguida, conclua as etapas a seguir para implementar a coleção de pedidos históricos.

>[!VIDEO](https://video.tv.adobe.com/v/3450232?captions=por_br)

#### Configurar o serviço de sincronização de pedidos

O serviço de sincronização de pedidos usa a [Estrutura da Fila de Mensagens](https://developer.adobe.com/commerce/php/development/components/message-queues/) e a RabbitMQ. Após concluir essas etapas, os dados do status do pedido podem ser sincronizados com o SaaS, que é necessário antes de ser enviado para a Experience Platform.

1. Verifique se você [forneceu](#add-service-account-and-credential-details) a conta de serviço e os detalhes da credencial.

1. [Habilitar](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html?lang=pt-BR) RabbitMQ.

   >[!NOTE]
   >
   >O RabbitMQ já está configurado para o Commerce versões 2.4.7 e posteriores, mas você deve habilitar os consumidores.

1. Habilite os consumidores da fila de mensagens pelo trabalho cron em `.magento.env.yaml` usando a variável de ambiente `CRON_CONSUMERS_RUNNER`.

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >Consulte a [documentação de variáveis de implantação](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=pt-BR#cron_consumers_runner) para saber mais sobre todas as opções de configuração disponíveis.

Com o serviço de sincronização de pedidos habilitado, você pode especificar o intervalo de datas do pedido histórico na página **[!UICONTROL [!DNL Data Connection]]**.

#### Especificar intervalo de datas do histórico da ordem

Especifique o intervalo de datas para o histórico de pedidos que você deseja enviar à Experience Platform.

1. No Admin, vá para **Sistema** > Serviços > **[!DNL Data Connection]**.

1. Selecione a guia **Histórico de pedidos**.

   ![[!DNL Data Connection] Histórico de pedidos](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. Em **Sincronização do Histórico de Pedidos**, a caixa de seleção **Copiar ID do Conjunto de Dados das Configurações** já está habilitada. Isso garante que você esteja usando o mesmo conjunto de dados especificado na guia **Configurações**.

1. Nos campos **De** e **Até**, especifique o intervalo de datas para os dados históricos de ordem que você deseja enviar. Não é possível selecionar um intervalo de datas que exceda cinco anos.

1. Selecione **[!UICONTROL Start Sync]** para iniciar a sincronização. Os dados históricos de pedidos são dados em lote, e não dados de vitrine e back-office que estão transmitindo dados. Os dados em lote levam cerca de 45 minutos para serem recebidos no Experience Platform.

##### Descrições dos campos

| Campo | Descrição |
|--- |--- |
| Copiar ID do conjunto de dados das configurações | Copia a ID do conjunto de dados inserida na guia **Configurações**. |
| ID do conjunto de dados (site) | ID do conjunto de dados que contém seus dados do Commerce. Este campo é obrigatório, a menos que você tenha desmarcado as caixas de seleção **Eventos da vitrine** ou **Eventos do back office**. Além disso, se você estiver usando sua própria Experience Platform Web SDK e, portanto, não tiver especificado uma ID de sequência de dados, ainda será necessário adicionar a ID do conjunto de dados associada à sequência de dados. Caso contrário, você não poderá salvar este formulário. |
| De | Data a partir da qual você deseja começar a coletar dados do histórico do pedido. |
| Para | Data a partir da qual você deseja terminar a coleta de dados do histórico da ordem. |
| Iniciar sincronização | Inicia o processo de sincronização dos dados do histórico do pedido com a borda do Experience Platform. Esse botão será desativado se o campo **[!UICONTROL Dataset ID]** estiver em branco ou se a ID do conjunto de dados for inválida. |

### Personalização de dados

Na guia **Personalização de Dados**, você pode exibir todos os atributos personalizados configurados em [!DNL Commerce] e enviados ao Experience Platform.

![[!DNL Data Connection] Personalização de dados](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>Verifique se a ID da sequência de dados que você [especificou](#data-collection) na guia **Coleção de Dados** corresponde à ID vinculada ao esquema para assimilar atributos personalizados.

Ao criar atributos personalizados para pedidos e enviá-los à Experience Platform, os nomes dos atributos no Commerce devem corresponder aos do esquema [!DNL Commerce] na Experience Platform. Se não corresponderem, pode ser difícil identificar as diferenças. Se houver nomes incompatíveis, a tabela **Atributos de Ordem Personalizada** poderá ajudar a resolver o problema.

A tabela **Atributos de Ordem Personalizados** fornece visibilidade sobre a configuração e o mapeamento de atributos de ordem personalizados entre o back office [!DNL Commerce] e o esquema [!DNL Commerce] no Experience Platform. Essa tabela permite exibir atributos personalizados no nível do pedido e no nível do item do pedido em diferentes origens, facilitando a identificação de atributos ausentes ou desalinhados. Ele também exibe IDs de conjunto de dados para ajudar a diferenciar entre conjuntos de dados dinâmicos e históricos, pois cada um pode ter seus próprios atributos personalizados.

Se você não vir uma marca de seleção verde ao lado de um nome de atributo personalizado na tabela, isso indica uma incompatibilidade entre os nomes de atributo nas fontes. Corrija o nome do atributo em uma origem e uma marca de seleção verde será exibida, indicando que os nomes agora correspondem.

- Se o nome do atributo for atualizado no esquema no Experience Platform, você deverá salvar a configuração na guia **Personalização de dados** para acionar a alteração no esquema do Experience Platform. Esta alteração será refletida na tabela **Atributos da Ordem Personalizada** quando você clicar no botão **[!UICONTROL Refresh]**.
- Se o nome do atributo for atualizado em [!DNL Commerce], um evento de ordem deverá ser gerado para atualizar o nome na tabela **Atributos de Ordem Personalizados**. A alteração será refletida em cerca de 60 minutos.

Saiba mais sobre como [configurar atributos personalizados](custom-attributes.md).

#### Descrições dos campos

| Campo | Descrição |
|--- |--- |
| Conjunto de dados | Exibe os conjuntos de dados que contêm os atributos personalizados. Conjuntos de dados dinâmicos e históricos podem ter seus próprios atributos personalizados. |
| Adobe Commerce | Exibe todos os atributos personalizados criados no back office [!DNL Commerce]. |
| Experience Platform | Exibe todos os atributos personalizados especificados no esquema [!DNL Commerce] na Experience Platform. |
| Atualizar | Recupera nomes de atributos personalizados do esquema [!DNL Commerce] na Experience Platform. |

## Confirmar se os dados do evento foram coletados

Para confirmar se os dados estão sendo coletados do seu armazenamento do Commerce, use o [Adobe Experience Platform debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=pt-BR) para examinar seu site do Commerce. Depois de confirmar que os dados estão sendo coletados, você pode verificar se os dados do evento da loja e do back office aparecem na borda executando uma consulta que retorna dados do [conjunto de dados criado](overview.md#prerequisites).

1. Selecione **Consultas** na navegação à esquerda do Experience Platform e clique em [!UICONTROL Create Query].

   ![Editor de consultas](assets/query-editor.png)

1. Quando o Editor de consultas for aberto, insira uma consulta que selecione dados do conjunto de dados.

   ![Criar consulta](assets/create-query.png)

   Por exemplo, sua consulta pode ser semelhante ao seguinte:

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. Após a execução da consulta, os resultados serão exibidos na guia **Resultados**, ao lado da guia **Console**. Essa exibição mostra a saída em tabela da sua query.

   ![Editor de consultas](assets/query-results.png)

Neste exemplo, você vê os dados do evento de [`commerce.productListAdds`](events.md#addtocart), [`commerce.productViews`](events.md#productpageview), [`web.webpagedetails.pageViews`](events.md#pageview) e assim por diante. Essa visualização permite verificar se os dados do Commerce chegaram à borda.

Se os resultados não forem os esperados, abra o conjunto de dados e procure qualquer importação de lotes com falha. Saiba mais sobre [solução de problemas de importações em lote](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html?lang=pt-BR).

### Verifique se os dados do perfil aparecem na Experience Platform

Se você não estiver vendo os dados do perfil na Experience Platform, consulte a [Base de Dados de Conhecimento Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) para obter sugestões de solução de problemas.

## Próximas etapas

Quando os dados do Commerce são enviados para a borda do Experience Platform, outros produtos da Adobe Experience Cloud, como o Adobe Journey Optimizer, podem usar esses dados. Por exemplo, você pode configurar o Journey Optimizer para acompanhar determinados eventos e, com base nesses dados, acionar um email para um usuário pela primeira vez ou se houver um carrinho abandonado. Saiba como estender sua plataforma do Commerce [criando jornadas para clientes](using-ajo.md) no Journey Optimizer.
