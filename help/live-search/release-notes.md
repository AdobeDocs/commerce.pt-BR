---
title: Notas de versão do [!DNL Live Search]
description: As informações da versão mais recente do  [!DNL Live Search] Adobe Commerce.
feature: Services, Search, Release Notes
exl-id: 099cf79c-968c-4381-b66d-7f6141ad2db3
source-git-commit: ac1f3497292cc586810eb44a408f7d4d7088a96d
workflow-type: tm+mt
source-wordcount: '2576'
ht-degree: 0%

---

# Notas de versão do [!DNL Live Search]

Essas notas de versão descrevem as versões mais recentes do [!DNL Live Search].

Há suporte para a versão mais recente lançada. As notas de versão para versões mais antigas são fornecidas para referência.
As atualizações incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos

## Atualizações do serviço hospedado

Essas notas descrevem atualizações que foram publicadas fora de uma versão com controle de versão ou melhorias no serviço hospedado.

_29 de abril de 2025_

![Correção](../assets/fix.svg) Corrigido um problema no qual o relatório **Exportar para CSV** na guia [**Desempenho**](./performance.md) não incluía todos os dados especificados no intervalo de datas.
![Correção](../assets/fix.svg) Corrigido um problema no qual você não podia salvar uma [regra de merchandising](./rules.md) se o filtro de consulta de pesquisa fosse usado.
![Correção](../assets/fix.svg) Corrigido um problema no qual [produtos fixados](./facets-manage.md#pinunpin-facet) não estavam listados na parte superior da página de resultados.

_21 de abril, 2025_

![Correção](../assets/fix.svg) Corrigido um problema com o filtro de intervalo de preços para que produtos iguais ao intervalo superior não fossem incluídos nos resultados. Essa alteração está alinhada à forma como as faixas de preços são definidas para os aspectos.

_3 de abril, 2025_

![Correção](../assets/fix.svg) atualizou a extensão Exportação de dados SaaS para remover a [limitação](boundaries-limits.md#b2b-and-category-permissions) de &quot;Produtos devem ser atribuídos à categoria raiz&quot; para comerciantes B2B. Consulte [Gerenciar a extensão de exportação de dados](../data-export/manage-extension.md) para saber como atualizar a extensão de Exportação de dados SaaS para a versão 103.4.0+.

_20 de fevereiro de 2025_

![Novo](../assets/new.svg) O Commerce dá suporte a sinônimos de várias palavras. [Saiba mais](synonyms-type.md#multi-word-synonym-behavior). O suporte para sinônimos de várias palavras só está disponível após a data de lançamento de 20 de fevereiro. Qualquer sinônimo de várias palavras existente requer uma reindexação completa para funcionar, que você pode solicitar ao [criar um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

_31 de janeiro de 2025_

![Novo](../assets/new.svg) Há uma nova política de retenção de dados para dados de catálogo não consultados em seu ambiente de teste. [Saiba mais](overview.md#catalog-data-retention-policy).

_19 de setembro de 2024_

![Novo](../assets/new.svg) Lançada uma versão beta que oferece suporte a três novos recursos de pesquisa: em camadas, começa com e contém. [Saiba mais](install.md#install-the-live-search-beta).

_4 de setembro de 2024_

![Correção](../assets/fix.svg) Aumento do número máximo de compartimentos que podem ser retornados [em uma faceta](boundaries-limits.md#facets) para 100.

_7 de agosto de 2024_

![Correção](../assets/fix.svg) Aumentou o valor do intervalo máximo ou o intervalo de preço para [facetas de preço](settings.md#price-faceting) de 10.000 para 40.000.000.

_13 de fevereiro de 2024_

![Novo](../assets/new.svg) [!DNL Live Search] agora dá suporte à configuração de uma regra padrão para [Pesquisar Merchandising](rules.md).

_12 de outubro de 2023_

![Novos](../assets/new.svg) administradores do Commerce podem agora especificar o idioma do índice para [!DNL Live Search]. Consulte [Configurações](settings.md).
![Correção](../assets/fix.svg) A guia &quot;Regras de pesquisa&quot; foi renomeada para &quot;Pesquisar merchandising&quot;.

_13 de junho de 2023_

![Correção](../assets/fix.svg) Corrigido um problema no qual alguns caracteres, como aspas ou apóstrofos, causavam problemas de classificação. A reindexação resolve esses problemas.

_25 de abril de 2023_

![Novos](../assets/new.svg) clientes do [!DNL Live Search] agora podem aproveitar o novo [indexador de preços do SaaS](../price-index/price-indexing.md).

### Widget do PLP

_22 de maio de 2025_

![Correção](../assets/fix.svg) Corrigido um problema no qual o botão Adicionar ao carrinho permanecia em inglês quando a localidade era alterada para francês, alemão, italiano ou espanhol.
![Correção](../assets/fix.svg) Corrigido um problema no qual o botão Adicionar ao carrinho era exibido para produtos indisponíveis.

_31 de maio de 2024_

![Novo](../assets/new.svg) Versão lançada 2.0.0 do widget PLP, que adiciona suporte para os seguintes recursos:

- Botões Adicionar ao carrinho - Disponível somente para produtos simples.
- Várias imagens por produto — a imagem pode mudar quando uma cor diferente é escolhida para um produto configurável.

_27 de outubro de 2023_

![Novo](../assets/new.svg) O widget PLP [!DNL Live Search] agora dá suporte a amostras de cores.

## [!DNL Live Search] 4.5.0

_5 de setembro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![O novo](../assets/new.svg) Live Search agora respeita totalmente o [modo de restrição de cookies](install.md#cookies), impedindo a coleta e o armazenamento de dados em cookies/armazenamento local quando as restrições são habilitadas.

## [!DNL Live Search] 4.4.1

_11 de agosto de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Ponto de extremidade de serviço de catálogo fixo para ambientes de sandbox.

## [!DNL Live Search] 4.4.0

_14 de julho de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Aumentou o limite de [agrupamento de preços](./settings.md#price-faceting) de 50 para 100.

## [!DNL Live Search] 4.3.0

_11 de março de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Fix](../assets/fix.svg) [!DNL Live Search] agora dá suporte ao PHP 8.4 para instalações que executam o Adobe Commerce 2.4.8-beta2.
![Correção](../assets/fix.svg) Corrigido um problema no qual o Adaptador de Pesquisa não era compatível com `psr/http-message:2.0`.

## [!DNL Live Search] 4.2.3

_13 de fevereiro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Corrigido um problema no qual a página de detalhes do pedido não tinha o número do pedido, a data e o botão **[!UICONTROL Reorder]**.

## [!DNL Live Search] 4.2.2

_6 de janeiro de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Corrigido um problema que causava um erro com a consulta GraphqL `categoryList` no Adobe Commerce versão 2.4.5 e anterior.

## [!DNL Live Search] 4.2.1

_31 de julho de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Corrigido um problema no qual determinados scripts não eram carregados na página de check-out.
![Correção](../assets/fix.svg) Corrigiu uma versão de dependência no arquivo `composer.json`.

## [!DNL Live Search] 4.2.0

_31 de maio de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Atualização da extensão do Live Search para usar widgets PLP versão 2.0.0.

## [!DNL Live Search] 4.1.2

_16 de maio de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

### Atualizações

![Correção](../assets/fix.svg) Corrigida a consulta do GraphQL [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-by-categories) para filtrar corretamente com base no `categoryPath` e `categoryList` para categorias.

## [!DNL Live Search] 4.1.1

_19 de março de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

### Novos recursos

![Novo](../assets/new.svg) Suporte a idiomas adicionado para polonês.
![Novo](../assets/new.svg) [!DNL Live Search] agora dá suporte ao PHP 8.3 para instalações que executam o Adobe Commerce 2.4.4.

## [!DNL Live Search] 4.1.0

_22 de fevereiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

### Novos recursos

![Novo](../assets/new.svg) O [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) está disponível agora. Este painel renovado fornece informações sobre fluxos de dados para [!DNL Product Recommendations], [!DNL Live Search] e [!DNL Catalog Service].

### Atualizações

![Correção](../assets/fix.svg) Corrigido um problema que causava um erro quando usuários convidados adicionavam produtos a um carrinho em exibições de lojas não padrão.
![Correção](../assets/fix.svg) Corrigido um problema que fazia com que o popover de pesquisa sempre exibisse o símbolo de moeda na frente do valor do preço, independentemente das configurações de localidade.
![Correção](../assets/fix.svg) Remoção de definições de tipo desnecessárias para plug-ins principais desativados para corrigir problemas de compatibilidade na instalação.

## [!DNL Live Search] 4.0.0

_13 de novembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

### Novos recursos

![Novo](../assets/new.svg) [!DNL Live Search] agora dá suporte a amostras de cores no widget PLP.
![Novo](../assets/new.svg) [!DNL Live Search] agora exibe o nome da categoria em vez da ID da categoria.
![Novo](../assets/new.svg) [!DNL Live Search] agora dá suporte a preços tachados no widget PLP.
![Novo](../assets/new.svg) Introdução ao botão &quot;Ocultar filtros&quot; para ocultar o painel de filtros.


### Atualizações

![Correção](../assets/fix.svg) O widget PLP [!DNL Live Search] agora está habilitado por padrão para novas instalações.
![Correção](../assets/fix.svg) O Adaptador de Pesquisa está obsoleto. O Search Adapter será atualizado somente para resolver problemas de segurança.
![Corrigir](../assets/fix.svg) Estilos CSS reconfigurados para melhor isolar classes de widget.
![Correção](../assets/fix.svg) de pequenos erros

Após instalar a versão 3.1.1 ou superior, ative os novos indexadores:

- Feed de preços do produto
- Feed de dados do site de escopos
- Feed de dados dos grupos de clientes dos escopos

Depois da atualização, teste a configuração atualizada no controle de qualidade ou preparo antes de enviar as alterações para a produção.

+++3.1.1 e anteriores

### [!DNL Live Search] 3.1.1

_15 de setembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Nova](../assets/new.svg) A guia Nova categoria de merchandising foi adicionada. Agora, os usuários podem adicionar Classificações inteligentes e Classificações manuais (fixar, impulsionar, enterrar, ocultar) por categoria
![Novos](../assets/new.svg) usuários podem adicionar uma única regra de categoria com classificação inteligente ou manual
![Novos](../assets/new.svg) usuários agora podem adicionar regras de Classificação inteligente a subcategorias
![Novo](../assets/new.svg) Informações detalhadas são fornecidas ao excluir subcategorias com classificação inteligente
![Novo](../assets/new.svg) adição da capacidade de excluir regras para estratégias de classificação herdadas
![Novo](../assets/new.svg) Adição da capacidade de excluir regras de uma única categoria
![Novos](../assets/new.svg) Usuários agora podem pesquisar por nome de categoria ao adicionar uma regra
![Novo](../assets/new.svg) Com a Exibição em árvore de categoria, os usuários agora podem exibir qual categoria tem regras aplicadas.
![Nova](../assets/new.svg) Visualização de Categoria mostra somente a categoria selecionada.
![Novos](../assets/new.svg) componentes do [widget Popover](https://github.com/adobe/aem-cif-guides-venia/pull/319) e do [widget PLP](https://github.com/adobe/aem-cif-guides-venia/pull/320) do AEM CIF permitem que os sites da AEM aproveitem o [!DNL Live Search].

#### Atualizações

![Correção](../assets/fix.svg) O tamanho da tabela dos feeds Produtos e Preço foi bastante reduzido. As tabelas `catalog_data_exporter_products` e `catalog_data_exporter_product_prices` devem ver uma redução substancial no tamanho.
![Correção](../assets/fix.svg) A guia &#39;Regras&#39; foi renomeada para &#39;Regras de Pesquisa&#39;
![Correção](../assets/fix.svg) Ao classificar por &quot;tendência&quot;, agora é possível escolher entre:
- 3 dias (padrão)
- 14 dias
- 30 dias
![Correção](../assets/fix.svg) de &#39;Eventos&#39; (Aumentar/Fixar/Ocultar) foi renomeado para &#39;Classificação Manual&#39;
![Correção](../assets/fix.svg) &#39;Tipo de classificação&#39; foi renomeada como &#39;Classificação inteligente&#39;
![Correção](../assets/fix.svg) de pequenas correções de erros

### [!DNL Live Search] 3.1.0

_1º de setembro de 2023_

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

#### Atualizações

![Correção](../assets/fix.svg) O widget Lista de produtos foi atualizado para usar a [API de Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).

### [!DNL Live Search] 3.0.2

_7 de agosto de 2023_

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

#### Novos recursos

![Novo](../assets/new.svg) Os seguintes valores foram adicionados ao objeto `storeDetails`:

- &quot;Permitir todos os produtos por página&quot;
- Taxa de câmbio
- &quot;Produtos por página em valores permitidos da grade&quot;
- &quot;Produtos por página no valor padrão da grade&quot;
- Idioma da loja

#### Atualizações

![Os módulos Correção](../assets/fix.svg) do Serviço de Catálogo foram adicionados ao metapackage para dar suporte à recuperação avançada de dados.
![Correção](../assets/fix.svg) A navegação de página **Minha Conta** não desaparece mais ao usar o widget Página de listagem de produtos.

Os comerciantes devem atualizar a versão da extensão [!DNL Live Search] >= 3.0.2 para acessar esses recursos.

É recomendável atualizar e testar antes de enviar para a produção. Considere atualizar o ambiente de produção fora do horário de pico após verificar os resultados do ambiente de teste.

#### Limitação

Usar o widget Página de listagem de produtos do Live Search causa falha no Google Tag Manager. Use o adaptador de pesquisa padrão se o Google Tag Manager for necessário.

### [!DNL Live Search] 3.0.1

_14 de março de 2023_

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

#### Novos recursos

![Novo](../assets/new.svg) Cartão de Item de Produto na visualização de Regras
![Novo](../assets/new.svg) [Widget de Página de Listagem de Produtos](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-storefront/plp-styling)
![Novas](../assets/new.svg) [Opções de filtragem de categoria](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#facets)
![Novo](../assets/new.svg) Adição da capacidade de arrastar e soltar para criar eventos de PIN
![Novas](../assets/new.svg) ações Novo PIN:
- Fixar no ponto - Botão Fixar para criar um evento Fixar com um clique
- Fixar no início - Coloca o produto na primeira posição
- Fixar na parte inferior - Coloca o produto na parte inferior dos resultados
- Desafixar um evento com um clique
![Novo](../assets/new.svg) [Classificação inteligente para regras](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/rules/rules-add)
O ![Novo](../assets/new.svg) [!DNL Live Search] agora oferece suporte aos recursos completos do [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) na Commerce (anteriormente conhecido como Inventário de Várias Source ou MSI). Para habilitar o suporte completo, você deve [atualizar](install.md#update) o módulo de dependência `commerce-data-export` para a versão 102.2.0+.

#### Atualizações

![Corrigir](../assets/fix.svg) Configurar regras agora classifica posições automaticamente de forma exclusiva
![Correção](../assets/fix.svg) Excluir um evento existente agora atualiza a visualização
![Corrigir](../assets/fix.svg) regras sem eventos podem ser salvas
![Correção](../assets/fix.svg) Remover o seletor &quot;Selecionar tipo&quot; de facetas
![Correção](../assets/fix.svg) Adição de um novo status de &quot;Edição&quot; para regras não salvas

#### Correções

![Corrigir](../assets/fix.svg) Corrigiu um erro de servidor quando havia um evento não concluído durante o salvamento
![Correção](../assets/fix.svg) Corrigida corretamente ao excluir um evento específico quando havia vários eventos
![Correção](../assets/fix.svg) Corrigido o evento de regra existente não sendo atualizado quando um novo evento foi adicionado
![Correção](../assets/fix.svg) Corrigido no segundo clique &quot;Editar&quot; dos detalhes, [!DNL Live Search] página que requer recarregamento
![Correção](../assets/fix.svg) Sinônimos: corrigiu um problema quando um usuário clicava fora da entrada, ele não podia retornar o foco para o campo
![Correção](../assets/fix.svg) Outras correções de pequenos erros e atualizações de desempenho
![Bug](../assets/bug.svg) - A classificação por &quot;Recomendado para você&quot; só tem suporte nos widgets do Live Search. Não é compatível com a funcionalidade de pesquisa padrão do Luma e do PWA.
![Bug](../assets/bug.svg) - As facetas de atributo de preço personalizado não são renderizadas corretamente no Luma, mas a API as filtra corretamente.

Os comerciantes devem atualizar a extensão [!DNL Live Search] versão >= 3.0.1 para acessar esses recursos.

É recomendável atualizar e testar antes de enviar para a produção. Considere atualizar o ambiente de produção fora do horário de pico após verificar os resultados do ambiente de teste.

### [!DNL Live Search] 2.0.5

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) - O Live Search geraria um erro quando os recursos do SDK não estivessem disponíveis devido a problemas de rede. Esse erro foi corrigido.

Os comerciantes devem atualizar a versão da extensão do Live Search >= 2.0.5 para acessar esses recursos.

É recomendável atualizar e testar antes de enviar para a produção. Considere atualizar o ambiente de produção fora do horário de pico após verificar os resultados do ambiente de teste.

### [!DNL Live Search] 2.0.4

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) O Live Search agora oferece suporte à filtragem pela configuração &#39;Produtos sem estoque exibido&#39; no administrador. Se &#39;Exibir Produtos sem Estoque&#39; estiver definido como falso, `inStock = true` será adicionado ao filtro.
![Correção](../assets/fix.svg) Para melhorar o desempenho, o bloco &#39;Sugestões&#39; foi removido do pop-up do Live Search. Os dados ainda são transmitidos pelo GraphQL, caso você queira substituir o recurso.
![Correção](../assets/fix.svg) `categories` e `categoryPath` substituíram `categoryIds` para filtragem de categoria. Leia mais no tópico [productSearch](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/).
![Correção](../assets/fix.svg) anteriormente, um usuário vinculado a uma empresa B2B receberia um Código de grupo de clientes incorreto ao fazer pesquisas. O Live Search agora retorna o valor correto.
![Correção](../assets/fix.svg) anteriormente, ao pesquisar um termo que não existe, o Live Search retornaria um erro. Esse erro foi corrigido.

Os comerciantes devem atualizar a versão da extensão [!DNL Live Search] >= 2.0.4 para acessar esses recursos.

Os usuários são aconselhados a atualizar e testar antes de enviar para a produção. Considere atualizar o ambiente de produção fora do horário de pico após verificar os resultados do ambiente de teste.

### [!DNL Live Search] 2.0.3

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) O Live Search agora oferece suporte a recursos B2B, respeitando permissões de categoria, catálogos compartilhados e preços específicos de grupos de clientes.

Os comerciantes devem atualizar a versão da extensão [!DNL Live Search] >= 2.0.3 para acessar esses recursos.

Os usuários são aconselhados a atualizar e testar antes de enviar para a produção. Considere atualizar o ambiente de produção fora do horário de pico após verificar os resultados do ambiente de teste.

### [!DNL Live Search] 2.0

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

As instalações existentes do [!DNL Live Search] devem ser atualizadas para o [!DNL Live Search] 2.0.0 para aproveitar os seguintes novos recursos, correções e melhorias:

![Novo](../assets/new.svg) [!DNL Live Search] agora dá suporte ao PHP 8.1 para instalações que executam o Adobe Commerce 2.4.4.
![Novo](../assets/new.svg) O módulo `Magento_ElasticsearchCatalogPermissionsGraphQl` é adicionado à lista de módulos que estão desabilitados durante a instalação.
![Novo](../assets/new.svg) O número de linhas disponíveis em [[!DNL storefront popover]](overview.md) pode ser configurado no *Administrador*.
![Novo](../assets/new.svg) Beta [PWA](https://developer.adobe.com/commerce/pwa-studio/) com suporte para [!DNL Live Search].
![Novo](../assets/new.svg) O processo de instalação do [!DNL Live Search] é atualizado com alterações avançadas no processo.
![Corrigir](../assets/fix.svg) link de [Pesquisa Avançada](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) removido do rodapé da loja.
![Bug](../assets/bug.svg) Os atributos de produto a seguir não têm suporte da [API do Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) quando usados em relação à versão beta do PWA: `description`, `name`, `short_description`
![Bug](../assets/bug.svg) A versão beta do PWA para [!DNL Live Search] não oferece suporte à [manipulação de eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/).

### [!DNL Live Search] 1.3.1

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Corrigir](../assets/fix.svg) [O atributo de preço personalizado](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) não retorna mais um erro quando configurado como [faceta](facets-add.md).
![Correção](../assets/fix.svg) Corrigido um problema que causava um erro quando nenhum [símbolo de moeda](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration#step-5-customize-currency-symbols-optional) (`data-currency-symbol`) estava disponível.
![Correção](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) agora mostra o [Preço Especial](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-special) (preço final mínimo) quando disponível.

### [!DNL Live Search] 1.3.0

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

O painel de relatórios ![Novo](../assets/new.svg) [Desempenho](performance.md) fornece à insight termos de pesquisa que os compradores usam.
![Novo](../assets/new.svg) [!DNL Live Search] [O Storefront Events SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) fornece acesso a uma camada de dados comum com métricas e serviços de assinatura e publicação de eventos.
![Correção](../assets/fix.svg) [[!DNL Storefront popover]](storefront-popover.md) tem uma nova classe `active` para o contêiner `.search-autocomplete` que controla a visibilidade.
![Correção](../assets/fix.svg) Na loja, o link de rodapé [Termos de Pesquisa](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-terms) foi removido e seu cache foi desabilitado para instalações de [!DNL Live Search].
![Bug](../assets/bug.svg) O Patch para o Adaptador de Pesquisa processa produtos duplicados.
![Bug](../assets/bug.svg) [!DNL Live Search] dá suporte a [locais de estoque (físico) de ](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/sources/sources-manage) de origem única com vários [estoques](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/stocks/stocks-manage) (virtuais). Agora, não há suporte para várias fontes de inventário.

### [!DNL Live Search] 1.2.0

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) [[!DNL Storefront popover]](storefront-popover.md) exibe os produtos sugeridos e as imagens em miniatura dos principais resultados da pesquisa à medida que os compradores digitam as consultas na caixa Pesquisa.
A sessão ![Nova](../assets/new.svg) do *Administrador* do Commerce permanece aberta durante longos períodos de inatividade do teclado
![Novo](../assets/new.svg) [!DNL Live Search] é habilitado automaticamente após a integração
![Correção](../assets/fix.svg) O tempo de indexação inicial é de menos de uma hora
![Correção](../assets/fix.svg) Atualizações incrementais do produto quase em tempo real (após instalação e instalação)
![Correção](../assets/fix.svg) Colunas classificáveis no editor de sinônimos
![Correção](../assets/fix.svg) [!DNL Live Search] não gera mais um erro se os critérios de pesquisa contiverem valores vazios de ordem de classificação
![Correção](../assets/fix.svg) A filtragem de intervalo não é mais interrompida se os códigos de atributo contiverem cadeias de caracteres &quot;para&quot; ou &quot;de&quot;

### [!DNL Live Search] 1.1.0

[!BADGE Com suporte]{type="Informative" tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Bug](../assets/bug.svg) O serviço [!DNL Live Search] dá suporte apenas à [moeda base](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) da instalação do Adobe Commerce.
![Bug](../assets/bug.svg) Ao adicionar uma faceta, o Feed de Atributos do Produto não é atualizado corretamente quando definido como `Update on Save`. Para evitar este problema, vá para [Gerenciamento de Índice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) e defina o Feed de Atributos do Produto como `Update by Schedule`.
Os sinônimos ![Bug](../assets/bug.svg) [!DNL Live Search] são definidos por exibição de armazenamento, mas estão armazenados por site no momento e identificados com uma combinação de `environmentId` e `storeViewCode`. Como resultado, todos os sites e exibições de armazenamento na instalação do Adobe Commerce compartilham sinônimos. O conjunto de sinônimos criado mais recentemente para a exibição de loja tem prioridade.
![Bug](../assets/bug.svg) Se um termo sinônimo contiver várias palavras, cada palavra será tratada como um sinônimo separado. Por exemplo, se você definir &quot;peça de tempo&quot; como um sinônimo de &quot;relógio&quot;, tanto &quot;tempo&quot; quanto &quot;peça&quot; serão tratados como sinônimos de relógio.

+++

## Documentação

Para saber mais:

- [Documentação do desenvolvedor do Adobe Commerce](https://developer.adobe.com/commerce/docs)
- [Guia do Usuário do Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce)
- [[!DNL Live Search] no Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html)
