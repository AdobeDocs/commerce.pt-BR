---
title: Notas de versão do [!DNL Adobe Commerce as a Cloud Service]
description: Saiba mais sobre os recursos e as melhorias mais recentes do  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 01b7e396f760258279d1314bb7fafe90957db577
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# Notas de versão

As notas de versão a seguir contêm atualizações para [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Se você estiver usando o Adobe Commerce no local ou o Adobe Commerce na infraestrutura em nuvem, consulte as [notas de versão do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## Janeiro de 2026 {#latest}

[!BADGE Produção]{type=Neutral tooltip="Os itens listados estão disponíveis atualmente em Ambientes de produção."}

Os itens a seguir foram lançados para os ambientes de Produção do [!DNL Adobe Commerce as a Cloud Service] em 20 de janeiro de 2026.

>[!BEGINSHADEBOX]

### Drop-ins B2B

As seguintes alterações foram feitas aos componentes de devolução direta B2B:

* [!DNL Commerce Storefront on Edge Delivery Services] agora inclui [componentes B2B](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). Os seguintes menus suspensos B2B agora estão disponíveis:

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

* Adicionados os pontos de extremidade `POST /V1/customers` e `PUT /V1/customers/{customerId}` à [API REST](https://developer.adobe.com/commerce/webapi/rest/reference/) para criar e atualizar clientes. Esses endpoints exigem autorização do administrador. <!-- CCSAAS-3112 -->

* Adicionada a [`exchangeOtpForCustomerToken` mutação](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), que requer um endereço de email do comprador e uma senha ocasional (OTP), e recebe um token de cliente em troca. Normalmente, essa mutação é usada em cenários em que um cliente precisa se autenticar usando um OTP enviado para seu email ou telefone.

* Se um endereço definido na tela de configuração [!UICONTROL **Armazenar Endereços de Email**] no Administrador contiver um valor que termina com `example.com`, a Commerce não enviará emails para esse endereço. Em vez disso, o sistema registra que o email não foi enviado.  <!-- CCSAAS-3533 -->

#### Atributos de ordem personalizados

* Os usuários administradores agora podem exibir e editar [atributos de pedido personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) diretamente nas telas Exibir, Editar e Criar Pedido no painel Administrador. Esse aprimoramento melhora o gerenciamento de dados de pedidos personalizados criados via GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
