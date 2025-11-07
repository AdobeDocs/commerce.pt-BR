---
title: Tutorial da extensão de classificações
description: Saiba como criar uma extensão de classificações de produto para o Adobe Commerce as a Cloud Service usando o App Builder e ferramentas de desenvolvimento assistido por IA.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - Pasta de trabalho do Adobe Commerce lab

Este laboratório orienta você na criação de uma extensão de classificações de produtos para o [!DNL Adobe Commerce as a Cloud Service] usando o [!DNL Adobe App Builder] e ferramentas de desenvolvimento assistido por IA.

## Verificar pré-requisitos

Verifique se os seguintes pré-requisitos estão instalados:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Faça logon na Adobe Developer Console

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Se você já estiver conectado, clique no ícone do seu perfil no canto superior direito e clique no botão **Sair**.
1. Faça logon usando a ID de e-mail do laboratório e a senha fornecida para a sua vaga.
1. Se for solicitado que você adicione um endereço de email ou número de telefone secundário, clique em **Não agora**.
1. Quando for solicitado que você selecione um perfil de organização, selecione **Adobe Commerce Labs**.

   ![selecionar-organização](./assets/select-org.png){width="600" zoomable="yes"}

1. Se você for solicitado a aceitar os termos e condições, clique no link para ler os termos e, em seguida, clique em **Aceitar e continuar**.

   ![aceitar-termos](./assets/accept-terms.png){width="600" zoomable="yes"}

## Executar o script de configuração

Se os [pré-requisitos](#verify-prerequisites) estiverem instalados e você tiver entrado no Adobe Developer Console, baixe e execute o script de instalação. Como alternativa, você pode configurar manualmente o script seguindo os [pré-requisitos do laboratório](workbook-prerequisites.md) etapas.

1. Clonar o repositório que contém o script de configuração:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >Se o script falhar, consulte os [pré-requisitos](workbook-prerequisites.md) e continue onde o script encontrou um erro.

1. Navegue até o repositório:

   ```bash
   cd commerce-adl-2025
   ```

1. Execute o script de configuração:

   ```bash
   bash adl-setup.sh
   ```

   Durante a execução do script, você será solicitado a digitar seu nome de usuário e senha, que serão fornecidos durante o laboratório. Seu nome de usuário refletirá sua localização e o número da vaga. Por exemplo, se você estiver em San Jose, CA, 123 lugares, seu nome de usuário será `sjc-adl-123@adobeeventlab.com`.

   Além disso, você deve selecionar o projeto que corresponde ao seu número de vagas e ao espaço de trabalho **estágio**. O nome do projeto refletirá a localização e o número da vaga. Por exemplo, se você estiver em San Jose, CA, 123 lugares, o nome do seu projeto será `SJC ADL 123`.

## Desenvolvimento de extensão

Esta seção orienta você pelo processo de desenvolvimento de uma extensão de classificações para o Adobe Commerce as a Cloud Service usando ferramentas de desenvolvimento assistido por IA.

### Instalar ferramentas de IA de extensibilidade

Configurar as ferramentas de desenvolvimento assistido por IA na pasta `extension`:

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![Instalar ferramentas de IA](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### Abrir Cursor

>[!NOTE]
>
>Ao trabalhar com ferramentas de desenvolvimento assistido por IA, haverá variações naturais no código e nas respostas geradas pelo agente.
>Se encontrar problemas com o código, você sempre poderá pedir ao agente para ajudá-lo a depurá-lo.

Abra o aplicativo [!DNL Cursor] e navegue até a pasta `extension` ou, se você tiver a [CLI do Cursor](https://cursor.com/docs/configuration/shell#installing-cli-commands) instalada, digite o seguinte comando no terminal:

```bash
cursor .
```

![Abrir Cursor](./assets/open-cursor.png){width="600" zoomable="yes"}

Neste ponto, todas as [!DNL Cursor] regras estão instaladas na pasta `.cursor/rules`. Você pode encontrar ferramentas MCP nas **Configurações de MCP** em [!DNL Cursor]. Verifique se o conjunto de ferramentas `commerce-extensibility` está habilitado sem erros. Se você vir erros, desligue e ligue o conjunto de ferramentas.

![Configurações do cursor](./assets/cursor-settings.png){width="600" zoomable="yes"}

Se você tiver alguma documentação adicionada ao contexto do cursor, precisará desabilitá-la. Navegue até [!UICONTROL **Cursor**] > [!UICONTROL **Configurações**] > [!UICONTROL **Configurações do cursor**] > [!UICONTROL **Indexação e documentos**] e exclua toda a documentação listada.

![Desabilitar documentação](./assets/disable-documentation.png){width="600" zoomable="yes"}

### Geração de código

Esta seção demonstra como usar as ferramentas assistidas por IA para gerar código para uma extensão de classificações do produto.

#### Definir requisitos

Você implementará uma extensão que serve classificações de produto como uma API. A extensão [!DNL App Builder] responde com detalhes de classificação para uma determinada SKU.

**Prompt inicial:**

Usar o seguinte prompt em [!DNL Cursor]:

1. Abra a janela de bate- papo no Cursor.
1. Selecione o modo **Agente**.
1. Digite o seguinte prompt:

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. Se o agente solicitar a pesquisa na documentação, permita.

![Inserir prompt no Cursor](./assets/enter-prompt.png){width="600" zoomable="yes"}

O agente pesquisa os requisitos e faz perguntas esclarecidas. Responda às perguntas do agente com precisão para ajudá-lo a gerar o melhor código.

![O agente faz perguntas mais claras](./assets/agent-questions.png){width="600" zoomable="yes"}

**Prompt de resposta:**

Use a seguinte resposta para responder às perguntas do agente:

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

O agente cria um arquivo `requirements.md` que serve como a fonte da verdade para a implementação.

![Arquivo de requisitos criado](./assets/requirements-file.png){width="600" zoomable="yes"}

#### Verificar os requisitos e planejar a arquitetura

1. Revise o arquivo `requirements.md`.
1. Se tudo estiver correto, instrua o agente a migrar para a **Fase 2 - Planejamento de Arquitetura**.
1. Revise o plano de arquitetura.
1. Instrua o agente a prosseguir com a geração de código.

![Planejamento de arquitetura](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### Gerar código

O agente gera o código necessário e fornece um resumo detalhado com as próximas etapas.

![Resumo da geração de código](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![Próximas etapas](./assets/next-steps.png){width="600" zoomable="yes"}

### Teste local

Peça ao agente para ajudá-lo a testar o código localmente.

```text
Test the ratings API locally on a dev server using cURL.
```

Siga as instruções do agente e confirme se a API está funcionando localmente.

![Teste local](./assets/local-testing.png){width="600" zoomable="yes"}

![Resultados de testes locais](./assets/local-testing-1.png){width="600" zoomable="yes"}

### Implantar a extensão

Depois de verificar o código gerado, você está pronto para implantar a extensão usando o seguinte prompt:

```text
Deploy the ratings API.
```

#### Avaliação pré-implantação

O agente realiza uma avaliação de prontidão antes da implantação.

![Avaliação pré-implantação](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### Implantar

Quando estiver confiante nos resultados da avaliação, instrua o agente a prosseguir com a implantação. O agente usa o kit de ferramentas MCP para verificar, compilar e implantar automaticamente.

![Implantação](./assets/deployment-process.png){width="600" zoomable="yes"}

### Testar a API

Você pode testar a API antes de integrá-la à loja.

O agente fornece o local da nova ação e uma estratégia de teste.

![Estratégia de teste](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### Testar manualmente com cURL

Testar a API manualmente usando cURL em um terminal:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![cTeste de URL](./assets/curl-test.png){width="600" zoomable="yes"}

### Integrar ao Edge Delivery Services

Para integrar a API de classificações a uma loja [!DNL Adobe Commerce] da plataforma [!DNL Edge Delivery Services], peça ao agente que crie um contrato de serviço com requisitos para a API de classificação:

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Contrato de serviço](./assets/create-contract.png){width="600" zoomable="yes"}

![Detalhes do contrato de serviço](./assets/contract.png){width="600" zoomable="yes"}

Retorne ao terminal e execute o seguinte comando na pasta `extension` para copiar o arquivo para a pasta `storefront`:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Conectar à loja

Esta seção ajudará você a implementar recursos da loja real, mostrando como se comunicar de forma eficaz com agentes de IA ao trabalhar com [!DNL Adobe Commerce] descartes e [!DNL Edge Delivery Services].

>[!NOTE]
>
>Os prompts fornecidos são pontos de partida, você deve se sentir livre para ter uma conversa natural com o agente. Ao trabalhar com ferramentas de desenvolvimento assistido por IA, haverá variações naturais no código e nas respostas geradas pelo agente.
>
>Se você encontrar algum problema com seu código, sempre poderá pedir ao agente para ajudá-lo a depurá-lo.

### Implementar estrelas de classificação e contagem de revisão

1. Navegue até a pasta `storefront`:

   ```bash
   cd storefront
   ```

1. Abra a pasta de vitrine em uma nova janela Cursor. Se você tiver a [CLI do Cursor](https://cursor.com/docs/configuration/shell#installing-cli-commands) instalada, digite o seguinte comando no terminal:

   ```bash
   cursor .
   ```

1. Iniciar o servidor de desenvolvimento local:

   ```bash
   npm run start
   ```

1. Em um navegador, navegue até a página Vestuário:

   ```text
   http://localhost:3000/apparel
   ```

1. Observe o layout da interface do usuário da vitrine eletrônica.

1. Use o seguinte prompt com seu agente:

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >Se for solicitado que você inicie o servidor de desenvolvimento local, informe ao agente que ele já está em execução.

1. Observe as alterações na base de código e observe as atualizações na página Vestuário.

**Resultado esperado:**

* Um &quot;componente&quot; de classificação de produto é criado automaticamente.
* O componente é integrado aos blocos de detalhes do produto, lista de páginas e recomendações de produtos usando Slots.
* As estrelas são exibidas com proporções de preenchimento apropriadas com base nos valores de classificação de simulações.

![Implementação de classificações do produto](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### Alterar as cores das estrelas

Use o seguinte aviso para seu agente:

```text
Change the star fill color to red.
```

**Resultado esperado:**

As estrelas são mudadas para vermelho.

![Cores de Estrela Vermelha](./assets/red-star-colors.png){width="600" zoomable="yes"}

## Recapitulação da loja

Neste tutorial, abordamos os seguintes tópicos:

* **Implementação de recursos**: como descrever a nova funcionalidade para um agente de IA.
* **Alterações iterativas**: fazer modificações rápidas no código existente.
* **Componentes complexos da interface do usuário**: criando recursos interativos com referências visuais.
* **Integração de descarte**: trabalhando com [!DNL Adobe Commerce] contêineres e slots de descarte.
* **Reutilização de componente**: criação de componentes compartilhados usados em vários blocos.

## Próximas etapas

Se o tempo permitir, você poderá personalizar ainda mais sua extensão de classificações adicionando os seguintes recursos:

### Adicionar modal de distribuição de classificação (opcional)

As etapas a seguir mostram como o agente lida com recursos complexos da interface do usuário com referências visuais.

1. **Antes de iniciar:** Salve a imagem de modelo a seguir e cole-a no chat com o agente da loja.

   ![Mockup de Distribuição de Classificação](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Siga as etapas abaixo para orientá-lo na criação do modal de distribuição de classificações com base na imagem de referência:

   * Atualize a API para retornar dados adicionais que representem a distribuição de classificações.
   * Atualize o Contrato de API.
   * Atualize o contato na base de código de vitrine.
   * Peça ao agente da loja que use a imagem de referência e o Contrato de API atualizado para adicionar a distribuição de classificações à página PDP.

1. Observe as seguintes alterações na base de código e observe as atualizações na página Vestuário:

   * Como o agente interpreta o modelo visual
   * Se ela usa a estrutura apropriada do HTML para acessibilidade
   * Como ele lida com os estados de posicionamento e interação

**Solução de problemas:**

* Se o modal não for exibido, verifique se há erros no console do navegador.
* Se o posicionamento estiver desativado, você poderá solicitar que o agente:

  ```text
  adjust the modal position to be...
  ```

![Modal de Distribuição de Classificação](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
