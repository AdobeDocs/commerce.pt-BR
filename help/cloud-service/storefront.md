---
title: Configurar a loja
description: Saiba como executar a ferramenta de andaime para configurar sua vitrine  [!DNL Adobe Commerce as a Cloud Service] .
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: c10d3b6a88fefb8680a039347960bfc7cfa13153
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Configurar a loja

As etapas a seguir demonstram como configurar rapidamente sua Adobe Commerce Storefront habilitada pela Edge Delivery usando o comando `aio commerce init`. Esse processo configura o seguinte:

* [Commerce Storefront baseado na Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=pt-BR) - Uma vitrine eficiente, escalável e segura que é baseada na Edge Delivery Services da Adobe.
* [Malha de API para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/) - uma plataforma de API que permite aos desenvolvedores combinar várias fontes de dados em um único ponto de extremidade do GraphQL. A API Mesh orquestra API de terceiros com a API do Adobe por meio de um único gateway. Uma consulta para o único endpoint do GraphQL pode retornar resultados de várias fontes.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - Uma coleção de ferramentas de desenvolvedor com acesso a APIs, eventos, funções de tempo de execução e plug-ins, que você pode usar para criar projetos para aplicativos do Adobe.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - Um mecanismo sem servidor para implantar código personalizado que responde a eventos e executa funções na nuvem.

## Pré-requisitos

Antes de executar o comando `aio commerce init`, você deve concluir os seguintes pré-requisitos:

1. Instale o Gerenciador de versão do nó (NVM).

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Instale o Node.js e o NPM. Para obter mais informações, consulte [Node.js](https://nodejs.org/en/).

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. Instale a [CLI do Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Instale o plug-in Adobe I/O API Mesh.

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Instale o plug-in do Adobe I/O Commerce.

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Atualize todos os plug-ins existentes.

   ```bash
   aio plugins:update
   ```

1. Faça logon em sua conta da Adobe Experience Cloud.

   ```bash
   aio login
   ```

   Se o comando `aio login` não iniciar uma janela de navegador, consulte a seção [Solução de problemas](#troubleshooting).

1. Selecione a Organização IMS, o projeto e o espaço de trabalho. Use as teclas de seta e pressione **Enter** para fazer a seleção. Para obter mais informações sobre os comandos `aio`, consulte a [documentação da CLI do Adobe I/O](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands).

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. Caso ainda não o tenha feito, aceite os Termos de Uso do Desenvolvedor no console do Adobe Developer navegando até https://developer.adobe.com/console/home e clicando em **Aceitar e continuar**.

## Executar o comando `aio commerce init`

A execução do comando a seguir criará um scaffolding para a loja do Commerce. Este andaime fornece um excelente ponto de partida para construir e entender sua loja. Para obter mais informações sobre como trabalhar com a loja, consulte a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR).


1. Execute o comando `init`:

   ```bash
   aio commerce init
   ```

1. Se você já estiver conectado ao GitHub, digite `Y` para criar o repositório com seu nome de usuário.

1. Insira o nome do repositório que deseja criar.

1. Selecione uma das seguintes opções:

   * **Usar o locatário de demonstração do Adobe Commerce** - Usar um locatário de demonstração.
      * Se você selecionar essa opção, será solicitado a instalar o bot AEM Code Sync em uma janela do navegador. Você deve especificar o repositório criado e autorizar o bot. Retorne à CLI e digite `y` para confirmar a instalação do bot AEM Code Sync.
   * **Escolher um locatário do Adobe Commerce disponível** - Selecione um locatário do Commerce existente na organização selecionada.
      * Se você selecionar essa opção, deverá selecionar o projeto e o espaço de trabalho para criar uma malha no.
   * **Forneça sua própria URL da API de locatário do Adobe Commerce** - Selecione esta opção se você for um participante do Programa de Acesso para Avaliação. Insira o URL da API fornecido em seu email de integração do Adobe.

   >[!NOTE]
   >
   >Se você selecionar a opção `Pick an available API (Mesh -> SaaS)`, deverá ter um Projeto e uma Workspace existentes na Adobe Developer Console. [Criar um projeto de modelo](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) e selecionar o App Builder criará automaticamente os espaços de trabalho necessários.

1. Quando o processo for concluído, você poderá personalizar a vitrine eletrônica usando os seguintes métodos:

   * Personalize seu código: `https://github.com/<username or org>/<repo name>`
   * Editar seu conteúdo: `https://da.live/#/<username or org>/<repo name>`
   * Gerenciar sua configuração: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Visualizar sua loja: `https://main--<repo name>--<username or org>.aem.page/`
   * Executar localmente: `aio commerce:dev`

Para personalizar sua loja, consulte a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR).

## Solução de problemas

Se você tiver problemas com o comando `aio login`, a Adobe recomenda sair totalmente da CLI e do navegador e, em seguida, fazer logon novamente.

1. Para fazer logout da CLI, execute:

   ```bash
   aio logout
   ```

1. No navegador, navegue até o [Adobe Developer Console](https://developer.adobe.com/console), clique no ícone do perfil no canto superior direito e selecione **Sair**.

1. Retorne à CLI e execute o comando `aio login` novamente, o que deve iniciar uma janela do navegador para fazer logon. Em seguida, selecione a organização, o projeto e o espaço de trabalho.

   ```bash
   aio console org select
   ```

   ```bash
   aio console workspace select
   ```

   ```bash
   aio console project select
   ```
