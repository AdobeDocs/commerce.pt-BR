---
title: Notas de versão do [!DNL Adobe Commerce as a Cloud Service]
description: Saiba mais sobre os recursos e as melhorias mais recentes do  [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
nudge: true
autotag-review: '2026-06-18T16:04:15.842Z'
TQID: 'https://experienceleague.adobe.com/MmwdYWe5Et9m0BvtrVYNK2jiJ3fZBnUe2K6xMdIbMUk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: adedf3b3-e153-47a3-ae73-b5d65067b544
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
last-update: 2026-08-07
source-git-commit: ecaeba0d36376bf7f9ac864135cbf225c7fd8634
workflow-type: tm+mt
source-wordcount: 5345
ht-degree: 0%

---

# Notas de versão

As notas de versão a seguir contêm atualizações para [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Se você estiver usando o Adobe Commerce no local ou o Adobe Commerce na infraestrutura em nuvem, consulte as [notas de versão do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## Agosto de 2026 - versão #1 {#latest}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram publicados na Produção em 12 de agosto de 2026.

>[!BEGINSHADEBOX]

### Assinar um evento para pagamentos de fatura

Um novo evento `observer.sales_order_invoice_pay` é emitido quando um pagamento de fatura é registrado, para que as integrações possam assinar o evento, em vez de sondar as alterações de status da fatura. <!-- CEXT-5983 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um problema em que a busca das empresas atribuídas de um cliente por meio do GraphQL podia ser lenta. <!-- ACCS-1425 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Julho de 2026

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

Os seguintes itens estarão disponíveis nos ambientes de produção a partir de 28 de julho de 2026.

>[!BEGINSHADEBOX]

### Editar pedidos com REST

>[!IMPORTANT]
>
>Esse recurso está desativado por padrão. Para ativá-lo, entre em contato com o Gerente de sucesso do cliente da Adobe Commerce ou crie um tíquete de suporte.

Novos pontos de extremidade de API [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/order-management) replicam o recurso [!DNL Commerce Admin] [!UICONTROL **Editar Pedido**], permitindo integrações para editar um pedido de forma programática:

| Método | Endpoint | Descrição |
| --- | --- | --- |
| `POST` | `/V1/orders/{orderId}/edit/start` | Copie o pedido em um novo carrinho editável e retorne a ID do carrinho. |
| `POST` | `/V1/orders/{orderId}/edit/submit` | Envie o carrinho modificado como um novo pedido e cancele o pedido original. |

Depois de chamar `edit/start`, modifique o carrinho retornado usando os pontos de extremidade REST padrão do carrinho e chame `edit/submit`. A nova ordem herda o método de pagamento da ordem original, a menos que você a substitua pelo carrinho e seja criada como uma substituição vinculada para o original cancelado. Ambos os pontos de extremidade exigem o recurso de ACL `Magento_Sales::actions_edit`. <!-- ACCS-1284 -->

### Filtrar pedidos e faturas por empresa

Os pontos de extremidade da API REST `GET /V1/orders` e `GET /V1/invoices` agora oferecem suporte à filtragem por `company_id` e `company_name`, permitindo que as integrações B2B recuperem pedidos ou faturas de uma empresa específica em uma única solicitação. <!-- ACCS-1111, CCSAAS-5076 -->

### Importar mais códigos de cupom por arquivo

O limite de importação de cupom em massa por arquivo pode ser ajustado entrando em contato com o Gerente de sucesso do cliente da Adobe Commerce ou criando um tíquete de suporte. <!-- CCSAAS-5176 -->

### Gerenciar modelos de email personalizados por meio da API

Os novos pontos de extremidade da REST API a seguir permitem que as integrações listem, recuperem e criem [modelos de email personalizados](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/):

| Método | Endpoint | Descrição |
| --- | --- | --- |
| `GET` | `/V1/custom-email/templates` | Liste seus modelos de email personalizados, retornando a ID, o código, o assunto e o tipo de cada modelo. |
| `GET` | `/V1/custom-email/templates/{id}` | Recupere um único modelo, incluindo seu corpo e estilos. |
| `POST` | `/V1/custom-email/templates` | Crie um modelo de email personalizado e retorne sua ID atribuída pelo servidor. |

Use uma ID de modelo retornada com o ponto de extremidade `POST /V1/custom-email/send` em vez de pesquisar a ID manualmente.

Todos os pontos de extremidade `custom-email` exigem acesso ao `Marketing > Communications > Email template` [recurso de função](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-user-roles#step-2assign-resources). <!-- CCSAAS-5089, CCSAAS-5090 -->

### Gerenciar toda a cadeia de pedidos por meio da REST API

>[!IMPORTANT]
>
>Esse recurso é experimental e deve ser ativado entrando em contato com o Gerente de sucesso do cliente da Adobe Commerce ou criando um tíquete de suporte.

Novos pontos de extremidade de API REST [`orderChain`](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/order-management) permitem que as integrações modifiquem uma ordem usando sua ID e resolvam automaticamente a cadeia completa de ordens editadas:

| Método | Endpoint | Descrição |
| --- | --- | --- |
| `POST` | `/V1/orderChain/{orderId}/invoice` | Criar uma fatura para a ordem, resolvendo os itens a serem faturados na cadeia de ordens. |
| `POST` | `/V1/orderChain/{id}/cancel` | Cancelar a ordem atual na cadeia. |
| `POST` | `/V1/orderChain/{id}/hold` | Colocar a ordem em espera. |
| `POST` | `/V1/orderChain/{id}/unhold` | Remover a suspensão da ordem. |
| `POST` | `/V1/orderChain/{id}/emails` | Enviar uma notificação por e-mail de pedido. |
| `POST` | `/V1/orderChain/{id}/comments` | Adicione um comentário ao pedido. |
| `GET` | `/V1/orderChain/{id}/comments` | Recuperar os comentários do pedido. |
| `GET` | `/V1/orderChain/{id}/statuses` | Recupera o status atual do pedido. |

`GET` pontos de extremidade que oferecem suporte à filtragem de faturas, remessas, avisos de crédito e devoluções agora oferecem suporte à filtragem por `order_original_id`. Filtrar por `order_original_id` retorna detalhes sobre toda a cadeia de pedidos, não apenas o pedido único. Um exemplo de terminal que suporta este recurso é `GET /V1/invoices`. <!-- ACCS-1004, ACCS-1005 -->

### Pesquisar a grade da ordem por valores de atributos personalizados

>[!IMPORTANT]
>
>Esse recurso está desativado por padrão. Para ativá-lo, entre em contato com o Gerente de sucesso do cliente da Adobe Commerce ou crie um tíquete de suporte.

Os comerciantes agora podem filtrar a grade de pedidos [!DNL Commerce Admin] pelos valores armazenados em ordem de atributos personalizados. Um filtro de [!UICONTROL **Atributos Personalizados**] está disponível na linha de filtro de grade de ordem.<!-- ACCS-923 -->

### Definir uma origem de inventário nomeada nos itens do carrinho

A nova mutação do GraphQL `setNominatedSourceOnCartItems` atribui uma origem de inventário específica aos itens do carrinho, suportando cenários como retirada na loja (BOPIS) e remessa da loja. A mutação aceita um `cart_id` e uma lista de itens, cada um com um `cart_item_uid` e um `source_code`, e retorna qualquer `rejected_items` com um código de erro estruturado: `UNKNOWN_SOURCE`, `SOURCE_DISABLED`, `NOT_ENOUGH_QTY` ou `SKU_SOURCE_CONFLICT`. Cada SKU em um carrinho é resolvido para uma única fonte nomeada e transmitir uma `source_code` nula ou vazia limpa a indicação. <!-- ACCS-932 -->

### Inscrever-se em um evento para carrinhos que correspondem às regras de lembrete

Um novo evento `observer.reminder_matched_carts` é emitido depois que as regras de lembrete de email executam a lógica correspondente, levando informações sobre os carrinhos que corresponderam. As integrações podem assinar esse evento e encaminhar os dados para um sistema externo, como uma plataforma de marketing, em vez de depender dos emails de lembrete nativos. <!-- CCSAAS-5173 -->

### Suprimir emails transacionais por área ou modelo

Uma nova configuração de [Supressão de Email](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/email-suppression) ([!UICONTROL **Lojas**] > [!UICONTROL **Configuração**] > [!UICONTROL **Serviços da Adobe**] > [!UICONTROL **Supressão de Email**]) permite que os administradores impeçam [!DNL Commerce] de enviar emails transacionais de forma seletiva. Você pode suprimir emails por área funcional (como Conta do Cliente, Order Management, Devoluções, Check-out, Marketing ou B2B) ou por uma lista exata de identificadores de modelo.<!-- ACCS-1025 -->

### Exibir o histórico de modificação de pedidos no Administrador

A página de detalhes do pedido [!DNL Commerce Admin] agora exibe a cadeia de modificação completa de um pedido que inclui o pedido original e todos os pedidos secundários criados por meio de edições subsequentes. Os comerciantes podem navegar entre pedidos, alternar a visibilidade de pedidos cancelados e acessar todas as faturas, remessas, avisos de crédito e comentários de pedidos associados na exibição em cadeia.<!-- ACCS-968 -->

>[!NOTE]
>
>Para ativar esse recurso, entre em contato com o Gerente de sucesso do cliente da Adobe Commerce.

### Exibir ativos sincronizados em [!DNL AEM Assets]

A integração [!DNL AEM Assets] agora inclui uma página [!UICONTROL **Status de Sincronização**] ([!UICONTROL **Lojas**] > [!UICONTROL **AEM Assets**] > [!UICONTROL **Status de Sincronização**]) com uma exibição de lista centrada em ativos de todos os ativos sincronizados, incluindo filtragem, colunas classificáveis, como a data da última sincronização, e detalhes de erros para sincronizações com falha.<!-- ACAP-1246 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Agora, catálogos compartilhados grandes são mais fáceis de gerenciar no Admin, com tempos de carregamento melhorados e probabilidade reduzida de tempos limite. <!-- CCSAAS-4946, CCSAAS-4925, CCSAAS-1245, CCSAAS-1246 -->

* Correção de uma falha na criação de remessa que ocorria ao criar remessas para pedidos que continham produtos configuráveis. <!-- ACCS-1095 -->

* Correção de um problema no [!DNL Commerce Admin] em que o menu de navegação esquerdo podia desaparecer. <!-- ACCS-1035 -->

* Melhora no desempenho da atribuição e do cancelamento de atribuição em catálogos compartilhados. <!-- ACCS-1324, CCSAAS-5177, CCSAAS-5190, CCSAAS-5192 -->

* Desempenho de integração [!DNL AEM Assets] aprimorado. <!-- ACAP-1242 -->

* Correção de um erro que poderia ocorrer ao adicionar uma SKU de produto simples a um produto configurável no [!DNL Commerce Admin]. <!-- ACCS-1132 -->

* Correção de um problema em que a fila de mensagens poderia parar de processar novas mensagens quando acumulava muitos registros desatualizados. <!-- ACCS-1292 -->

* Correção de um problema em que a criação do pedido do administrador falhava com um erro &quot;SKU não disponível no catálogo compartilhado&quot;. <!-- ACCS-1318 -->

* Solução de uma falha que ocorria ao criar ou editar produtos agrupados. <!-- CCSAAS-5211 -->

* Correção de um problema em que o posicionamento da ordem não reservava estoque na origem nomeada para itens que usavam retirada na loja ou entrega na loja. <!-- ACCS-1374 -->

* As taxas personalizadas obsoletas agora são apagadas da resposta de consulta do carrinho. <!-- ACCS-1400 -->

* Solução de um problema na integração [!DNL AEM Assets] em que os atributos da função de ativo do produto perderam dados de localidade durante a exportação do catálogo. <!-- ACCS-1401 -->

* Aviso recebido ao salvar uma integração indicando que [!DNL Dynamic Media] não está habilitado foi aprimorado. <!-- ACAP-1298 -->

* Agora, os campos de nome do evento e alias ficam em minúsculas quando você assina um evento. <!-- CEXT-6164 -->

* Os padrões de regra regex do Webhook agora são validados ao salvar um webhook condicional. <!-- CEXT-6287 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Junho de 2026 - versão #1

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

Os itens a seguir foram lançados para ambientes de Produção em 4 de junho de 2026.

>[!BEGINSHADEBOX]

### Adicionar e editar códigos de cupom personalizados no Administrador

Os comerciantes agora podem [criar e editar códigos de cupom personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-coupon#method-3-custom-coupon-codes) diretamente de [!DNL Commerce Admin] nas regras manuais de preços do carrinho. Um novo botão [!UICONTROL **Adicionar cupom personalizado**] está disponível na seção [!UICONTROL **Gerenciar códigos de cupom**] ao editar uma regra de preço de carrinho. <!-- CCSAAS-4508 -->

### Rastrear remessas usando transportadoras padrão e personalizadas

O rastreamento de pedidos agora é confiável para transportadoras padrão e personalizadas no [!DNL Commerce Admin], ajudando os comerciantes a fornecerem experiências consistentes de rastreamento pós-compra. Anteriormente, selecionar uma operadora, como UPS ou FedEx, e aplicar uma ID de rastreamento poderia impedir a exibição do link de rastreamento. Nenhuma ação do comerciante é necessária para restaurar esse comportamento. O suporte para link de rastreamento também está disponível para [operadoras personalizadas](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-reference/) criadas com o [!DNL App Builder Integration Starter Kit]. <!-- ACCS-891 -->

### Exibir tipos de entrada de atributo na grade Atributos do Produto

Uma nova coluna [!UICONTROL **Tipo de Atributo**] agora está visível na grade de Atributos de Produto em ([!UICONTROL **Lojas**] > _[!UICONTROL Attributes]_>[!UICONTROL **Produto**]), que exibe o tipo de entrada (como campo de texto, lista suspensa ou sim/não) para cada atributo de produto, incluindo os tipos contribuídos por extensões. Isso facilita a identificação e o gerenciamento de atributos ao trabalhar com conjuntos de atributos grandes. <!-- ACCS-925 -->

### Personalizar o cabeçalho Responder para emails personalizados

Agora os comerciantes podem configurar o cabeçalho [!UICONTROL **Responder para**] usado pelo ponto de extremidade [POST /rest/V1/custom-email/send](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/), para que as respostas dos clientes possam ser encaminhadas a um endereço diferente do remetente. <!-- ACCS-1037 -->

### Exibir preços de camada na página de edição do produto em grandes ambientes de catálogo compartilhado

Os comerciantes com um grande número de catálogos compartilhados agora podem acessar a guia somente leitura [!UICONTROL **Preços da Camada**] na página de edição do produto no [!DNL Commerce Admin]. <!-- CCSAAS-4922 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um problema em que o ponto de extremidade REST do POST `V1/async/custom-email/send` retornava um erro de validação `UnstructuredArray`. O ponto de extremidade assíncrono agora funciona de forma consistente com o ponto de extremidade POST `V1/custom-email/send` síncrono. <!-- ACCS-921 -->

* Correção de um problema em que os atributos serializáveis personalizados em entidades como Empresa eram limpos involuntariamente ao atualizar a entidade por meio do REST sem incluir os atributos personalizados na carga. Os atributos personalizados agora são preservados quando não fornecidos. <!-- ACCS-946 -->

* Correção de um erro &quot;o consumidor não está autorizado&quot; que poderia impedir logons do GraphQL convidado quando o cabeçalho `X-Adobe-Company` estava presente na solicitação. <!-- ACCS-949 -->

* Correção de um problema em que a edição ou exclusão de uma empresa no [!DNL Commerce Admin] poderia falhar com um erro &quot;Nenhuma entidade&quot; após atribuir um cliente à empresa por meio do ponto de extremidade REST PUT `V1/customers/companies`. <!-- ACCS-856 -->

* Solução de um problema com status de grade de ordens de venda obsoletas. <!-- CCSAAS-4915 -->

* Correção de um problema no [!DNL Commerce Admin] em que os arquivos anexados como amostras e links em produtos baixáveis retornavam um erro `404` quando acessados na página de edição do produto. <!-- CCSAAS-4394 -->

* Correção de um erro &quot;Undefined array key &#39;simple_sku&#39;&quot; que poderia ocorrer ao criar uma remessa de um pedido que continha produtos configuráveis. <!-- CCSAAS-4877 -->

* A consulta do GraphQL `guestOrderByToken` agora retorna uma mensagem de erro mais informativa quando chamada com um token malformado, em vez de um erro de servidor interno. <!-- CCSAAS-4921 -->

* A consulta do GraphQL `customer` agora retorna uma mensagem de erro mais informativa quando os pedidos do cliente não podem ser carregados. <!-- ACCS-867 -->

* O ponto de extremidade REST GET `V1/customers/{customerId}` agora retorna o campo de configuração `assistance_allowed`. <!-- USF-4132 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Maio de 2026 - versão #1

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para ambientes de Produção em 7 de maio de 2026.

>[!BEGINSHADEBOX]

### Ignorar reCAPTCHA para autenticação OTP programática

Uma nova opção de configuração permite ignorar a validação do reCAPTCHA para a mutação do GraphQL [`exchangeOtpForCustomerToken`](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/). Isso permite workflows de punchout B2B em que a troca de senha ocasional (OTP) é iniciada de forma programática sem uma entrada de formulário, tornando desnecessária a validação do reCAPTCHA. Esse recurso se baseia no recurso [logon com código único](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer){target="_blank"} introduzido na versão de março de 2026. A mutação `exchangeOtpForCustomerToken` continua a exigir o reCAPTCHA por padrão quando o reCAPTCHA é habilitado para logon do cliente. Entre em contato com o Gerente de sucesso do cliente da Adobe Commerce para ativar essa opção. <!-- ACCS-850 -->

### Editar ordens parcialmente faturadas

O botão [!UICONTROL **Editar**] agora está disponível na tela [!UICONTROL **Exibição de Pedido**] para pedidos parcialmente faturados, dando aos comerciantes maior flexibilidade para modificar pedidos que ainda estão em andamento. Anteriormente, os pedidos com qualquer fatura não podiam ser editados, mesmo quando itens não faturados permaneciam. Desde que qualquer item no pedido ainda possa ser faturado, o pedido pode ser editado. Os comerciantes com integrações personalizadas que dependam da restrição de edição anterior devem revisar seus workflows. <!-- ACCS-849 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um problema em que o atributo de extensão `stock_item` não era retornado no ponto de extremidade da lista de API REST `GET /V1/products`. A resposta agora corresponde ao contrato de API documentado. <!-- ACCS-819 -->

* Correção de um problema em que os links de redefinição de senha em emails retornavam um erro 404. <!-- ACCS-797 -->

* Desempenho de consulta de histórico de pedidos aprimorado para empresas que usam filtros de intervalo de datas. <!-- ACCS-859 -->

* Correção de um problema em que os usuários da empresa B2B podiam visualizar pedidos de pares de antes que um usuário entrasse na empresa. <!-- ACCS-859 -->

* Solução de problemas de tempo limite de check-out que poderiam afetar o desempenho da API REST ao carregar cotações com `trigger_recollect` habilitado. <!-- CCSAAS-4904 -->

* Correção de problemas de carregamento de página que podem ocorrer após o envio de um pedido no [!DNL Commerce Admin]. <!-- CCSAAS-4413 -->

* Correção de um problema em que pedidos com o mesmo carimbo de data e hora podiam exibir informações desatualizadas do status do pedido na grade da ordem de venda. <!-- CCSAAS-4890 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Abril de 2026 - versão #3

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para ambientes de Produção em 27 de abril de 2026.

>[!BEGINSHADEBOX]

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Adição do ponto de extremidade da API REST `GET /V1/order-statuses` para recuperar todos os status de pedido configurados com suas atribuições de estado. <!-- CEXT-6100 -->

* Solução de um problema que fazia com que `custom_attributes` entidades como Pedido, Carrinho, Fatura, Aviso de Crédito e Empresa não fossem exibidas no esquema REST. <!-- CCSAAS-4818 -->

* Correção de erros de processamento de mensagens duplicadas (`MessageLockException`) no consumidor assíncrono de API em massa. <!-- CCSAAS-4805 -->

* Numerar atributos de produto agora é renderizado como filtros de/para intervalo na grade de produtos [!DNL Commerce Admin] quando o atributo está habilitado para opções de filtro. <!-- ACCS-761 -->

* Correção de um problema em que os emails de lembrete de abandono de carrinho não exibiam imagens do produto ao usar o [!DNL AEM Assets]. <!-- ACCS-798 -->

* Correção de um problema em que um erro falso &quot;tamanho máximo de upload&quot; podia aparecer ao adicionar arquivos, amostras ou links a produtos baixáveis. <!-- ACCS-813 -->

* Correção de um problema em que salvar um produto atribuído a vários catálogos compartilhados poderia causar um erro. <!-- ACCS-788 -->

* Correção de um problema em que a consulta do histórico de pedidos podia ser lenta e causar erros de falta de memória no banco de dados para empresas com muitos pedidos. <!-- ACCS-808 -->

* Correção de um problema em que a validação do arquivo de importação podia falhar. <!-- CCSAAS-4364 -->

* A configuração **[!UICONTROL Recently Viewed/Compared Products]** foi removida da seção **[!UICONTROL Catalog]** em **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**, pois não é suportada pelo administrador [!DNL Adobe Commerce as a Cloud Service]. <!-- ACCS-793 -->

>[!ENDSHADEBOX]

## Abril de 2026 - versão #2

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

<!-- [!BADGE Sandbox]{type=Caution tooltip="The items listed are currently only available in Sandbox environments. Adobe makes new releases available in Sandbox environments first to provide time to test upcoming changes before the release is available on Production environments."} -->

Os itens a seguir foram lançados para ambientes de Produção em 16 de abril de 2026.

>[!BEGINSHADEBOX]

### Implementar totais de cotação personalizados com webhooks

O `plugin.magento.out_of_process_totals_collector.api.get_total_modifications.execute` [webhook](https://developer.adobe.com/commerce/extensibility/webhooks/) agora está disponível em [!DNL Adobe Commerce as a Cloud Service]. Use-a para implementar modificações personalizadas de totais de cotação por meio da extensibilidade fora do processo. <!-- CEXT-5896 -->

### Regras de lembrete de email reutilizáveis (experimental)

>[!IMPORTANT]
>
>Esse recurso é experimental e deve ser ativado entrando em contato com o Gerente de sucesso do cliente da Adobe Commerce ou criando um tíquete de suporte.

[As regras de lembrete de email](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules#rule-repeatability) agora oferecem suporte a uma configuração de reutilização de regra opcional que permite que a mesma regra seja reaplicada a um cliente depois que a condição de acionador original não se aplicar mais.

Por exemplo, se um cliente abandonar um carrinho, concluir a compra e depois abandonar um novo carrinho, a regra poderá ser acionada novamente. Sem essa configuração, um cliente que limpa o acionador original é excluído permanentemente de correspondências futuras da mesma regra.

### Exibir o relatório de Transações de Serviços de Pagamento

Se você tiver o [[!DNL Payment Services]](https://experienceleague.adobe.com/en/docs/commerce/payment-services/get-started/production) habilitado, a [Interface do Usuário do Painel](../payment-services/payments-home.md) agora estará disponível no [!DNL Commerce Admin], fornecendo acesso ao [Relatório de transações](../payment-services/reporting.md#transactions-report-view) para exibir e gerenciar transações de pagamento. <!-- PAY-6510 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um erro 500 na página Empresas de Atribuição do Catálogo Compartilhado que poderia ocorrer ao usar catálogos compartilhados grandes com a SDK da Interface do Administrador. <!-- CCSAAS-4783 -->

* Correção de um problema em que os clientes da empresa não podiam ver seus próprios pedidos se esses pedidos fossem feitos antes de o cliente ser atribuído à empresa. <!-- ACCS-746 -->

>[!ENDSHADEBOX]

## Abril de 2026

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para ambientes de Produção em 1 de abril de 2026.

>[!BEGINSHADEBOX]

### Adicionar arquivos aos produtos

[!DNL Adobe Commerce as a Cloud Service] agora dá suporte a [adição de arquivos a produtos](./product-files.md) usando atributos de produto do tipo arquivo. Você pode carregar arquivos manualmente na página de edição do produto, de forma programática por meio da API REST ou em massa fornecendo URLs externas em CSV. <!-- ACCS-535, ACCS-565 -->

### Verificar o status de assinatura do alerta de preço e estoque por meio do GraphQL

Novas consultas ao GraphQL, [`isSubscribedProductAlertStock`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-stock/){target="_blank"} e [`isSubscribedProductAlertPrice`](https://developer.adobe.com/commerce/webapi/graphql/schema/products/queries/is-subscribed-product-alert-price/){target="_blank"}, permitem que as vitrines determinem se um comprador já está inscrito no estoque ou alertas de preço de um produto. <!-- ACCS-334 -->

### Criar atributos de produto numéricos que oferecem suporte a valores negativos

Um novo `numeric` [tipo de entrada de atributo de produto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) permite que os comerciantes criem atributos decimais que oferecem suporte a valores negativos. <!-- ACCS-600 -->

### Consultar a configuração do reCAPTCHA para vários formulários em uma solicitação do GraphQL

A consulta [`recaptchaFormConfigs` &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/store/queries/recaptcha-form-configs/) pode retornar detalhes de configuração para vários tipos de formulário em uma única solicitação. <!-- ACCS-628 -->

### Exibir todas as ordens da empresa com uma nova permissão B2B

Uma nova `view_all_company_orders` [função da empresa](https://developer.adobe.com/commerce/webapi/rest/b2b/roles/) permite que os clientes da empresa B2B visualizem todos os pedidos dentro da empresa, incluindo pedidos históricos criados por usuários administradores. <!-- ACCS-675 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Agora é possível filtrar os resultados de Pedido e API REST da empresa usando atributos personalizados aplicáveis e cenários compatíveis, como pesquisas de pedido no escopo da empresa. <!-- ACCS-633 -->

* Correção de um erro que poderia aparecer no console do desenvolvedor do navegador. <!-- CCSAAS-4650 -->

* Correção de um erro que poderia ocorrer ao cancelar um pedido de convidado com comentários de pedido. <!-- ACCS-674 -->

* Correção de um erro que poderia ocorrer ao adicionar um produto agrupado com muitos itens associados a uma lista de requisições. <!-- ACCS-627 -->

>[!ENDSHADEBOX]

## Março de 2026 - lançamento #2

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para ambientes de Produção em 24 de março de 2026.

>[!BEGINSHADEBOX]

### Fazer logon como cliente usando códigos únicos

Agora os administradores podem gerar [códigos únicos](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customer-accounts/manage/login-as-customer) para representação do cliente por meio da [!DNL Commerce Admin] e da API REST. O código único pode ser trocado por um token de acesso do cliente por meio das mutações do GraphQL `generateCustomerToken` ou `exchangeOtpForCustomerToken`, permitindo fluxos de &quot;Logon como Cliente&quot; sem senha para cenários de compras com auxílio do vendedor. <!-- ACCS-404 -->

Para obter orientação sobre como implementar este recurso usando APIs, consulte a documentação da [API REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/login-as-customer/) e do [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/).

### Gerenciar contas de cartão-presente por meio da REST API

[Contas de cartão-presente](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/gift-card-accounts/) agora podem ser criadas, atualizadas, excluídas e consultadas por meio da API REST. Além disso, o suporte à importação em massa de JSON está disponível por meio do endpoint `/V1/import/json`, permitindo integrações de terceiros para sincronizar programaticamente cartões-presente. <!-- ACCS-476 -->

### Acionar emails transacionais por meio da API REST

Um novo ponto de extremidade da API REST (`POST /V1/custom-email/send`) permite [acionar emails transacionais](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/custom-email/) sob demanda especificando uma ID de modelo de email, email de destinatário e variáveis de modelo. A API é compatível com matrizes aninhadas como variáveis de modelo para conteúdo de email complexo. <!-- ACCS-325, ACCS-481 -->

### Assine o webhook get-rates de envio fora de processo

O webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` agora está disponível na lista de Webhooks de Administração em [!DNL Adobe Commerce as a Cloud Service]. Use-o para implementar [métodos de envio personalizados](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#shipping-methods). <!-- ACCS-478 -->

### Fazer upload de PDFs e outros arquivos por meio de atributos de produto

Um novo &quot;arquivo&quot; [Tipo de Entrada de Atributo](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) permite criar conjuntos de atributos onde você pode carregar arquivos, como PDFs, para produtos individuais. Você pode configurar as extensões de arquivo permitidas e o tamanho máximo de arquivo navegando até [!UICONTROL **Lojas**] > [!UICONTROL **Configuração**] > [!UICONTROL _Catálogo_] > [!UICONTROL **Atributos de Arquivo de Produto**]. <!-- ACCS-535, ACCS-565 -->

### Configurar atributos personalizados da empresa

Agora, os administradores podem gerenciar atributos personalizados da empresa na página Empresa - Editar na [!DNL Commerce Admin]. Os atributos personalizados podem ser configurados, salvos e validados na interface do usuário do Administrador para [!DNL Adobe Commerce as a Cloud Service].

Para configurar atributos personalizados da empresa, navegue até [!UICONTROL **Clientes**] > [!UICONTROL **Empresas**] e selecione uma empresa para abrir a página de edição. Em seguida, selecione a guia [!UICONTROL **Atributos personalizados**] para adicionar novos atributos.
<!-- ACCS-294 -->

### Assinar alertas de preço e estoque por meio do GraphQL

Agora as vitrines EDS funcionam com [alertas de preço e estoque](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/product-alerts/alert-setup). <!-- ACCS-334 -->

Além disso, há várias novas mutações do GraphQL para assinar e cancelar a assinatura de alertas de preço e estoque:

+++Novas mutações do GraphQL

```graphql
mutation {
  subscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStock(input: { sku: "ADB111" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertStockAll {
    success
    message
  }
}
```

```graphql
mutation {
  subscribeProductAlertPrice(input: { sku: "ADB112" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPrice(input: { sku: "ADB115" }) {
    success
    message
  }
}
```

```graphql
mutation {
  unsubscribeProductAlertPriceAll {
    success
    message
  }
}
```

+++

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* A função da empresa [!UICONTROL Sales] > [!UICONTROL View Orders] agora funciona conforme esperado. <!-- ACCS-604 -->

* O atributo de extensão do cliente `last_login_at` agora está disponível por meio da REST API, permitindo que as integrações recuperem a data de logon mais recente para cada cliente. <!-- ACCS-555 -->

* Correção de um problema com as sugestões do formulário de integração [!DNL AEM Assets]. <!-- ACCS-209 -->

* Correção de um problema em que as ações de atribuição e cancelamento de atribuição em massa da empresa na grade Catálogo compartilhado podiam causar um erro. <!-- CCSAAS-4614 -->

* Correção de um problema em que os preços do carrinho personalizado eram substituídos quando o mesmo produto era adicionado ao carrinho novamente com uma quantidade ou preço personalizado diferente. <!-- ACCS-529 -->

* Os UIDs de item de lista de requisição agora são consistentes com os UIDs de item de carrinho e lista de desejos. <!-- ACCS-349 -->

* Correção do tempo limite da página de edição do produto que poderia ocorrer com catálogos compartilhados grandes. <!-- CCSAAS-4657 -->

* Os pontos de extremidade da API REST GET `/V1/directory/countries` e GET `/V1/directory/countries/:countryId` foram habilitados novamente para integrações de administrador, permitindo que os clientes pesquisem dados válidos de país e região. <!-- ACCS-518 -->

* Correção de um problema de tempo limite que poderia ocorrer na API REST quando um usuário tem um catálogo compartilhado grande. <!-- ACCS-4657 -->

* Correção de um problema em que as empresas B2B bloqueadas ainda podiam adicionar produtos ao carrinho. <!-- ACCS-552 -->

* Se você tiver uma grande quantidade de dados nas grades do Cliente ou da Empresa, os botões de exportação não estarão mais disponíveis para evitar erros. <!-- ACCS-320 -->

* Correção de um problema em que os tamanhos de arquivo anexados não eram exibidos corretamente. <!-- ACCS-566 -->

* Correção de um problema com a criação e exclusão dos tipos de atributos &quot;Arquivo&quot; no [!DNL Commerce Admin]. <!-- ACCS-605, ACCS-606 -->

>[!ENDSHADEBOX]


## Março de 2026 - lançamento #1

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para ambientes de Produção do [!DNL Adobe Commerce as a Cloud Service] em 9 de março de 2026.

>[!BEGINSHADEBOX]

### Ferramentas e tutoriais de codificação do App Builder AI

Agora você pode usar a [Ferramenta de desenvolvimento de codificação de IA](https://developer.adobe.com/commerce/extensibility/developer-agent/){target="_blank"} para criar novos aplicativos [!DNL App Builder] e converter extensões PHP [!DNL Adobe Commerce] existentes em aplicativos [!DNL App Builder]. Os seguintes tutoriais estão disponíveis para demonstrar como usar as ferramentas:

* [Pré-requisitos do tutorial](./tutorials/tutorial-prerequisites.md)
* [Tutorial da extensão de classificações](./tutorials/ratings-extension.md)
* [Tutorial de extensão do método de envio](./tutorials/shipping-method-extension.md)

### Acesse o gerenciamento de aplicativos do App Builder por meio do Administrador

O [!DNL Commerce Admin] agora inclui um item de menu vinculado ao [Gerenciamento de Aplicativos](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, um shell unificado para gerenciar aplicativos [!DNL App Builder] associados à instância do Commerce. Essa adição é habilitada pela atualização mais recente do SDK da interface do administrador. <!-- CEXT-5755 -->

### Solicitar alteração de limite de criação de entidade

O limite de sites, lojas e visualizações de loja era anteriormente limitado a 50. Agora você pode enviar uma [solicitação de suporte](https://experienceleague.adobe.com/home?support-tab=home#support) para modificar esses limites, se necessário. <!-- ACCS-398 -->

### Personalizar mensagens de autenticação da loja com códigos de erro estruturados

A [`generateCustomerToken` mutação do GraphQL &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} agora retorna códigos de erro digitados junto com mensagens de erro, permitindo que as vitrines exibam mensagens de interface do usuário específicas por motivo de falha. Os códigos de erro disponíveis são: `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` e `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Enviar lembretes de email automatizados para inatividade do carrinho e da lista de desejos

O [módulo de Lembrete de Email](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) agora está ativo no [!DNL Adobe Commerce as a Cloud Service], permitindo que os comerciantes criem regras automatizadas de lembrete que acionam emails para clientes com base na inatividade do carrinho e da lista de desejos. <!-- CCSAAS-4597 -->

### Assinar o webhook de eventos de exclusão de categoria

O webhook `observer.catalog_category_delete_before` agora está disponível em [!DNL Adobe Commerce as a Cloud Service]. Use-a para executar a lógica antes da exclusão de uma categoria. <!-- CEXT-5862 -->

### Rastrear pedidos de convidados feitos com um email registrado

Uma nova configuração opcional de nível de loja permite que os clientes [rastreiem pedidos de convidados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-guest#allow-guest-order-access-for-registered-emails) feitos por eles, caso o pedido tenha sido feito usando um endereço de email que corresponda a uma conta de cliente registrada. <!-- ACCS-289 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um problema em que alguns administradores de organização podiam acessar incorretamente instâncias de locatários sem direitos por locatário. <!-- ACCS-335 -->

* Correção de um problema que poderia desconectar um usuário do [!DNL Commerce Admin] ao fazer alterações em um catálogo compartilhado. <!-- ACCS-318 -->

* Correção de um problema que fazia com que alguns campos de webhooks fossem exibidos incorretamente na interface do usuário do [!DNL Commerce Admin]. <!-- CEXT-5874 -->

>[!ENDSHADEBOX]

## Fevereiro de 2026 - versão #2

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para os ambientes de Produção do [!DNL Adobe Commerce as a Cloud Service] em 24 de fevereiro de 2026.

>[!BEGINSHADEBOX]

### Enviar campos de contexto com eventos de comércio

[!DNL Adobe Commerce as a Cloud Service] agora oferece suporte a [campos de contexto](https://developer.adobe.com/commerce/extensibility/events/context-fields/) em cargas de evento, permitindo incluir dados que não fazem parte do evento por padrão. <!-- CEXT-5713 -->

### Assinar eventos de salvamento de item de cotação usando um novo webhook

O webhook `observer.sales_quote_item_save_before` agora está disponível em [!DNL Adobe Commerce as a Cloud Service]. Use-a para executar a lógica antes que um item de cotação seja salvo. <!-- ACCS-346 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um erro que poderia causar problemas de exibição na lista de produtos [!DNL Commerce Admin]. A lista de produtos agora limita o número de catálogos compartilhados exibidos para melhorar o desempenho. <!-- CCSAAS-1242 -->

* Correção de um erro no GraphQL que poderia impedir a adição de cartões-presente personalizáveis ao carrinho. <!-- ACCS-313 -->

>[!ENDSHADEBOX]

## Fevereiro de 2026 - versão #1

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para os ambientes de Produção do [!DNL Adobe Commerce as a Cloud Service] em 10 de fevereiro de 2026.

>[!BEGINSHADEBOX]

### Personalizar métodos de envio e exibir relatórios de administração

Os seguintes aprimoramentos foram feitos no [!DNL Commerce Admin]:

* [cargas de webhook de envio](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) fora de processo aprimoradas para incluir atributos personalizados de endereço de envio. Essa alteração permite que os comerciantes implementem métodos de envio personalizados. <!-- ACCS-235 -->

* Acesso adicionado aos relatórios de Administração, incluindo relatórios de [Clientes](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [Produtos](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports) e [Vendas](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Os relatórios não disponíveis em [!DNL Adobe Commerce as a Cloud Service] são rotulados como somente PaaS ([!BADGE PaaS somente]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."}).

### Capturar valores de fatura personalizados por meio da API REST

A API de fatura agora oferece suporte a [valores de captura personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) usando atributos de extensão. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>Devido a restrições legais, o valor de captura personalizado só está disponível na região da América do Norte (NA) e em outras regiões onde a captura excessiva de pagamento é permitida.

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção do filtro Grade de cupons para exibir todos os cupons personalizados criados por meio da API ou por importação. <!-- CCSAAS-4509 -->

* Correção de um problema no [!DNL Storefront Compatibility B2B Package] em que a mutação `setNegotiableQuoteShippingAddress` não salvava endereços inseridos manualmente no catálogo de endereços do cliente, mesmo quando `save_in_address_book` estava definido como `true`. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* Solução de um problema em que as imagens do produto não eram exibidas corretamente em [!DNL Edge Delivery Services] devido a valores `no_selection` corrompidos nos atributos personalizados relacionados às funções do ativo. <!-- ACAP-1206 -->

* Solução de um problema que impedia que contas de usuários federados com valores nulos de nome ou sobrenome acessassem o administrador do Commerce. <!-- ACCS-200 -->

* Simplificação da configuração do Seletor de ativos ao fornecer automaticamente IDs de cliente IMS específicas da região. Os comerciantes não precisam mais enviar tíquetes de suporte para configurar o Seletor de ativos para mapear imagens de categoria de produto com ativos. O sistema agora usa automaticamente IDs de clientes IMS dedicadas com base na região do Commerce. <!-- ACCS-175 -->

* Várias melhorias de desempenho e otimização. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

>[!ENDSHADEBOX]

## Janeiro de 2026

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para os ambientes de Produção do [!DNL Adobe Commerce as a Cloud Service] em 20 de janeiro de 2026.

>[!BEGINSHADEBOX]

### Drop-ins B2B

As seguintes alterações foram feitas aos componentes de devolução direta B2B:

* [!DNL Commerce Storefront on Edge Delivery Services] agora inclui [componentes B2B](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). Os seguintes menus suspensos B2B agora estão disponíveis:

  * **[Gerenciamento da empresa](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)** - Habilita o gerenciamento de perfis da empresa e permissões com base em funções para vitrines da Adobe Commerce.
  * **[Alternador de empresa](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)** - Fornece um componente de interface do usuário para que os usuários alternem entre várias empresas às quais estão associados.
  * **[Ordens de compra](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)** - Gerencia fluxos de trabalho de ordem de compra, regras de aprovação e histórico de ordens de compra para transações B2B.
  * **[Gerenciamento de cotações](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)** - Habilita cotações negociáveis para clientes B2B com fluxos de trabalho de solicitação de cotação, negociação e aprovação.
  * **[Listas de requisições](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)** - Fornece ferramentas para criar e gerenciar listas de requisições para compras repetidas e pedidos em massa.

* Lançado o pacote de compatibilidade da vitrine B2B. Este pacote aprimora o esquema do GraphQL B2B [!DNL Adobe Commerce] para ajudar a melhorar o desenvolvimento em sistemas B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. 
-->

### Links clicáveis para rastreadores de envio externos

Transforme os números de rastreamento de remessa incluídos nos emails do comprador de texto sem formatação em links clicáveis ao [habilitar as URLs de Rastreamento Personalizado](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Este recurso é suportado para USPS, UPS, FedEx e DHL. <!-- See PR #716 in commerce-admin -->

### Suporte corporativo ao Google reCAPTCHA

[!DNL Adobe Commerce as a Cloud Service] vitrines agora oferecem suporte a [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Esse recurso oferece proteção avançada de bot usando análise de risco adaptável e aprendizado de máquina para distinguir com precisão os usuários humanos dos bots automatizados. Ele fortalece a segurança do site, previne atividades fraudulentas e reduz o spam e o abuso para manter uma experiência de compra confiável. <!-- CCSAAS-4242 -->

### Acesso de administrador específico à instância

Agora você pode [atribuir acesso](./user-management.md#add-users) aos usuários a instâncias [!DNL Adobe Commerce as a Cloud Service] individuais na Admin Console. <!-- CCSAAS-4337 -->
<!-- See PR #332 -->

### Observabilidade

Ao usar o [!DNL App Builder], você pode obter maior visibilidade da instância do [!DNL Adobe Commerce as a Cloud Service] com a [observabilidade do OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), agora disponível automaticamente. O OpenTelemetry fornece métricas, registros e rastreamentos para ajudá-lo a monitorar o desempenho, solucionar problemas com mais rapidez e otimizar sua loja. Esse recurso permite insights proativos sobre a integridade do sistema e melhora a confiabilidade para seus clientes.

>[!NOTE]
>
>A observabilidade de OpenTelemetry requer o uso de [!DNL App Builder] ou outras ofertas de extensibilidade fora de processo (OOPE).

### Camada de preços para regras de preço de catálogo

Agora você pode combinar descontos de preço em camadas com descontos de regra de catálogo usando [regras de preço de catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Esse aprimoramento permite criar estratégias de preços mais dinâmicas e competitivas, recompensando compras em massa e aplicando descontos promocionais ao mesmo tempo. O resultado é maior flexibilidade para atrair clientes, aumentar o valor do pedido e gerar conversões.<!-- See PR #708 in commerce-admin -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados foram incluídos nesta versão:

* Correção de um erro que poderia ocorrer ao carregar um arquivo para S3. <!-- CCSAAS-4189 -->

* Correção de um erro `User is not entitled to access this instance` que poderia ocorrer ao fazer logon no Administrador do Commerce ou acessar a API REST. <!-- CCSAAS-4324 -->

* Correção de um erro que ocorria ao pré-visualizar ou enfileirar um informativo na grade Modelo de informativo. <!-- CCSAAS-4398 -->

* Correção de um erro de `404` que ocorria ao clicar no botão [!UICONTROL **Recarregar Dados**] no painel Administrador. <!-- CCSAAS-4468 -->

* Solução de um problema em que os atributos personalizados de produto não podiam ser atualizados por meio da REST API quando [!DNL AEM Assets integration] era habilitado e o produto tinha imagens. <!-- ACAP-1178 -->

* Várias melhorias de desempenho e otimização.
<!-- CCSAAS-4255 -->
<!-- CCSAAS-4233 -->
<!-- CCSAAS-4220 -->
<!-- CCSAAS-4252 -->
<!-- CCSAAS-4330 -->
<!-- CCSAAS-3669 -->
<!-- CCSAAS-4462 -->

>[!ENDSHADEBOX]

## Novembro de 2025

>[!BEGINSHADEBOX]

### Aprimoramentos

* [Gerenciamento de usuários](./user-management.md) - Alteração da função de **Administrador de Produtos** no Admin Console para atualizar automaticamente o acesso de usuários ao Administrador do Commerce. <!-- CCSAAS-3012 -->

* Adicionada a capacidade de carregar e recuperar anexos de cotações negociáveis, bem como arquivos e imagens associados a clientes e endereços de clientes no Amazon S3 usando URLs pré-assinadas no [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) e [REST](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads). Com REST, você também pode carregar imagens de categoria. <!-- CCSAAS-3250 -->

* Adicionados os pontos de extremidade `POST /V1/customers` e `PUT /V1/customers/{customerId}` à [API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) para criar e atualizar clientes. Esses endpoints exigem autorização IMS. <!-- CCSAAS-3112 -->

* Adicionada a [`exchangeOtpForCustomerToken` mutação](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), que requer um endereço de email do comprador e uma senha ocasional (OTP), e recebe um token de cliente em troca. Normalmente, essa mutação é usada em cenários em que um cliente precisa se autenticar usando um OTP enviado para seu email ou telefone.

* Se um endereço definido na tela de configuração [!UICONTROL **Armazenar Endereços de Email**] no Administrador contiver um valor que termina com `example.com`, a Commerce não enviará emails para esse endereço. Em vez disso, o sistema registra que o email não foi enviado.  <!-- CCSAAS-3533 -->

#### Atributos de ordem personalizados

* Os usuários administradores agora podem exibir e editar [atributos de pedido personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) diretamente nas telas Exibir, Editar e Criar Pedido no painel Administrador. Esse aprimoramento melhora o gerenciamento de dados de pedidos personalizados criados via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
