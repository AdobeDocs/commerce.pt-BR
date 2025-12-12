---
title: Tutorial da extensão de classificações
description: Saiba como criar uma extensão de classificações de produto para o Adobe Commerce as a Cloud Service usando o App Builder e ferramentas de desenvolvimento assistido por IA.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: d0b9fd3ebbf0c88abbbf12821c5c4825ffcf10f0
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Tutorial da extensão de classificações (Beta)

>[!NOTE]
>
>A ferramenta de IA usada neste tutorial está atualmente no Beta e pode incluir bugs ou outros problemas.

Este tutorial o orienta por meio da criação de uma extensão de classificações de produto para o [!DNL Adobe Commerce as a Cloud Service] usando o [!DNL Adobe App Builder] e ferramentas de desenvolvimento assistido por IA.

Antes de começar, conclua os [pré-requisitos](./tutorial-prerequisites.md).

## Verificar pré-requisitos

Verifique se os seguintes pré-requisitos estão instalados:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

Se qualquer um dos comandos anteriores não retornar os resultados esperados, consulte os [pré-requisitos](tutorial-prerequisites.md) para obter orientação.

## Desenvolvimento de extensão

Esta seção orienta você pelo processo de desenvolvimento de uma extensão de classificações para o Adobe Commerce as a Cloud Service usando ferramentas de desenvolvimento assistido por IA.

1. Navegue até **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]** e verifique se o conjunto de ferramentas `commerce-extensibility` está habilitado sem erros. Se você vir erros, desligue e ligue o conjunto de ferramentas.

   ![Configurações do cursor](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Ao trabalhar com ferramentas de desenvolvimento assistido por IA, haverá variações naturais no código e nas respostas geradas pelo agente.
   >Se encontrar problemas com o código, você sempre poderá pedir ao agente para ajudá-lo a depurá-lo.

1. Se você tiver alguma documentação adicionada ao contexto do cursor, desative-a:

   - Navegue até [!UICONTROL **Cursor**] > [!UICONTROL **Configurações**] > [!UICONTROL **Configurações do cursor**] > [!UICONTROL **Indexação e documentos**] e exclua toda a documentação listada.

   ![Desabilitar documentação](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Gerar código para uma extensão de classificações de produto:
   - Em Cursor, na janela de bate-papo do cursor, selecione o modo **Agente**.
   - Digite o seguinte prompt:

   ```plain
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >Se o agente solicitar a pesquisa na documentação, permita.

1. Responda às perguntas do agente com precisão para ajudá-lo a gerar o melhor código.

   ![Inserir prompt no Cursor](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![O agente faz perguntas mais claras](../assets/agent-questions.png){width="600" zoomable="yes"}

1. Use o seguinte texto de exemplo para responder às perguntas do agente para configurar dados de classificações aleatórias:

   ```plain
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension will be called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   O agente cria um arquivo `requirements.md` que serve como a fonte da verdade para a implementação.

   ![Arquivo de requisitos criado](../assets/requirements-file.png){width="600" zoomable="yes"}

1. Revise o arquivo `requirements.md` e verifique o plano.

   Se tudo estiver correto, instrua o agente a migrar para a **Fase 2 - Planejamento de Arquitetura**.
1. Revise o plano de arquitetura.
1. Instrua o agente a prosseguir com a geração de código.

   O agente gera o código necessário e fornece um resumo detalhado com as próximas etapas.

   ![Planejamento de arquitetura](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![Resumo da geração de código](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![Próximas etapas](../assets/next-steps.png){width="600" zoomable="yes"}

### Teste local

1. Peça ao agente para ajudá-lo a testar o código localmente.

   ```plain
   Test the ratings API locally on a dev server using cURL.
   ```

1. Siga as instruções do agente e confirme se a API está funcionando localmente.

   ![Teste local](../assets/local-testing.png){width="600" zoomable="yes"}

   ![Resultados de testes locais](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Implantar a extensão

1. Depois de verificar o código gerado, implante a extensão usando o seguinte prompt:

   ```plain
   Deploy the ratings API.
   ```

   O agente realiza uma avaliação de prontidão antes da implantação.

   ![Avaliação pré-implantação](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. Quando estiver confiante nos resultados da avaliação, instrua o agente a prosseguir com a implantação.

   O agente usa o kit de ferramentas MCP para verificar, compilar e implantar automaticamente.

   ![Implantação](../assets/deployment-process.png){width="600" zoomable="yes"}

### Pós-implantação

Você pode testar a API antes de integrá-la à loja. O agente deve fornecer o local da nova ação e uma estratégia de teste.

![Estratégia de teste](../assets/testing-strategy.png){width="600" zoomable="yes"}

Também é possível testar a API manualmente usando o cURL em um terminal:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cTeste de URL](../assets/curl-test.png){width="600" zoomable="yes"}

### Integrar ao Edge Delivery Services

Para integrar a API de classificações a uma loja [!DNL Adobe Commerce] da plataforma [!DNL Edge Delivery Services], peça ao agente que crie um contrato de serviço com requisitos para a API de classificação:

```plain
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Contrato de serviço](../assets/create-contract.png){width="600" zoomable="yes"}

![Detalhes do contrato de serviço](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### Próximas etapas

Agora que você tem o contrato de API de classificação, pode começar a criar a parte da loja (front-end) da extensão de classificação.

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```plain
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```plain
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots?lang=pt-BR).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```plain
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```plain
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
