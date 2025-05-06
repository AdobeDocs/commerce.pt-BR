---
title: Introdução ao  [!DNL Live Search]
description: Saiba mais sobre os requisitos de sistema e as etapas de instalação do  [!DNL Live Search] na Adobe Commerce.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '3139'
ht-degree: 0%

---

# Configurar para sucesso com [!DNL Live Search]

O Adobe Commerce [!DNL Live Search] e o [[!DNL Catalog Service]](../catalog-service/guide-overview.md) trabalham juntos para fornecer uma solução de pesquisa intuitiva, relevante e eficiente, que permite aos clientes encontrar o que precisam com rapidez. Especificamente, [!DNL Catalog Service] exibe seus dados de catálogo para serviços SaaS, como [!DNL Live Search] para usar.

Este artigo fornece as instruções passo a passo para implementar o [!DNL Live Search] com o [!DNL Catalog Service].

>[!IMPORTANT]
>
>Quando se trata de pesquisa no site, o Adobe Commerce oferece opções. Leia [Limites e Limites](boundaries-limits.md) antes de implementar o, para garantir que o [!DNL Live Search] seja adequado às suas necessidades comerciais.

## Público-alvo

Este artigo destina-se ao desenvolvedor ou ao integrador de sistemas de sua equipe responsável pela instalação e configuração da instância do Adobe Commerce.

## Requisitos

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP versão 8.1, 8.2 ou 8.3
- [!DNL Composer]

## Plataformas compatíveis

- Adobe Commerce na nuvem (ECE): 2.4.4+
- Adobe Commerce no local (EE) : 2.4.4+

## Visão geral do fluxo de trabalho

Em um nível superior, a integração do [!DNL Live Search] exige que você:

1. [Instalar](#1-install-the-live-search-extension) a extensão [!DNL Live Search]
1. [Configurar](#2-configure-api-keys) as chaves de API
1. [Sincronizar](#3-sync-your-catalog-data) seus dados de catálogo
1. [Verificar](#4-verify-that-the-data-was-exported) se os dados do catálogo foram exportados
1. [Configurar](#5-configure-the-data) os dados
1. [Testar](#6-test-the-connection) a conexão
1. [Verificar](#7-validate-events-are-capturing-data) se os eventos estão capturando dados
1. [Personalizar](#8-customize-for-your-storefront) sua loja

## 1. Instalar a extensão [!DNL Live Search]

[!DNL Live Search] está instalado como uma extensão do [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) até o [Composer](https://getcomposer.org/). Após instalar e configurar o [!DNL Live Search], o Adobe [!DNL Commerce] começa a compartilhar dados de pesquisa e catálogo com serviços SaaS. Neste ponto, os usuários do *Administrador* podem configurar, personalizar e gerenciar aspectos de pesquisa, sinônimos e regras de merchandising.

>[!NOTE]
>
>A partir de [!DNL Live Search] 3.0.2, a extensão [!DNL Catalog Service] é agrupada na instalação [!DNL Live Search].

>[!IMPORTANT]
>
>A partir de [!DNL Live Search] 4.0.0, o Adaptador de Pesquisa será descontinuado. O Search Adapter será atualizado somente para resolver problemas de segurança.

1. Confirme se os [trabalhos do cron](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) e os [indexadores](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/index-management) estão em execução.

   >[!IMPORTANT]
   >
   >Devido ao anúncio do fim do suporte do Elasticsearch 7 para agosto de 2023, é recomendável que todos os clientes do Adobe Commerce migrem para o mecanismo de pesquisa OpenSearch 2.x. Para obter informações sobre como migrar o mecanismo de pesquisa durante uma atualização de produto, consulte [Migrando para OpenSearch](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) no _Guia de Atualização_.

1. Baixe o pacote `live-search` do [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html).

1. Execute o seguinte a partir da linha de comando:

   ```bash
   composer require magento/live-search
   ```

   Se você estiver adicionando a extensão [!DNL Live Search] a uma instalação do Adobe Commerce **new**, execute o seguinte comando para desabilitar temporariamente o [!DNL OpenSearch] e os módulos relacionados, e instale o [!DNL Live Search]. Em seguida, prossiga para a etapa 4.

   ```bash
      bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   Se você estiver adicionando a extensão [!DNL Live Search] a uma instalação do Adobe Commerce **existente**, execute o procedimento a seguir para desabilitar os módulos [!DNL Live Search] que apresentam resultados de pesquisa de vitrine. Em seguida, siga para a etapa 4:

   ```bash
      bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing 
   ```

   O [!DNL Elasticsearch] continua gerenciando solicitações de pesquisa da loja enquanto o serviço do [!DNL Live Search] sincroniza dados de catálogo e indexa produtos em segundo plano.

1. Execute o seguinte:

   ```bash
   bin/magento setup:upgrade
   ```

1. Verifique se os [indexadores](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/index-management) a seguir estão definidos como &quot;Atualizar por Agendamento&quot;:

   - Feed do produto
   - Feed de variante de produto
   - Feed de atributos do catálogo
   - Feed de preços do produto
   - Feed de dados do site de escopos
   - Feed de dados dos grupos de clientes dos escopos
   - Feed de categorias
   - Feed de permissões de categoria

1. Se estiver instalando o [!DNL Live Search] em uma nova instância do Commerce, você está pronto e pode pular para o [2. Configurar seção de chaves de API ](#2-configure-api-keys). Se estiver instalando o Live Search em uma instância existente do Commerce, continue para a próxima etapa.

1. Execute os seguintes comandos para habilitar a extensão [!DNL Live Search], desabilitar [!DNL OpenSearch] e executar `setup`.

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing 
   ```

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch 
   Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   ```bash
   bin/magento setup:upgrade
   ```

### Instalar o beta do [!DNL Live Search]

>[!IMPORTANT]
>
>O recurso a seguir está na versão beta. Para participar da versão beta, envie uma solicitação de email para [commerce-store-services](mailto:commerce-storefront-services@adobe.com).

Esta versão beta oferece suporte a três novos recursos na consulta [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/):

- **Pesquisa em camadas** - Pesquisar em outro contexto de pesquisa - Com esse recurso, você pode realizar até duas camadas de pesquisa para suas consultas de pesquisa. Por exemplo:

   - **Pesquisa de Camada 1** - Pesquise por &quot;motor&quot; em &quot;product_attribute_1&quot;.
   - **Pesquisa de camada 2** - Pesquise por &quot;part number 123&quot; em &quot;product_attribute_2&quot;. Este exemplo procura por &quot;número de peça 123&quot; nos resultados por &quot;motor&quot;.

  A pesquisa em camadas está disponível para a indexação de pesquisa `startsWith` e a indexação de pesquisa `contains`, conforme descrito abaixo:

- **startsWith indexação de pesquisa** - Pesquisar usando a indexação `startsWith`. Esse novo recurso permite:

   - Procurando produtos em que o valor do atributo começa com uma string específica.
   - Configurar uma pesquisa &quot;termina com&quot; para que os compradores possam pesquisar produtos em que o valor do atributo termina com uma determinada string. Para habilitar uma pesquisa &quot;termina com&quot;, o atributo de produto precisa ser assimilado na ordem inversa, e a chamada de API também deve ser uma sequência invertida.

- **contém a indexação de pesquisa** -Pesquise um atributo usando a indexação contains. Esse novo recurso permite:

   - Procurando uma consulta em uma cadeia de caracteres maior. Por exemplo, se um comprador procurar o número de produto &quot;PE-123&quot; na cadeia de caracteres &quot;HAPE-123&quot;.

      - Observação: este tipo de pesquisa é diferente da [pesquisa de frase](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#phrase) existente, que executa uma pesquisa de preenchimento automático. Por exemplo, se o valor do atributo do seu produto for &quot;calças de ar livre&quot;, uma pesquisa de frase retornará uma resposta para &quot;fora da panela&quot;, mas não retornará uma resposta para &quot;ou formigas&quot;. A contém busca, no entanto, retorna uma resposta para &quot;ou formigas&quot;.

Essas novas condições aprimoram o mecanismo de filtragem de consultas de pesquisa para refinar os resultados da pesquisa. Essas novas condições não afetam a consulta de pesquisa principal.

Você pode implementar essas novas condições na página de resultados da pesquisa. Por exemplo, você pode adicionar uma nova seção na página, onde o comprador pode refinar ainda mais os resultados da pesquisa. Você pode permitir que os compradores selecionem atributos específicos do produto, como &quot;Fabricante&quot;, &quot;Número da peça&quot; e &quot;Descrição&quot;. A partir daí, eles pesquisam dentro desses atributos usando as condições `contains` ou `startsWith`. Consulte o Guia do administrador para obter uma lista de [atributos](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/attributes-input-types) pesquisáveis.

1. Para instalar a versão beta, adicione a seguinte dependência ao seu projeto:

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. Confirme e envie por push as alterações nos arquivos do `composer.json` e do `composer.lock` para o projeto de nuvem. [Saiba mais](https://experienceleague.adobe.com/pt-br/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension).

   Este beta adiciona **[!UICONTROL Search types]** caixas de seleção para **[!UICONTROL Autocomplete]**, **[!UICONTROL Contains]** e **[!UICONTROL Starts with]** no Administrador. Ela também atualiza a API do GraphQL [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) para incluir esses novos recursos de pesquisa.

1. No Administrador, [defina um atributo de produto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) para ser pesquisável e especifique o recurso de pesquisa para esse atributo, como **Contém** (padrão) ou **Começa com**. Você pode especificar no máximo seis atributos a serem habilitados para **Contém** e seis atributos a serem habilitados para **Começa com**. Para beta, esteja ciente de que o Administrador não impõe essa restrição, mas ela é imposta em pesquisas de API.

   ![Especificar recurso de pesquisa](./assets/search-filters-admin.png)

1. Consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability) para saber como atualizar suas chamadas de API do [!DNL Live Search] usando os novos recursos de pesquisa do `contains` e do `startsWith`.

### Descrições dos campos

| Campo | Descrição |
|--- |--- |
| `Autocomplete` | Ativado por padrão e não pode ser modificado. Com `Autocomplete` você pode usar `contains` no [filtro de pesquisa](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering). Aqui, a consulta de pesquisa em `contains` retorna uma resposta de pesquisa do tipo preenchimento automático. A Adobe recomenda usar esse tipo de pesquisa para campos de descrição, que normalmente têm mais de 50 caracteres. |
| `Contains` | Ativa uma pesquisa de &quot;texto contido em uma sequência de caracteres&quot; verdadeira em vez de uma pesquisa de preenchimento automático. Use `contains` no [filtro de pesquisa](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability). Consulte as [Limitações](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations) para obter mais informações. |
| `Starts with` | Permite consultar strings que começam com um valor específico. Use `startsWith` no [filtro de pesquisa](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#filtering-using-search-capability). |

## 2. Configurar chaves de API

A chave de API do Adobe Commerce e sua chave privada associada são necessárias para conectar o [!DNL Live Search] a uma instalação do Adobe Commerce. A chave de API é gerada e mantida na conta do detentor da licença [!DNL Commerce], que pode compartilhá-la com o desenvolvedor ou com o integrador de sistemas. Em seguida, o desenvolvedor poderá criar e gerenciar os Espaços de dados SaaS em nome do detentor da licença. Se você já tiver um conjunto de chaves de API, não será necessário gerá-las novamente.

Saiba como configurar suas chaves de API no artigo [Commerce Services Connector](../landing/saas.md).

## 3. Sincronizar os dados do catálogo

O [!DNL Live Search] move dados de catálogo para a infraestrutura SaaS da Adobe. Os dados são indexados e os resultados da pesquisa são enviados desse índice diretamente para a loja. Dependendo do tamanho e da complexidade, a indexação pode levar de 30 minutos a algumas horas.

Para iniciar a sincronização inicial dos dados do catálogo com os serviços SaaS, execute os seguintes comandos nesta ordem:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

Quando você executa esses comandos, a sincronização inicial dos dados do catálogo com os serviços SaaS é iniciada.

>[!WARNING]
>
> Embora os dados sejam indexados e sincronizados, as operações de pesquisa e navegação de categoria não estão disponíveis na loja. Dependendo do tamanho do catálogo, o processo pode levar pelo menos uma hora a partir do momento em que `cron` é executado para sincronizar os dados com os serviços SaaS.

### Monitorar progresso da sincronização

Você pode exibir os dados sincronizados e compartilhados usando o [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-dashboard). Esse painel fornece informações valiosas sobre a disponibilidade de dados de produtos para sua loja, garantindo que eles possam ser exibidos imediatamente para seus compradores.

![Painel de gerenciamento de dados](assets/data-management-dashboard.png)

Você também pode executar comandos de sincronização e solucionar problemas do processo de sincronização usando a [CLI do Commerce](../data-export/data-export-cli-commands.md#troubleshooting) e os logs de extensão de exportação de dados.

#### Futuras atualizações do produto

Após a sincronização inicial, pode levar até 15 minutos para que atualizações de produtos incrementais sejam disponibilizadas para pesquisa na loja. Para saber mais, consulte [Streaming de Atualizações de Produto](indexing.md) na documentação de Indexação.

## 4. Verifique se os dados foram exportados

Para verificar se os dados do catálogo foram exportados do Adobe Commerce e sincronizados com o [!DNL Live Search], você tem algumas opções:

- Procure entradas nas seguintes tabelas:

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >Se você receber um erro `table does not exist`, procure entradas nas tabelas `catalog_data_exporter_products` e `catalog_data_exporter_product_attributes`. Estes nomes de tabela são usados em [!DNL Live Search] versões anteriores à 4.2.1.

- Use a [área de jogo do GraphQL](https://experienceleague.adobe.com/pt-br/docs/commerce/live-search/live-search-admin/graphql) com a consulta padrão (consulte a [referência do GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) para obter mais detalhes) para verificar o seguinte:

   - A contagem de produtos retornada está próxima do que você espera da exibição da loja.
   - Os aspectos são retornados.

Para obter ajuda adicional, consulte [[!DNL Live Search] catálogo não sincronizado](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) na Base de Dados de Conhecimento de Suporte.

## 5. Configurar os dados

A configuração correta dos dados do produto garante bons resultados de pesquisa para os clientes. Nesta seção, você ativa os widgets da lista de produtos e atribui categorias.

### Ativar widgets de lista de produtos

Quando você instala o [!DNL Live Search] 4.0.0+, os widgets de lista de produtos são habilitados por padrão. Quando os widgets são ativados, um componente de interface do usuário diferente é usado para a página de resultados da pesquisa e a página da lista de produtos da navegação por categorias. Este componente da interface faz chamadas diretas à [API do Serviço de Catálogo](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/), o que resulta em tempos de resposta mais rápidos.

Se você tiver uma versão do [!DNL Live Search] anterior à 4.0.0+, deverá habilitar manualmente o Widget de listagem de produtos.

1. No *Admin*, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Em **[!UICONTROL Live Search]**, selecione **[!UICONTROL Storefront Features]**.
1. Defina **[!UICONTROL Enable Product Listing Widgets]** como `Yes`.

   ![Habilitar Widgets de Listagem de Produtos](assets/ls-admin-enable-widget.png)

Quando você alterar essa configuração, a mensagem `Page cache is invalidated` será exibida. É necessário liberar o cache do Magento para salvar a alteração.

1. Acesse a página [Gerenciamento de Cache](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/tools/cache-management) seguindo um destes procedimentos:

   - Clique no link **[!UICONTROL Cache Management]** na mensagem acima do espaço de trabalho.
   - Na barra lateral _Admin_, vá para **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**.

1. Selecione a **Configuração** [!UICONTROL Cache Type] e clique em **[!UICONTROL Flush Magento Cache]**.

   As alterações na loja são imediatas depois de liberar o cache.

### Atribuir categorias

Os produtos retornados em [!DNL Live Search] devem ser atribuídos a uma [categoria](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/categories/categories). Na Luma, por exemplo, os produtos são colocados em categorias como &quot;Homens&quot;, &quot;Mulheres&quot; e &quot;Engrenagens&quot;. As subcategorias também são configuradas para &quot;Topos&quot;, &quot;Partes inferiores&quot; e &quot;Inspeções&quot;. Essas atribuições de categoria melhoram a granularidade ao filtrar.

## 6. Testar a conexão

Com seus dados de catálogo agora em SaaS, teste para garantir que os dados do produto sejam retornados nas seguintes situações:

- A caixa [!UICONTROL Search] retorna os resultados corretamente
- A pesquisa de categoria retorna os resultados corretamente
- Os aspectos estão disponíveis como filtros nas páginas de resultados da pesquisa

Se tudo funcionar corretamente, [!DNL Live Search] está instalado, conectado e pronto para uso.

Se você encontrar problemas na loja, verifique o arquivo `var/log/system.log` em busca de falhas de comunicação da API ou erros no lado dos serviços.

Para permitir [!DNL Live Search] por meio de um firewall, adicione `commerce.adobe.io` ao arquivo de inclui na lista de permissões.

## 7. Verifique se os eventos estão capturando dados

Verifique se os eventos da loja implantados em seu site estão funcionando. Isso é especialmente importante para implementações headless.

- Revise os [eventos](events.md) necessários para [!DNL Live Search].
- Verifique se o [painel do Live Search](performance.md) está exibindo dados de seu(s) ambiente(s) de não produção.
- [Verificar coleção de eventos](../product-recommendations/verify.md). Enquanto esta página estiver no guia [!DNL Product Recommendations], as etapas de verificação também se aplicam a [!DNL Live Search].

## 8. Personalize para sua loja

Você instalou a extensão [!DNL Live Search], sincronizou, validou e configurou seus dados. A próxima etapa é garantir que os widgets do [!DNL Live Search] estejam de acordo com a aparência da sua loja.

Você pode estilizar os widgets popover e PLP definindo regras CSS personalizadas, conforme necessário. Consulte [Elementos Popover de estilo](storefront-popover.md#styling-popover-example) e [widget da página de listagem de produtos](plp-styling.md#styling-example).

Se você quiser estender a funcionalidade dos widgets, o código-fonte de cada um deles estará disponível em um repositório público.
Nesse cenário, você pode personalizar o JavaScript de acordo com suas necessidades e, em seguida, hospedar seu código personalizado no CDN. Este script personalizado se comunica com o serviço [!DNL Live Search] e retorna os resultados normalmente, permitindo que você controle a funcionalidade do widget.

- [repositório de widgets PLP](https://github.com/adobe/storefront-product-listing-page)
- [Repo de barra de pesquisa](https://github.com/adobe/storefront-search-as-you-type)

## Atualizando [!DNL Live Search]

Antes de atualizar o Live Search, execute o seguinte na linha de comando para verificar a versão do Live Search instalada:

```bash
composer show magento/module-live-search | grep version
```

Para atualizar [!DNL Live Search], execute o seguinte na linha de comando:

```bash
composer update magento/live-search --with-dependencies
```

Para atualizar para uma versão principal, como 3.1.1 para 4.0.0, edite o arquivo [!DNL Composer] `.json` raiz do projeto da seguinte maneira:

1. Se sua versão do `magento/live-search` instalada no momento for a `3.1.1` ou inferior, e você estiver atualizando para a versão `4.0.0` ou superior, execute o seguinte comando antes da atualização:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Para obter informações sobre a versão `magento/live-search` instalada no momento, execute o seguinte comando:

   ```bash
   composer show magento/live-search
   ```

1. Abra o arquivo raiz `composer.json` e procure por `magento/live-search`.

1. Na seção `require`, atualize o número da versão da seguinte maneira:

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. Salve `composer.json`. Em seguida, execute o seguinte a partir da linha de comando:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Desinstalando [!DNL Live Search]

Para desinstalar o [!DNL Live Search], consulte [Desinstalar módulos](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] pacotes

A extensão [!DNL Live Search] consiste nos seguintes pacotes:

| Pacote | Descrição |
|--- |--- |
| `module-live-search` | Permite que os comerciantes definam suas configurações de pesquisa para facetas, sinônimos, regras de consulta e assim por diante, além de fornecer acesso a um playground do GraphQL somente leitura para testar consultas do *Administrador*. |
| `module-live-search-adapter` | Encaminha solicitações de pesquisa da loja para o serviço [!DNL Live Search] e renderiza os resultados na loja. <br />- Navegação de categoria - Encaminha solicitações da [navegação superior](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/catalog/navigation/navigation-top) da vitrine para o serviço de pesquisa.<br />- Pesquisa global - Encaminha solicitações da caixa [pesquisa rápida](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/catalog/search/search) no canto superior direito da loja para o serviço [!DNL Live Search]. |
| `module-live-search-storefront-popover` | Um popover &quot;pesquisar ao digitar&quot; substitui a pesquisa rápida padrão e retorna dados e miniaturas dos principais resultados da pesquisa. |

## [!DNL Live Search] dependências

O metapackage [!DNL Composer] para instalar a extensão [!DNL Live Search] inclui as seguintes dependências de módulo.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Conceitos avançados

As seções a seguir fornecem tópicos mais avançados ao usar [!DNL Live Search] e [!DNL Catalog Service].

### Endpoint

[!DNL Live Search] se comunica através do ponto de extremidade em `https://catalog-service.adobe.io/graphql`.

Como [!DNL Live Search] não tem acesso ao banco de dados completo do produto, as APIs principais do GraphQL do Commerce e do GraphQL [!DNL Live Search] não têm paridade completa.

A Adobe recomenda chamar as APIs SaaS diretamente — especificamente, o endpoint do Serviço de catálogo.

- Obter desempenho e reduzir a carga do processador, ignorando o processo de banco de dados/Graphql do Commerce
- Aproveite a federação [!DNL Catalog Service] para chamar [!DNL Live Search], [!DNL Catalog Service] e [!DNL Product Recommendations] de um único ponto de extremidade.

Para alguns casos de uso, talvez seja melhor ligar para [!DNL Catalog Service] para obter detalhes sobre o produto e casos semelhantes. Consulte [refineProduct](https://developer.adobe.com/commerce/services/graphql/catalog-service/refine-product/) para obter mais informações.

Se você tiver uma implementação headless personalizada, confira as [!DNL Live Search] implementações de referência:

- [Widget do PLP](https://github.com/adobe/storefront-product-listing-page)
- [Campo do Live Search](https://github.com/adobe/storefront-search-as-you-type)

A coleta automática de dados de interação do usuário não funciona por padrão quando você não usa os componentes padrão, como o Adaptador de pesquisa, os widgets do Luma ou os Widgets do AEM CIF. O Adobe Sensei usa esses dados coletados para um merchandising inteligente e para o rastreamento de desempenho. Para resolver esse problema, é necessário desenvolver uma solução personalizada para implementar essa coleção de dados de forma headless.

A última versão de [!DNL Live Search] já usa [!DNL Catalog Service].

### Suporte de idioma

Os widgets [!DNL Live Search] oferecem suporte aos seguintes idiomas:

|  |  |  |  |
|--- |--- |--- |--- |
| Idioma | Região | Código do idioma | Localidade do Magento |
| Búlgaro | Bulgária | bg_BG | bg_BG |
| Catalão | Espanha | ca_ES | ca_ES |
| Tcheco | República Checa | cs_CZ | cs_CZ |
| Dinamarquês | Dinamarca | da_DK | da_DK |
| Alemão | Alemanha | de_DE | de_DE |
| Grego | Grécia | el_GR | el_GR |
| Inglês | Reino Unido | en_GB | en_GB |
| Inglês | Estados Unidos | pt_BR | pt_BR |
| Espanhol | Espanha | es_ES | es_ES |
| Estoniano | Estônia | et_EE | et_EE |
| Basco | Espanha | eu_ES | eu_ES |
| Persa | Irã | fa_IR | fa_IR |
| Finlandês | Finlândia | fi_FI | fi_FI |
| Francês | França | fr_FR | fr_FR |
| Galego | Espanha | gl_ES | gl_ES |
| Hindi | Índia | hi_IN | hi_IN |
| Húngaro | Hungria | hu_HU | hu_HU |
| Indonésio | Indonésia | id_ID | id_ID |
| Italiano | Itália | it_IT | it_IT |
| Coreano | Coreia do Sul | ko_KR | ko_KR |
| Lituano | Lituânia | lt_LT | lt_LT |
| Letão | Letônia | lv_LV | lv_LV |
| Norueguês | Noruega - Bokmal | nb_NO | nb_NO |
| Holandês | Holanda | nl_NL | nl_NL |
| Polonês | Polônia | pl_PL | pl_PL |
| Português | Brasil | pt_BR | pt_BR |
| Português | Portugal | pt_PT | pt_PT |
| Romeno | Romênia | ro_RO | ro_RO |
| Russo | Rússia | ru_RU | ru_RU |
| Sueco | Suécia | sv_SE | sv_SE |
| Tailandês | Tailândia | th_TH | th_TH |
| Turco | Turquia | tr_TR | tr_TR |
| Chinês | China | zh_CN | zh_Hans_CN |
| Chinês | Taiwan | zh_TW | zh_Hant_TW |

Se o widget detectar que a configuração de idioma do administrador do Commerce corresponde a um idioma suportado, o padrão será esse idioma. Caso contrário, o widget usará o inglês como padrão. No Admin, a configuração de idioma é definida navegando até _[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options].

Os administradores também podem definir o idioma do [índice de pesquisa](settings.md#language), para ajudar a garantir melhores resultados de pesquisa.

### Repositório de código do widget

O código do widget página da lista de produtos e do widget de campo do Live Search está disponível para download no GitHub.

Os desenvolvedores que têm acesso ao código podem personalizar completamente o funcionamento e a aparência. Eles hospedam o código em seus próprios servidores, mas ainda usam o serviço [!DNL Live Search].

- [Widget do PLP](https://github.com/adobe/storefront-product-listing-page)
- [Barra de pesquisa](https://github.com/adobe/storefront-search-as-you-type)

### Extensão Data Export

Depois que o Live Search é ativado, a extensão Exportação de dados sincroniza os dados do Commerce entre o aplicativo Commerce e o Live Search. Esse processo garante que os dados mais atuais do Commerce estejam disponíveis na loja. No Admin, você pode verificar o status da sincronização usando o painel Gerenciamento de dados. Você pode gerenciar e solucionar problemas do processo de exportação de dados usando a CLI e os logs do Commerce. Para obter detalhes, consulte o [Guia de Exportação de Dados](../data-export/overview.md).

### Inventory management

O [!DNL Live Search] oferece suporte aos recursos do [Inventory management](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/introduction) na Commerce (anteriormente conhecido como Inventário de Várias Source, ou MSI). Para habilitar o suporte completo, você deve [atualizar](install.md#updating-live-search) o módulo de dependência `commerce-data-export` para a versão 102.2.0+.

[!DNL Live Search] retorna um valor booleano observando se um produto está disponível no Inventory management, mas não contém informações sobre qual origem tem o estoque.

### Indexador de preços

Os clientes do Live Search podem usar o [indexador de preços do SaaS](../price-index/price-indexing.md), que fornece atualizações de alteração de preço e tempo de sincronização mais rápidos.

### Suporte de preço

Os widgets do Live Search são compatíveis com a maioria, mas não com todos os tipos de preço compatíveis com o Adobe Commerce.

Atualmente, os preços básicos são suportados. Os preços avançados que não são compatíveis são:

- Custo
- Preço Mínimo Anunciado

Examine a [API Mesh](../catalog-service/mesh.md) para cálculos de preço mais complexos.

O formato de preço oferece suporte à definição de configuração de localidade na instância do Commerce: *Lojas* > Configurações > *Configuração* > Geral > *Geral* > Opções Locais > Localidade.

### Suporte a vitrine headless

Opcionalmente, talvez seja necessário instalar o módulo `module-data-services-graphql` que expande a cobertura de GraphQL existente do aplicativo para incluir campos necessários para a coleta de dados comportamentais da loja.

```bash
composer require magento/module-data-services-graphql
```

Esse módulo adiciona contextos adicionais às consultas do GraphQL:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Suporte B2B

[!DNL Live Search] dá suporte à [funcionalidade B2B](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/b2b/guide-overview) com [limitações](boundaries-limits.md#b2b-and-category-permissions) adicionais.

### Suporte ao PWA

O [!DNL Live Search] funciona com o PWA Studio, mas os usuários podem ver pequenas diferenças em comparação a outras implementações do Commerce. Funcionalidades básicas, como pesquisa e listagem de produtos, funcionam em Venia, mas algumas permutas de Graphql podem não funcionar corretamente. Também pode haver diferenças de desempenho.

- A implementação atual do PWA de [!DNL Live Search] requer mais tempo de processamento para retornar resultados de pesquisa do que [!DNL Live Search] com a loja nativa do Commerce.
- [!DNL Live Search] no PWA não oferece suporte a [manipulação de eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Como resultado, os relatórios de pesquisa e o merchandising inteligente não funcionam nas vitrines do PWA.
- Ao usar o [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/), o GraphQL não oferece suporte à filtragem diretamente em `description`, `name`, `short_description`, mas esses campos podem ser retornados com um filtro mais geral.

Para usar o [!DNL Live Search] com o PWA Studio, os integradores também devem:

1. Instale o [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Defina o `environmentId` no objeto `storeDetails`.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookies

O [!DNL Live Search] coleta dados de interação do usuário como parte de sua funcionalidade base e os cookies são usados para armazenar esses dados. Ao coletar qualquer informação do usuário, ele deve concordar em armazenar cookies. [!DNL Live Search] e [!DNL Product Recommendations] compartilham o fluxo de dados e, portanto, o mesmo mecanismo de cookie. Leia mais sobre isso em [Manipular restrições de cookies](https://experienceleague.adobe.com/pt-br/docs/commerce/product-recommendations/developer/setting-cookie).
