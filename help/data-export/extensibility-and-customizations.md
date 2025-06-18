---
title: Estender e personalizar dados do feed de exportação de dados SaaS
description: Saiba como estender e personalizar os dados do feed  [!DNL SaaS Data Export] .
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Estender e personalizar dados do feed de exportação de dados SaaS

A extensão [!DNL Commerce Data Export] fornece uma maneira de exportar dados do aplicativo [!DNL Commerce] para os Serviços da Commerce, como o Live Search, o Serviço de Catálogo e as Recomendações de Produto. Se necessário, você pode estender e personalizar os dados do feed para incluir dados de atributo adicionais ou modificar os dados coletados.

Depois de adicionar dados de atributo, ele pode ser acessado no [campo de atributos](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) do esquema GraphQL para o serviço de vitrine.

>[!NOTE]
>
>A adição ou modificação de dados de feed pode afetar o desempenho e a lógica de processamento no back-end do Commerce. Teste o código personalizado antes de mesclar com a produção. Em vez de adicionar dados ao backend, use a API Mesh para estender o esquema do GraphQL do Serviço de catálogo. Para obter detalhes sobre a configuração, consulte [Serviço de Catálogo e API Mesh](../catalog-service/mesh.md).

## Estender dados de atributos do sistema no feed de produtos

O feed de produtos inclui atributos de sistema padrão que são necessários para o processamento do produto ou que são usados com frequência pelos consumidores. Você pode incluir atributos de sistema adicionais no feed de produtos adicionando-os ao feed.

Para concluir esta tarefa, atualize o módulo `magento/catalog-data-exporter` para adicionar os atributos de sistema adicionais ao [arquivo de configuração de injeção de dependência](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`).

Adicione os atributos à consulta de Atributo de Produto (`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`).

**Exemplo**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Adicionar atributos do produto ao Adobe Commerce

Os desenvolvedores podem adicionar atributos de produto que podem ser acessados no [campo de atributos de produto](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields) usando um dos seguintes métodos:

- Adicione o atributo ao Adobe Commerce para inclusão nos dados de feed `products` exportados para os serviços da loja da Commerce.
- Adicione o atributo dinamicamente durante o processo de sincronização de feed usando um plug-in.

### Adicionar o atributo ao Adobe Commerce

Você pode adicionar um atributo de produto do Commerce Admin ou programaticamente usando um módulo PHP personalizado para definir o atributo e atualizar o Adobe Commerce. Adicionar o atributo do administrador do Commerce é o método mais simples, pois você pode adicionar o atributo e todos os metadados necessários de uma só vez. O novo atributo e suas propriedades de metadados são exportados para os serviços SaaS automaticamente durante a próxima sincronização programada.

#### Criar o atributo de produto do Administrador

1. No Administrador do Commerce, crie o atributo na página de configuração de atributo do produto ([!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]).

1. Adicione o atributo a um conjunto de atributos, conforme necessário.

Consulte [Criar atributos de produto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) no *Guia de Administração do Adobe Commerce*.

#### Criar o atributo de produto de forma programática

Adicione um atributo de produto de forma programática criando um patch de dados que implemente o `DataPatchInterface` e instancie uma cópia da classe `EavSetup Factory` dentro do construtor para configurar as opções de atributo.

Quando você define as opções de atributo, todos os parâmetros de atributo exceto `type`, `label` e `input` são opcionais. Defina os seguintes parâmetros adicionais e outros que diferem das configurações padrão.

- **`user_defined`=`1`**—Exporta o atributo para serviços de vitrine durante a sincronização de dados
- **`used_in_product_listing`=`1`** — Tornar o atributo acessível na consulta do banco de dados da lista de produtos

Para obter informações sobre como criar patches de dados, consulte [Desenvolver patches de dados e esquemas](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) no *Guia do Desenvolvedor do PHP*.

### Adicionar o atributo de produto dinamicamente

Para obter detalhes sobre como criar atributos de produto dinamicamente sem introduzir novos atributos EAV, consulte [Adicionar atributo dinamicamente](add-attribute-dynamically.md).
