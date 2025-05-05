---
title: Configurar a loja
description: Saiba como configurar sua  [!DNL Adobe Commerce Optimizer] loja.
role: Developer
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# Configurar a loja

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

Este tutorial demonstra como configurar e usar a [Loja do Adobe Commerce habilitada pelo Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) para criar uma vitrine do Commerce eficiente, escalável e segura habilitada por dados da sua instância [!DNL Adobe Commerce Optimizer].


## Pré-requisitos

* Verifique se você tem uma conta GitHub (github.com) que pode criar repositórios e está configurada para desenvolvimento local.

* Familiarize-se com o fluxo de trabalho básico e o vocabulário relacionado à criação de uma vitrine para os serviços de entrega do Adobe Edge revisando a [Visão geral](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) na documentação da Adobe Commerce Storefront.
* Configurar o ambiente de desenvolvimento


### Configurar o ambiente de desenvolvimento

Para configurar seu ambiente de desenvolvimento, instale a versão necessária do Node.js e a extensão do navegador Sidekick.

#### Instalar Node.js

Para desenvolver e testar a loja do [!DNL Adobe Commerce Optimizer] no projeto do Edge Delivery Services localmente, você precisa da versão 22.13.1 LTS do Node.js.

Se necessário, conclua as seguintes etapas para instalar o Gerenciador de versão do nó (NVM) e a versão necessária do Node.js.

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
>Esta configuração é para desenvolvimento com [!DNL Adobe Commerce Optimizer] e a Adobe Commerce Edge Delivery Service Store. Recursos adicionais para estender e personalizar a solução do [!DNL Adobe Commerce Optimizer] estão disponíveis por meio do [App Builder para Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) e da [API Mesh para Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Para obter informações de acesso e uso, entre em contato com o representante de conta da Adobe.

#### Instalar o Sidekick

Instale a extensão do navegador Sidekick para editar, visualizar e publicar conteúdo da loja. Consulte [instruções de instalação do Sidekick](https://www.aem.live/docs/sidekick#installation).


## Criar sua loja

A vitrine criada para o projeto [!DNL Adobe Commerce Optimizer] é criada usando uma versão personalizada da matriz da Adobe Commerce na Edge Delivery Services Storefront. O modelo é um conjunto de arquivos e pastas que fornecem um ponto de partida para a criação de sua vitrine eletrônica.

Este processo de configuração da vitrine eletrônica foi personalizado especificamente para [!DNL Adobe Commerce Optimizer] projetos. O fluxo é diferente do fluxo para o Adobe Systems padrão [Comércio na configuração da Storefront dos serviços de](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) entrega do Edge.

>[!NOTE]
>
>Essa tutorial usa os Code de macOS, Cromo e Visual Studio como ambiente de desenvolvimento. As capturas e as instruções da tela refletem essa configuração. Você pode usar um sistema operacional, navegador e editor de código diferentes, mas as interface que você vê e as etapas que você deve tomar variam de acordo.

### Visão geral do fluxo de trabalho

Siga estas etapas para configurar uma vitrine para usar com o Adobe Systems Comércio Optimizer.

1. **[Criar uma pasta](#step-1-create-a-content-folder)** conteúdo Criar uma pasta de conteúdo compartilhada no Google Drive ou Sharepoint. Esta pasta contém o conteúdo de amostra e o ativos para sua vitrine.

1. **[Criar um código repositório-Criar](#step-1-create-a-code-repository)** uma repositório gitHub da Adobe Systems Comércio + modelo de padrão Edge Delivery Services. Inclua todas as ramificações do repositório de origem.
1. **[Atualize o estereoplicativo](#step-2-update-the-storefront-boilerplate)** de storefront - Atualize a modelo de estereoplicativo personalizado na `aco` ramificação do repostiory para conectar sua pasta conteúdo à vitrine e reveja a configuração da vitrine que fornece dados da demonstração Comércio otimizador Adobe Systems instância à vitrine.
1. **[Carregue o código](#step-3-upload-the-updated-boilerplate-code)** de estereoplicado de vitrine atualizado- Substitua o `main` código no ramificação com o código atualizado do `aco` ramificação.
1. **[Adicione o aplicativo](#step-4-add-the-aem-code-sync-app)** CodeSync connect your repositório to the Edge Delivery Service. Não conecte o aplicativo Code Sync até que você tenha concluído a personalização do código-fonte e esteja pronto para enviar o código para o `main` ramificação.
1. **[Pré-visualizar e publicar seu conteúdo](#step-5-preview-and-publish-your-content)**-Use a extensão do Sidekick para pré-visualizar e publicar o conteúdo do site da pasta de conteúdo na loja.
1. **[Visualize seu site e exiba dados de exemplo](#step-6-preview-your-site-and-view-sample-data)** - Conecte-se ao site da loja para exibir o conteúdo de exemplo e os dados da instância de demonstração [!DNL Adobe Commerce Optimizer].
1. **[Desenvolva a loja em seu ambiente local](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)**-Instale as dependências necessárias. Início o servidor de desenvolvimento local e atualize a configuração da vitrine para se conectar aos [!DNL Adobe Commerce Optimizer] instância que Adobe Systems provisionadas para você.
1. **[Gerencie conteúdo](#step-8-manage-site-content)** do site: saiba mais sobre como atualizar e gerenciar conteúdo de site.

### Etapa 1: Criar uma pasta de conteúdo

Siga as instruções na documentação da Adobe Commerce Storefront para adicionar uma pasta de conteúdo compartilhado no Google Drive ou Sharepoint e adicionar o conteúdo de amostra. A amostra de conteúdo inclui imagens, texto e outros ativos que compõem o site.

* [Criar e compartilhar uma Google Drive ou uma pasta do Sharepoint](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
* [Carregue o conteúdo de exemplo](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) na sua pasta.

### Etapa 2: criar um repositório de código

Crie um repositório de código no GitHub usando o modelo padronizado do Edge Delivery Services + Adobe Commerce. Este modelo fornece o código de teste da sua vitrine eletrônica.

1. Faça logon em sua conta GitHub.

1. Navegue até o [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) repositório do GitHub.

1. Selecione **Usar este modelo** e **Criar um novo repositório** no menu suspenso.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Isso abre a página de configuração do repositório.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Preencha o formulário de configuração com os seguintes detalhes:

   * **Modelo de repositório**—`hlxsites/aem-boilerplate-commerce` (padrão).
   * **Incluir todas as ramificações** — Selecione a opção para incluir todas as ramificações.
   * **Proprietário** — Sua organização ou conta (obrigatório).
   * **Nome do repositório** — Um nome exclusivo para o novo repositório (obrigatório).
   * **Descrição** — Uma breve descrição do repositório (opcional).
   * **Público ou Privado**—A Adobe recomenda público (padrão).

1. Selecione **Criar repositório**.

   Após um ou dois minutos, o novo repositório será aberto.

   Ignore quaisquer notificações de pull requests exibidas no novo repositório.

### Etapa 3: atualizar a placa estrutural da vitrine

Nesta seção, você concluirá as seguintes tarefas:

* Confira a ramificação `aco` do seu repositório para atualizar o modelo padrão personalizado para projetos [!DNL Adobe Commerce Optimizer]
* Conecte sua pasta de conteúdo à loja atualizando o arquivo `fstab.yaml` para apontar para sua pasta de conteúdo.
* Revise o arquivo de configuração da loja, `config.json`
* Configure a extensão do Sidekick para editar, pré-visualizar e publicar conteúdo da pasta de conteúdo compartilhado.

Você precisa das seguintes informações para concluir essas etapas:

* **URL do repositório do GitHub da Etapa 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` é o nome da organização ou o nome de usuário do repositório

   * `{SITE}` é o seu nome de repositório

* **URL da pasta de conteúdo da Etapa 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` é a identificação da pasta que você criou com os dados de conteúdo de exemplo.

#### Atualize o código padronizado para se conectar à pasta de conteúdo

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

1. Atualize o arquivo de configuração da loja para apontar para o URL de conteúdo.

   1. Abra o arquivo de configuração [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. Substitua `{YOUR_MOUNTPOINT_URL}` pela URL do seu sistema de gerenciamento de conteúdo.

      Por exemplo, se você estiver usando o Google Drive, o código atualizado deverá ter esta aparência.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
      ```

   1. Salve o arquivo.

#### Revisar a configuração da conexão de dados

A conexão de dados estabelece a comunicação entre o Adobe Commerce Optimizer e a loja, garantindo que os dados do catálogo fluam perfeitamente para a loja. Este processo preenche várias interfaces de loja, incluindo o componente de pesquisa, a lista de produtos e as páginas de detalhes do produto necessárias para [!DNL Adobe Commerce Optimizer].

Para a configuração inicial da loja, o Adobe fornece um arquivo de configuração padrão que se conecta a uma instância de demonstração do Adobe Commerce Optimizer com dados de amostra.

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
          "ac-price-book-id": "west_coast_inc",
          "ac-scope-locale": "en-US"
        }
      },
      "analytics": {
        "base-currency-code": "USD",
        "environment": "Production",
        "store-id": 1,
        "store-name": "ACO Demo",
        "store-url": "https://www.aemshop.net",
        "store-view-id": 1,
        "store-view-name": "Default Store View",
        "website-id": 1,
        "website-name": "Main Website"
      }
    }
  }
}
```

Revise o arquivo de configuração da loja em seu repositório para entender como a conexão de dados é estabelecida.

1. No repositório de código, navegue até o diretório raiz.

1. Abra o arquivo `config.json`.

   Neste arquivo, os seguintes valores principais especificam a Adobe Systems Comércio Optimizer instância para se conectar e determinar os dados que fluem para a vitrine:

   * `commerce-endpoint` define a Adobe Systems Comércio do Optimizer instância para se conectar.
   * `headers` determinam os dados que fluem para a vitrine.
      * `ac-channel-id` está definida como `west_coast_inc`
      * `ac-price-book-id` está definida como `west_coast_inc`
      * `ac-scope-locale` está definido como `en-US`
      * `ac-price-book-id` está definido como `west_coast_inc`

   Esses valores definem a ID do canal, o local e a ID do catálogo de preços para enviar dados de catálogo para um canal de vendas específico e filtrar esses dados com base nos valores do local e do catálogo de preços especificados. Posteriormente, você aprenderá a alterar a instância do Adobe Commerce Optimizer e a atualizar os cabeçalhos para definir quais dados são entregues à loja.

1. Depois de revisar o arquivo, feche-o e continue o tutorial.


#### Configurar a extensão do Sidekick

Adicione a configuração do projeto para a extensão do Sidekick. O Sidekick é usado para editar, visualizar e publicar o conteúdo da loja. Essa configuração garante que você possa usar o Sidekick para gerenciar conteúdo na pasta de conteúdo compartilhado e nas páginas do site publicadas nos ambientes de preparo e produção.

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

   * `{ORG}` é o nome do repositório ou nome de usuário para seu repositório de códigos

   * `{SITE}` é o nome do repositório

1. Salve o arquivo.

### Etapa 4: Fazer upload do código padronizado atualizado

Para usar o código de modelo personalizado da vitrine personalizada, substitua o código na ramificação `main` pelas atualizações.

1. A partir do editor ou do IDE, confirme e salve os arquivos atualizados.

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Enviar as alterações na ramificação `aco` e substituir a ramificação `main`:

   ```bash
   git push origin aco:main -f
   ```

### Etapa 5: adicionar o aplicativo Sincronização de código do AEM

Conecte seu repositório ao Edge Delivery Service adicionando o aplicativo GitHub da sincronização de código da AEM ao seu repositório.

>[!IMPORTANT]
>
>Não conecte o aplicativo Sincronização de código até ter carregado o código padronizado atualizado na ramificação principal do seu repositório GitHub.

1. Abra a página de configuração do [aplicativo de sincronização de código do AEM](https://github.com/apps/aem-code-sync).

1. Selecione **Configurar** e autentique com a **organização** ou a **conta** que contém o repositório criado.

1. No formulário, escolha **Selecionar apenas repositórios** e selecione o repositório que você criou.

1. Selecione **Instalar** para adicionar o aplicativo AEM Code Sync ao seu repositório.

   Você deve ver uma mensagem informando que o aplicativo foi instalado com êxito.

### Etapa 6: Pré-visualizar e publicar seu conteúdo

Para adicionar conteúdo à loja, é necessário visualizar e publicar o conteúdo usando a extensão do Sidekick.

1. Abra a pasta de conteúdo no Google Drive ou Sharepoint.

1. Ative o Sidekick clicando no ícone Sidekick na barra de ferramentas do navegador.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

1. Use a barra de ferramentas do Sidekick para visualizar e publicar seu conteúdo.

   ![[Selecionar arquivos para visualizar e publicar]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

1. Selecione os arquivos em cada pasta separadamente e use a barra de ferramentas do Sidekick para visualizar e publicar todos os arquivos.

   * **&#x200B;**&#x200B;Visualização- Faz upload conteúdo para o ambiente de preparo. Os URLs de armazenamento à beira da loja terminam com `.aem.page`.

   * **&#x200B;**&#x200B;Publish-Faz upload de conteúdo para o ambiente de produção. Os URLs de produção terminam com `aem.live`.

Para obter mais informações, consulte a documentação Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) .

### Etapa 7: Visualização seu site

Visualização site para verificar se as amostras conteúdo e os dados de demonstração da Adobe Systems Comércio Optimizer estão sendo exibidos corretamente.

* **O conteúdo de amostra** é exibido na pasta de conteúdo compartilhada. Ele inclui os página layouts, banners e outras conteúdo publicados usando o Sidekick.
* **Os dados** de amostra são exibidos a [!DNL Adobe Commerce Optimizer] partir do instância de demonstração. Os dados incluem dados do produto com atributos de produto, imagens, descrições de produtos e preços preenchidos com base nos valores especificados no arquivo `config.json`de configuração da vitrine.


#### Conecte-se ao seu site para visualização conteúdo e dados de amostra

1. Conecte-se ao seu site navegando até `https://main--{SITE}--{ORG}.aem.live`.

   Substitua `{ORG}` e `{SITE}` pela organização e pelo nome do seu repositório padrão.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Se a página retornar um 404, verifique se você publicou o conteúdo usando a extensão do Sidekick. Além disso, verifique se o arquivo `fstab.yaml` atualizado está usando a URL da pasta de conteúdo.

1. Visualize os dados de catálogo de amostra provenientes da instância de demonstração do Commerce Optimizer.

   1. Procure por `tires` para ver uma lista suspensa de produtos de pneu disponíveis.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   O componente de pesquisa faz parte do código de projeto da vitrine da loja. Os dados dos resultados da pesquisa são preenchidos com base na configuração da loja.

   1. Pressione **Enter** para exibir a página da lista de produtos.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. Exiba uma página de detalhes do produto selecionando qualquer produto de pneu na página.

      Se você explorar a loja, observe que alguns dos componentes não funcionam. Por exemplo, adicionar um produto ao carrinho de compras retorna um erro e os componentes de gerenciamento de conta não funcionam. Isso ocorre porque esses componentes não foram configurados para receber dados de um back-end do Commerce. Os dados da sua Adobe Systems Comércio Optimizer instância preenche apenas as páginas de componente pesquisa, lista do produto e detalhes do produto.

   1. Depois de explorar a vitrine, continue com o tutorial.


### Etapa 8: desenvolva a vitrine no seu ambiente local

Nesta seção, você experimenta a configuração da vitrine em seus ambiente de desenvolvimento local conectando a vitrine às [!DNL Adobe Commerce Optimizer] instância que Adobe Systems provisionadas para você.

Para fazer a conexão, você precisa do terminal GraphQL para os Serviços de comercialização fornecidos no seu email integrado.

```text
https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

#### desenvolvimento local Início

1. No IDE, faça checkout da ramificação principal do seu repositório de códigos do GitHub.

   ```bash
   git checkout main
   ```

1. Instale as dependências necessárias.

   ```bash
   npm install
   ```

1. Inicie o servidor de desenvolvimento local.

   ```bash
   npm start
   ```

   A primeira página da sua vitrine estereoplicada deve estar visível na sua navegador em `http://localhost:3000`.

![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Atualizar a configuração da vitrine

Atualize o arquivo de configuração da loja e visualize as alterações no ambiente de desenvolvimento local.


1. No IDE, atualize a configuração da vitrine eletrônica para se conectar à instância [!DNL Adobe Commerce Optimizer] que o Adobe provisionou para você.

   1. Abra o arquivo `config.json`.

   1. Atualize os seguintes valores usando o ponto de extremidade para sua instância [!DNL Adobe Commerce Optimizer]:

      * **`commerce-endpoint`**-Substitua o valor existente pela URL do ponto de extremidade.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** — Substitua o valor existente pela ID do locatário da URL do ponto de extremidade.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. Salve o arquivo.

      Se a visualização local estiver funcionando corretamente, as atualizações serão aplicadas à loja local.

1. Verifique o site para ver os resultados da alteração de configuração.

   1. No navegador, navegue até `http://localhost:3000` e atualize a página.

   1. No cabeçalho da loja, clique na lupa para procurar por `tires`.

      ![Procurar pneus](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

      Observe que a lista suspensa não é preenchida.

   1. Pressione **Enter** para exibir a página Lista de produtos.

      ![Resultados de pesquisa vazios com valores de cabeçalho inválidos](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      A pesquisa não retorna nenhum resultado porque os cabeçalhos no arquivo de configuração da loja usam valores de cabeçalhos com base na instância de demonstração. Agora que a configuração aponta para a instância [!DNL Adobe Commerce Optimizer] provisionada para você, esses valores são inválidos.

### Próximas etapas

Consulte o [caso de uso completo do Storefront e do Catalog Administrator](./use-case/admin-use-case.md) para saber como exibir conteúdo na sua loja atualizando a configuração da loja usando valores da sua instância [!DNL Adobe Commerce Optimizer].

>[!MORELIKETHIS]
>
>* Se você planeja usar [!DNL Adobe Commerce Optimizer] sem um back-end Adobe Systems Comércio, consulte a [documentação](https://experienceleague.adobe.com/developer/commerce/storefront/) de vitrine Adobe Experience Manager para saber mais sobre como atualizar conteúdo do site e integrar com seus Comércio componentes de frontend e dados de back-end.
></br></br>
>* Se você planeja usar [!DNL Adobe Commerce Optimizer] com um backend Comércio Adobe Systems, consulte a [documentação](https://experienceleague.adobe.com/developer/commerce/storefront/) Adobe Systems Comércio Storefront para saber como atualizar conteúdo e configurar componentes de vitrine para gerenciamento de conta, check-out e outros recursos.
