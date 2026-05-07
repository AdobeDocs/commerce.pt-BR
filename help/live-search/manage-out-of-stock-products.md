---
title: Gerenciar Produtos Sem Estoque em  [!DNL Live Search]
description: Saiba como gerenciar produtos indisponíveis no [!DNL Live Search] for Adobe Commerce. Configure a exibição do inventário, o filtro do InStock e a filtragem da API do GraphQL.
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Gerenciar produtos indisponíveis

Você pode controlar como os produtos indisponíveis são exibidos em [!DNL Live Search] resultados de pesquisa e categoria usando a configuração de inventário, filtros de tempo de consulta e sinalizadores de recursos de back-end opcionais. Essas opções têm limites importantes, que este tópico explica.

## Filtros de status do estoque

O atributo de estoque do Adobe Commerce `quantity_and_stock_status` não tem suporte como uma faceta e não aparece na caixa de diálogo **[!UICONTROL Add Facet]**. No entanto, [!DNL Live Search] expõe um campo `inStock` que você pode usar como filtro no momento da consulta.

## Ocultar produtos indisponíveis

Use uma das seguintes abordagens para ocultar produtos indisponíveis.

### Configuração do Commerce

1.No *Administrador*, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**.

1.Defina **[!UICONTROL Display Out of Stock Products]** como **[!UICONTROL No]**.

1. Clique em **[!UICONTROL Save Config]**.

Quando **[!UICONTROL Display Out of Stock Products]** está definido como `No`, [!DNL Live Search] adiciona `inStock = 'no` às consultas de vitrine através do widget PLP, assim os produtos indisponíveis não são retornados.

### Filtro de API

Ao chamar a API [!DNL Live Search] diretamente (GraphQL ou REST), filtre explicitamente os produtos indisponíveis, por exemplo:

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

Use esta abordagem quando você não encaminhar a solicitação pelo [Widget PLP do Live Search](plp-styling.md).

### Mostrar resultados esgotados após em estoque

Para manter os produtos indisponíveis no conjunto de resultados, mas sempre após os produtos em estoque ao classificar por relevância, o Adobe pode ativar um sinalizador de recurso interno para seu ambiente.

- Este sinalizador de recurso não está exposto na interface do usuário do Administrador [!DNL Live Search].
- Para solicitar, [entre em contato com o Suporte da Adobe](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"} e consulte o recurso para mover produtos indisponíveis para o final dos resultados da pesquisa.

>[!NOTE]
>
>Depois que o sinalizador é habilitado, qualquer produto indisponível restante no conjunto de resultados é movido para o final ao classificar por *Relevância*. Outras ordens de classificação (por exemplo, *Preço* ou *Nome do produto*) não serão afetadas.

### Pesquisar regras de merchandising e ações

As regras de merchandising de pesquisa se baseiam em consultas e têm como alvo produtos individuais, não grupos inteiros por estado de estoque ou valor de faceta:

- As condições da regra dependem somente da frase de pesquisa do comprador (`Query is`, `Query contains`, `Query starts with`, `Query ends with`).
- Os eventos de regra (Aumentar, Enterrar, Fixar, Ocultar) se aplicam a uma SKU por evento.

Por causa dessas restrições:

- Não é possível criar uma regra que enterra ou oculta todos os produtos esgotados com base somente no status do estoque.
- Você pode ocultar ou enterrar manualmente SKUs específicas adicionadas como eventos em uma regra (sujeito a limites de 50 regras e 25 eventos por regra).

Para ocultar ou priorizar produtos indisponíveis no catálogo, use a configuração de estoque e o filtro `inStock` (e o sinalizador de recurso opcional) descritos neste tópico, em vez das regras de Merchandising de Pesquisa.

>[!MORELIKETHIS]
>
> - [Pesquisar regras de merchandising](rules.md)
> - [Configurar as opções globais do Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/configuration)
