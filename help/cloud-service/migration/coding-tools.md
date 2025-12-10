---
title: Ferramentas de codificação de IA para extensões
description: Saiba como usar as ferramentas de IA para criar extensões do Commerce App Builder.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 8f7b5536388e8f4cb1e763b430bdca8644d1da5c
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# Ferramentas de codificação de IA para extensões

Ao migrar para o [!DNL Adobe Commerce as a Cloud Service], você pode usar as ferramentas de codificação da IA para converter extensões existentes do PHP [!DNL Adobe Commerce] em extensões [!DNL Adobe Developer App Builder]. Ele também pode ser usado para criar novas extensões para o [!DNL App Builder].

O uso das ferramentas de codificação de IA oferece os seguintes benefícios:

* **Fluxo de trabalho de desenvolvimento aprimorado**: ferramentas de desenvolvimento integradas do Adobe Commerce.
* **Assistência fornecida por IA**: geração e depuração de código com reconhecimento de contexto.
* **Recursos específicos do Commerce**: ferramentas especializadas para desenvolvimento do Adobe Commerce App Builder.
* **Fluxos de trabalho automatizados**: processos simplificados de desenvolvimento e implantação.

## Pré-requisitos

* Um dos seguintes agentes de codificação:
   * [Cursor](https://cursor.com/download) (recomendado)
   * [Github Copilot](https://github.com/features/copilot)
   * [CLI do Google Gemini](https://github.com/google-gemini/gemini-cli)
   * [Código Claude](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download): versão LTS
* Gerenciador de Pacotes: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) ou [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): para clonagem de repositório e controle de versão

## Instalação

1. Instale globalmente a [Adobe I/O CLI](https://github.com/adobe/aio-cli) mais recente:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Instale os seguintes plug-ins:

   * [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime)
   * [CLI DO App Builder](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. Clonar o [kit inicial de integração](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration) do Commerce:

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Navegue até o diretório do kit inicial:

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Instale as ferramentas de extensibilidade do Commerce AI executando o comando de configuração interativo:

   ```bash
   aio commerce extensibility tools-setup
   ```

O processo de instalação solicitará as opções de configuração. Para o local de configuração, escolha &quot;Diretório atual&quot; para instalar as ferramentas em seu espaço de trabalho atual:

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Ao selecionar o agente de codificação, a Adobe recomenda selecionar `Cursor` para obter a melhor experiência de desenvolvimento:

```terminal
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

Ao selecionar o gerenciador de pacotes, a Adobe recomenda o uso de `npm` para consistência:

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. Após instalar com êxito as ferramentas de codificação, o processo de instalação configura:

   * Integração do servidor MCP para desenvolvimento do Adobe Commerce
   * Regras do IDE de cursor para uma experiência de desenvolvimento aprimorada
   * Fluxos de trabalho e ferramentas de desenvolvimento específicos do Commerce

   Os seguintes arquivos são adicionados ao seu espaço de trabalho:

   **Cursor**

   * Configuração de MCP: `.cursor/mcp.json`
   * Diretório de Regras: `.cursor/rules/`

   **Copilot**

   * Configuração de MCP: `.vscode/mcp.json`
   * Diretório de Regras: `.github/copilot-instructions.md`

>[!NOTE]
>
>Antes de implantar o projeto, será necessário concluir as seguintes tarefas de configuração:
>
>* Faça logon no [Adobe Developer Console](https://developer.adobe.com/console) usando a CLI do Adobe I/O.
>* Criar um projeto do App Builder (consulte [Configuração do projeto](https://developer.adobe.com/commerce/extensibility/events/project-setup)).
>* Configure variáveis de ambiente em um arquivo `.env`.
>
>Você pode concluir essas etapas de configuração manualmente ou aproveitar as ferramentas de codificação de IA para orientá-lo pelo processo. Consulte [Criar uma integração](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/) para obter instruções detalhadas sobre configuração.

## Configuração pós-instalação

### Fazer logon no [!DNL Adobe I/O CLI]

Após instalar o [!DNL Adobe I/O CLI], você precisa fazer login sempre que quiser usar o servidor MCP.

```bash
aio auth login
```

Para verificar se você está conectado, execute o seguinte comando:

```bash
aio where
```

Se encontrar problemas, tente fazer logoff e logon novamente em:

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>Alguns recursos do servidor MCP funcionarão sem fazer logon, mas o serviço RAG (Retrieval-Augmented Generation) não funcionará. O serviço RAG fornece ao agente de codificação de IA acesso em tempo real ao conjunto completo de documentações do Adobe Commerce, permitindo que ele responda a perguntas e gere código com base nas práticas atuais de desenvolvimento, APIs e padrões de arquitetura do Commerce.
>
>Em uma versão futura, o serviço RAG estará acessível independentemente, sem a necessidade de instalar outras ferramentas.

### Cursor

1. Reinicie o Cursor IDE para carregar as novas ferramentas e configuração do MCP.

1. Verifique a instalação confirmando se as regras estão presentes na pasta `.cursor/rules/`.

1. Ativar o servidor MCP:

   * Abra as Configurações de MCP do Cursor usando **Cmd+Shift+P** (macOS) ou **Ctrl+Shift+P** (Windows e Linux).
   * Tipo **Exibir: Abrir Configurações de MCP**
   * Localizar **Servidor MCP de extensibilidade de comércio** na lista
   * Ative o servidor **ON** para habilitar as ferramentas de codificação

1. Verifique o status do servidor - o servidor MCP de extensibilidade do Commerce deve aparecer como:

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. Use o prompt a seguir para ver se o agente usa o servidor MCP. Caso contrário, peça explicitamente ao agente para usar as ferramentas MCP disponíveis.

```terminal
What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
```

### Copilot

1. Reinicie o Visual Studio Code para carregar as novas ferramentas e configuração do MCP.

1. Verifique a instalação confirmando se o arquivo `copilot-instructions.md` existe na pasta `.github`.

1. Ativar o servidor MCP:

   * Abra o Painel Extensões clicando no ícone **Extensões** na Barra de Atividades na barra lateral esquerda ou usando **Cmd+Shift+X** (macOs) ou **Ctrl+Shift+X** (Windows e Linux).
   * Clique em **SERVIDORES MCP - INSTALADOS**.
   * Clique no ícone de engrenagem ao lado de **Commerce-extensibility MCP Server** e selecione **Iniciar Servidor**, se o servidor estiver parado.
   * Clique no ícone de engrenagem novamente e selecione **Mostrar saída**.

1. Verifique o status do servidor. A saída `MCP:commerce-extensibility` deve corresponder ao seguinte:

   ```terminal
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. Use o prompt a seguir para ver se o agente usa o servidor MCP. Caso contrário, peça explicitamente ao agente para usar as ferramentas MCP disponíveis.

   ```terminal
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## Exemplo de prompt

O prompt de amostra a seguir cria uma extensão para enviar notificações quando um pedido é feito.

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## Comandos do Prompt

Além do prompt, você pode usar o comando `/search-commerce-docs` para pesquisar a documentação em conversas com seu agente. Por exemplo:

```text
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Práticas recomendadas

A Adobe recomenda seguir as seguintes práticas recomendadas ao usar as ferramentas de codificação de IA:

### Lista de verificação

Antes de iniciar qualquer sessão de desenvolvimento:

* Verificar `REQUIREMENTS.md`
* Verificar se as ferramentas de MCP estão funcionando
* Revisar a fase e as metas atuais
* Comece com código de amostra ou projetos com andaime

Durante o desenvolvimento:

* Confiar no [protocolo](#protocol) de quatro fases
* Solicitar planos de implementação para desenvolvimento complexo
* Usar ferramentas MCP quando disponíveis
* Testar cada recurso após a implementação
* Teste localmente primeiro, depois implante e teste novamente
* Aproveitar as ferramentas de codificação para testar o suporte
* Questionar a complexidade desnecessária
* Implante de forma incremental para um desenvolvimento mais rápido

Ao iniciar o novo chat:

* Fornecer entrega de sessão adequada
* Arquivos de chave de referência com `@`
* Definir objetivos claros para a sessão
* Usar limites com base em fase

### Fluxo de trabalho (WRK)

Ao desenvolver com as ferramentas de codificação de IA, comece com códigos de amostra ou projetos com andaimes. Essa abordagem garante que você esteja construindo uma base sólida em vez de começar do nada, enquanto também otimiza o fluxo de trabalho de desenvolvimento de IA.

Isso também permite que você aproveite os modelos do Adobe e crie com base em padrões e arquiteturas comprovados, mantendo estruturas e convenções de diretório estabelecidas.

Consulte os seguintes recursos para começar:

* [Kit de início de integração](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [modelos do kit inicial do Adobe Commerce](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [modelos iniciais do Adobe I/O Events](https://experienceleague.adobe.com/pt-br/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [aplicativos de exemplo do App Builder](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Por que você deve usar esses recursos

* **Padrões comprovados**: os kits iniciais incorporam as práticas recomendadas e as decisões de arquitetura da Adobe
* **Desenvolvimento mais rápido**: reduz o tempo gasto na preparação e configuração
* **Consistência**: garante que sua extensão siga as convenções estabelecidas
* **Capacidade de manutenção**: mais fácil de manter e atualizar ao seguir padrões padrão
* **Documentação**: os kits iniciais vêm com exemplos e documentação
* **Suporte da comunidade**: é mais fácil obter ajuda ao usar as abordagens padrão
* **Eficiência do contexto de IA**: use padrões e estruturas familiares para trabalhar, reduzindo a necessidade de explicações extensas e melhorando a precisão da geração de código
* **Uso reduzido do token**: faça referência a padrões existentes em vez de gerar tudo do zero, resultando em conversas mais eficientes e menos resumos de contexto

### Protocolo

O protocolo de quatro fases a seguir é aplicado automaticamente pelo sistema de regras. As ferramentas devem seguir esse protocolo automaticamente ao desenvolver extensões:

* Fase 1: Análise e esclarecimento dos requisitos
   * Quando você for solicitado a esclarecer perguntas, forneça respostas completas.
* Fase 2: Planejamento de arquitetura e aprovação do usuário
   * Quando um plano for apresentado, revise-o cuidadosamente antes de aprová-lo.
* Fase 3: Geração e implementação de código
* Fase 4: Documentação e validação

### Solicitar planos de implementação para desenvolvimento complexo

Para um desenvolvimento complexo envolvendo várias ações de tempo de execução, pontos de contato ou integrações, solicite explicitamente que as ferramentas de IA criem um plano de implementação detalhado. Quando você vir um plano de alto nível na [Fase 2](#protocol) que envolve vários componentes, peça um plano de implementação detalhado para separá-lo em tarefas gerenciáveis:

```terminal
Create a detailed implementation plan for this complex development.
```

Extensões complexas do Adobe Commerce geralmente envolvem:

* Várias ações em tempo de execução
* Configuração de evento em vários pontos de contato
* Integração com sistemas externos
* Requisitos de gerenciamento de estado
* Teste em vários componentes

### Usar ferramentas MCP

>[!NOTE]
>
>Antes de usar as ferramentas do MCP, verifique se você está [conectado à Adobe I/O CLI](#log-in-to-the-adobe-io-cli).

O padrão de ferramenta são as ferramentas MCP, mas, em determinadas circunstâncias, é possível usar comandos CLI. Se quiser garantir o uso da ferramenta MCP, solicite-os explicitamente no prompt.

Se você vir comandos CLI sendo usados e quiser usar ferramentas MCP, use o seguinte prompt:

```terminal
Use only MCP tools and not CLI commands
```

* Ferramentas do MCP: aio-app-deploy, aio-app-dev, aio-dev-invoke
* Comandos da CLI: implantação de aplicativo aio, desenvolvimento de aplicativo aio

Os comandos da CLI podem ser usados para os seguintes cenários:

* Cenários complexos de implantação
* Depuração de problemas específicos
* Quando as ferramentas MCP têm limitações
* Operações pontuais que não se beneficiam da integração do MCP

### Desenvolvimento

É importante questionar a complexidade desnecessária criada pelas ferramentas de IA.

Quando arquivos desnecessários forem adicionados (`validator.js`, `transformer.js`, `sender.js`) para pontos de extremidade somente leitura simples, use os seguintes prompts:

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### Testes

Use as seguintes práticas recomendadas ao testar:

#### Testar cada recurso após a implementação

Após concluir o desenvolvimento de um recurso no seu plano de implementação, teste-o imediatamente. Os testes antecipados evitam problemas compostos e facilitam a depuração.

* Não espere até que todos os recursos estejam concluídos
* Teste incremental para capturar problemas antecipadamente
* Validar a funcionalidade antes de passar para o próximo recurso

#### Testar localmente primeiro

Sempre testar localmente primeiro usando a ferramenta `aio-app-dev`. Isso fornece feedback imediato e permite ciclos de iteração mais rápidos, depuração mais fácil e nenhuma sobrecarga de implantação.

1. Iniciar servidor de desenvolvimento local:

   ```bash
   aio-app-dev
   ```

1. Testar ações localmente:

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### Implante e teste novamente

Depois que o teste local for bem-sucedido, implante e teste no ambiente de tempo de execução. Os ambientes de tempo de execução podem ter um comportamento diferente do desenvolvimento local.

1. Implantar para tempo de execução:

   ```bash
   aio-app-deploy
   ```

1. Testar ações implantadas

1. Usar navegador da Web ou solicitações HTTP diretas

1. Verificar logs de ativação para depuração

#### Aproveitar as ferramentas de codificação para testar o suporte

Solicitar ajuda com testes. As ferramentas podem ajudar na depuração, análise de log e criação de dados de teste apropriados para suas ações específicas de tempo de execução.

**Testar ações de tempo de execução**:

```terminal
Help me test the customer-created runtime action running locally
```

**Falhas de depuração**:

```terminal
Why did the subscription-updated runtime action activation fail?
```

**Verificar logs**:

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Criar cargas de teste**:

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**Localizar pontos de extremidade de tempo de execução**:

```terminal
What's the URL for this deployed action?
```

**Manipular autenticação**:

```terminal
How do I authenticate with this external API?
```

**Solução de problemas**:

```terminal
Help me debug why this action is returning 500 errors
```

### Depuração

Pare e avalie quando as coisas dão errado. Se você encontrar problemas:

* Parar e avaliar - Não continuar em um estado interrompido
* Verificar logs - Use logs de ativação para identificar problemas
* Simplifique — elimine a complexidade para isolar problemas
* Teste incremental - Corrija um problema de cada vez
* Validar - Teste cada correção antes de continuar

### Implantação

Use as seguintes práticas recomendadas ao implantar:

#### Implantar de forma incremental

Implante somente ações modificadas para acelerar o desenvolvimento. Isso reduzirá o risco de romper a funcionalidade existente e fornecerá feedback mais rápido sobre as alterações. Também reduz o risco de romper a funcionalidade existente.

* Usar ferramentas MCP para implantar ações específicas

  ```bash
  aio-app-deploy --actions action-name
  ```

* Implantar ações individuais após o teste localmente
* Implante de forma incremental e evite implantações completas de aplicativos durante o desenvolvimento

#### Limpeza em tempo de execução

Após grandes alterações, aproveite as ferramentas para limpar ações órfãs. Deixe a ferramenta de IA lidar com o processo de limpeza sistematicamente, ela pode identificar com eficiência ações órfãs, verificar seu status e removê-las com segurança sem intervenção manual.

```terminal
Help me identify and clean up orphaned runtime actions
```

Solicite a ferramenta de IA para listar as ações implantadas e identificar as não usadas

```terminal
List all deployed actions and identify which ones are no longer needed
```

Faça com que as ferramentas de IA removam ações órfãs usando comandos apropriados

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### Monitoramento

Use as seguintes práticas recomendadas ao monitorar seu aplicativo:

#### Fique atento aos indicadores de qualidade do contexto

* **Contexto adequado**: a IA lembra decisões recentes, faz referência a arquivos corretos
* **Contexto insatisfatório**: a IA solicita informações fornecidas anteriormente, repete problemas resolvidos

#### Rastrear a velocidade de desenvolvimento

* **Alta velocidade**: progresso claro, esclarecimentos mínimos necessários
* **Baixa velocidade**: explicações repetidas, confusão de IA, progresso lento

#### Monitorar a eficiência de custos

Rastrear padrões de uso de token:

* **Eficiente**: baixo uso de token, poucos resumos de contexto
* **Ineficiente**: alto uso de token, vários resumos, trabalho repetido

## O que evitar

Você deve evitar os seguintes padrões de proteção ao usar as ferramentas de codificação de IA:

* **Não ignore a fase de esclarecimento**. Sempre verifique se a Fase 1 foi concluída antes da implementação.
* **Não ignore os testes após cada recurso** - Teste de forma incremental, não espere até que tudo esteja concluído.
* **Não adicione complexidade sem análise da causa raiz** - Questione adições desnecessárias de arquivos e solicite uma investigação adequada.
* **Não declarar sucesso sem teste de dados reais** - Sempre testar com dados reais, não apenas casos de borda.
* **Não se esqueça da limpeza do tempo de execução** - Sempre limpe as ações órfãs após grandes alterações.
