---
title: Pré-requisitos do tutorial
description: Saiba mais sobre os pré-requisitos e as etapas de configuração para tutoriais do Adobe Commerce as a Cloud Service, incluindo ferramentas de desenvolvimento de extensão e vitrine.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 0ece7b58bdafd664297cbdee809c53ef2389fb12
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# Pré-requisitos do tutorial

Esta página lista os pré-requisitos e as etapas de configuração para os tutoriais do [!DNL Adobe Commerce as a Cloud Service], como o [tutorial de extensão de classificações](./ratings-extension.md) e o [tutorial de extensão do método de envio](./shipping-method-extension.md).

## Pré-requisitos gerais

As ferramentas a seguir são necessárias para a extensão e o desenvolvimento da loja neste tutorial.

* [!DNL Node.js] (versão `22.x.x`) e npm (`9.0.0` ou superior): verifique sua instalação usando o seguinte comando:

  ```bash
  node --version
  npm --version
  ```

* Instalar o [Git](https://git-scm.com) - Verifique a instalação:

  ```bash
  git --version
  ```

* Bash shell
   * macOS/Linux: não é necessária instalação
   * Windows: Use o [Git Bash](https://git-scm.com/install) ou o [Subsistema do Windows para Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* Baixe um IDE assistido por IA, como [Cursor](https://cursor.com/download) (recomendado). Outros IDEs, como Claude Code, Gemini CLI ou Copilot também são suportados, mas podem exigir modificações nos prompts e outras etapas no tutorial.

## [!DNL Adobe Commerce as a Cloud Service] pré-requisitos

* Instalar o [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Instale os plug-ins [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) e [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev):

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

Depois de instalar o [!DNL Adobe I/O CLI] e os plug-ins necessários, configure o espaço de trabalho de extensibilidade. A Adobe recomenda usar a configuração automatizada para obter a experiência mais rápida.

* **[Configuração automatizada](#automated-setup) (Recomendada)** — Execute um único comando para configurar o seu espaço de trabalho automaticamente.
* **[Configuração manual](#manual-setup)** — siga as instruções passo a passo para configurar cada componente individualmente.

### Configuração automatizada (recomendado) {#automated-setup}

>[!TIP]
>
>Se você encontrar problemas com a configuração automatizada, siga as etapas de [configuração manual](#manual-setup) abaixo.

O comando `app-setup` automatiza o processo de configuração do espaço de trabalho, incluindo a criação de um projeto [!DNL Adobe Developer Console], a adição das APIs necessárias, a configuração do [!DNL Adobe I/O CLI], a clonagem do kit inicial, a conexão do espaço de trabalho local e a instalação das ferramentas de IA de extensibilidade.

O comando `app-setup` orienta você pelas seguintes etapas:

* Selecionando ou criando um projeto [!DNL Adobe Developer Console] com as APIs necessárias
* Configurando o [!DNL Adobe I/O CLI] com sua organização, projeto e espaço de trabalho
* Clonagem do kit inicial apropriado e configuração do projeto
* Configurar o ambiente e conectar o espaço de trabalho local ao espaço de trabalho remoto
* Instalação das ferramentas de extensibilidade do Commerce e habilidades do agente de codificação

Execute o seguinte comando e siga os prompts interativos:

```bash
aio commerce extensibility app-setup
```

Depois que o comando for concluído, navegue até o diretório do projeto e reinicie o agente de codificação para carregar as novas ferramentas e habilidades do MCP. Se o tutorial exigir uma vitrine, execute novamente o comando e selecione o kit inicial [!DNL AEM Boilerplate Commerce].

O exemplo de instalação a seguir mostra os prompts interativos e a saída do kit iniciador de check-out.

+++Exemplo de instalação (verificar kit inicial)

```shell-session
aio commerce extensibility app-setup

🚀 Adobe Commerce Extensibility App Setup

✔ Logged in
📁 Working directory: /Users/username/projects/my-commerce-project

✔ Which starter kit would you like to use? Checkout Starter Kit
✔ Enter a name for your project directory: my-extension
✔ Which coding agent would you like to install the skills for? Cursor

📦 Cloning Checkout Starter Kit...
   ✔ Repository cloned
   Using npm (package-lock.json found)
   ✔ Dependencies installed

📋 Current Adobe I/O Console configuration:
   Org: My Organization (1234567)
   Project: My Commerce Project (1234567890123456789)
   Workspace: Stage (9876543210987654321)
✔ Do you want to continue with this configuration? (Answer "No" to select a different org/project/workspace)
No

🔧 Selecting Adobe I/O Console org, project, and workspace...

? Select Org: My Organization
Org selected My Organization
You are currently in:
1. Org: My Organization
2. Project: <no project selected>
3. Workspace: <no workspace selected>

? Select Project: My Commerce Project
Project selected : My Commerce Project
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: <no workspace selected>

? Select Workspace: Stage
Workspace selected Stage
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: Stage

✅ Console configured:
   Org: My Organization
   Project: My Commerce Project
   Workspace: Stage

🔐 Configuring workspace credentials and services...
   ✔ Workspace configuration loaded
   ✔ OAuth server-to-server credentials already configured
   ✔ All required services available in organization
   ✔ Subscribed to: Adobe Commerce as a Cloud Service

📋 Configuring Checkout Starter Kit...
   Creating .env from env.dist...
✔ Select tenant (type to search) My Commerce Instance:
https://<region>.api.commerce.adobe.com/<tenant-id>/graphql
   ✔ Commerce instance configured
✔ Enter the event prefix for your workspace: my-prefix
   ✔ Workspace IDs configured
   ✔ OAuth credentials configured
   ✔ Checkout Starter Kit configured

🔧 Installing Commerce Extensibility tools and agent skills...
   ✔ Commerce Extensibility tools installed

🎉 App setup complete!

📁 Project directory: /Users/username/projects/my-commerce-project/my-extension

Next steps:
   1. cd into your project directory
   2. Restart your coding agent to load the Commerce Extensibility tools and skills
```

+++

### Configuração manual {#manual-setup}

As seções a seguir descrevem como configurar manualmente cada componente do seu espaço de trabalho de extensibilidade. Siga estas etapas se preferir a configuração manual ou se encontrar problemas com a [configuração automatizada](#automated-setup).

### Pré-requisitos do Adobe Developer Console

Configure um projeto no Adobe Developer Console com as APIs e credenciais necessárias.

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Faça logon usando seu email e senha.

#### Criar um novo projeto

Crie um projeto do App Builder na Adobe Developer Console para hospedar sua extensão.

1. Navegue até [Adobe Developer Console](https://developer.adobe.com/).
1. Clique em **[!UICONTROL Create project from a template]**.
1. Selecione o modelo **[!UICONTROL App Builder]**.
1. Insira um **[!UICONTROL Project Title]** e **[!UICONTROL App Name]**.
1. Certifique-se de que a caixa de seleção **[!UICONTROL Include Runtime]** esteja marcada.

   ![Criação de projeto do Adobe Developer Console com modelo do App Builder selecionado](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Clique em **[!UICONTROL Save]**.

#### Adicionar APIs ao espaço de trabalho

Adicione as APIs necessárias ao espaço de trabalho do Stage para gerenciamento de eventos e integração do Commerce.

1. Clique no espaço de trabalho **[!UICONTROL Stage]** e repita as etapas a seguir para cada API.

   ![Espaço de trabalho de preparo com a opção Adicionar Serviço para APIs](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Clique em **[!UICONTROL Add Service]** e selecione **[!UICONTROL API]**.

1. Selecione uma das seguintes APIs. Repita esse processo para cada API listada abaixo:

   * **[!UICONTROL Adobe Services]** filtro:
      * **[!UICONTROL I/O Management API]**
      * API **[!UICONTROL I/O Events]**
   * **[!UICONTROL Experience Cloud]** filtro:
      * API **[!UICONTROL Adobe I/O Events for Adobe Commerce]**

1. Clique em **[!UICONTROL Next]**.

1. Clique em **[!UICONTROL Save configured API]**.

1. Repita as etapas anteriores até adicionar todas as APIs ao espaço de trabalho.

   ![Workspace mostrando todas as APIs necessárias adicionadas com êxito](../assets/apis-added.png){width="600" zoomable="yes"}

### Configurar a CLI do Adobe I/O

Conecte o [!DNL Adobe I/O CLI] à sua organização, projeto e espaço de trabalho.

1. Limpar qualquer configuração existente:

   ```bash
   aio config clear
   ```

1. Fazer logon usando o [!DNL Adobe I/O CLI]:

   ```bash
   aio auth login -f
   ```

1. Selecione a organização, o projeto e o espaço de trabalho usando cada um dos seguintes comandos:

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

```bash
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Copie esses valores da página **[!UICONTROL Credential details]** no [Developer Console](https://developer.adobe.com/) clicando na guia **[!UICONTROL OAuth Server-to-Server]** do seu espaço de trabalho.

![Página de credenciais de servidor para servidor do OAuth no Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Adicionar a configuração do Commerce

Adicione os seguintes detalhes da instância do Commerce ao arquivo `.env`:

```bash
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Para localizar esses valores:

1. Navegue até [instâncias do Commerce Cloud Service](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Clique no ícone de informações ao lado da instância.
1. Copie o ponto de extremidade REST como `COMMERCE_BASE_URL`.
1. Copiar o ponto de extremidade do GraphQL como `COMMERCE_GRAPHQL_ENDPOINT`.

#### Definir o prefixo do evento

Defina um valor temporário para o prefixo do evento:

```bash
EVENT_PREFIX=test
```

### Baixar a configuração do espaço de trabalho

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

### Instalar as ferramentas de IA de extensibilidade

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

## Configuração manual da vitrine

Esta seção descreve como configurar manualmente sua loja para o [Tutorial de extensão de classificações](./ratings-extension.md) e outros tutoriais da loja.

Para configurar automaticamente sua loja, execute o comando `app-setup` descrito na seção [Configuração automatizada](#automated-setup) e selecione o kit inicial [!DNL AEM Boilerplate Commerce].

### Pré-requisitos

Os itens a seguir são necessários para concluir a seção [vitrine](./ratings-extension.md#connect-to-the-storefront) do [Tutorial de extensões de classificações](./ratings-extension.md) e exibir classificações de produto em sua loja.

* [Google Chrome](https://www.google.com/chrome/) - Necessário para testar a vitrine

* Um projeto de vitrine conectado à sua instância [!DNL Commerce]. Se você não tiver um projeto de vitrine eletrônica, siga as etapas em [Criar uma vitrine eletrônica](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=pt-BR){target="_blank"}, incluindo a seção [Vincular repositório aos dados de comércio](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=pt-BR#link-repo-to-commerce-data){target="_blank"}.

### Clonar o repositório da loja

Abra o terminal e clone o repositório:

```bash
git clone https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### Instalar as dependências

Instale as dependências do projeto:

```bash
npm install
```

### Instalar as ferramentas de IA da loja

Configure as ferramentas de desenvolvimento assistido por IA na pasta `storefront`.

Execute o seguinte comando a partir da raiz do seu projeto padronizado. O comando instala o pacote `@adobe-commerce/commerce-extensibility-tools` como uma dependência de desenvolvimento, copia os arquivos de habilidades no diretório de habilidades do agente e configura o MCP (Model Context Protocol) para que o agente possa acessar as ferramentas de pesquisa de documentação do Commerce.

```bash
aio commerce extensibility tools-setup
```

O comando o guiará por dois prompts:

1. **Selecione um kit inicial** — Escolha **AEM Boilerplate Commerce**.

1. **Selecione seu agente de codificação** — escolha seu agente na lista de agentes suportados.
