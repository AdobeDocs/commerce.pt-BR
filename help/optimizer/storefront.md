---
title: Configurar a loja
description: Saiba como configurar sua  [!DNL Adobe Commerce Optimizer] loja.
role: Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: c00cb55bd7b61d6506ee8b9b81d28118c1adde00
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 0%

---

# Configurar a loja

Este guia orienta você na configuração de uma loja para sua instância do [!DNL Adobe Commerce Optimizer] usando os Serviços de entrega de borda da Adobe. Sua loja inclui código padronizado, conteúdo de amostra e suporte para páginas de detalhes do produto e descoberta de produtos (pesquisa e filtragem).

**Tempo estimado para conclusão:** 30-45 minutos

## Pré-requisitos

* **Conta do GitHub** que pode criar repositórios e está configurada para desenvolvimento local (github.com)
* **[!DNL Adobe Commerce Optimizer]instância** com dados de exemplo e exibições e políticas de catálogo configuradas
   * Consulte [Adicionar dados de amostra](get-started.md#add-sample-data) para obter instruções de configuração.

### Dados de instância necessários

Antes de começar, colete as seguintes informações da instância do [!DNL Adobe Commerce Optimizer]:

* **ID do Locatário** (também chamada de ID de instância)
   * Disponível na [página de detalhes da instância](get-started.md#manage-instances)
* **Ponto de extremidade do GraphQL** para sua instância
   * Disponível na [página de detalhes da instância](get-started.md#manage-instances)
* **ID de exibição de catálogo** para a exibição de catálogo global
   * Disponível na [página de detalhes do catálogo](./setup/catalog-view.md#manage-catalog-view)
* **localidade do Source** para exibição do catálogo
   * O padrão para dados de exemplo é `en_US`

>[!NOTE]
>
>Os clientes com acesso de avaliação podem encontrar o endpoint do GraphQL no email de boas-vindas recebido quando sua instância foi criada. As instâncias de avaliação vêm pré-configuradas com dados de amostra, visualizações de catálogo e políticas.

## Configurar etapas

1. **[Criar projeto de vitrine eletrônica](#create-your-storefront-project)**-Use a [ferramenta do Criador de Sites](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) para criar um novo projeto de vitrine eletrônica com código padronizado, conteúdo de amostra e um arquivo de configuração.

1. **[Personalizar a configuração da vitrine eletrônica](#customize-the-storefront-configuration)**-Atualize o arquivo `config.json` no repositório para se conectar à sua instância [!DNL Adobe Commerce Optimizer].

1. **[Verificar configuração](#verify-your-setup)** (10 minutos)
   * Visualizar o site da loja
   * Testar páginas de detalhes do produto e funcionalidade de pesquisa

## Criar projeto da loja

A ferramenta Criador de sites cria um projeto completo da loja com os seguintes componentes:

* **Site**: página de aterrissagem de vitrines com conteúdo padrão
* **Código**: repositório com arquivos de origem padronizados
* **Conteúdo**: ambiente de Autor de Documentos com arquivos de conteúdo do site
* **Configuração do Commerce**: arquivo `config.json` para configuração específica de instância

### Etapa 1: gerar o projeto

1. Abra a [ferramenta do Criador de Sites](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Selecione **Criar Novo Site (Código e Conteúdo)**.

1. Conclua a configuração do site:

   * **Organização/nome de usuário do GitHub**: digite seu nome de usuário ou nome de organização do GitHub
   * **Nome do Site**: escolha um nome descritivo para sua vitrine eletrônica
   * **Ponto de extremidade do Commerce GraphQL (opcional)**: insira o ponto de extremidade do GraphQL para sua instância [!DNL Adobe Commerce Optimizer]

1. Clique em **Criar Site** para criar o repositório GitHub com o código padrão da loja.

   Quando o repositório é criado, o Criador do site atualiza e solicita que você instale o aplicativo Sincronização de código.

### Etapa 2: instalar o aplicativo de sincronização de código

1. Clique em **[!UICONTROL Install AEM Code Sync App]** para abrir o instalador da Sincronização de Código em uma nova guia.

1. Configure o aplicativo Sincronização de código:
   * Selecione sua organização do GitHub e clique em **[!UICONTROL Configure]**.
   * Na interface de Sincronização de Código, clique em **[!UICONTROL Only select repositories]**.
   * Clique no menu **[!UICONTROL Select repositories]** e escolha o repositório de código da loja que você criou.
   * Clique em **[!UICONTROL Save]** para registrar seu repositório.

1. Retorne à janela do navegador onde o Criador de Sites está aberto e clique em **Criar Site**.

   O Criador de sites copia o conteúdo do modelo da loja para o ambiente do Autor do documento. Esse processo leva de 1 a 2 minutos.

### Etapa 3: salvar os links do projeto

1. Na seção Detalhes do site, analise os links do projeto da loja:

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Use esses links para gerenciar o código, o conteúdo e a configuração da loja.

1. Copie e salve estes links para referência futura: clique em **[!UICONTROL Copy].

## Configurar a loja

Atualize a configuração da loja para se conectar à instância do [!DNL Adobe Commerce Optimizer].

1. Abra o gerenciador de configurações usando o link salvo anteriormente:

   `https://da.live/sheet#/<username or org>/<repo name>/config.json`

1. Localize a seção `cs` (Serviço de Catálogo) na configuração.

1. Substitua os valores de espaço reservado pelos valores da sua instância. Consulte [Pré-requisitos](#prerequisites).

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Environment-ID": "{tenantId}",
      "AC-Source-Locale": "en_US"
   }
   ```

1. Salve o arquivo de configuração.

>[!NOTE]
>
>As alterações na configuração podem levar alguns minutos para se propagarem. Se você não vir os dados imediatamente, aguarde de 2 a 3 minutos antes de solucionar o problema.

## Verificar sua configuração

Teste sua loja para garantir que ela esteja conectada corretamente à sua instância do [!DNL Adobe Commerce Optimizer].

### Etapa 1: Exibir a página inicial da loja

1. Navegue até o URL de visualização ao vivo:

   `https://main--{SITE}--{ORG}.aem.live`

   Substitua `{ORG}` e `{SITE}` pela sua organização do GitHub e pelo nome do site.

1. **Critério de sucesso**: você deve ver a página inicial da loja com conteúdo padronizado.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### Etapa 2: testar páginas de detalhes do produto

Consulte a página de detalhes do produto padrão para verificar se os dados do produto estão carregando corretamente.

1. Acesse uma página de produto de exemplo:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   Use qualquer SKU dos dados de amostra, por exemplo:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   Para a vitrine padrão, você pode usar o valor `placeholder` no roteiro para ver o produto. Quando você começa a personalizar a loja, pode personalizar o código da loja para definir o caminho para a página de detalhes do produto com base nas rotas do produto definidas no catálogo.

   >[!TIP]
   >
   >Exibir SKUs disponíveis na página [Sincronização de Dados](./setup/data-sync.md) na sua instância [!DNL Adobe Commerce Optimizer].

1. **Critério de sucesso**: a página deve exibir:
   * Nome, descrição e preço do produto
   * Imagens do produto
   * Adicionar à funcionalidade do carrinho
   * Dados recuperados da sua instância [!DNL Adobe Commerce Optimizer]

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### Etapa 3: testar a funcionalidade de pesquisa padrão

Testar os recursos padrão do produto, incluindo pesquisa e filtragem.

1. Na página inicial da loja, clique no ícone de lupa no cabeçalho.

1. Digite a sequência de pesquisa `tires` e pressione **Enter**.

1. **Critério de sucesso**: você deve ver:
   * Página de resultados da pesquisa com produtos para pneus
   * Opções de filtragem na barra lateral
   * Listagens de produtos com imagens e preços

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. Clique em qualquer produto de pneu para exibir a página de detalhes.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Solução de problemas

Se você encontrar problemas durante a configuração, use o console do Inspetor de páginas da Web para verificar se há erros. Além disso, tente limpar o cache do navegador ou usar um navegador diferente.

Use as orientações a seguir para verificar problemas comuns:

### Problemas comuns

| Problema | Sintomas | Solução |
|-------|----------|----------|
| **Falha na instalação da Sincronização de Código** | Não é possível concluir a configuração da Sincronização de código | <ul><li>Verifique se você tem acesso de administrador à sua organização do GitHub.</li><li>Tente usar um repositório pessoal em vez de uma organização.</li><li>Verifique as permissões do GitHub e tente novamente.</li></ul> |
| **Site não carregando** | 404 ou erros de conexão | <ul><li>Verifique o formato da URL do site: `https://main--{SITE}--{ORG}.aem.live`</li><li>Verifique se o aplicativo de sincronização de código foi instalado corretamente.</li><li>Certifique-se de que o repositório seja público ou configurado corretamente.</li></ul> |
| **Nenhum dado de produto exibido** | As páginas de produto mostram espaços reservados ou erros | <ul><li>Verifique seus valores de configuração em `config.json`</li><li>Na instância [!DNL Adobe Commerce Optimizer], verifique a página Sincronização de Dados para saber se os produtos de exemplo foram carregados. Se nenhum produto estiver disponível, recarregue os dados de amostra ou adicione um produto usando a [API de assimilação de dados](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request). Espere alguns minutos para que as alterações de configuração se propaguem.</li><li>Tente recuperar os detalhes do produto usando a [consulta de produtos](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) do Serviço de Merchandising, usando os mesmos cabeçalhos configurados no arquivo `config.json`. Se você puder recuperar os dados, isso provavelmente será um problema com a configuração de exibição de catálogo ou um erro de índice.</li></ul> |
| **A pesquisa não retorna resultados** | Página de resultados de pesquisa vazia | <ul><li>Verifique se você pode recuperar os resultados da pesquisa de produtos usando a [consulta productSearch](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search) dos Serviços de merchandising usando os mesmos cabeçalhos configurados no arquivo `config.json`. Se você puder recuperar os dados, isso provavelmente será um problema com a configuração de exibição de catálogo ou um erro de índice.</li><li>Confirme se a ID de exibição de catálogo no arquivo `config.json` corresponde à ID de exibição de catálogo em [!DNL Adobe Commerce Optimizer].</li><li>No Adobe Commerce Optimizer, verifique a configuração das políticas, o local e os catálogos de preços usados na configuração do cabeçalho da loja.</li><li>Verifique se as [configurações de metadados do atributo](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) estão definidas corretamente para pesquisa.</li></ul> |

### Lista de verificação de validação

Antes de prosseguir para as próximas etapas, verifique se a vitrine eletrônica está funcionando corretamente verificando o seguinte:

![Lista de verificação](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Os valores de configuração correspondem às suas configurações de instância<br>
![Lista de verificação](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Carregamentos de página inicial da Storefront sem erros<br>
![Lista de verificação](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Pelo menos uma página de detalhes do produto exibe informações completas<br>
A funcionalidade de pesquisa ![Lista de verificação](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) retorna resultados relevantes<br>
![Lista de verificação](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) As imagens do produto estão carregando corretamente<br>
![Lista de verificação](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Os valores de configuração correspondem às suas configurações de instância<br>

### Obter ajuda

Se os problemas persistirem:

* Revise a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR)
* Verifique o [guia do desenvolvedor do Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/)
* Visite os [recursos de Suporte da Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/overview)

## Próximas etapas

Depois de configurar e verificar sua loja, você pode:

1. **[Instalar o Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=pt-BR#install-and-configure-sidekick)** - Extensão do navegador para editar, visualizar e publicar conteúdo diretamente do seu site

2. **[Configurar um ambiente de desenvolvimento local](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=pt-BR#set-up-local-environment)** - Criar um ambiente local para personalizar o código e o conteúdo da vitrine

### Aprender e explorar

* **[Conclua o caso de uso completo](./use-case/admin-use-case.md)** - Saiba mais sobre a instalação de vitrine e o gerenciamento de catálogos usando o [!DNL Adobe Commerce Optimizer]

* **[Explorar a personalização de vitrine](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=pt-BR)** - Saiba mais sobre as opções avançadas de instalação e configuração

* **[Use os suplementos do Commerce para personalizar a experiência da vitrine eletrônica](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=pt-BR)**-Adicione componentes pré-construídos para aprimorar sua experiência com a vitrine eletrônica

>[!MORELIKETHIS]
>
> Consulte a [documentação da Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR) para saber mais sobre a atualização do conteúdo do site e a integração com componentes de front-end e dados de back-end do Commerce.
