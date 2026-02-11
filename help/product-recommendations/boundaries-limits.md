---
title: Limites e limites
description: Saiba mais sobre os limites do  [!DNL Product Recommendations]  para garantir que ele atenda às necessidades da sua empresa.
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Limites e limites

Revise os limites e limites a seguir para garantir que o [!DNL Product Recommendations] atenda às necessidades da sua empresa. Entender essas restrições ajuda a planejar a implementação, configurar filtros e evitar problemas comuns.

## Geral

- **Tipos de produtos** - Os tipos de produtos compatíveis incluem _simple_, _configurable_, _virtual_, _downloadable_ e _vale-presente_. Não há suporte para _Pacotes_, _agrupados_ e tipos de produtos personalizados. Se seu catálogo contiver um grande número de tipos de produtos não suportados, você pode esperar uma baixa [pontuação de preparação](create.md#readiness-indicators). Consulte [Filtrar por tipo de produto](filters.md#type).
- **SKUs com espaços** - SKUs que contêm espaços podem reduzir a relevância da recomendação e devem ser evitadas quando possível.
- **Página de carrinho** - Recomendações de produto não têm suporte na página de carrinho quando a loja está configurada para [exibir a página do carrinho de compras imediatamente após adicionar um produto ao carrinho](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). Consulte [Criar recomendações](create.md).
- **Produtos secundários** - Os produtos secundários de um produto configurável (visibilidade _Não visível individualmente_) não são exibidos em uma unidade de recomendação. Somente o produto configurável (principal) pode ser exibido. Consulte [Filtrar produtos](filters.md#product).
- **Produtos desabilitados ou não visíveis** - Os produtos desabilitados ou não visíveis individualmente nunca podem aparecer nas recomendações e não podem ser selecionados nos filtros de produto.
- **Preços especiais** - [Preços especiais](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/products/pricing/product-price-special) com datas de início e término não são suportados em unidades de recomendação. Um produto com um preço especial pode aparecer nas recomendações, mas a unidade não exibe o preço especial, a data inicial ou a data final. Os compradores veem o preço normal (ou outros dados de preço fornecidos pelo seu catálogo/feed de preço) até abrirem a página do produto.

## Unidades de recomendação

- **Unidades ativas por tipo de página** - Você pode criar até 50 unidades de recomendação ativas para cada tipo de página (Página inicial, Categoria, Detalhes do produto, Carrinho, Confirmação). O tipo de página fica esmaecido no fluxo de criação quando o limite é atingido.
- **Produtos por unidade** - O número de produtos exibidos em uma unidade de recomendação pode ser definido de 5 (padrão) a no máximo 20.
- **Estado do rascunho** - Depois de salvar uma recomendação como rascunho, você não poderá modificar o tipo de página ou de recomendação para essa unidade. Outras configurações podem ser editadas antes da ativação.

## Filtros e condições

- **Condições dinâmicas** - Condições dinâmicas (como &quot;produtos na mesma categoria do produto atual&quot; ou &quot;intervalo de preços relativo&quot;) estão disponíveis em todos os tipos de página, exceto na Página inicial. Elas também não estão disponíveis nas páginas em que as recomendações são colocadas com o Page Builder. Consulte [Condições](filters.md#conditions).

## Ambientes de visualização e não produção

- **Visualização visualizada recentemente** - O tipo de recomendação _Visualizado recentemente_ não pode ser visualizado no Administrador porque os dados se baseiam no histórico do navegador e não estão disponíveis no contexto de Administrador. Consulte [Visualizar recomendações](create.md#preview).
- **Recomendações de outro espaço de dados** - Quando você [buscar recomendações de um espaço de dados SaaS diferente](settings.md) (por exemplo, produção) em uma loja de não produção, poderá exibir as recomendações, mas não poderá clicar nelas para acessar as páginas do produto. Isso ocorre por design para visualização e teste.
- **Espaço de dados alternativo e do GraphQL** - Ao usar Recomendações de Produto via [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/), o parâmetro `alternateEnvironmentId` (usado para buscar recomendações de outro espaço de dados) não está disponível. Use a REST API ou as Configurações do administrador para alternar a origem das recomendações em caso de não produção.

## API e configuração

- **Chaves de API (4.x e superior)** - Você deve fornecer chaves de API públicas e privadas para os ambientes de sandbox e produção. Se você não fornecer ambos os pares de chaves de API, não poderá acessar o recurso Recomendações de produto no Admin. A coleta de dados na loja e as recomendações existentes continuam funcionando. Consulte [Instalar e configurar](install-configure.md).

## Restrições de cookie

- Quando o [modo de restrição de cookies](setting-cookie.md) está habilitado e os compradores não aceitaram cookies, alguns tipos de recomendação que dependem de dados comportamentais podem não ser exibidos ou mostrar resultados limitados.
- Os tipos de recomendação que não dependem de dados comportamentais (por exemplo, _Mais visualizados_, _Semelhança visual_) continuam a funcionar quando as restrições de cookie são habilitadas.
- Quando as restrições de cookies são ativadas, as Recomendações de produto não coletam nem armazenam dados comportamentais em cookies ou armazenamento local até que o comprador dê o seu consentimento.

## Page Builder

- **Métricas e exibições de armazenamento** - As métricas das unidades de recomendação do Page Builder aparecem somente na exibição de armazenamento padrão no espaço de trabalho Recomendações do produto. Para ver as métricas de recomendação do Page Builder em uma exibição de armazenamento não padrão, abra e [edite](edit.md) a unidade de recomendação do Page Builder na exibição de armazenamento e salve-a; as métricas serão exibidas na exibição de armazenamento. Consulte [Integração do Page Builder](page-builder.md).

## B2B

- As Recomendações de produto respeitam as [permissões de categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), os [catálogos compartilhados](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) e os preços específicos do grupo de clientes. Os compradores veem apenas recomendações de produtos que podem ser acessados de acordo com a atribuição de segmento e catálogo. Consulte [Integração](onboarding.md).

## Dados e disponibilidade

- **Dados comportamentais** - Muitos tipos de recomendações exigem dados comportamentais de vitrine suficientes (exibições, adicionar ao carrinho, compras). Novos armazenamentos ou armazenamentos de tráfego baixo podem ver resultados limitados ou inexistentes para esses tipos até que os dados adequados sejam coletados. Monitorar [indicadores de preparação](create.md#readiness-indicators) no Administrador.
- **Preparo sem dados de produção** - Em um ambiente de não produção sem dados comportamentais, o único tipo de recomendação que você pode testar sem buscar dados de produção é o _Mais semelhante a este_, que usa somente similaridade baseada em catálogo. Consulte [Ambiente de preparo](staging-environment.md).

## Solução de problemas

Para obter ajuda com a sincronização do catálogo, com a não exibição de recomendações ou com outros problemas comuns, pesquise a [Base de Dados de Conhecimento Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/overview) ou contate o [suporte](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
