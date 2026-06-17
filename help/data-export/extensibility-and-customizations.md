---
title: Estender e personalizar dados do feed de exportação de dados SaaS
description: Saiba como estender e personalizar os dados do feed  [!DNL SaaS Data Export] .
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# Estender e personalizar dados do feed de exportação de dados SaaS

A extensão [!DNL Commerce Data Export] fornece uma maneira de exportar dados do aplicativo [!DNL Commerce] para os Serviços da Commerce, como o Live Search, o Serviço de Catálogo e as Recomendações de Produto. Se necessário, você pode estender e personalizar os dados do feed para incluir dados de atributo adicionais ou modificar os dados coletados.

Depois de adicionar dados de atributo, ele pode ser acessado no [campo de atributos](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type) do esquema do GraphQL para serviços de vitrine.

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

Consulte [Criar atributos de produto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) no *Guia de Administração do Adobe Commerce*.

#### Criar o atributo de produto de forma programática

Adicione um atributo de produto de forma programática criando um patch de dados que implemente o `DataPatchInterface` e instancie uma cópia da classe `EavSetup Factory` dentro do construtor para configurar as opções de atributo.

Quando você define as opções de atributo, todos os parâmetros de atributo exceto `type`, `label` e `input` são opcionais. Defina os seguintes parâmetros adicionais e outros que diferem das configurações padrão.

- **`user_defined`=`1`**—Exporta o atributo para serviços de vitrine durante a sincronização de dados
- **`used_in_product_listing`=`1`** — Tornar o atributo acessível na consulta do banco de dados da lista de produtos

Para obter informações sobre como criar patches de dados, consulte [Desenvolver patches de dados e esquemas](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) no *Guia do Desenvolvedor do PHP*.

### Adicionar o atributo de produto dinamicamente

Para obter detalhes sobre como criar atributos de produto dinamicamente sem introduzir novos atributos EAV, consulte [Adicionar atributos de produto dinamicamente](add-attribute-dynamically.md).

## Visão geral do esquema de feed (`et_schema.xml`) {#feed-schema-overview}

Cada estrutura de dados de feed é declarada em `etc/et_schema.xml` usando um DSL XML simples. O framework lê este arquivo para determinar quais campos coletar e quais classes de provedor PHP chamar.

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

Principais elementos:

- `<record>` - define a entidade de feed
- `<field>` - declara um campo de dados; o atributo `provider` aponta para uma classe PHP implementando `DataProcessorInterface` que busca os dados
- `repeated="true"` - o campo é uma matriz de objetos
- `<using>` - parâmetros de entrada passados do contexto de registro pai para o provedor

>[!IMPORTANT]
>
>Adicionar um novo campo a `et_schema.xml` altera apenas o que [!DNL Adobe Commerce] coleta localmente. O serviço SaaS de recebimento também deve ser atualizado para aceitar e processar o novo campo antes que ele tenha qualquer efeito na loja.

## Observar dados após o envio {#observe-data-after-submission}

[!DNL SaaS Data Export] despacha o evento `data_sent_outside` após cada envio de lote bem-sucedido para um serviço SaaS. Use este evento para logs de auditoria, acionadores de webhook ou coleções de métricas.

**Evento:** `data_sent_outside`

**Dados disponíveis:**

| Chave | Descrição |
|---|---|
| `timestamp` | Carimbo de data e hora Unix do envio |
| `type` | Nome do feed (por exemplo, `products`, `prices`) |
| `data` | A carga do feed enviada |

**Exemplo de observador:**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

Registrar o observador em `etc/events.xml`:

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

Para obter informações gerais sobre eventos e observadores, consulte [Eventos e observadores](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"} na Documentação do desenvolvedor do Adobe Commerce.

## Filtrar dados antes de enviar

Use o ponto de extensão `Magento\SaaSCommon\Model\DataFilter` para redigir campos confidenciais ou ignorar entidades específicas antes que os dados sejam enviados ao serviço SaaS. Isso é útil para requisitos de conformidade, como GDPR ou PCI, em que determinados campos não devem sair da instância do Commerce.

Implemente a interface e conecte-a por meio de uma preferência ID em `etc/di.xml`:

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>A filtragem é aplicada após a coleta de dados. Se `PERSIST_EXPORTED_FEED=1` estiver definido, a tabela de feed armazenará a carga não filtrada antes da filtragem.

>[!MORELIKETHIS]
>
> - [Adicionar atributo de produto dinamicamente](add-attribute-dynamically.md)
> - [Adicionar classe de imposto, conjunto de atributos e metadados de estoque](add-tax-attribute-set-inventory-attributes.md)
> - [Como a sincronização funciona](sync-overview.md)
