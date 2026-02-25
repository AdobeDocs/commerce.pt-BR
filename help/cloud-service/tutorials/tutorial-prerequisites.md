---
title: Pré-requisitos do tutorial
description: Saiba mais sobre os pré-requisitos do laboratório de extensões de classificações.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: 68e34cecbc1b16194ccc2e0296c2d66f37855b7c
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Pré-requisitos do tutorial

Esta página lista os pré-requisitos e as etapas de configuração para os tutoriais do [!DNL Adobe Commerce as a Cloud Service], como o [tutorial de extensão de classificações](./ratings-extension.md) e o [tutorial de extensão do método de envio](./shipping-method-extension.md).

## Pré-requisitos do Adobe Commerce as a Cloud Service

* Instalar o [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Instale os plug-ins [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) e [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev):

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

* Baixar um IDE assistido por IA, como [Cursor](https://cursor.com/download) (recomendado). Outros IDEs, como Claude Code, Gemini CLI ou Copilot também são suportados, mas podem exigir modificações nos prompts e em outras etapas do tutorial.

### Pré-requisitos do Adobe Developer Console

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Faça logon usando seu email e senha.

#### Criar um novo projeto

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/).
1. Clique em [!UICONTROL **Criar projeto a partir de um modelo**].
1. Selecione o modelo [!UICONTROL **App Builder**].
1. Insira um [!UICONTROL **Título do projeto**] e [!UICONTROL **Nome do aplicativo**].
1. Certifique-se de que a caixa de seleção **[!UICONTROL Include Runtime]** esteja marcada.

   ![Criação de projeto do Adobe Developer Console com modelo do App Builder selecionado](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Clique em [!UICONTROL **Salvar**].

#### Adicionar APIs ao espaço de trabalho

1. Clique no espaço de trabalho [!UICONTROL **Preparo**] e repita as etapas a seguir para cada API.

   ![Espaço de trabalho de preparo com a opção Adicionar Serviço para APIs](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Clique em [!UICONTROL **Adicionar Serviço**] e selecione [!UICONTROL **API**].

1. Selecione uma das seguintes APIs. Você precisará repetir esse processo para cada API listada abaixo:

   * Filtro [!UICONTROL **Serviços da Adobe**]:
      * [!UICONTROL **API de gerenciamento de E/S**]
      * API de [!UICONTROL **Eventos de E/S**]
   * Filtro [!UICONTROL **Experience Cloud**]:
      * API [!UICONTROL **Adobe I/O Events para Adobe Commerce**]

1. Clique em [!UICONTROL **Avançar**].

1. Clique em [!UICONTROL **Salvar API configurada**].

1. Repita as etapas anteriores até que todas as APIs sejam adicionadas ao espaço de trabalho.

   ![Workspace mostrando todas as APIs necessárias adicionadas com êxito](../assets/apis-added.png){width="600" zoomable="yes"}

### Configurar a CLI do Adobe I/O

1. Limpar qualquer configuração existente:

   ```bash
   aio config clear
   ```

   Fazer logon usando o [!DNL Adobe I/O CLI]:

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

   ![Terminal mostrando a seleção do projeto e do espaço de trabalho da organização da CLI do Adobe I/O](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Clonar os kits iniciais

Clonar um dos seguintes repositórios do Commerce starter kit para a extensão que você está criando e preparar seu projeto:

Kit inicial de integração:

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

Kit inicial de check-out:

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB Kit de início de integração]

### Criar um arquivo .env

Crie seu arquivo de configuração de ambiente:

```bash
cp env.dist .env
```

Abra o arquivo `.env` em um editor de texto e adicione as seguintes credenciais OAuth:

```shell-session
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Você pode copiar esses valores da página **[!UICONTROL Credential details]** no [Developer Console](https://developer.adobe.com/) clicando na guia **[!UICONTROL OAuth Server-to-Server]** do seu espaço de trabalho.

![Página de credenciais de servidor para servidor do OAuth no Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Adicionar a configuração do Commerce

Adicione os seguintes detalhes da instância do Commerce ao arquivo `.env`:

```shell-session
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Para localizar esses valores:

1. Navegue até [instâncias do Commerce Cloud Service](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Clique no ícone de informações ao lado da instância.
1. Copie o ponto de extremidade REST como `COMMERCE_BASE_URL`.
1. Copiar o ponto de extremidade do GraphQL como `COMMERCE_GRAPHQL_ENDPOINT`.

#### Definir prefixo do evento

Defina um valor temporário para o prefixo do evento:

```shell-session
EVENT_PREFIX=test
```

### Baixar configuração do espaço de trabalho

Execute o seguinte comando para baixar o arquivo de configuração do espaço de trabalho:

```bash
aio console workspace download workspace.json
```

Copie o arquivo de configuração do espaço de trabalho para o diretório `scripts`:

```bash
cp workspace.json scripts/
```

### Conectar o espaço de trabalho local ao espaço de trabalho remoto

Vincular o projeto local ao espaço de trabalho remoto:

```bash
aio app use workspace.json -m
```

![Terminal mostrando conexão de espaço de trabalho bem-sucedida com o comando de uso do aplicativo aio](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!TAB Kit inicial de check-out]

### Conectar o espaço de trabalho local ao espaço de trabalho remoto

Vincule o projeto local ao espaço de trabalho remoto. Na raiz do projeto (a pasta `extension`), execute:

```bash
aio app use --merge
```

Quando solicitado, escolha a opção que usa a organização, o projeto e o espaço de trabalho selecionados ao configurar a CLI do Adobe I/O. Isso grava a configuração do espaço de trabalho no aplicativo para que a implantação e o desenvolvimento local usem esse espaço de trabalho.

![Terminal mostrando conexão de espaço de trabalho bem-sucedida com o comando de uso do aplicativo aio](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### Instalar ferramentas de IA de extensibilidade

Este processo cria a configuração de MCP (`.<agent>/mcp.json`), o diretório de habilidades (`.<agent>/skills/`) e adiciona `AGENTS.md` à raiz do projeto. Você deverá escolher um kit inicial, um agente de codificação e um gerenciador de pacotes.


1. Configure as ferramentas de desenvolvimento assistido por IA na pasta `extension` usando os seguintes comandos:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Terminal mostrando a saída do comando de instalação das ferramentas de extensibilidade de IA](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. Depois que a configuração for concluída, reinicie o agente de codificação para permitir que ele carregue as novas ferramentas e habilidades do MCP. As ferramentas do Commerce App Builder agora estão disponíveis em seu ambiente.

   >[!NOTE]
   >
   >Se você vir um aviso de que nenhuma habilidade foi encontrada para o kit inicial, algo deu errado, geralmente porque a configuração foi executada em uma pasta diferente do local onde o kit inicial foi clonado. Execute `aio commerce extensibility tools-setup` na pasta `extension` (a raiz do projeto do kit inicial) e selecione o kit inicial apropriado quando solicitado.

   ![Terminal mostrando a configuração das ferramentas de extensibilidade de IA com o kit de início de check-out selecionado](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```shell-session
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
