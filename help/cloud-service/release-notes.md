---
title: Notas de versão do [!DNL Adobe Commerce as a Cloud Service]
description: Saiba mais sobre os recursos e as melhorias mais recentes do  [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: f0f667254bb8b33905543afe83f17428bc3dbdc2
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# Notas de versão

As notas de versão a seguir contêm atualizações para [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Se você estiver usando o Adobe Commerce no local ou o Adobe Commerce na infraestrutura em nuvem, consulte as [notas de versão do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## Março de 2026 {#latest}

[!BADGE Sandbox]{type=Caution tooltip="Os itens listados estão disponíveis atualmente apenas em ambientes de sandbox. A Adobe disponibiliza novas versões em ambientes de sandbox primeiro para fornecer tempo para testar alterações futuras antes que a versão esteja disponível em ambientes de produção."}

Os itens a seguir estão disponíveis atualmente em ambientes de sandbox do [!DNL Adobe Commerce as a Cloud Service] e serão lançados para ambientes de produção em 9 de março de 2026.

>[!BEGINSHADEBOX]

### Ferramentas e tutoriais de codificação do App Builder AI

Agora você pode usar a [Ferramenta de desenvolvimento de codificação de IA](./migration/coding-tools.md) para criar novos aplicativos [!DNL App Builder] e converter extensões PHP [!DNL Adobe Commerce] existentes em aplicativos [!DNL App Builder]. Os seguintes tutoriais estão disponíveis para demonstrar como usar as ferramentas:

* [Pré-requisitos do tutorial](./tutorials/tutorial-prerequisites.md)
* [Tutorial da extensão de classificações](./tutorials/ratings-extension.md)
* [Tutorial de extensão do método de envio](./tutorials/shipping-method-extension.md)

### Acesse o gerenciamento de aplicativos do App Builder por meio do Administrador

O [!DNL Commerce Admin] agora inclui um item de menu vinculado ao [Gerenciamento de Aplicativos](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, um shell unificado para gerenciar aplicativos [!DNL App Builder] associados à instância do Commerce. Essa adição é habilitada pela atualização mais recente do SDK da interface do administrador. <!-- CEXT-5755 -->

### Solicitar alteração de limite de criação de entidade

O limite de sites, lojas e visualizações de loja era anteriormente limitado a 50. Agora você pode enviar uma [solicitação de suporte](https://experienceleague.adobe.com/home?support-tab=home#support) para modificar esses limites, se necessário. <!-- ACCS-398 -->

### Personalizar mensagens de autenticação da loja com códigos de erro estruturados

A [`generateCustomerToken` mutação do GraphQL ](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} agora retorna códigos de erro digitados junto com mensagens de erro, permitindo que as vitrines exibam mensagens de interface do usuário específicas por motivo de falha. Os códigos de erro disponíveis são: `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` e `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Enviar lembretes de email automatizados para inatividade do carrinho e da lista de desejos

O [módulo de Lembrete de Email](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) agora está ativo no [!DNL Adobe Commerce as a Cloud Service], permitindo que os comerciantes criem regras automatizadas de lembrete que acionam emails para clientes com base na inatividade do carrinho e da lista de desejos. <!-- CCSAAS-4597 -->

### Assinar o webhook de eventos de exclusão de categoria

O webhook `observer.catalog_category_delete_before` agora está disponível em [!DNL Adobe Commerce as a Cloud Service]. Use-a para executar a lógica antes da exclusão de uma categoria. <!-- CEXT-5862 -->

### Rastrear pedidos de convidados feitos com um email registrado

Uma nova configuração opcional no nível da loja (desativada por padrão) permite que os comerciantes rastreiem os pedidos de convidados feitos usando um endereço de email que corresponda a uma conta de cliente registrada. Quando ativado, os pedidos de check-out de convidado feitos com um email registrado permanecem acessíveis e também aparecem no histórico de pedidos do cliente.

Para habilitar este recurso, navegue até **Lojas** > Configurações > **Configuração** > Vendas > **Vendas** > **Check-out de Convidado** e defina a configuração **Permitir Acesso de Pedido de Convidado para Emails Registrados** como `Yes`.
<!-- ACCS-289 -->

### Melhorias e correções de erros

Os seguintes aprimoramentos, otimizações e correções de erros selecionados estão incluídos nesta versão:

* Correção de um problema em que alguns administradores de organização podiam acessar incorretamente instâncias de locatários sem direitos por locatário. <!-- ACCS-335 -->

* Correção de um problema que poderia desconectar um usuário do [!DNL Commerce Admin] ao fazer alterações em um catálogo compartilhado. <!-- ACCS-318 -->

* Correção de um problema que fazia com que alguns campos de webhooks fossem exibidos incorretamente na interface do usuário do [!DNL Commerce Admin]. <!-- CEXT-5874 -->

### Interno (A SER EXCLUÍDO)

As seguintes melhorias de infraestrutura estão incluídas:

* Atualização do núcleo [!DNL Adobe Commerce] de 2.4.8-p3 para 2.4.8-p4. <!-- CCSAAS-4588 -->

* Correção do tratamento da sessão de checkout de convidado para que a cotação do carrinho seja associada e mantida corretamente durante todo o fluxo de checkout de convidado. <!-- ACCS-261 -->

* Registro de erros do GraphQL estendido para capturar rastreamentos completos de pilha de exceção, melhorando a depuração. <!-- ACCS-305 -->

* Suíte de testes GraphQL com resolvedor de empresa portada para o ambiente de teste CCSaaS. <!-- CCSAAS-2122 -->

* Correção de falhas do cenário Admin em compilações CI de devbox PAT. <!-- ACCS-351 -->

* Adição do cenário de criação de produtos às compilações de tendências PAT. <!-- CCSAAS-4498 -->

* Conjunto de testes GraphQL BundleRequisitionList transferido para o ambiente de teste CCSaaS. <!-- CCSAAS-2113 -->

* Paralelização da execução do teste funcional de API do GraphQL no CI para reduzir o tempo de feedback. <!-- CCSAAS-4607 -->

* Atualização da documentação README. <!-- ACCS-404 -->

* Regras da IA de cursor expandidas para o contexto do repositório CCSaaS. <!-- PR #1295 -->

* Arquivos de migração obsoletos removidos. <!-- PR #1296 -->

* Processamento de modelo desativado durante a geração de dados de desempenho. <!-- PR #1297 -->

* Adição das regras de cursor e da documentação da CLI do Magento. <!-- PR #1300 -->

* Adição do script auxiliar do banco de dados local para desenvolvimento. <!-- PR #1305 -->

* Foram introduzidas regras de codificação de segurança do cursor. <!-- PR #1306 -->

* Análise estática de CI otimizada para ser executada somente em arquivos alterados. <!-- PR #1309 -->

{{accs-release}}

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

{{accs-release}}

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

{{accs-release}}

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

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Links clicáveis para rastreadores de envio externos

Transforme os números de rastreamento de remessa incluídos nos emails do comprador de texto sem formatação em links clicáveis ao [habilitar as URLs de Rastreamento Personalizado](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Este recurso é suportado para USPS, UPS, FedEx e DHL. <!-- See PR #716 in commerce-admin -->

### Suporte corporativo ao Google reCAPTCHA

[!DNL Adobe Commerce as a Cloud Service] vitrines agora oferecem suporte a [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Esse recurso oferece proteção avançada de bot usando análise de risco adaptável e aprendizado de máquina para distinguir com precisão os usuários humanos dos bots automatizados. Ele fortalece a segurança do site, previne atividades fraudulentas e reduz o spam e o abuso para manter uma experiência de compra confiável. <!-- CCSAAS-4242 -->

### Acesso de administrador específico à instância

Agora você pode [atribuir acesso](./user-management.md#add-users) aos usuários a instâncias [!DNL Adobe Commerce as a Cloud Service] individuais na Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

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

* Várias melhorias de desempenho e otimização.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Novembro de 2025

>[!BEGINSHADEBOX]

### Aprimoramentos

* [Gerenciamento de usuários](./user-management.md) - Alteração da função de **Administrador de Produtos** no Admin Console para atualizar automaticamente o acesso de usuários ao Administrador do Commerce. <!-- CCSAAS-3012 -->

* Adicionada a capacidade de carregar e recuperar anexos de cotações negociáveis, bem como arquivos e imagens associados a clientes e endereços de clientes no Amazon S3 usando URLs pré-assinadas no [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) e [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Com REST, você também pode carregar imagens de categoria. <!-- CCSAAS-3250 -->

* Adicionados os pontos de extremidade `POST /V1/customers` e `PUT /V1/customers/{customerId}` à [API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) para criar e atualizar clientes. Esses endpoints exigem autorização IMS. <!-- CCSAAS-3112 -->

* Adicionada a [`exchangeOtpForCustomerToken` mutação](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), que requer um endereço de email do comprador e uma senha ocasional (OTP), e recebe um token de cliente em troca. Normalmente, essa mutação é usada em cenários em que um cliente precisa se autenticar usando um OTP enviado para seu email ou telefone.

* Se um endereço definido na tela de configuração [!UICONTROL **Armazenar Endereços de Email**] no Administrador contiver um valor que termina com `example.com`, a Commerce não enviará emails para esse endereço. Em vez disso, o sistema registra que o email não foi enviado.  <!-- CCSAAS-3533 -->

#### Atributos de ordem personalizados

* Os usuários administradores agora podem exibir e editar [atributos de pedido personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) diretamente nas telas Exibir, Editar e Criar Pedido no painel Administrador. Esse aprimoramento melhora o gerenciamento de dados de pedidos personalizados criados via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
