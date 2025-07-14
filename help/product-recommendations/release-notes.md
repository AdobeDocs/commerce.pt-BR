---
title: Notas de versão do [!DNL Product Recommendations]
description: As informações da versão mais recente do  [!DNL Product Recommendations] Adobe Commerce.
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 0d69d893d616a5e75ee264ebc652f3793a359486
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 0%

---

# Notas de versão do [!DNL Product Recommendations]

As notas de versão contêm atualizações para os seguintes [!DNL Product Recommendations] módulos:

* [!DNL Product Recommendations] metapackage: `magento/product-recommendations`
* Suporte ao Page Builder no módulo [!DNL Product Recommendations] (opcional): `magento/module-page-builder-product-recommendations`
* Suporte a tipo de recomendação de similaridade visual para o módulo [!DNL Product Recommendations] (opcional): `magento/module-visual-product-recommendations`

O suporte é fornecido para a versão principal atual lançada. As notas de versão para versões mais antigas são fornecidas para referência.
As notas de versão incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos

Consulte a documentação do desenvolvedor para [saber mais sobre o suporte ao produto](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Atualizações do serviço hospedado

Essas notas descrevem atualizações ou problemas conhecidos que foram publicados ou descobertos fora de uma versão com versão ou de melhorias no serviço hospedado.

_31 de janeiro de 2025_

![Novo](../assets/new.svg) Há uma nova política de retenção de dados para dados de catálogo não consultados em seu ambiente de teste. [Saiba mais](overview.md#catalog-data-retention-policy).

_28 de junho de 2024_

![Bug](../assets/bug.svg) Os produtos adicionados ao carrinho a partir de uma unidade [!DNL Product Recommendations] na página do carrinho não são removidos da lista de produtos recomendados quando a página do carrinho é recarregada.
![Bug](../assets/bug.svg) Os produtos removidos do carrinho continuam a persistir na matriz `cartSkus` até que a página do carrinho seja recarregada.

_18 de julho de 2023_

![Novo](../assets/new.svg) [!DNL Product Recommendations] agora tem uma consulta GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/).

_25 de abril de 2023_

![Novos](../assets/new.svg) clientes do [!DNL Product Recommendations] agora podem aproveitar a [indexação de preços do SaaS](../price-index/price-indexing.md).

## Versão principal atual

### 6.2.1 do magento/product-recommendations

_14 de julho de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Aprimoramentos feitos no painel [recomendações de visualização](./create.md#preview-recommendations).

### Versões anteriores

### 6.2.0 do magento/product-recommendations

_4 de abril, 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Atualizou as URLs CDN de `recommendations-admin-ui` para o domínio `adobe.io`.

### 6.1.0 do magento/product-recommendations

_11 de março de 2025_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) adicionou suporte ao PHP 8.4.

### 6.0.3 do magento/product-recommendations

_6 de novembro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Corrigido um problema no qual o [filtro de categoria](filters.md#category) incluía categorias que não pertenciam à loja atual.
![Correção](../assets/fix.svg) Corrigiu um problema de dependência no metapackage `magento/product-recommendations`.

### 6.0.2 do magento/product-recommendations

_9 de maio de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) Corrigido um problema no qual um clique no botão **[!DNL Add to Cart]** em um produto simples dentro de uma unidade do Product Recommendations redirecionava o comprador para a home page em vez de permanecer na página atual.
![Bug](../assets/bug.svg) Há um erro de validação causado pelo elemento `referenceBlock` no arquivo XML `ProductRecommendations Layout`.

### 6.0.1 do magento/product-recommendations

_19 de março de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) adicionou suporte ao PHP 8.3.

### 6.0.0 do magento/product-recommendations

_22 de fevereiro de 2024_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) [!DNL Catalog Sync Dashboard] agora é [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Este painel renovado fornece informações sobre fluxos de dados para [!DNL Product Recommendations], [!DNL Live Search] e [!DNL Catalog Service].
![Correção](../assets/fix.svg) Corrigido um problema que causava erros de check-out para [!DNL Product Recommendations].

+++5.0.0 e anteriores

### 5.0.1 do magento/product-recommendations

_15 de setembro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adição de novos módulos para dar suporte ao [Indexador de Preços Saas](../price-index/price-indexing.md).
![Novo](../assets/new.svg) Foram adicionados novos módulos de exportação de dados para oferecer suporte à exportação de mais tipos de produtos, incluindo produtos agrupados e cartões-presente.
![Correção](../assets/fix.svg) O tamanho da tabela dos feeds Produtos e Preço foi bastante reduzido. As tabelas `catalog_data_exporter_products` e `catalog_data_exporter_product_prices` devem ver uma redução substancial no tamanho.

#### Limitações conhecidas

* O valor `websiteCode` será retornado incorretamente se contiver um sublinhado (_).

### 5.0.0 do magento/product-recommendations

_20 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Atualizado em [!DNL Product Recommendations] para oferecer suporte ao Adobe Commerce 2.4.6.
![Novo](../assets/new.svg) Esta é uma versão principal. [Edite](install-configure.md#update) o arquivo `composer.json` raiz do seu projeto.
Os ![Novos](../assets/new.svg) [!DNL Product Recommendations] agora oferecem suporte aos recursos completos do [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) na Commerce (anteriormente conhecido como Inventário de Várias Source, ou MSI). Para habilitar o suporte completo, você deve [atualizar](install-configure.md#update) o módulo de dependência `commerce-data-export` para a versão 102.2.0+.

### 4.0.1 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Correção](../assets/fix.svg) anteriormente, [!DNL Product Recommendations] mostraria um erro quando a moeda de exibição fosse trocada por uma moeda não padrão. A troca de moedas agora funciona corretamente.

### 4.0.0 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.4 e mais recentes

![Novo](../assets/new.svg) Adicionados [indicadores de disponibilidade](create.md) para ajudá-lo a visualizar o progresso do treinamento de cada tipo de recomendação.
![Novo](../assets/new.svg) Esta é uma versão principal. [Edite](install-configure.md#update) o arquivo `composer.json` raiz do seu projeto. Esta versão também requer que você forneça duas chaves de API ao instalar e configurar o [!DNL Product Recommendations]: [uma chave de produção e uma chave de sandbox](../landing/saas.md).

#### Limitações conhecidas

* O valor `websiteCode` será retornado incorretamente se contiver um sublinhado (_).

### 3.3.7 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) adicionou suporte ao PHP 8.1
![Novo](../assets/new.svg) redimensionamento de imagem aprimorado para que o dimensionamento de imagens seja tratado de forma mais consistente no modelo de exibição de referência

### 3.3.6 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) otimizou o metapackage [!DNL Product Recommendations] listando explicitamente as dependências

### 3.3.5 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Adicionado [suporte B2B](onboarding.md#b2bsupport) em [!DNL Product Recommendations]
![Novo](../assets/new.svg) Adicionou novos feeds a [sincronizar dados de catálogo](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) com os Serviços Commerce através da linha de comando

### 3.3.3 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Adicionado aos novos [tipos de recomendação](type.md): Conversão (exibir para carrinho), Conversão (exibir para compra) e Visualizado recentemente. Esses novos tipos de recomendações estão disponíveis no `magento/product-recommendations` módulo 3.2.2 e posterior.
![Correção](../assets/fix.svg) Corrigido um problema no qual o WAF (Web Application Firewall) do Fastly bloqueava incorretamente um cookie
![Correção](../assets/fix.svg) Corrigido um problema no qual os produtos atribuídos ao Modo de Exibição de Loja não padrão não eram exibidos no painel _Visualização de Produto do Recommendations_ ao criar uma recomendação para esse Modo de Exibição de Loja específico
![Correção](../assets/fix.svg) Corrigido um problema no qual certos nomes de unidades de recomendação no Page Builder impediam que a unidade de recomendação fosse exibida na loja

### 3.3.2 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Corrigida a dependência ausente para suporte B2B

### 3.3.1 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para preços de grupo de clientes B2B. Ao definir um [filtro de preço](filters.md) em uma unidade de recomendação, os clientes B2B que estão conectados verão o conjunto de preços do grupo de clientes para os produtos exibidos.

### 3.3.0 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) adição de suporte à Camada de dados de clientes Adobe para padronizar a coleta de dados comportamentais entre os recursos e serviços da Adobe Commerce. Consulte o [readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md) para saber mais.

### 3.2.6 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Corrigiu um erro modal de JavaScript
![Correção](../assets/fix.svg) Corrigido um problema no qual o WAF (Web Application Firewall) do Fastly bloqueava incorretamente um cookie

### 3.2.5 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Magento Services renomeados para [Commerce Services](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) e usabilidade aprimorada no Administrador

### 3.2.4 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Corrigido o erro &quot;Não é possível recuperar dados de opções do produto configuráveis&quot; ao indexar atributos do produto

### 3.2.3 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Corrigido o erro &quot;Não é possível recuperar dados de opções do produto configuráveis&quot; durante a Sincronização do Catálogo
![Correção](../assets/fix.svg) Corrigido um problema no qual o código de armazenamento não estava sendo definido corretamente quando você habilitou a configuração &quot;Adicionar código de armazenamento à URL&quot;
![Correção](../assets/fix.svg) Detecção aprimorada de alterações de configuração do Painel de Administração para garantir que essas alterações sejam refletidas nos dados de Sincronização do Catálogo

### 3.2.2 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Adicionou a capacidade de [visualizar os resultados da recomendação](create.md) no momento da criação. Isso pode exigir que você atualize seu módulo para a versão mais recente.
![Novo](../assets/new.svg) Adicionou a capacidade de [monitorar e gerenciar](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) o processo de sincronização de catálogo do Administrador.
![Novo](../assets/new.svg) Adicionados [filtros](filters.md) para controlar quais produtos são exibidos nas recomendações.
![Novo](../assets/new.svg) Adicionou o tipo de recomendação [Semelhança visual](type.md#visualsim).

### 1.2.1 do magento/module-page-builder-product-recommendations para o Page Builder

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Suporte adicionado para a versão 3.2.0+ do módulo `magento/product-recommendations`

### 3.1.0 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Adicionou a capacidade de [ressincronizar](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) seu catálogo para serviços SaaS por meio da linha de comando.
![Novo](../assets/new.svg) Suporte adicionado para prefixos de tabela de banco de dados
![Correção](../assets/fix.svg) removeu o suporte ao PHP 7.1

### 3.0.8 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Corrigido um problema no qual eventos eram enviados para coleta de dados antes da configuração do módulo, causando tráfego inválido

### 3.0.6 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) **(Beta)** Inclui suporte para o novo tipo de recomendação [Semelhança visual](type.md#visualsim).

### 1.0.0 do magento/module-visual-product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) **(Beta)** [Similaridade visual](type.md#visualsim). Com o tipo de recomendação _Similaridade visual_, você pode implantar uma unidade de recomendação na página de detalhes do produto que exiba produtos visualmente semelhantes ao produto que está sendo visualizado.

### 3.0.5 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Corrigido o erro &quot;Não é possível recuperar dados de opções do produto&quot; que poderia ocorrer durante a exportação do catálogo.
![Correção](../assets/fix.svg) O símbolo de moeda na coluna _Receita_ do painel _[!DNL Product Recommendations]_agora reflete corretamente a moeda base configurada.

### 3.0.4 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Suporte adicionado para o Adobe Commerce 2.4.0

### 3.0.3 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Correção](../assets/fix.svg) Implementação de símbolo aprimorada no modelo de vitrine

### 1.0.4 do magento/module-page-builder-product-recommendations para o Page Builder

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Adição do nome de recomendação do produto ao editar o tipo de conteúdo do Page Builder

### 3.0.2 magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) Adicionou uma coluna de status na grade ao selecionar unidades de recomendação no Page Builder
![Correção](../assets/fix.svg) Corrigido um problema com protocolos http/https incorretos em URLs de produtos e imagens

### 3.0.1 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

Esta é uma versão principal. [Edite](install-configure.md#update) o arquivo composer.json raiz do seu projeto.

![Novo](../assets/new.svg) Buscar [!DNL Product Recommendations] de Espaços de Dados SaaS alternativos. Isso permite que você use o [!DNL Product Recommendations] computado no seu ambiente de produto em outros ambientes que não sejam de produção. [Alternar Espaços de Dados SaaS](settings.md) descreve esse recurso.

![Correção](../assets/fix.svg) Corrigido um problema no qual o check-out era inibido para compradores que usavam o uBlock Origin
![Correção](../assets/fix.svg) corrigido um problema ao enviar eventos irrelevantes de adição ao carrinho

### 1.0.3 do magento/module-page-builder-product-recommendations para o Page Builder

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Novo](../assets/new.svg) suporte ao Page Builder. Com a integração do Page Builder, você pode colocar unidades de recomendação de maneira precisa e granular em qualquer local arbitrário no conteúdo criado pelo Page Builder. Também é possível estilizar os cabeçalhos e as próprias unidades de recomendação. Acesse [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) para obter mais informações.

### 2.0.0 do magento/product-recommendations

[!BADGE Com suporte]{type=Informative tooltip="Compatível"} Adobe Commerce versões 2.4.x e mais recentes

![Nova](../assets/new.svg) Versão de disponibilidade geral!

+++

## Documentação

Para saber mais sobre o desenvolvimento de [!DNL Product Recommendations] e [!DNL Product Recommendations]:

* [Guia do usuário](overview.md)
* [Documentação do desenvolvedor](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
