---
title: Configurar a loja
description: Saiba como executar a ferramenta de andaime para configurar sua vitrine  [!DNL Adobe Commerce as a Cloud Service] .
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 408f28bdc20708022c8eca0fbfea4adb17014bf7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Configurar a loja

Para configurar sua Adobe Commerce Storefront com a tecnologia do Edge Delivery Services para Adobe Commerce as a Cloud Service (SaaS), siga as etapas abaixo.

Para obter uma apresentação mais personalizável e detalhada, consulte a [documentação sobre vitrines](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=pt-BR).

1. Abra a [ferramenta do criador do site](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Selecione **Criar Novo Site (Código e Conteúdo)**.

1. Insira a **Organização/Nome de usuário do Github** onde deseja criar o repositório de código de vitrine.

1. Insira um **Nome do Site**.

1. No campo **Ponto de Extremidade do Commerce GraphQL (opcional)**, digite seu ponto de extremidade do Adobe Commerce as a Cloud Service (SaaS) GraphQL, que você pode acessar no Commerce Cloud Manager após [criar sua instância](./getting-started.md#create-an-instance).

   Como alternativa, se você estiver usando a [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), insira o ponto de extremidade da API Mesh GraphQL no campo **Commerce GraphQL Endpoint (opcional)**. Consulte [criar uma malha](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) para obter mais informações.

1. Clique em **Criar Site**. Siga as instruções na tela para autorizar o acesso ao repositório do Github.

Quando o processo for concluído, você poderá personalizar a vitrine eletrônica usando os seguintes métodos:

* Personalize seu código: `https://github.com/<username or org>/<repo name>`
* Editar seu conteúdo: `https://da.live/#/<username or org>/<repo name>`
* Gerenciar sua configuração: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Visualizar sua loja: `https://main--<repo name>--<username or org>.aem.page/`

## Próximas etapas

Consulte os seguintes artigos para obter mais informações:

* Para saber mais sobre como gerenciar e exibir conteúdo e dados na loja, consulte [atualização de conteúdo da loja](./use-cases.md#update-storefront-content).
* Para obter mais informações sobre recursos de experimentação contextual, consulte [experimentação contextual](./use-cases.md#contextual-experimentation).
* Para obter mais informações sobre como usar a IA de geração para automatizar a geração de conteúdo de alta qualidade, consulte [Gerar variações](./use-cases.md#generate-variations).
* Para saber mais sobre como atualizar o conteúdo do site e integrar com componentes de front-end e dados de back-end do Commerce, consulte a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR).
