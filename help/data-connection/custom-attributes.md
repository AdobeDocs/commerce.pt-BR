---
title: Adicionar atributos de ordem personalizados
description: Saiba como adicionar atributos de pedido personalizados aos dados de back office e enviar esses atributos à Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# Adicionar atributos de ordem personalizados

Neste artigo, você aprenderá a adicionar atributos personalizados a eventos de back office. Com atributos personalizados, você pode capturar insights de dados avançados para aprimorar as análises e criar experiências personalizadas para seus compradores.

Os atributos personalizados são aceitos em dois níveis:

- Nível do pedido
- Nível do item da ordem

>[!NOTE]
>
>O Adobe [!DNL Commerce] oferece suporte a atributos personalizados que têm um tipo de dados de cadeia de caracteres, Booleano ou data.

Adicionar atributos personalizados aos eventos de back office requer que você:

1. Crie um projeto na instalação do [!DNL Commerce].
1. Atualize seu esquema para que os novos atributos personalizados possam ser assimilados corretamente na Experience Platform.
1. Em Admin, confirme se os atributos personalizados estão sendo capturados e enviados para a Experience Platform.

>[!IMPORTANT]
>
>A estrutura de diretório e os exemplos de código abaixo ilustram como você pode implementar atributos personalizados. A estrutura de diretório e o código real necessários dependem da configuração e do ambiente da loja.

## Etapa 1: criar a estrutura de diretório

1. Navegue até o diretório `app/code` em sua instalação do [!DNL Commerce] e crie um diretório de módulo. Por exemplo: `Magento/AepCustomAttributes`. Esse diretório contém os arquivos necessários para seus atributos personalizados.
1. No diretório do módulo, crie um subdiretório chamado `etc`. O diretório `etc` contém os arquivos `module.xml`, `query.xml`, `di.xml` e `et_schema.xml`.

## Etapa 2: definir as dependências e a versão de configuração

Crie um arquivo `module.xml` que defina as dependências e a versão da instalação. Por exemplo:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Magento_AepCustomAttributes">
        <sequence>
            <module name="Magento_SalesOrderDataExporter"/>
        </sequence>
    </module>
</config>
```

## Etapa 3: Recuperar dados da ordem de venda

Criar um arquivo `query.xml` que recupere dados de ordem de venda. Por exemplo:

```xml
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:Module:Magento_QueryXml:etc/query.xsd">
  <query name="salesOrdersV2">
    <source name="sales_order">
      <link-source name="sales_order_inventory_source" link-type="inner">
        <attribute name="inventory_source_code" alias="inventory_source" />
        <using glue="and">
          <condition attribute="order_id" operator="eq" type="identifier">entity_id</condition>
         </using> 
        </link-source>
    </source>
  </query>
  </config>
```

## Etapa 4: configurar a injeção de dependência

Crie um arquivo `di.xml` que configure a injeção de dependência. Por exemplo:

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
      <type name="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">commerceOrderId</argument>
          </arguments>
      </type>
      <type name="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
          <arguments>
              <argument name="usingField" xsi:type="string">entityId</argument>
          </arguments>
      </type>
      <type name="Magento\DataServices\Model\ProductContext">
          <plugin name="product-context-plugin" type="Magento\AepCustomAttributes\Plugin\Model\ProductContext"/>
      </type>
  </config>
```

## Etapa 5: definir os serviços usados para a injeção de dependência

Crie um arquivo `et_schema.xml` que defina os serviços usados para a injeção de dependência. Por exemplo:

```xml
  <?xml version="1.0"?>
  <config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:module:Magento_DataExporter:etc/et_schema.xsd">
      <record name="OrderV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\CustomAttribute">
              <using field="commerceOrderId"/>
          </field>
      </record>
      <record name="OrderItemV2">
          <field name="additionalInformation" type="CustomAttribute" repeated="true" provider="Magento\AepCustomAttributes\Model\Provider\OrderItemCustomAttribute">
              <using field="entityId"/>
          </field>
      </record>
  </config>
```

## Etapa 6: criar um diretório para os arquivos PHP

No mesmo nível que o diretório `etc`, crie um diretório chamado `Module/Provider`. Este diretório contém os arquivos PHP `OrderCustomAttributes` e `OrderItemCustomAttributes`.

## Etapa 7: definir OrderCustomAttributes

Crie um arquivo `OrderCustomAttributes.php` que defina a ordem dos atributos personalizados. Por exemplo:

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class CustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param string $usingField
   * @param Json $jsonSerializer
   */
  public function __construct(
      string $usingField,
      Json $jsonSerializer
  ) {
      $this->usingField = $usingField;
      $this->jsonSerializer = $jsonSerializer;
  }

  /**
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];

      /**
       * Entity IDs
       */
      $ids = array_column($values, $this->usingField);

      foreach ($this->flatten($values) as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];

          if (isset($row)) {
              $unserializedData['order_channel'] = 'order_channel';
              $unserializedData['order_status'] = 'order_status';

              $additionalInformation = [];
              foreach ($unserializedData as $name => $value) {
                  $additionalInformation[] = [
                      'name' => $name,
                      'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
                  ];
              }
              foreach ($additionalInformation as $information) {
                  $output[] = [
                      'additionalInformation' => $information,
                      $this->usingField => $row[$this->usingField],
                  ];
              }
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Etapa 8: definir OrderItemCustomAttributes

Criar um arquivo `OrderItemCustomAttributes.php` que defina os atributos personalizados do item de pedido. Por exemplo:

```php
declare(strict_types=1);

namespace Magento\AepCustomAttributes\Model\Provider;

use Magento\Framework\Serialize\Serializer\Json;

class OrderItemCustomAttribute
{
  /**
   * @var Json
   */
  private Json $jsonSerializer;

  /**
   * @var string
   */
  private string $usingField = '';

  /**
   * @param Json $jsonSerializer
   * @param string $usingField
   */
  public function __construct(
      Json $jsonSerializer,
      string $usingField
  ) {
      $this->jsonSerializer = $jsonSerializer;
      $this->usingField = $usingField;
  }

  /**
   * Getting additional attributes data.
   *
   * @param array $values
   * @return array
   */
  public function get(array $values): array
  {
      $output = [];
      $values = $this->flatten($values);

      foreach ($values as $row) {
          $info = \is_string($row['additionalInformation']) ? $row['additionalInformation'] : '{}';
          $unserializedData = $this->jsonSerializer->unserialize($info) ?? [];
          $unserializedData['product_brand'] = implode(',', ['label 1', 'label 2']);

          $additionalInformation = [];
          foreach ($unserializedData as $name => $value) {
              $additionalInformation[] = [
                  'name' => $name,
                  'value' => \is_string($value) ? $value : $this->jsonSerializer->serialize($value)
              ];
          }
          foreach ($additionalInformation as $information) {
              $output[] = [
                  'additionalInformation' => $information,
                  $this->usingField => $row[$this->usingField],
              ];
          }
      }
      return $output;
  }

  /**
   * @param $values
   * @return array
   */
  private function flatten($values): array
  {
      if (isset(current($values)[0])) {
          return array_merge([], ...array_values($values));
      }
      return $values;
  }
}
```

## Etapa 9: criar um diretório para o arquivo productContext

No mesmo nível que o diretório `etc`, crie um diretório chamado `Plugin/Module`. Este diretório contém o arquivo `ProductContext.php`.

## Etapa 10: definir a classe ProductContext

Crie um arquivo chamado `ProductContext.php` que defina a classe `ProductContext`. Por exemplo:

```php
<?php>
namespace Magento\AepCustomAttributes\Plugin\Model;
use Magento\Catalog\Model\Product;
use Magento\DataServices\Model\ProductContext as Subject;
use Magento\Framework\App\ResourceConnection;

class ProductContext
{
    private ?array $brandCache = [];
    public function __construct(
        private ResourceConnection $resourceConnection ) {
    }  

    public function afterGetContextData(Subject $subject, array $result Product $product)
    {
        $brand = $product->getCustomAttribute('cust_attr1');
        if (!empty($brand) && $brand->getValue()) {
            $result['brands'] = ['brand_label_1', 'brand_label_2'];
            }
            return $result;
      }
  }
```

## Etapa 11: Registrar o módulo

No mesmo nível que o diretório `etc`, crie um arquivo `registration.php` que registre o módulo. Por exemplo:

```php
<?php>
declare(strict_types=1);

use \Magento\Framework\Component\ComponentRegistrar;

ComponentRegistrar::register(
    ComponentRegistrar::MODULE,
    'Magento_AepCustomAttributes',
    __DIR__
);
```

## Etapa 12: estender o esquema XDM existente

Para garantir que os novos atributos de pedido personalizados possam ser assimilados pelo esquema [!DNL Commerce] no Experience Platform, é necessário estender o esquema para incluir esses campos personalizados.

Para saber como estender um esquema XDM existente para incluir esses campos personalizados, consulte o artigo [Criar e editar esquemas na interface](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/ui/resources/schemas#custom-fields-for-standard-groups) na documentação da Experience Platform. O campo ID do locatário é gerado dinamicamente; no entanto, a estrutura do campo deve se parecer com o exemplo fornecido na documentação do Experience Platform.

>[!IMPORTANT]
>
>Os atributos personalizados XDM devem corresponder aos atributos enviados de [!DNL Commerce].

Para `commerce.order`, adicione um campo para o nível Ordem:

![Nível do pedido](assets/order-level.png)

Para `productListItems`, adicione campos para o nível de item Ordem:

![Nível do Item da Ordem](assets/order-item-level.png)

## Etapa 12: Confirmar se os dados estão sendo capturados

Exiba a guia [Personalização de Dados](connect-data.md#data-customization) no Administrador para confirmar se os dados do atributo personalizado estão sendo capturados e enviados para a Experience Platform.

### Solução de problemas

Se você vir a mensagem `No custom order attributes found.` na guia **[!UICONTROL Data Customization]**, confirme o seguinte:

1. Você concluiu os pré-requisitos para habilitar a [extensão do Conector de Dados](overview.md#prerequisites).
1. Você configurou [atributos de pedido personalizados](#add-custom-order-attributes).
1. Pelo menos um evento de pedido foi gerado.
