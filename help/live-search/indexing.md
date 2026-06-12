---
title: Indexação
description: Saiba como o  [!DNL Live Search] indexa propriedades de atributos de produto.
exl-id: 01cbbf56-2e12-4ad0-a56d-de0fe13df50f
TQID: https://experienceleague.adobe.com/8STop-AunMGpKCLgjQaywtpPRNHF-l7sobRnh82QOXI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: f7ea996f3adcd3beb2a9c064ce57d251f49ae5b3
workflow-type: tm+mt
source-wordcount: 812
ht-degree: 0%

---

# Indexação

O processo de indexação do [!DNL Live Search] lê o catálogo de atributos do produto e cria um índice para que os produtos possam ser pesquisados, filtrados e apresentados rapidamente.

As propriedades do atributo de produto (metadados) determinam:

* Como um atributo pode ser usado no catálogo
* Sua aparência e comportamento na loja
* Os dados incluídos nas operações de transferência de dados

O escopo dos metadados do atributo é `website/store/store view`.

A API [!DNL Live Search] permite que um cliente classifique por qualquer atributo de produto que tenha a `Use in Search` ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) [propriedade de vitrine definida como `Yes` no Administrador do Adobe Commerce. Quando habilitado, `Search Weight` pode ser definido para o atributo.

[!DNL Live Search] não indexa produtos excluídos ou produtos definidos como `Not Visible Individually`.

>[!NOTE]
>
> Os clientes da Commerce com [!DNL Live Search] podem aproveitar as vantagens das atualizações de alterações de preço e do tempo de sincronização mais rápidos em seus sites com o [indexador de preços SaaS](../price-index/price-indexing.md).

## Pipeline de indexação

O cliente chama o serviço de pesquisa da loja para recuperar (filtrável, classificável) os metadados do índice. O serviço de pesquisa pode chamar apenas atributos de produto pesquisáveis com a propriedade *Usar na Navegação em Camadas* definida como `Filterable (with results)` e *Usar para Classificação na Listagem de Produtos* definida como `Yes`.

Para construir uma consulta dinâmica, o serviço de pesquisa precisa saber quais atributos podem ser pesquisados e seus [weight](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results). [!DNL Live Search] respeita os pesos de pesquisa do Adobe Commerce (1-10, onde 10 é a prioridade mais alta). A lista de dados sincronizados e compartilhados com o serviço de catálogo pode ser encontrada no schema, que é definido em:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

Para entender como os atributos e pesos pesquisáveis interagem com a correspondência **exata**, **próxima**, de mesmo campo e entre campos no momento da consulta, consulte [Correspondência e classificação de pesquisa](search-relevance-matching.md).

![[!DNL Live Search] diagrama de pesquisa de cliente de indexação](assets/indexing-pipeline.svg)

1. Verifique se o comerciante tem o direito de [!DNL Live Search].
1. Obtenha exibições da loja com alterações nos metadados do atributo.
1. Armazenar atributos de indexação.
1. Reindexe o índice de pesquisa.

### Índice completo

Quando o [!DNL Live Search] é configurado e sincronizado durante a integração, pode levar até 60 minutos para criar o índice inicial. Catálogos grandes podem levar mais tempo para serem indexados. O processo começa depois que `cron` envia o feed e termina a execução.

Os seguintes eventos acionam uma criação de índice e sincronização completa:

* Integrando [sincronização de dados de catálogo](install.md#sync)
* Alterações nos metadados do atributo

Por exemplo, alterar a propriedade `Use in Search` do atributo `color` de `No` para `Yes` altera os metadados do atributo para `searchable=true` e dispara uma sincronização completa e reindexação. Os metadados de atributo a seguir acionam uma sincronização completa e reindexação quando alterados:

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### Streaming de atualizações de produto

Depois que o índice inicial for criado durante a [integração](install.md#sync), as seguintes atualizações de produtos incrementais serão continuamente sincronizadas e reindexadas:

* Novos produtos adicionados ao catálogo
* Alterações nos valores de atributo de produto

Por exemplo, adicionar um novo valor de amostra ao atributo `color` é manipulado como uma atualização de produto de streaming.

Fluxo de trabalho de atualização de transmissão:

1. Os produtos atualizados são sincronizados da instância do Adobe Commerce para o serviço de catálogo.
1. O serviço de indexação procura continuamente atualizações de produtos no serviço de catálogo. Os produtos atualizados são indexados à medida que chegam ao serviço de catálogo.
1. Pode levar até 15 minutos para uma atualização de produto ficar disponível no [!DNL Live Search].

#### Atualizações que afetam a visibilidade do produto

Quando você atualiza as configurações do administrador do [!DNL Live Search], as configurações do administrador do Adobe Commerce ou as atualizações dos dados do catálogo, pode esperar um atraso antes que essas alterações apareçam na loja.

A tabela a seguir descreve várias alterações e o tempo de espera aproximado antes que elas apareçam na loja.

| Atualizações | Atraso até que fique visível na loja |
|---|---|
| [!DNL Live Search] Alterações do administrador em facetas, configurações de preço, pesquisa ou regras de merchandising de categoria. | 15-20 minutos. |
| [!DNL Live Search] Alterações de administrador que exigem reindexação: configurações de idioma ou sinônimos. | Até 15 minutos após a conclusão da reindexação. |
| Alterações no administrador do Adobe Commerce que exigem uma reindexação completa: metadados de atributos pesquisáveis, classificáveis ou filtráveis | Até 15 minutos após a conclusão da reindexação. |
| Alterações incrementais nos dados do catálogo que não precisam de reindexação: inventário de produto, preço, nome e assim por diante. | Até 15 minutos após a atualização do índice de Pesquisa Elástica com os dados mais recentes. |

## Pesquisa de cliente

A API [!DNL Live Search] permite que um cliente classifique por qualquer atributo de produto classificável definindo a [propriedade de vitrine](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes), *Usada para classificar nas listagens de produtos* a `Yes`. Dependendo do tema, essa configuração faz com que o atributo seja incluído como uma opção no controle de paginação [Classificar por](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation) em páginas de catálogo. Até 200 atributos de produto podem ser indexados por [!DNL Live Search], com [propriedades de vitrine](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) que podem ser pesquisadas e filtradas.

Os metadados do índice são armazenados no pipeline de indexação e podem ser acessados pelo serviço de pesquisa.

![[!DNL Live Search] diagrama da API de metadados do índice ](assets/index-metadata-api.svg)

### Fluxo de trabalho de atributo classificável

1. O cliente chama o serviço de pesquisa.
1. O serviço de pesquisa chama o Serviço de administração de pesquisa.
1. O serviço de pesquisa chama o pipeline de indexação.

## Indexado para todos os produtos

A ordem dos campos nesta lista reflete a ordem típica das colunas nos dados do produto exportados.

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

O campo a seguir é indexado para todos os produtos configuráveis:

* `childrenSkus`
