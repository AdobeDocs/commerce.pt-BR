---
title: Tutorial da extensão de análises do produto
description: Saiba como criar análises de produto e extensões de perguntas e respostas para o Adobe Commerce as a Cloud Service usando o App Builder, o Edge Delivery Services e ferramentas de desenvolvimento assistido por IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '2533'
ht-degree: 0%

---

# Tutorial de extensão de análises do produto

Este tutorial o orienta por meio da criação de uma extensão que permite aos clientes enviar revisões de produtos e conteúdo de perguntas e respostas (P&amp;R) para vitrines com um back-end do [!DNL Adobe Commerce as a Cloud Service] usando o [!DNL Adobe App Builder] e ferramentas de desenvolvimento assistidas por IA. A extensão fornece endpoints da API REST para que os compradores visualizem e enviem conteúdo de revisão e pergunta e resposta (P&amp;R) do produto e o exibam na página de detalhes do produto (PDP).

Você constrói duas partes:

- **Extensão do App Builder** — uma API REST com operações GET e POST para criar e exibir análises de produtos e conteúdo de perguntas e respostas com validação, paginação e persistência em `aio-lib-state`.
- **Integração com a Loja** — Um bloco de revisão de produto no PDP que exibe revisões e perguntas e respostas, com formulários para os compradores enviarem revisões, perguntas e respostas.

>[!NOTE]
>
>Os agentes de IA são não determinísticos. Os prompts, as perguntas e as saídas deste tutorial são exemplos. Seu agente pode produzir diferentes perguntas, requisitos ou propostas de arquitetura. Use os exemplos deste tutorial para orientar o agente em direção a um resultado semelhante.

Antes de começar, conclua os [pré-requisitos](./tutorial-prerequisites.md). Este tutorial usa o **kit inicial de integração**. Verifique se você já a clonou e concluiu as etapas de configuração descritas na página de pré-requisitos.

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

Se qualquer um dos comandos anteriores não retornar os resultados esperados, consulte os [pré-requisitos](./tutorial-prerequisites.md) para obter orientação.

Além disso, verifique o seguinte:

- Você tem uma instância [!DNL Adobe Commerce as a Cloud Service] com dados de produto. Consulte [Instâncias do Commerce Cloud Service](https://experienceleague.adobe.com/pt-br/docs/commerce/cloud-service/overview){target="_blank"}.
- Você tem um projeto de vitrine conectado à sua instância [!DNL Commerce]. Se você não tiver uma, siga as etapas em [Criar uma vitrine](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=pt-BR){target="_blank"}.
- A CLI do `aem` está instalada:

  ```bash
  npm install -g @adobe/aem-cli
  ```

## Desenvolvimento de extensão

Esta seção orienta você no desenvolvimento de uma extensão para enviar e exibir a revisão do produto e o conteúdo de perguntas e respostas da extensão para as lojas com um back-end do [!DNL Adobe Commerce as a Cloud Service] usando ferramentas de desenvolvimento assistido por IA. A extensão fornece uma API REST para enviar e exibir a revisão do produto e o conteúdo de perguntas e respostas e para exibi-lo no PDP.

1. Navegue até as configurações de MCP no seu agente de codificação. Por exemplo, no Cursor, vá para **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Verifique se o conjunto de ferramentas `commerce-extensibility` está habilitado sem erros. Se você vir erros, desligue e ligue o conjunto de ferramentas.

   >[!NOTE]
   >
   >Ao trabalhar com ferramentas de desenvolvimento assistidas por IA, espere variações naturais no código e nas respostas geradas pelo agente.
   >Se encontrar algum problema com seu código, peça ao agente para ajudá-lo a depurá-lo.

1. Se você tiver alguma documentação adicionada ao contexto do cursor, desative-a.

   Navegue até **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** e exclua qualquer documentação listada.

### Etapa 1: fornecer o prompt inicial

Solicitar que o agente de IA inicie a implementação. Dizer ao agente para parar e fazer perguntas ajuda a orientar a implementação antecipadamente.

Digite o seguinte prompt na janela de bate-papo do agente:

```shell-session
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Dizer ao agente para PARAR e fazer perguntas antes de continuar ajuda a orientar a implementação no início do processo. Isso garante que as principais suposições e os requisitos ausentes sejam identificados antecipadamente e seja necessário para iniciar o fluxo de trabalho guiado neste tutorial.

### Etapa 2: Responda às perguntas do agente

O agente retorna com uma série de perguntas que precisa responder antes de começar a formar uma solução. O exemplo a seguir mostra perguntas e respostas típicas. Seu agente pode fazer perguntas diferentes, mas os tópicos geralmente são os mesmos.

**Exemplo de perguntas sobre o agente:**

1. **API REST — host e consumidores** — a API REST CRUD deve fazer parte deste aplicativo App Builder (ações da Web no Adobe I/O Runtime) para o qual as chamadas de vitrine? Quem o chamará (loja EDS, loja personalizada/headless ou ambas)? Você precisa do CORS, acesso público (não autenticado) ou os chamadores usarão chaves de API ou OAuth?
1. **Modelo de dados** — O que uma &quot;revisão&quot; ou &quot;pergunta&quot; representa? Identificador do cliente (somente email ou também ID do cliente)? Identificador de produto (somente SKU ou SKU + exibição de loja)? O mesmo cliente pode enviar várias revisões para o mesmo SKU?
1. **Persistência** — `aio-lib-state` é o local certo para persistir revisões e perguntas e respostas ou você tem um armazenamento externo? O design deve assumir vários locatários ou um único locatário?
1. **Semântica de paginação** — Para o Q&amp;A GET, o `limit` se aplica somente a perguntas (com respostas aninhadas) ou à contagem total de perguntas mais respostas?

**Exemplo de respostas:**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>Seu agente pode fazer perguntas diferentes. Use essas respostas como orientação para direcionar o agente para o mesmo resultado funcional: uma API REST pública com revisões e perguntas e respostas, persistência de `aio-lib-state` e nenhuma autenticação.

### Etapa 3: analisar requisitos e arquitetura

O agente gera requisitos e documentos de arquitetura para que você os revise. Verifique se os requisitos correspondem às respostas fornecidas e se a arquitetura abrange:

- Quatro ações da Web: `reviews-get`, `reviews-post`, `qa-get`, `qa-post`
- Persistência usando `aio-lib-state` com chaves que estão em conformidade com o padrão permitido (`[a-zA-Z0-9-_.]` — sem dois-pontos)
- Valores de estado armazenados como strings JSON (não objetos brutos ou matrizes)
- Pacote independente — código compartilhado (utils, constantes) dentro do pacote `product-reviews`, não através de caminhos `../../` que escapam do pacote

>[!NOTE]
>
>Os agentes de IA são não determinísticos e seus comportamentos diferem dependendo do modelo e do IDE. Você pode obter um conjunto diferente de perguntas que produzem um conjunto diferente de requisitos e arquitetura. Em caso positivo, tente orientar o agente na direção de forma que a implementação corresponda ao que é apresentado neste tutorial antes de continuar.

### Etapa 4: Selecionar um plano de implementação

O agente oferece a opção de criar um plano de implementação detalhado ou de concluir uma implementação direta.

- Se quiser um plano revisável que possa ser executado em fases com mais controle, selecione a primeira opção.
- Se desejar que o agente faça a implementação completa com intervenção mínima, selecione a segunda opção.

### Etapa 5: implantar a extensão

Depois que o agente concluir a implementação, implante a extensão:

```bash
aio app deploy
```

Se o agente adicionou `require-adobe-auth: true` às ações, peça a ele para remover a autenticação para que os pontos de extremidade possam ser chamados diretamente da loja:

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

Em seguida, reimplante:

```bash
aio app deploy
```

### Etapa 6: criar dados de modelo e pré-preencher para teste

Crie um arquivo de dados fictício e use o curl para preencher previamente a API, de modo que você tenha amostra de revisão e conteúdo de perguntas e respostas para testes na CLI e na loja.

1. Crie um arquivo `docs/mock-product-reviews-data.json` (ou similar) com dados de exemplo. Por exemplo:

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. Use curl para POSTAR os dados na API implantada.

   Substitua `<your-runtime-url>` pela URL de tempo de execução real do App Builder (por exemplo, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`):

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. Verifique os dados com solicitações do GET:

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>Use o SKU `ADB153` para um produto que tenha conteúdo de revisão e de perguntas e respostas, e `ADB152` para um produto sem análises. Essa configuração de dados permite testar os estados preenchido e vazio na loja.

### Etapa 7: testar a extensão

Peça ao agente para fornecer etapas de teste ou use os exemplos de curl da etapa anterior. Os exemplos a seguir mostram comandos de teste típicos.

**Enviar uma revisão:**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**Listar análises:**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**Enviar uma pergunta:**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**Enviar uma resposta** (use `id` da resposta de pergunta como `questionId`):

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### Criar o contrato de serviço

Agora que a implementação do serviço foi concluída, peça ao agente para criar um contrato de serviço para o trabalho da loja:

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

Copie esse arquivo no projeto da loja para que o agente da loja possa referenciá-lo.

## Conectar à loja

Esta seção orienta você na implementação da parte da loja das análises de produtos e da extensão de Perguntas e Respostas usando o [!DNL Edge Delivery Services] e as ferramentas de desenvolvimento assistido por IA. Você adiciona um bloco de análise do produto ao PDP que exibe o conteúdo de análise e de perguntas e respostas e permite que os compradores enviem novo conteúdo.

>[!NOTE]
>
>Os prompts fornecidos são pontos de partida. Embora você possa usá-los sem modificação, considere ter uma conversa natural com o agente.
>
>Ao trabalhar com ferramentas de desenvolvimento assistido por IA, há sempre variações naturais no código e nas respostas geradas pelo agente.
>
>Se encontrar algum problema com seu código, peça ao agente para ajudá-lo a depurá-lo.

### Pré-requisitos da loja

Antes de iniciar a integração da loja, verifique se você tem o seguinte:

- Um projeto de vitrine conectado à sua instância [!DNL Commerce]
- Ferramentas de IA da vitrine do Commerce [instaladas usando a CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- O arquivo `PRODUCT_REVIEW_QA_CONTRACT.md` copiado para o projeto da loja

### Etapa 1: Validar o ambiente

Abra o arquivo `config.json` e verifique se os valores de `commerce-core-endpoint` e `commerce-endpoint` apontam para o ponto de extremidade do GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Etapa 2: fornecer o prompt inicial

Com o contrato de serviço já em seu projeto, solicite que o agente implemente o bloco de análise do produto. Use o modo **Plano**, se disponível em seu agente, para impedir que o agente continue sem um plano.

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>Especificamente, solicitar o uso da habilidade do gerente de projeto aciona o fluxo de trabalho em fases que ajuda a orientar a implementação. Isso garante que as principais suposições e os requisitos ausentes sejam identificados no início do processo.

### Etapa 3: Responda a perguntas de esclarecimento

O agente retorna com uma série de perguntas que precisa responder antes de começar a formar uma solução. O exemplo a seguir mostra perguntas e respostas típicas. Seu agente pode fazer perguntas diferentes, mas os tópicos geralmente são os mesmos.

**Exemplo de perguntas sobre o agente:**

1. **URL base da API** — Como a loja deve obter o URL base da API de revisões de produtos? As opções podem incluir um bloco de configuração (por exemplo, uma tabela com `apiBaseUrl`), espaços reservados globais ou outra abordagem.
1. **Origem da SKU** — O bloco deve ler a SKU do contexto de PDP (produto atual) ou da configuração de bloco?
1. **Comportamento do formulário** — Após um envio bem-sucedido, o formulário deve ser ocultado, mostrar uma mensagem de êxito ou permanecer visível, mas desabilitado?

**Exemplo de respostas:**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>Substitua o espaço reservado na configuração de bloco pela URL de tempo de execução real do App Builder (por exemplo, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`).
>
>Seu agente pode fazer perguntas diferentes. Use essas respostas como orientação:
>
>- O URL de base da API deve vir da tabela de bloqueios para que possa ser alterado sem modificações de código.
>- SKU da tabela de blocos, se definida; caso contrário, do produto atual no PDP.
>- Após um envio bem-sucedido, mostre uma mensagem de sucesso e desative o formulário.

### Etapa 4: analisar requisitos e arquitetura

O agente atualiza o documento de requisitos para que você o revise. Verifique se:

- O bloco renderiza revisões (com classificação, usuário, data, texto) e perguntas e respostas (perguntas com respostas aninhadas).
- O Forms existe para enviar revisões, perguntas e respostas.
- A paginação é compatível com revisão e conteúdo de perguntas e respostas.
- A integração da API usa o URL de base da tabela de bloqueios.
- Os estados de sucesso e erro são tratados de acordo com o contrato.

>[!NOTE]
>
>Os agentes de IA são não determinísticos e seus comportamentos diferem dependendo do modelo e do IDE. Você pode obter um conjunto diferente de perguntas que produzem um conjunto diferente de requisitos e arquitetura. Em caso positivo, tente orientar o agente na direção de forma que a implementação corresponda ao que é apresentado neste tutorial antes de continuar.

### Etapa 5: Selecionar um plano de implementação

O agente oferece a opção de criar um plano de implementação detalhado ou de concluir uma implementação direta.

- Se quiser um plano revisável que possa ser executado em fases com mais controle, selecione a primeira opção.
- Se desejar que o agente faça a implementação completa com intervenção mínima, selecione a segunda opção.

Durante a implementação, o agente cria e modifica arquivos de bloqueio. Observe o código que está sendo gerado e faça perguntas ou redirecione o agente, conforme necessário. Se o bloco não for renderizado, peça ao agente para analisar a decoração da seção e o padrão de descoberta de blocos — o elemento de bloco deve ser um filho direto da seção para que a estrutura possa encontrá-lo.

### Etapa 6: adicionar o bloco à página do produto na Criação de documentos

Adicione o bloco de revisão do produto ao modelo da página do produto para que ele seja exibido em todos os PDPs. Use o serviço de Criação de documentos (da.live) para adicionar e configurar o bloco.

1. Abra o serviço de autoria de documentos, por exemplo [da.live](https://da.live/)

1. Clique no espaço do projeto, abra a pasta **produtos** e selecione **padrão** (`products/default`).

1. Adicione uma nova seção de bloco.

   Na tabela de bloqueios, adicione uma linha com o nome de bloco **product-review** (ou o nome de bloco que seu agente criou).

1. Configure o bloco com as configurações necessárias:
   - **apiBaseUrl** — Sua URL de tempo de execução do App Builder (por exemplo, `https://<namespace>-<app-name>-stage.adobeioruntime.net`).
   - **sku** — Deixe em branco para usar o SKU do produto atual no PDP ou insira um SKU específico para exibir comentários somente para esse produto.

1. Clique em **[!UICONTROL Publish]** para publicar suas alterações.

### Etapa 7: iniciar o servidor e testar

Depois de adicionar o bloco à página do produto na Criação de documentos, inicie o servidor de desenvolvimento e teste o bloco.

1. Iniciar o servidor de desenvolvimento local:

   ```bash
   npm run start
   ```

1. Em um navegador, navegue até uma página de produto que tenha revisões e conteúdo de perguntas e respostas pré-preenchidos. Por exemplo:

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. Verifique se o bloco de revisão do produto exibe revisões e conteúdo de Perguntas e Respostas e se os formulários de envio funcionam.

Você pode fazer testes manuais ou solicitar que o agente use os recursos do navegador para testar:

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### Etapa 8: limpar

Após ignorar ou concluir o teste, o agente solicitará que você prossiga para a fase final de **Limpeza**. Após a confirmação, o agente arquiva todos os artefatos de documentação criados durante a implementação.

## Solução de problemas

Use as seguintes dicas se encontrar problemas durante o tutorial.

### Infraestrutura (App Builder)

| Sintoma | Causa | Correção |
|---------|-------|-----|
| GET ou POST retorna 500 &quot;Não é possível encontrar o módulo&quot; | As ações de análise de produtos usam `require("../../utils")` ou `require("../../constants")`, que escapam ao pacote. Esses arquivos não são incluídos quando o pacote é implantado. | Tornar o pacote de análises do produto independente. Adicione `actions/product-reviews/lib/constants.js` e `actions/product-reviews/lib/utils.js`, e atualize todas as quatro ações para exigir de `../lib/...` em vez de `../../`. |
| O GET retorna 500 com &quot;a chave deve corresponder ao padrão&quot; | As chaves de estado usam dois pontos (por exemplo, `reviews:ADB153`). `aio-lib-state` permite somente `[a-zA-Z0-9-_.]`. | Alterar prefixos de `reviews:` e `qa:` para `reviews.` e `qa.`. Adicione um auxiliar `stateKey(prefix, sku)` que limpa o SKU (substitua caracteres inválidos por `_`). |
| POST retorna 500 com &quot;o valor deve ser string&quot; | `aio-lib-state` aceita somente valores de sequência de caracteres. O código passa matrizes ou objetos para `state.put()`. | Serializar com `JSON.stringify()` ao gravar e `JSON.parse()` ao ler. Atualize todas as quatro ações. |

{style="table-layout:auto"}

### Loja (Edge Delivery Services)

| Sintoma | Causa | Correção |
|---------|-------|-----|
| O bloco não é renderizado na página de teste | O elemento de bloco está aninhado dentro de um `div` extra, portanto, após `decorateSections` o seletor de bloco (`div.section > div > div`) não corresponde. | Torne o bloco um filho direto da seção. Estrutura: `section > div.product-review` (ou classe de bloco equivalente). Evite `section > div > div.product-review`. |
| Tokens CSS inválidos | O bloco usa tokens de design que não existem em `styles/styles.css` (por exemplo, `--color-error-100`, `--type-detail-font-size`). | Peça ao agente para validar tokens em relação a `styles/styles.css` do projeto e substituir tokens inválidos por outros existentes (por exemplo, `--color-alert-*`, `--type-details-caption-*`). |

{style="table-layout:auto"}

## Resumo do tutorial

Este é um resumo dos tópicos abordados neste tutorial:

- **Desenvolvimento de extensão:** descrevendo a funcionalidade para criar e exibir revisão do produto e conteúdo de perguntas e respostas em uma loja com um back-end do Adobe Commerce as a Cloud Service para um agente de IA e como implementar essa funcionalidade gerando uma API REST funcional com quatro pontos de extremidade usando [!DNL App Builder].
- **Persistência:** usando `aio-lib-state` com o formato de chave correto e valores serializados JSON.
- **Dados simulados e pré-preenchimento:** Criação de um arquivo de dados simulados e uso de curl para pré-popular a API para teste de CLI e vitrine.
- **Contratos de serviço:** criando contratos de API que conectam extensões de back-end e implementações de vitrine.
- **Integração de vitrine em fases:** Trabalhando com requisitos, arquitetura e implementação usando habilidades assistidas por IA.
- **Bloco PDP:** adicionar um bloco de revisão de produto ao PDP que exibe revisões e perguntas e respostas com formulários de envio e paginação.

## Próximas etapas

Use as seguintes sugestões para estender o serviço de análises de produtos:

- **Adicionar moderação:** implemente um fluxo de trabalho de moderação para revisar e fazer perguntas e respostas antes de publicá-lo.
- **Adicionar autenticação:** Exigir que os compradores estejam conectados para enviar revisões ou conteúdo de perguntas e respostas e associar envios a contas de clientes.
- **Adicione uma página de gerenciamento de assinatura:** Crie uma página de vitrine onde os compradores possam exibir e editar suas análises.
- **Suporte a implantações com vários locatários:** estenda o gerenciamento de estado para oferecer suporte a vários locatários do Commerce em um único aplicativo App Builder.
- **Adicionar limitação de taxa:** Implemente limites de taxa na API para evitar abuso.
