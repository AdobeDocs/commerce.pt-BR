---
title: Configurar a loja
description: Saiba como executar a ferramenta de andaime para configurar sua vitrine  [!DNL Adobe Commerce as a Cloud Service] .
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
source-git-commit: 7f7a674b856090bd02752a9e2ad29475b2b56fcf
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Configurar a loja

{{accs-early-access}}

As etapas a seguir demonstram como configurar rapidamente sua Adobe Commerce Storefront habilitada pela Edge Delivery usando o comando `aio commerce init`. Esse processo configura o seguinte:

* [Commerce Storefront baseado na Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) - Uma vitrine eficiente, escalável e segura que é baseada na Edge Delivery Services da Adobe.
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

A execução do comando a seguir criará um scaffolding para a loja do Commerce. Este andaime fornece um excelente ponto de partida para construir e entender sua loja. Para obter mais informações sobre como trabalhar com a loja, consulte a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).


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

   >[!NOTE]
   >
   >Se você selecionar a opção `Pick an available API (Mesh -> SaaS)`, deverá ter um Projeto e uma Workspace existentes na Adobe Developer Console. [Criar um projeto de modelo](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) e selecionar o App Builder criará automaticamente os espaços de trabalho necessários.

1. Quando o processo for concluído, você poderá personalizar a vitrine eletrônica usando os seguintes métodos:

   * Personalize seu código: `https://github.com/<username or org>/<repo name>`
   * Editar seu conteúdo: `https://da.live/#/<username or org>/<repo name>`
   * Gerenciar sua configuração: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Visualizar sua loja: `https://main--<repo name>--<username or org>.aem.page/`
   * Executar localmente: `aio commerce:dev`

Para personalizar sua loja, consulte a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).
