---
title: Pré-requisitos do laboratório do ADL Commerce
description: Saiba mais sobre os pré-requisitos do laboratório de extensões de classificações.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Pré-requisitos do laboratório da Adobe Commerce

Esta página lista os pré-requisitos e outras etapas de configuração manual do [laboratório de extensões de classificações](./workbook.md). O laboratório também contém um script que automatiza a maioria dessas etapas.

## Pré-requisitos da extensão

Antes de começar, conclua os seguintes pré-requisitos:

* Instalar o [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Instalar o plug-in do Commerce

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Baixar um IDE assistido por IA, como [Cursor](https://cursor.com/download) (recomendado). Outros IDEs, como Claude Code, Gemini CLI ou Copilot também são suportados, mas podem exigir modificações nos prompts e em outras etapas deste tutorial.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### Configurar a CLI AIO

1. Limpar a configuração existente:

   ```bash
   aio config clear
   ```

   Faça logon usando a CLI AIO:

   ```bash
   aio auth login -f
   ```

1. Selecione a organização, o projeto e o espaço de trabalho, usando cada um dos seguintes comandos:

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![Configuração de CLI](./assets/cli-configuration.png){width="600" zoomable="yes"}

### Clonar kit inicial de integração

Clonar o repositório do kit inicial de integração do Commerce e preparar seu projeto:

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Clonar kit inicial](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Criar o arquivo .env

Crie seu arquivo de configuração de ambiente:

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### Baixar configuração do espaço de trabalho

Execute o seguinte comando para baixar o arquivo de configuração do espaço de trabalho:

```bash
aio console workspace download workspace.json
```

### Conectar o espaço de trabalho local ao espaço de trabalho remoto

Vincular o projeto local ao espaço de trabalho remoto:

```bash
aio app use workspace.json -m
```

![Conectar ao espaço de trabalho](./assets/connect-workspace.png){width="600" zoomable="yes"}

## Pré-requisitos da loja

Os itens a seguir são necessários para concluir a seção [vitrine](#connect-to-the-storefront) deste tutorial e ver as classificações de produtos em sua loja.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### Obter os arquivos do projeto

Você pode obter os arquivos de projeto de uma das duas formas a seguir:

<!-- 
#### Option A: Clone the repository (recommended) -->

Se você tiver o [!DNL Git] instalado, abra o terminal e clone o repositório:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### Instalar dependências raiz

Instale as dependências do projeto principal:

```bash
npm install
```

Isso instalará todos os pacotes necessários para o aplicativo da loja.

### Instalar dependências do servidor MCP

Navegue até o diretório do servidor MCP e instale suas dependências:

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### Ativar MCP no cursor

O servidor MCP (Protocolo de Contexto de Modelo) fornece aos agentes de IA acesso à documentação de vitrine do [!DNL Adobe Commerce].

#### Configurações de MCP de Cursor Aberto

![Abrir Configurações de MCP do Cursor](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Abrir [!DNL Cursor]
1. Ir para **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### Habilitar e configurar recursos MCP

O projeto inclui um arquivo de configuração MCP em `.cursor/mcp.json`. Este arquivo já deve estar configurado para usar o servidor MCP local.

Verifique a configuração do MCP:

1. Verifique se o servidor &quot;commerce-documentation-rag&quot; está listado e ativado

A configuração deve ser semelhante a esta:

![Configuração de MCP](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>O script `start-mcp.sh` carregará automaticamente as variáveis de ambiente do arquivo `.env` no diretório `mcp-server`.

#### Reiniciar o cursor

Depois de habilitar o MCP e configurar o servidor:

1. Sair [!DNL Cursor] completamente
1. Reabra [!DNL Cursor] e abra o projeto `aem-boilerplate-commerce`

#### Verificar conexão MCP

Verifique se o servidor MCP está sendo executado corretamente:

1. Abrir um novo chat em [!DNL Cursor]
1. Procure um indicador mostrando que o servidor MCP está conectado (geralmente na interface de chat)
1. Tente fazer uma pergunta como: &quot;Pesquise nos documentos da loja para obter informações sobre slots&quot;

Se o servidor MCP estiver funcionando, você deverá ver os resultados relevantes da documentação.

![Conexão MCP verificada](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### Iniciar o servidor de desenvolvimento

Iniciar o servidor de desenvolvimento local:

```bash
npm run start
```

O servidor de desenvolvimento iniciará em `http://localhost:3000`.

Navegue até a página de vestuário em `http://localhost:3000/apparel`.

![Servidor de desenvolvimento em execução](./assets/development-server-running.png){width="600" zoomable="yes"}
