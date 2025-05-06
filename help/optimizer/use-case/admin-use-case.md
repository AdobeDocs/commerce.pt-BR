---
title: Caso de uso Carvelo
description: Saiba como usar o [!DNL Adobe Commerce Optimizer] para gerenciar seu catálogo usando canais e políticas e como configurar sua loja com base na configuração do catálogo.
hide: true
role: Admin, Developer
feature: Personalization, Integration
exl-id: d11663f8-607e-4f1d-b68f-466a69bcbd91
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 0%

---

# Caso de uso Carvelo

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

O caso de uso a seguir demonstra como você pode usar o [!DNL Adobe Commerce Optimizer] para organizar seu catálogo para corresponder operações de varejo usando um único catálogo base. Ele também demonstra como configurar uma loja habilitada pelo Edge Delivery Services.

## Pré-requisito

Antes de examinar este caso de uso, verifique se você [configurou sua vitrine](../storefront.md).

## Vamos começar

Nesse caso de uso, você trabalhará com o seguinte:

1. Interface do usuário do [!DNL Adobe Commerce Optimizer] - Configure os canais e políticas necessários para gerenciar configurações operacionais complexas de catálogos.

1. Commerce Storefront - Renderize a loja com os dados de catálogo configurados na interface do usuário do [!DNL Adobe Commerce Optimizer] e os arquivos de configuração da Commerce Storefront, `fstab.yaml` e `config.json`.

### ‌Principais pontos

No final deste artigo, você deverá:

- Conheça os fundamentos do [!DNL Adobe Commerce Optimizer] com seu modelo de dados de catálogo escalável e com desempenho exclusivo.
- Saiba como o modelo de dados de catálogo se vincula perfeitamente aos componentes de vitrine independentes de plataforma criados pela Adobe.
- Saiba como usar canais e políticas da Adobe Commerce Optimizer para criar visualizações de catálogo e filtros de acesso a dados personalizados e enviar os dados para uma loja da Adobe Commerce alimentada pela Edge Delivery.

## Cenário de negócios - Carvelo Automobile

Carvelo Automobile é um conglomerado de automóveis fictício com uma configuração operacional complexa.

![Carvelo Automobile](../assets/carvelo.png)

Neste diagrama, você vê que a Carvelo vende automóveis de três marcas. Cada marca é uma empresa secundária diferente:

- Aurora (veículos elétricos)
- Parafuso (SUVs)
- Cruz (híbrido)

Ela vende essas marcas por meio de três revendedores:

- Arkbridge
- Kingsbluff
- Celport

Estes concessionários pertencem a duas sociedades-mãe diferentes:

- West Coast Inc. (Arkbridge)
- East Coast Inc. (Kingsbluff, Celport)

Cada empresa tem dois catálogos de preços usados para vender produtos a um preço específico para compradores diferentes (base, VIP).

- `west_coast_inc` e `vip_west_coast_inc`
- `east_coast_inc` e `vip_east_coast_inc`

Como você pode ver, esse é um caso de uso de negócios muito complexo. Com o [!DNL Adobe Commerce Optimizer], um comerciante pode oferecer suporte a uma estrutura de negócios complexa usando um catálogo de base única para agregar dados sem duplicação de catálogo, dimensionar catálogos de preços (mais de 30 mil catálogos de preços) e entregar todos esses dados a uma loja da Edge Delivery Services.

Agora que você tem uma visão geral do caso de uso de negócios, este é seu objetivo ao trabalhar neste tutorial:

>[!BEGINSHADEBOX]

A Carvelo quer vender peças em suas três marcas (Aurora, Bolt e Cruz) por meio de diferentes concessionárias (Akbridge, Kingsbluff e Celport). A Carvelo quer garantir que as concessionárias tenham acesso apenas às peças e aos preços corretos de acordo com seus respectivos contratos de licenciamento.

Em última análise, Carvelo tem dois objetivos principais:

1. Mantenha um site &quot;global&quot;, que tenha todas as SKUs nas três marcas.
1. Forneça um caminho para que as concessionárias configurem suas próprias lojas com base na visibilidade exclusiva do SKU e nos preços de cada SKU para cada concessionária. Tudo isso ao usar um único catálogo básico, o que elimina a duplicação do catálogo.

>[!ENDSHADEBOX]

Agora, acesse sua instância do [!DNL Adobe Commerce Optimizer].

## 1. Acessar a instância [!DNL Adobe Commerce Optimizer]

Depois que você integrar o programa de Acesso antecipado, o Adobe enviará um email com o URL para acessar a instância do [!DNL Adobe Commerce Optimizer] provisionada para você. Esta instância é pré-configurada com tudo o que você precisa para concluir com êxito as etapas descritas neste tutorial, incluindo dados de catálogo que oferecem suporte ao caso de uso Carvelo Automobile.

Ao iniciar o [!DNL Adobe Commerce Optimizer], você verá o seguinte:

![[!DNL Adobe Commerce Optimizer] UI](../assets/user-interface.png)

>[!NOTE]
>
>Consulte o artigo [visão geral](../overview.md) para saber mais sobre as diferentes partes que compõem a interface do usuário do [!DNL Adobe Commerce Optimizer].

Na navegação à esquerda, expanda a seção **[!UICONTROL Catalog]** e clique em **[!UICONTROL Channels]**. Observe que as concessionárias Arkbridge e Kingsbluff já criaram canais:

![Canais pré-configurados](../assets/existing-channels-list.png)

>[!NOTE]
>
>Você pode ignorar o canal **Global** por enquanto.

Clique no ícone de informações para analisar os detalhes do canal.

A Arkbridge tem as seguintes políticas:

- Marca
- Modelo
- Marcas West Coast Inc
- Categorias de peças Arkbridge

Kingsbluff tem as seguintes políticas:

- Marca
- Modelo
- Marcas East Coast Inc
- Categorias de peças Kingsbluff

Na próxima seção, você criará um canal e políticas para a concessionária Celport.

## 2. Criar uma política e um canal

O gerente de comércio da Carvelo precisa configurar uma nova loja para um revendedor chamado *Celport* que pertence à empresa *East Coast Inc*. A Celport venderá freios e suspensões para as marcas Bolt e Cruz.

![Celport Dealer](../assets/celport-dealer.png)

Usando o [!DNL Adobe Commerce Optimizer], o gerente de comércio irá:

1. Crie uma nova política chamada *Categorias de peças do Celport* para o Celport vender somente peças de freio e suspensão.
1. Crie um novo canal para a loja Celport.

   Este canal usa sua política recém-criada *Categorias de partes do Celport* e as *Marcas da East Coast Inc* existentes para garantir que o Celport possa vender somente as marcas Bolt e Cruz como parte do contrato com a East Coast Inc. O canal Celport usará a tabela de preços `east_coast_inc` para dar suporte às programações de preços de produtos que se alinham aos contratos de licenciamento de marca.
1. Atualize a configuração da loja de comércio para usar os dados do canal Celport criado.

No final desta seção, a Celport estará pronta para vender os produtos da Carvelo.

### Criar uma política

Vamos criar uma nova política chamada *Categorias de peças do Celport* para filtrar as SKUs que o revendedor Celport vende, que incluem peças de freio e suspensão.

1. Na navegação à esquerda, expanda a seção **[!UICONTROL Catalog]** e clique em **[!UICONTROL Policies]**.

1. Clique em **[!UICONTROL Add Policy]**.

   Uma nova página é exibida para adicionar os detalhes da política.

1. Adicione os detalhes necessários:

   **Nome** = *Categorias De Partes Celport*

1. Clique em **[!UICONTROL Add Filter]**.

   Uma caixa de diálogo é exibida para adicionar detalhes do filtro.

1. Adicione os detalhes do filtro:

   - **Atributo** = *parte_categoria*
   - **Operador** = **EM**
   - **Source de Valor** = **ESTÁTICO**
   - **Valor** = *freios*, *suspensão*

   >[!IMPORTANT]
   >
   >Verifique se o nome do atributo especificado corresponde exatamente ao nome do atributo SKU no catálogo.

   Para saber mais sobre a diferença entre uma origem de valor STATIC e TRIGGER, consulte [tipos de origem de valor](../catalog/policies.md#value-source-types).

1. Na caixa de diálogo **[!UICONTROL Filter details]**, clique em **[!UICONTROL Save]**.

1. Para habilitar o filtro recém-criado, clique nos pontos de ação (...) e selecione **Habilitar**.

1. Clique em **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Se o botão **[!UICONTROL Save]** não estiver ativo (azul), o nome da política pode estar ausente. Clique no ícone de lápis ao lado de *Nova política* para adicioná-la.

1. Volte para a lista de políticas clicando na seta para trás.

   Sua nova política de *Categorias de parte do Celport* aparece na lista.

### Criar um canal

Crie um novo canal para o revendedor *Celport* e vincule as seguintes políticas: *Marcas da East Coast Inc* e *Categorias de Peças Celport*.

1. Na navegação à esquerda, expanda a seção **[!UICONTROL Catalog]** e clique em **[!UICONTROL Channels]**.

   ![Canais](../assets/channels.png)

   Observe os canais existentes: *Arkbridge*, *Kingsbluff* e *Global*.

   ![Página de canais existente](../assets/existing-channels-list.png)

1. Clique em **[!UICONTROL Add Channel]**.

1. Preencher detalhes do canal:

   - **Nome** = *Celport*
   - **Escopos** = *en-US* (centro de ocorrências)
   - **Políticas** (use a lista suspensa) = *Marcas da East Coast Inc*; *Categorias de partes do Celport*; *Marca*; *Modelo*                          

1. Clique em **[!UICONTROL Add]** para criar o canal.

   A página Canais é atualizada para exibir o novo canal.

   ![Lista de Canais Atualizada](../assets/updated-channels-list.png)

   >[!NOTE]
   >
   >Se o botão **[!UICONTROL Add]** não estiver azul, certifique-se de que o escopo esteja selecionado colocando o cursor na seção **[!UICONTROL Scopes]** e pressionando **enter**.

1. Obtenha a ID de canal do Celport.

   Clique no ícone de informações do canal Celport na página **Canais**.

   ![Celport Channel ID](../assets/celport-channel-id.png)

   Copie e salve a ID do canal. Você precisa dessa ID ao atualizar a configuração da loja para entregar dados ao seu novo catálogo do Celport.

Depois de criar o canal Celport e as políticas associadas, o próximo passo é configurar a loja para criar seu novo catálogo Celport.

## 3. Atualize sua loja

A parte final deste tutorial envolve a atualização da loja que [você já criou](#prerequisite) para entregar dados ao novo catálogo do Celport. Nesta seção, você substitui a ID de canal no arquivo de configuração da loja pela ID de canal do Celport.

1. No ambiente de desenvolvimento local, abra a pasta onde você clonou o repositório GitHub com os arquivos de configuração padrão da loja.

1. No diretório raiz da pasta, abra o arquivo `config.json`.

   +++config.json código

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

   Observe que o cabeçalho do canal contém as seguintes linhas:

   - `ac-channel-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-environment-id`: `"Fwus6kdpvYCmeEdcCX7PZg"`
   - `ac-price-book-id`: `"west_coast_inc"`

+++

1. Substitua o valor `ac-channel-id` pela ID de canal Celport copiada anteriormente.
1. Substitua o valor `ac-environment-id` pela ID do locatário da instância [!DNL Adobe Commerce Optimizer]. Você pode encontrar a ID no email de integração do programa de acesso antecipado ou entrando em contato com o representante de conta da Adobe.

   >[!IMPORTANT]
   >
   >Verifique se o valor `commerce-endpoint` corresponde ao ponto de extremidade do GraphQL para a instância [!DNL Adobe Commerce Optimizer]. Isso é fornecido no email de boas-vindas.

1. Substitua o valor `ac-price-book-id` por `"east_coast_inc"`.
1. Salve o arquivo.

Ao salvar as alterações, você atualiza a configuração do catálogo para usar o canal Carvelo que foi configurado para vender apenas peças de freio e suspensão.

1. Inicie a loja para visualizar a experiência de catálogo específica do Celport criada pela configuração da loja.

   1. Na janela do terminal no IDE, inicie a visualização da vitrine local.

      ```shell
      npm start
      ```

   O navegador abre para a visualização de desenvolvimento local em `http://localhost:3000`.

   Se o comando falhar ou o navegador não abrir, revise as [instruções para desenvolvimento local](../storefront.md) no tópico de configuração Loja.

   1. No navegador, procure por `brakes` e pressione **Enter**.

      A loja atualiza para exibir a página da lista de produtos mostrando as peças de freio.

   ![Página da Lista de Produtos Brakes](../assets/brakes-listing-page.png)

   Clique em uma imagem de peça de freio para visualizar os detalhes do produto com informações de preço e anotar as informações de preço do produto.

1. Agora pesquise por `tires`, que é outra categoria de parte disponível nos dados de caso de uso na sua instância [!DNL Adobe Commerce Optimizer].

   ![Configuração de vitrine com cabeçalhos incorretos](../assets/storefront-configuration-with-incorrect-headers.png)

   Observe que nenhum resultado é retornado. Isso ocorre porque o canal Celport foi configurado para vender apenas peças de freio e suspensão.

1. Experimente atualizar o arquivo de configuração da loja (`config.json`).

   1. Altere os valores de `ac-channel-id` e `ac-price-book`.

      Por exemplo, você pode alterar a ID do canal para o canal Kingsbluff e a ID do catálogo de preços para `east_coast_inc`. Você pode ver as categorias de partes disponíveis para Kingsbluff revisando a política *categorias de partes Kingsbluff*.

   1. Salve o arquivo.

      Ao salvar o arquivo, a visualização da vitrine local é atualizada automaticamente.

   1. Pré-visualize as alterações no navegador usando o recurso Pesquisar para localizar as partes do pneu.

      Observe os diferentes tipos de peças disponíveis e observe os preços atribuídos ao canal Kingsbluff.

      Ao alterar os valores do cabeçalho no arquivo de configuração da loja e explorar a loja atualizada, você pode ver como é fácil atualizar a visualização do catálogo e os filtros de dados para personalizar a experiência da loja.

## Pronto!

Neste tutorial, você aprendeu como o [!DNL Adobe Commerce Optimizer] pode ajudar a organizar seu catálogo para corresponder às suas operações de varejo usando um único catálogo base. Você também aprendeu a configurar uma loja habilitada pelo Edge Delivery Services.

## Aonde ir daqui

Para saber como você pode usar a Descoberta de Produtos e o Recommendations para personalizar a experiência de compra para seus clientes, consulte a [visão geral de merchandising](../merchandising/overview.md).
