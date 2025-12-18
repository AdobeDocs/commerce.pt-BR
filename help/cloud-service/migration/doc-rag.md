---
title: Serviço de documentação RAG
description: Saiba como usar o serviço de pesquisa de documentação habilitado para IA para desenvolvimento em Adobe Commerce.
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Serviço de documentação RAG (Beta)

>[!NOTE]
>
>A documentação do serviço RAG está atualmente no Beta e a experiência está sujeita a alterações.

O serviço de documentação RAG (Retrieval-Augmented Generation) fornece recursos de pesquisa semântica alimentados por IA em toda a documentação relevante do Adobe Commerce e do App Builder.

Este RAG fornece uma interface IDE para fazer perguntas sobre o Adobe Commerce e pode aconselhá-lo sobre as práticas recomendadas para o desenvolvimento de aplicativos e outras tarefas de migração.

O serviço RAG faz parte do servidor MCP (Model Context Protocol) das [ferramentas de extensibilidade do Commerce](./coding-tools.md), que se integra ao Cursor e a outros assistentes de IA compatíveis com MCP.

## Documentação disponível

A tabela a seguir descreve qual documentação está atualmente indexada pelo serviço RAG e as palavras-chave que você pode usar para acionar a pesquisa no índice associado. A documentação incluída continuará a expandir à medida que desenvolvemos o serviço RAG.

| Categoria | Índice | Conteúdo incluído | Palavras-chave |
|-------|---------|---------|------------------------|
| [Vitrine](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR) | commerce-storefront-docs | Edge Delivery Services, drop-ins, componentes de vitrine | loja, drop-in, EDS, lista de produtos, check-out |
| [Extensibilidade](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhooks, eventos, extensões, integrações | webhook, evento, extensão, malha de API, GraphQL |
| [Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce/cloud-service/overview) | commerce-core-docs | Commerce principal (catálogo, clientes, pedidos) | catálogo, produto, cliente, ordem, estoque |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, ações em tempo de execução, extensões da interface do usuário | app builder, ação de tempo de execução, React Spectrum |

Para obter mais informações sobre a seleção de índice, consulte [Seleção automática de índice](#automatic-index-selection-recommended) e [Seleção explícita de índice](#explicit-index-selection).

Para obter informações detalhadas sobre a documentação incluída em cada índice, consulte a [lista de origens assimiladas](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md).

## Segurança e privacidade

* **Autenticação IMS** - Todas as chamadas de API usam tokens OAuth2 do Adobe IMS.
* **Nenhum armazenamento de dados** - O servidor MCP não armazena credenciais ou dados.
* **Execução local** - Todas as ferramentas são executadas localmente no computador.
* **Comunicação segura** - A pesquisa de documentação usa HTTPS com validação de token.

O ponto de extremidade de produção é protegido pela [Porta Frontal do Azure](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview), que inclui as seguintes proteções:

* Firewall de aplicativo web (WAF) com conjunto de regras padrão do Microsoft 2.1 e conjunto de regras do gerenciador de bot 1.0
* Bloqueio geográfico para regiões sob embargo dos EUA (Cuba, Irã, Coreia do Norte, Síria, Crimeia, Luhansk, Donetsk)
* Proteção de DDoS na borda
* Infraestrutura de gerenciamento de API bloqueada para aceitar apenas tráfego da porta frontal

Para diferentes requisitos de segurança, você pode usar um terminal personalizado. Consulte [Ponto de extremidade personalizado do Front Door](#custom-front-door-endpoint) para obter mais informações.

## Pré-requisitos

Antes de instalar, verifique se você tem:

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (LTS recomendado)
* [IDE de Cursor](https://cursor.com/download){target="_blank"} (recomendado) ou outro IDE compatível com MCP

  >[!NOTE]
  >
  >Embora outros IDEs compatíveis com MCP sejam suportados, o Cursor é o IDE recomendado para obter a melhor experiência. Se estiver usando outro IDE, você precisará modificar os prompts e outras etapas na documentação para trabalhar com o IDE selecionado.

## Instalação

1. Instale a [Adobe I/O CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) globalmente:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Autentique com o Adobe IMS:

   ```bash
   aio auth login
   ```

1. Clonar o repositório de ferramentas de extensibilidade do Commerce e navegar até o diretório:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Instalar dependências:

   ```bash
   npm install
   ```

1. Crie ou atualize `.cursor/mcp.json` no diretório do projeto do Commerce (não globalmente) para incluir o servidor MCP `commerce-extensibility-tools`:

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Substitua `<your-project-directory>` pelo caminho real onde você clonou o repositório.

   >[!NOTE]
   >
   >No Windows, se você tiver problemas ao fornecer o caminho para o diretório do projeto, consulte [Solução de problemas de caminho](#path-issues-windows).

1. Reinicie o Cursor IDE para carregar o servidor MCP.

1. Verifique a instalação solicitando ao assistente de IA:

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## Uso

Depois de instalado, você pode chamar os índices [automaticamente](#automatic-index-selection-recommended) ou [explicitamente](#explicit-index-selection). Você também pode usar o comando [`/search-commerce-docs` &#x200B;](#command-based-search).

>[!NOTE]
>
>O serviço RAG retorna os 5 principais resultados mais relevantes.

### Seleção automática de índice (recomendado)

Ao fazer perguntas em linguagem natural sobre o seu projeto do Commerce, a ferramenta pesquisará automaticamente no índice de documentação apropriado e fornecerá informações relevantes:

>[!BEGINSHADEBOX]

O prompt a seguir seleciona automaticamente o índice `commerce-storefront-docs`:

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

O prompt a seguir seleciona automaticamente o índice `commerce-extensibility-docs`:

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

O prompt a seguir seleciona automaticamente o índice `commerce-core-docs`:

```shell-session
"How to configure product catalog settings?"
```

O prompt a seguir seleciona automaticamente o índice `app-builder-docs`:

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### Seleção de índice explícita

Como alternativa, você pode especificar o índice que deseja usar no prompt.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### Pesquisa baseada em comandos

Se quiser garantir que o serviço RAG seja usado, chame manualmente o comando de Cursor `/search-commerce-docs` para pesquisar a documentação com seu prompt:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Ponto de extremidade personalizado da porta frontal

Por padrão, a pesquisa de documentação usa o ponto de extremidade de produção [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) com proteção de WAF. Para fins de teste ou desenvolvimento, é possível substituir isso pela variável de ambiente `FRONT_DOOR_URL`.

Para usar um endpoint personalizado, adicione-o à configuração de MCP do cursor:

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>A maioria dos desenvolvedores deve usar o ponto de extremidade de produção padrão e não precisa definir a variável `FRONT_DOOR_URL`.

## Solução de problemas

As seções a seguir fornecem dicas de solução de problemas comuns que você pode encontrar ao usar o serviço de documentação RAG.

### Erros de autenticação

A ferramenta de pesquisa de documentação exige autenticação do Adobe IMS. Se encontrar erros de autenticação, use as seguintes etapas para solucionar e resolver o problema.

1. Verifique se você está conectado:

   ```bash
   aio where
   ```

1. Verifique se você pode ver o token IMS:

   ```bash
   aio auth login --bare
   ```

1. Se os erros de autenticação persistirem, tente fazer logoff e logon novamente:

   ```bash
   aio auth logout
   aio auth login
   ```

### O servidor MCP não está carregando

Se o servidor MCP não estiver se conectando ou se o seu agente informar que não pode se conectar ao RAG, use as seguintes etapas para solucionar o problema.

1. Abra as Configurações do Cursor usando **Cmd,** (macOS) ou **Ctrl ,** (Windows e Linux).

1. Procure por &quot;MCP&quot; e verifique se `commerce-extensibility-tools` está listado e habilitado.

1. Verifique se há mensagens de erro no painel de configurações MCP.

1. Verifique se o arquivo `mcp.json` existe em seu projeto:

   ```bash
   cat .cursor/mcp.json
   ```

1. Verifique se o caminho está correto e absoluto:

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### Ferramenta não encontrada

1. Saia do cursor e reabra-o.

1. Verifique os logs do servidor MCP no console de desenvolvedor do Cursor usando **Cmd+Shift+P** (macOS) ou **Ctrl+Shift+P** (Windows/Linux) e procurando por &quot;Desenvolvedor: Pasta de Logs Abertos&quot;.

1. Verifique a instalação:

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   O servidor deve ser iniciado sem erros.

### Problemas de caminho (Windows)

No Windows, use barras `/` ou barras invertidas com escape `\\`:

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Recursos adicionais

* [documentação para desenvolvedores do Adobe Commerce](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [Documentação do App Builder](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Protocolo de Contexto de Modelo](https://modelcontextprotocol.io/){target="_blank"}
* [IDE de cursor](https://cursor.sh/docs){target="_blank"}
