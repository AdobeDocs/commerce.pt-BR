---
title: Tutorial da extensão de estimativas de entrega
description: Saiba como criar uma extensão de estimativa de data de entrega para o Adobe Commerce as a Cloud Service usando o App Builder, o Edge Delivery Services e ferramentas de desenvolvimento assistido por IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# Tutorial de extensão de estimativas de entrega

Este tutorial o orienta por meio da criação de uma extensão de estimativa de data de entrega para [!DNL Adobe Commerce as a Cloud Service] usando [!DNL Adobe App Builder], [!DNL Edge Delivery Services] e ferramentas de desenvolvimento assistido por IA. A extensão busca estimativas de tempo e data de entrega de uma API externa e as exibe na loja.

Você constrói duas partes:

- **Extensão do App Builder** — Uma ação de back-end para front-end (BFF) que envolve uma API de estimativa de entrega externa, um webhook que enriquece os métodos de envio com datas de entrega no check-out e uma página de configuração da interface do Administrador para gerenciar configurações sem reimplantação.
- **Integração da loja** — estimativas de datas de entrega exibidas na PDP (página de detalhes do produto), na página do carrinho e na página de check-out usando componentes de entrega [!DNL Edge Delivery Services] e um módulo de cliente compartilhado.

>[!NOTE]
>
>Os agentes de IA são não determinísticos. Os prompts, as perguntas e as saídas deste tutorial são exemplos. Seu agente pode produzir diferentes perguntas, requisitos ou propostas de arquitetura. Use os exemplos deste tutorial para orientar o agente em direção a um resultado semelhante.

Antes de começar, conclua os [pré-requisitos](./tutorial-prerequisites.md). Este tutorial usa o **kit inicial de check-out**. Verifique se você já a clonou e concluiu as etapas de configuração descritas na página de pré-requisitos.

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

- Você tem uma **conta de comprador** — um cliente registrado em [!DNL Commerce] com um endereço de entrega padrão salvo. As estimativas de delivery nas páginas PDP e Carrinho são mostradas apenas para compradores conectados. O check-out mostra estimativas para todos os compradores, independentemente do status de autenticação.

>[!IMPORTANT]
>
>Este tutorial usa o **Checkout Starter Kit** (não o Integration Starter Kit). O kit inicial de checkout fornece extensibilidade baseada em webhook para pagamento, envio, impostos e eventos. Certifique-se de inicializar a partir do kit de check-out.

## Configurar a API de estimativa de entrega de modelo

A extensão chama uma API de estimativa de entrega externa para obter estimativas de data e hora de envio. Para este tutorial, você usa uma API fictícia para que possa executar o fluxo completo sem uma conta de operadora real. Duas opções estão disponíveis:

- **Opção A: fluxo de trabalho Pipedream** — Camada gratuita, configuração rápida, mas com limites de invocação mensais.
- **Opção B: Ação do App Builder Runtime** — Nenhuma dependência externa, criada durante as etapas de desenvolvimento de back-end.

>[!TIP]
>
>Durante o desenvolvimento, você pode começar com Pipedream (Opção A) e alternar para uma ação em tempo de execução (Opção B) se atingir a cota de chamada de camada livre. Ambas as opções implementam o mesmo contrato de API.

### Especificação da API

A API fictícia aceita uma solicitação POST e retorna as estimativas de data de entrega com transportadora, dias de trânsito, tempo limite e uma melhor estimativa.

**Corpo da solicitação** (todos os campos opcionais para o modelo):

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**Resposta (200 OK):**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**Respostas de erro:** 401 (chave de API ausente/inválida), 400 (formato `ship_date` inválido), 503 (tempo de inatividade simulado).

### Configurar o modelo

>[!BEGINTABS]

>[!TAB Fluxo de trabalho do Pipedream]

A opção Pipedream usa autenticação de token de portador e aceita uma solicitação POST para o URL do acionador do fluxo de trabalho.

| Item | Descrição |
|------|-------------|
| URL base | A URL completa do gatilho do fluxo de trabalho Pipedream (por exemplo `https://<id>.m.pipedream.net`) |
| Autenticação | `Authorization: Bearer <API_KEY>` |
| Método | POST |

{style="table-layout:auto"}

**Criar o fluxo de trabalho:**

1. Crie um novo fluxo de trabalho em [Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**).

1. Adicione um gatilho **HTTP / Webhook** configurado para POST. Pipedream atribui um URL de webhook.

1. Adicione uma etapa **Executar código Node.js** e cole o seguinte código de manipulador:

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. (Opcional) Adicione uma variável de ambiente `MOCK_API_KEY` nas configurações do fluxo de trabalho para impor a autenticação do token do portador. Se não for definido, qualquer solicitação será aceita.

1. Implante o workflow.

   Seu ponto de extremidade é o URL do acionador do webhook.

**Testar o modelo:**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB Ação do App Builder Runtime]

A opção de ação App Builder Runtime implanta o modelo como uma ação Runtime no mesmo projeto [!DNL App Builder]. Essa abordagem não tem dependência externa e nenhuma cota de invocação.

Solicitar que o agente crie a ação fictícia:

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

O agente cria `actions/mock-delivery-api/index.js` com o mesmo contrato de API que a opção Pipedream. Após a implantação, o endpoint é:

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

A autenticação é validada contra uma variável de ambiente `MOCK_API_KEY` em `.env`.

>[!ENDTABS]

## Desenvolvimento de extensão

Esta seção orienta você no desenvolvimento do back-end do [!DNL App Builder] para a extensão de estimativas de entrega. O back-end do fornece três ações:

| Ação | Tipo | Finalidade |
|--------|------|---------|
| `delivery-estimates` | Ação da Web autônoma | BFF para vitrine — o PDP e o carrinho chamam isso para datas de delivery |
| `shipping-methods` | Ação do Webhook | Enriquece as taxas de envio com datas de entrega em `additional_data` no check-out |
| `delivery-estimates-config` | Ação de back-end do administrador | CRUD para configuração armazenada em `aio-lib-state` |

{style="table-layout:auto"}

1. Nas configurações de MCP em seus agentes de codificação, verifique se o conjunto de ferramentas `commerce-extensibility` está habilitado sem erros.

   Por exemplo, no Cursor, vá para **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

   Se você vir erros, desligue e ligue o conjunto de ferramentas.

   >[!NOTE]
   >
   >Ao trabalhar com ferramentas de desenvolvimento assistidas por IA, espere variações naturais no código e nas respostas geradas pelo agente.
   >Se encontrar algum problema com seu código, peça ao agente para ajudá-lo a depurá-lo.

1. Se você tiver alguma documentação adicionada ao contexto do cursor, desative-a.

   Navegue até **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** e exclua qualquer documentação listada.

### Etapa 1: fornecer o prompt inicial

Forneça ao agente a especificação da API externa para o contexto e solicite que ele comece. Dizer ao agente para parar e fazer perguntas ajuda a orientar a implementação antecipadamente.

Digite o seguinte prompt na janela de bate-papo do agente:

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>A referência ao arquivo de especificação da API externa (`@docs/API_SPEC.md`) no prompt fornece ao agente um contexto concreto sobre o contrato de API de terceiros. O agente usa isso para projetar a ação BFF, o cliente HTTP compartilhado e os campos de configuração da interface do usuário Admin. Dizer ao agente para PARAR e fazer perguntas aciona o fluxo de trabalho guiado e ajuda a orientar a implementação antecipadamente.

### Etapa 2: Responda às perguntas do agente

O agente retorna com uma série de perguntas esclarecedoras que abrangem tópicos como ambiente de destino (PaaS versus SaaS), escopo (ação BFF independente, enriquecimento do webhook ou ambos), fonte de endereço de origem, estratégia de cache e preferência de teste. O exemplo a seguir mostra perguntas e respostas típicas. Seu agente pode fazer perguntas diferentes, mas os tópicos geralmente são os mesmos.

**Exemplo de perguntas sobre o agente:**

1. **Ambiente do Target** — Você está criando para PaaS (no local) ou SaaS (Adobe Commerce as a Cloud Service)?
2. **Escopo** — deve ser uma ação BFF autônoma (a vitrine a chama diretamente), enriquecimento do webhook (estender métodos de envio no check-out) ou ambos?
3. **Capacidade de configuração do administrador** — Configurações como URL da API, chave da API e endereço de origem devem ser configuráveis por meio do Administrador do Commerce ou armazenadas em `.env`?
4. **Endereço de origem** — De onde vem o endereço de origem (depósito)? Deve ser uma configuração estática ou resolvida dinamicamente?
5. **Armazenamento em cache** — As estimativas de entrega devem ser armazenadas em cache no lado do servidor para reduzir as chamadas para a API externa? Em caso afirmativo, qual TTL?

**Exemplo de respostas:**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>Perguntar ao agente se a loja deve chamar a API de terceiros diretamente ou passar por uma ação de tempo de execução aciona uma discussão útil de arquitetura. O agente explica os benefícios do padrão BFF (Back-end-for-Frontend): a chave da API permanece no lado do servidor, o CORS é manipulado, o armazenamento em cache é centralizado e você obtém a abstração do fornecedor. Solicitar a capacidade de configuração da interface do administrador faz com que o agente armazene todas as configurações em `aio-lib-state` em vez de `.env`, eliminando reimplantações ao alterar configurações.

>[!NOTE]
>
>Seu agente pode fazer perguntas diferentes. Use essas respostas como orientação para direcionar o agente para o mesmo resultado funcional: uma ação BFF para chamadas de vitrine, um webhook de métodos de envio para enriquecimento de check-out e uma página de configuração da interface do Administrador que armazena configurações em `aio-lib-state`.

### Etapa 3: analisar requisitos e arquitetura

O agente gera requisitos e documentos de arquitetura para que você os revise. Verifique se os requisitos correspondem às respostas fornecidas e se a arquitetura abrange:

- Uma **ação BFF** (`delivery-estimates`) — Uma ação autônoma da Web que a loja chama do PDP e das páginas do carrinho. Ele lê a configuração de `aio-lib-state`, chama a API de estimativa de entrega externa e retorna estimativas formatadas.
- Uma **ação de webhook** (`shipping-methods`) — Enriquece as taxas de envio com as datas de entrega em `additional_data` durante o check-out. Usa o método de webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`.
- Uma **Ação de configuração de administrador** (`delivery-estimates-config`) — CRUD para configuração (URL da API, chave da API, endereço de origem, operadoras, TTL de cache) armazenada em `aio-lib-state`.
- **Bibliotecas compartilhadas** — Um cliente HTTP para a API externa e um módulo de configuração para leitura e gravação `aio-lib-state`.

>[!NOTE]
>
>Os agentes de IA são não determinísticos e seus comportamentos diferem dependendo do modelo e do IDE. Você pode obter um conjunto diferente de perguntas que produzem um conjunto diferente de requisitos e arquitetura. Se sim, tente orientar o agente em uma direção de modo que a implementação corresponda ao que é apresentado neste tutorial antes de continuar.

### Etapa 4: Selecionar um plano de implementação

O agente oferece a opção de criar um plano de implementação detalhado ou concluir uma implementação direta.

- Se quiser um plano revisável que possa ser executado em fases com mais controle, selecione a primeira opção.
- Se desejar que o agente faça a implementação completa com intervenção mínima, selecione a segunda opção.

### Etapa 5: limpar e implantar

Depois que o agente concluir a implementação, ele continuará a limpeza. Como somente o domínio de envio está em uso, o agente remove os andaimes não utilizados:

- Ações de pagamento e configuração (`validate-payment/`, `filter-payment/`, `payment-methods.yaml`)
- Ações e configuração de impostos (`collect-taxes/`, `collect-adjustment-taxes/`, `tax-integrations.yaml`)
- Ações e configuração de eventos (`commerce-events/`, `3rd-party-events/`, `events.config.yaml`)
- Estrutura genérica (`generic/`)
- Componentes SPA da interface do administrador de outros domínios (por exemplo, páginas e ganchos relacionados a impostos)
- Scripts não utilizados, arquivos de teste e variáveis de ambiente

>[!TIP]
>
>Peça ao agente que também verifique o SPA da interface do administrador para ver se há sobras de outros domínios. A página Classes de Imposto e seus ganchos ainda podem estar presentes no andaime do kit inicial e precisam ser removidos.

Após a limpeza, implante usando estas etapas **nesta ordem**:

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>Não ignore nem reordene as etapas. As etapas 1 a 3 são pré-requisitos para a implantação. O comando `aio app deploy` falhará se nenhuma credencial tiver sido configurada.

### Etapa 6: configurar o webhook e a interface do administrador

Após a implantação, configure o webhook de envio. O agente pode criar um script para assinar programaticamente:

```bash
npm run subscribe-webhook
```

Este comando assina o webhook de envio com as seguintes configurações:

| Campo | Valor |
|-------|-------|
| Método Webhook | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Tipo de Webhook | `after` |
| Obrigatório | Opcional (permite o fallback para envio padrão) |
| Tempo-limite | 5000 ms |

{style="table-layout:auto"}

>[!NOTE]
>
>Para SaaS, o nome do método webhook descarta `magento.` do caminho. O nome do webhook para PaaS é `plugin.magento.out_of_process_shipping_methods...`, enquanto o nome do webhook para SaaS é `plugin.out_of_process_shipping_methods...`.

Em seguida, configure a interface do usuário do administrador:

1. Habilitar a **Interface do Administrador do SDK** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**).

1. Configure extensões selecionando o espaço de trabalho e a extensão [!DNL App Builder].

1. Clique em **[!UICONTROL Refresh registrations]**.

1. Navegue até **[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]** na barra lateral [!DNL Admin].

1. Conclua a configuração ativando o recurso e especificando as configurações necessárias, incluindo o URL da API e a chave da API, o endereço de origem, as operadoras padrão, o TTL de cache e os mapeamentos de código da operadora.

### Etapa 7: testar a extensão

Testar a ação direta da BFF de estimativa de delivery:

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

A resposta deve ser semelhante a:

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### Criar o contrato de serviço

Agora que o backend foi concluído, peça ao agente para criar um contrato de serviço para o trabalho da loja:

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

O agente produz `docs/STOREFRONT_API_SPEC.md` com o contrato completo de ponto de extremidade BFF (formato de solicitação e resposta, exemplo de cargas, tratamento de erros) e um prompt pronto para uso para o espaço de trabalho de vitrine.

Copie este arquivo no projeto da loja antes de iniciar as etapas de desenvolvimento da loja.

>[!TIP]
>
>Fazer com que o agente gere um contrato de serviço **e**, um prompt para o outro espaço de trabalho garante uma transferência limpa entre o back-end e as equipes (ou agentes) da loja. O agente da loja pode começar a trabalhar imediatamente sem precisar fazer perguntas sobre a API.

## Conectar à loja

Esta seção orienta você na implementação da parte da loja da extensão de estimativas de entrega usando o [!DNL Edge Delivery Services] e ferramentas de desenvolvimento assistido por IA. Você adiciona estimativas de datas de entrega à PDP, à página do carrinho e à página de finalização.

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
- O arquivo `STOREFRONT_API_SPEC.md` copiado na pasta `docs/` do projeto da vitrine

### Etapa 1: Validar o ambiente

Abra o arquivo `config.json` e verifique se os valores de `commerce-core-endpoint` e `commerce-endpoint` apontam para o ponto de extremidade do GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Etapa 2: fornecer o prompt inicial

Com o contrato de serviço já em seu projeto, solicite que o agente implemente a integração da loja. Use o modo **Plano**, se disponível em seu agente, para impedir que o agente continue sem um plano.

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>O prompt é detalhado porque o contrato completo da API já está disponível no agente de back-end. Referenciando `@docs/STOREFRONT_API_SPEC.md`, o agente conhece a URL do ponto de extremidade, o formato de solicitação e resposta e o tratamento de erros. A lista de requisitos explícitos impede que o agente invente o escopo. Especificamente, a solicitação do modo de plano aciona o workflow em fases que ajuda a orientar a implementação antecipadamente.

### Etapa 3: Responda a perguntas de esclarecimento

O agente retorna com perguntas sobre escopo de autenticação, abordagem de check-out e estilo. O exemplo a seguir mostra perguntas e respostas típicas.

**Exemplo de perguntas sobre o agente:**

1. **Usuários anônimos vs. usuários conectados** — As estimativas devem ser exibidas nas páginas PDP e Carrinho para todos os compradores ou apenas para os autenticados?
2. **Abordagem de check-out** — O contêiner de entrega ShippingMethods não expõe `additional_data`. Portanto, o agente propõe duas opções:
   - **Opção A:** Chame o BFF no check-out e nas datas de entrega DOM-inject (mais simples, consistente com PDP/Carrinho)
   - **Opção B:** estenda o fragmento do GraphQL de check-out via `overrideGQLOperations` para incluir `additional_data`
3. **Estilo** — Emojis versus tokens de design existentes

**Exemplo de respostas:**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>Mostrar estimativas apenas para compradores conectados é uma opção pragmática. O agente pode usar o endereço de envio padrão do comprador automaticamente (via GraphQL), de modo que nenhuma entrada de código postal é necessária. Compradores anônimos em PDP e Carrinho exigiriam a inserção de um código postal, o que adiciona atrito. No check-out, todos os compradores veem as datas de entrega porque o endereço de entrega já foi inserido.

>[!NOTE]
>
>Seu agente pode fazer perguntas diferentes. Use essas respostas como orientação:
>
>- Exibir estimativas de PDP e carrinho somente para compradores conectados (nenhuma entrada de código postal é necessária).
>- Para o check-out, use a Opção A (chamada BFF + injeção DOM) para simplificar.
>- Use tokens de design existentes para o estilo.

### Etapa 4: analisar requisitos e arquitetura

O agente projeta uma arquitetura de módulo compartilhada. Verifique se abrange:

| Componente | Finalidade |
|-----------|---------|
| `scripts/delivery-estimates.js` | Módulo compartilhado — cliente BFF, armazenamento em cache (sessionStorage, TTL de 30 minutos), formatação de data, lógica de contagem regressiva, pesquisa de endereço do cliente, mapeamento da operadora |
| Integração com PDP | Exibe &quot;Obtenha até [data]&quot; com contagem regressiva opcional entre preço e descrição |
| Integração do carrinho | Exibe o intervalo de datas (&quot;quinta-feira, 12 de março - sexta-feira, 13 de março&quot;) na coluna direita acima do resumo da ordem |
| Integração de check-out | Chama BFF quando a etapa de envio está ativa, DOM injeta datas de entrega via `MutationObserver` |

{style="table-layout:auto"}

Principais decisões de design a serem verificadas:

- Todas as chamadas BFF são não bloqueadas — as páginas são renderizadas primeiro, as estimativas são exibidas de forma assíncrona.
- Todas as falhas são silenciosas — somente `console.debug`, sem erros do comprador.
- `CARRIER_MAP` mapeia os códigos de operadora do Commerce (DPS, Fedex) para códigos de operadora BFF (padrão, expresso).
- O `import()` dinâmico mantém o módulo de entrega fora do caminho de renderização crítico.

>[!NOTE]
>
>Os agentes de IA são não determinísticos e seus comportamentos diferem dependendo do modelo e do IDE. Você pode obter um conjunto diferente de perguntas que produzem um conjunto diferente de requisitos e arquitetura. Se sim, tente orientar o agente em uma direção de modo que a implementação corresponda ao que é apresentado neste tutorial antes de continuar.

### Etapa 5: Selecionar um plano de implementação

O agente oferece a opção de criar um plano de implementação detalhado ou concluir uma implementação direta.

- Se quiser um plano revisável que possa ser executado em fases com mais controle, selecione a primeira opção.
- Se desejar que o agente faça a implementação completa com intervenção mínima, selecione a segunda opção.

Durante a implementação, o agente cria e modifica os seguintes arquivos:

**Novo arquivo:**

- `scripts/delivery-estimates.js` — Módulo compartilhado com `fetchDeliveryEstimates()`, `getCustomerShippingAddress()`, `formatDeliveryDate()`, `buildCountdownText()`, `findEstimateForCarrier()`

**Arquivos modificados:**

- `blocks/product-details/product-details.js` + `.css` — Div de estimativa de entrega na coluna direita, busca assíncrona após renderização principal
- `blocks/commerce-cart/commerce-cart.js` + `.css` — Div de estimativa de entrega acima do resumo do pedido
- `blocks/commerce-checkout/commerce-checkout.js`, `containers.js`, `.css` — Injeção de DOM com base em `MutationObserver` para rótulos de método de envio

Observe o código que está sendo gerado e faça perguntas ou redirecione o agente, conforme necessário.

### Etapa 6: iniciar o servidor e testar

Depois que o agente concluir a implementação, inicie o servidor de desenvolvimento e teste as estimativas de delivery.

1. Iniciar o servidor de desenvolvimento local:

   ```bash
   npm run start
   ```

1. Em um navegador, faça logon na conta do comprador.

   As estimativas de entrega em PDP e Carrinho exigem uma sessão autenticada com um endereço de entrega padrão salvo.

1. Navegue até a página de um produto e verifique os seguintes resultados:

   | Página | Resultado esperado | Autenticação necessária |
   |------|-----------------|---------------|
   | PDP | &quot;Obtenha-o até quinta-feira, 12 de março&quot; com contagem regressiva opcional | Sim (apenas com logon) |
   | Carrinho | &quot;Entrega estimada: quinta-feira, 12 de março - sexta-feira, 13 de março&quot; | Sim (apenas com logon) |
   | Check-out | &quot;Entrega estimada: quinta-feira, 12 de março&quot; por método de envio | Não (endereço inserido no check-out) |

   {style="table-layout:auto"}

>[!NOTE]
>
>Os métodos de envio sem uma transportadora correspondente (por exemplo, Taxa Uniforme) não mostram nenhuma estimativa. Isso ocorre por design — somente as operadoras mapeadas em `CARRIER_MAP` obtêm as datas de entrega.

Você pode fazer testes manuais ou solicitar que o agente use os recursos do navegador para testar:

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### Etapa 7: limpar

Depois que você ignorar ou concluir o teste, o agente solicitará que você prossiga com a limpeza. Após a confirmação, o agente arquiva todos os artefatos de documentação produzidos durante a implementação.

## Solução de problemas

Use as seguintes dicas se encontrar problemas durante o tutorial.

### Infraestrutura (App Builder)

| Sintoma | Causa | Correção |
|---------|-------|-----|
| A ação de configuração da interface do administrador retorna `400 Bad Request` com &quot;A solicitação define parâmetros que não são permitidos (propriedades reservadas)&quot; | O gancho de front-end está enviando `__ow_method` no corpo da solicitação. Propriedades com o prefixo `__ow_` são reservadas pelo OpenWhisk e rejeitadas quando a ação tem `final: true`. | Enviar uma propriedade `method` personalizada em vez de `__ow_method`. A ação de back-end lê `params.method` primeiro e depois retorna para `params.__ow_method` (que o Tempo de Execução fornece automaticamente). |
| `aio app deploy` falha com &quot;maxVersion é necessário em productDependencies&quot; | A validação da CLI requer `minVersion` e `maxVersion` em `app.config.yaml` dependências de produto. | Adicione um valor `maxVersion` a cada entrada `productDependencies` em `app.config.yaml`. |
| Falha no comando de implantação | Credenciais não configuradas antes da implantação. `.env`, seleção de espaço de trabalho e sincronização OAuth devem acontecer primeiro. | Siga a ordem correta: `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`. |

{style="table-layout:auto"}

### Loja (Edge Delivery Services)

| Sintoma | Causa | Correção |
|---------|-------|-----|
| A estimativa de entrega de PDP não aparece para compradores conectados | O bloco PDP não inicializa o menu suspenso `account`, portanto `getCustomerAddress()` falha silenciosamente e nenhuma estimativa é buscada. | Use `CORE_FETCH_GRAPHQL.fetchGraphQl()` diretamente para consultar endereços de comprador, em vez de depender da API de destino da conta. Isso funciona em qualquer página. |
| O PDP ainda não é exibido após a correção do GraphQL | Erro de digitação no nome do método: `CORE_FETCH_GRAPHQL.fetch()` foi usado em vez de `CORE_FETCH_GRAPHQL.fetchGraphQl()`. | Use o nome de método correto: `fetchGraphQl` (Q maiúsculo, l minúsculo). |
| As datas de entrega de check-out não aparecem na primeira carga | O ouvinte de eventos `checkout/updated` foi registrado depois que `checkout/initialized` já tinha sido acionado, portanto, os dados iniciais foram perdidos. | Adicione um ouvinte `checkout/initialized` com `{ eager: true }` para capturar eventos emitidos antes do registro. Mantenha o ouvinte `checkout/updated` para alterações subsequentes. |
| Estimativa de entrega do carrinho não aparece | `block.appendChild(fragment)` move todos os filhos para fora do fragmento, portanto `fragment.querySelector('.cart__delivery-estimate')` retorna nulo. | Consulta de `block` em vez de `fragment` após a operação de acréscimo. |
| Taxa única de envio não mostra nenhuma data de entrega no check-out | Por design — `CARRIER_MAP` mapeia somente DPS para padrão e Fedex para expresso. A taxa uniforme não tem uma operadora correspondente na API externa. | Não é um erro. Para adicionar estimativas para outras operadoras, estenda a `CARRIER_MAP` em `scripts/delivery-estimates.js` e configure a operadora na extensão de back-end. |

{style="table-layout:auto"}

### Sandbox SaaS para Commerce

| Sintoma | Causa | Correção |
|---------|-------|-----|
| O Webhook retorna `429 Too Many Requests` | O espaço de trabalho [!DNL App Builder] está no modo de depuração, que tem limites de taxa por minuto estritos. [!DNL Commerce] recalcula as taxas de envio com frequência durante o check-out, esgotando a cota. | Implante em um espaço de trabalho de Produção (`aio app use` para alternar, depois `aio app deploy`). Os espaços de trabalho de produção não têm limites de taxa de depuração. |
| Aviso de tempo limite flexível do Webhook (>1000 ms) | A ação de webhook de métodos de envio demorou mais do que o tempo limite flexível de [!DNL Commerce] 1000 ms. | Habilite o cache do lado do servidor no `aio-lib-state` de forma mais agressiva ou aumente o tempo limite do webhook em [!DNL Commerce Admin] (configuração do Commerce Webhooks). |

{style="table-layout:auto"}

## Resumo do tutorial

Este é um resumo dos tópicos abordados neste tutorial:

- **Configuração da API Mock:** Criação de uma API de estimativa de entrega mock usando Pipedream ou uma ação de Tempo de Execução [!DNL App Builder].
- **Padrão BFF:** criando uma ação de back-end para front-end que envolve a API externa, mantém credenciais no lado do servidor e centraliza o armazenamento em cache.
- **Enriquecimento do Webhook:** extensão do webhook de métodos de envio para inserir datas de entrega em cada opção de envio no check-out.
- **Capacidade de configuração da interface do administrador:** adicionar uma página de configuração usando o [!DNL Admin UI SDK] para que os comerciantes possam gerenciar configurações de API, endereço de origem e mapeamentos de operadora sem reimplantação.
- **Contratos de serviço:** criando contratos de API que conectam extensões de back-end e implementações de vitrine.
- **Integração com a loja:** exibindo estimativas de entrega em PDP (&quot;Obter por&quot;), carrinho (intervalo de datas) e check-out (por método de envio) usando um módulo de cliente compartilhado.
- **UX sem bloqueio:** garantir que as estimativas de entrega nunca bloqueiem o fluxo de compra — as páginas são renderizadas primeiro e as estimativas são exibidas de forma assíncrona.

## Próximas etapas

Use as seguintes sugestões para estender o serviço de estimativa de entrega:

- **Conecte uma API de operadora real:** Substitua o modelo por uma API de remessa ao vivo, como UPS, FedEx ou USPS, alterando a URL de Serviço e a chave da API no [!DNL Admin UI].
- **Suporte a compradores anônimos:** adicione uma entrada de código postal nas páginas PDP e do carrinho para que os compradores que não estão conectados também possam ver as estimativas de entrega.
- **Estender mapeamentos de transportadoras:** Adicione mais códigos de transportadoras a `CARRIER_MAP` para exibir datas de entrega para métodos de remessa adicionais.
- **Adicionar cache do lado do servidor:** Implemente o cache `aio-lib-state` na ação BFF para reduzir as chamadas à API externa para pares de origem e destino repetidos.
- **Mostrar estimativas na confirmação do pedido:** Exiba a data de entrega estimada na página de confirmação do pedido e nos emails transacionais.
