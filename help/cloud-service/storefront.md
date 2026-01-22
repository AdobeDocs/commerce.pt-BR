---
title: Configurar a loja
description: Saiba como executar a ferramenta de andaime para configurar sua  [!DNL Adobe Commerce as a Cloud Service] vitrine.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Configurar a loja

Para configurar seu [!DNL Adobe Commerce Storefront] com a tecnologia [!DNL Edge Delivery Services] para [!DNL Adobe Commerce as a Cloud Service] (SaaS), conclua as etapas a seguir.

Para obter uma apresentação mais personalizável e detalhada, consulte a [documentação sobre vitrines](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

1. Abra a [ferramenta do criador do site](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Selecione **[!UICONTROL Create New Site (Code & Content)]**.

1. Insira o **[!UICONTROL Github Organization/Username]** onde deseja criar o repositório de código de vitrine.

1. Insira um **[!UICONTROL Site Name]**.

1. No campo **[!UICONTROL Commerce GraphQL Endpoint (optional)]**, digite seu ponto de extremidade do GraphQL [!DNL Adobe Commerce as a Cloud Service] (SaaS), que você pode acessar no Commerce Cloud Manager após [criar sua instância](./getting-started.md#create-an-instance).

   Como alternativa, se você estiver usando o [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), insira o ponto de extremidade do GraphQL [!DNL API Mesh] no campo **[!UICONTROL Commerce GraphQL Endpoint (optional)]**. Consulte [criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) para obter mais informações.

1. Clique em **[!UICONTROL Create Site]**. Siga as instruções na tela para autorizar o acesso ao seu repositório GitHub.

Quando o processo for concluído, você poderá personalizar a vitrine eletrônica usando os seguintes métodos:

* Personalize seu código: `https://github.com/<username or org>/<repo name>`
* Editar seu conteúdo: `https://da.live/#/<username or org>/<repo name>`
* Gerenciar sua configuração: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Visualizar sua loja: `https://main--<repo name>--<username or org>.aem.page/`

## Próximas etapas

Consulte os seguintes artigos para obter mais informações:

* [Atualizando conteúdo da loja](./use-cases.md#update-storefront-content)—Gerencie e exiba conteúdo e dados na loja.
* [Experimentação contextual](./use-cases.md#contextual-experimentation) — crie e gerencie experimentos em sua loja.
* [Gerar variações](./use-cases.md#generate-variations) — Use a IA de geração para automatizar a geração de conteúdo de alta qualidade.
* [Documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) — obtenha informações detalhadas sobre a atualização do conteúdo do site e a integração com componentes de front-end e dados de back-end do Commerce.
* [Serviço de Configuração](https://www.aem.live/docs/config-service-setup)—Saiba mais sobre como migrar a configuração da loja do `config.json` para usar o Serviço de Configuração, que oferece suporte a casos de uso avançados, como configuração de resposta e sobreposições.
