---
title: Configurar a loja
description: Saiba como configurar sua  [!DNL Adobe Commerce Optimizer] loja.
role: Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Configurar a loja

Este tutorial demonstra como configurar e usar a [Loja do Adobe Commerce habilitada pelo Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) para criar uma vitrine do Commerce eficiente, escalável e segura habilitada por dados da sua instância [!DNL Adobe Commerce Optimizer].


## Pré-requisitos

- Verifique se você tem uma conta GitHub (github.com) que pode criar repositórios e está configurada para desenvolvimento local.

- Saiba mais sobre os conceitos e o fluxo de trabalho para desenvolver vitrines do Commerce nos Serviços de entrega do Adobe Edge revisando a [Visão geral](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) na documentação da Adobe Commerce Storefront.
- Configurar o ambiente de desenvolvimento


### Configurar o ambiente de desenvolvimento

Instale o Node.js e a extensão do navegador Sidekick necessária para desenvolver e testar sua vitrine do [!DNL Adobe Commerce Optimizer] no Edge Delivery Services.

#### Instalar Node.js

Instale o Gerenciador de versão do nó (NVM) e a versão necessária do Node.js (22.13.1 LTS).

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

1. Verifique a instalação.

   ```bash
   npm -v
   ```

>[!TIP]
>
>Recursos adicionais para estender e personalizar a solução do [!DNL Adobe Commerce Optimizer] estão disponíveis por meio do [App Builder para Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) e da [API Mesh para Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Para obter informações de acesso e uso, entre em contato com o representante de conta da Adobe.

#### Instalar o Sidekick

Instale a extensão do navegador Sidekick para editar, visualizar e publicar conteúdo na loja. Consulte [instruções de instalação do Sidekick](https://www.aem.live/docs/sidekick#installation).

## Criar sua loja

A vitrine criada para o projeto [!DNL Adobe Commerce Optimizer] usa uma versão personalizada do modelo da Adobe Commerce na Edge Delivery Services Storefront. O modelo é um conjunto de arquivos e pastas que fornecem um ponto de partida para o desenvolvimento da loja. Este processo de instalação é diferente do processo padrão para uma [Adobe Commerce na Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>Este tutorial usa macOS, Chrome e Visual Studio Code como ambiente de desenvolvimento. As capturas de tela e as instruções refletem essa configuração. Você pode usar um sistema operacional, navegador e editor de código diferentes, mas a interface do usuário exibida e as etapas executadas variam de acordo.

### Visão geral do fluxo de trabalho

Siga estas etapas para configurar uma vitrine para usar com o [!DNL Adobe Commerce Optimizer].

1. **[Criar um repositório de código](#step-1-create-site-code-repository)**-Crie um repositório GitHub a partir do modelo padrão do Adobe Commerce + Edge Delivery Services. Incluir todas as ramificações do repositório de origem.
1. **[Atualizar modelo padrão da loja](#step-2-update-the-storefront-boilerplate)**-Atualizar o modelo padrão personalizado na ramificação `aco` para conectar a pasta de conteúdo à loja.
1. **[Implantar alterações](#step-3-deploy-changes)**-Substituir o código na ramificação `main` pelo código atualizado da ramificação `aco`.
1. **[Adicionar o aplicativo CodeSync](#step-5-add-the-aem-code-sync-app)**-Conecte seu repositório ao Serviço Edge Delivery. Não conecte o aplicativo Sincronização de Código até concluir a personalização do código-fonte e ter enviado o código para a ramificação `main`.
1. **[Adicionar conteúdo](#step-6-add-content)**-Use a ferramenta de clonagem de conteúdo de demonstração para criar e inicializar o conteúdo da loja no ambiente de Autor de Documentos hospedado em `https://da.live`.
1. **[Visualizar site de demonstração](#step-7-preview-demo-site)**-Conecte-se ao site da loja para exibir o conteúdo de exemplo e os dados da instância de demonstração [!DNL Adobe Commerce Optimizer].
1. **[Desenvolver em seu ambiente local](#step-8-develop-in-your-local-environment)**-Instale as dependências necessárias. Inicie o servidor de desenvolvimento local e atualize a configuração da loja para se conectar à instância [!DNL Adobe Commerce Optimizer] que o Adobe provisionou para você.
1. **[Próximas etapas](#next-steps)** - Saiba mais sobre como gerenciar e exibir conteúdo e dados na loja.


### Etapa 1: criar repositório de código do site

Crie um repositório GitHub para o código do modelo do site da sua vitrine eletrônica usando o modelo do Edge Delivery Services + Adobe Commerce Boilerplate.

1. Faça logon em sua conta GitHub.

1. Navegue até o [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) repositório do GitHub.

1. Selecione **Usar este modelo** e **Criar um novo repositório** no menu suspenso.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   A página de configuração do repositório é exibida.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Preencha o formulário de configuração com os seguintes detalhes:

   - **Modelo de repositório**—`hlxsites/aem-boilerplate-commerce` (padrão).
   - **Incluir todas as ramificações** — Selecione a opção para incluir todas as ramificações.
   - **Proprietário** — Sua organização ou conta (obrigatório).
   - **Nome do repositório** — Um nome exclusivo para o novo repositório (obrigatório).
   - **Descrição** — Uma breve descrição do repositório (opcional).
   - **Público ou Privado**—A Adobe recomenda público (padrão).

1. Selecione **Criar repositório**.

   Após alguns minutos, o novo repositório será aberto.

   Ignore qualquer notificação de solicitação de pull exibida na interface do usuário do GitHub.

### Etapa 2: atualizar a placa estrutural da vitrine

Você precisa das seguintes informações para atualizar o código de modelo padrão da loja:

- **URL do repositório do GitHub da Etapa 2**— `github.com/{ORG}/{SITE}`
   - `{ORG}` é o nome da organização ou o nome de usuário do repositório
   - `{SITE}` é o seu nome de repositório
- **URL da pasta de conteúdo da Etapa 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}` é a identificação da pasta que você criou com os dados de conteúdo de exemplo.

#### Vincular o repositório ao ambiente de Autor de documentos

1. Clonar o repositório no computador local.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Se você encontrar erros ao clonar o repositório, consulte [Solucionar erros de clonagem](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) na documentação do GitHub.

1. Abra o repositório no terminal ou IDE.

1. Confira a ramificação `aco`

   ```bash
   git checkout aco
   ```

1. Crie seu arquivo de configuração copiando o arquivo `default-fstab.yaml` para `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Atualize o ponto de montagem no arquivo de configuração da loja para apontar para o URL do conteúdo.

   1. Abra o arquivo de configuração [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. Substitua as cadeias de caracteres `{ORG}` e `{SITE}` pelos valores do repositório GitHub criado para seu código padronizado.

      Por exemplo, o código atualizado deve ter esta aparência.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. Salve o arquivo.

#### Configurar a extensão do Sidekick

1. Adicione a configuração do projeto para a extensão do Sidekick. Essa configuração garante que o Sidekick esteja disponível para gerenciar o conteúdo do projeto da loja.

>[!NOTE]
>
>Verifique se você instalou a [extensão do Sidekick](https://www.aem.live/docs/sidekick#installation) em seu navegador.

1. Abra o arquivo `tools/sidekick/config.json`.

   +++Arquivo de configuração do Sidekick

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   Consulte a [documentação da Biblioteca da Sidekick](https://www.aem.live/docs/sidekick-library) para obter mais informações.

   +++

1. Atualize os valores da chave `url` com os valores do seu repositório GitHub.

   - Substitua a cadeia de caracteres `{ORG}` pela organização ou pelo nome de usuário de seu repositório.

   - Substituir a cadeia de caracteres `{SITE}` pelo nome do repositório

   +++Exemplo de arquivo de configuração atualizado

   Se o nome do repositório GitHub for `aco-storefront` e sua organização for `early-adopter`, a URL atualizada deverá ser semelhante a:

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
