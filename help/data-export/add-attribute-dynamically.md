---
title: Adicionar atributos de produto dinamicamente
description: Saiba como adicionar atributos de produto personalizados ao feed de exportação de dados de forma dinâmica durante o processo de sincronização de dados.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Adicionar atributos de produto dinamicamente durante a sincronização de dados

É possível estender atributos do produto sem registrá-los no Adobe Commerce criando um plug-in para adicionar os atributos durante o processo de sincronização de dados.

>[!NOTE]
>
>A melhor maneira de estender os atributos do produto é [adicioná-los ao Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce), onde você pode configurá-los e gerenciá-los no Administrador do Commerce. Adicione-os dinamicamente somente se você precisar deles apenas para serviços da loja da Commerce e não quiser registrá-los no Adobe Commerce. Você também tem a opção de gerenciar atributos personalizados usando a [API Mesh com o Serviço de Catálogo](../catalog-service/mesh.md) para estender o esquema do GraphQL do Serviço de Catálogo.

## Adicionar atributos de produto

Crie um plug-in que adicione um `customer_attribute` à classe `Magento\CatalogDataExporter\Model\Provider\Product\Attributes`.

1. Atualize o [arquivo de configuração de injeção de dependência](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) para definir o plug-in.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. Crie o plug-in.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(Attributes $subject, array $result, $arguments): array
         {
              $productIds = \array_column($arguments, 'productId');
   
              foreach ($productIds as $productId) {
                    $result[] = [
                         'productId' => $productId,
                         // "storeViewCode" must be specified for products where the customer attribute value should be set
                         'storeViewCode' => 'default',
                         'attributes' => [
                              // specify the customer attribute code
                              'attributeCode' => 'customer_attribute',
                              // provide single or multiple values for the attribute
                              'value' => [
                                    rand(41,43)
                              ]
                         ]
                    ];
              }
   
              return $result;
         }
    }
   ```

   Após adicionar o plug-in, as alterações são sincronizadas com os serviços da loja conectados durante a próxima sincronização agendada. Para enviar as atualizações imediatamente, use o seguinte comando da CLI para iniciar o processo de sincronização manualmente.

   ```
   bin/magento saas:resync --feed=products
   ```

## Declarar metadados de atributo de produto personalizado

Se você criar dinamicamente um atributo de produto personalizado e quiser usá-lo para exibição, pesquisa ou filtragem nos serviços da loja, adicione os metadados do atributo de produto para configurar o comportamento da loja.

1. Atualize o [arquivo de configuração de injeção de dependência](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) para definir o plug-in para os metadados de atributo de produto.

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Crie o plug-in para o seguinte provedor `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`.

   Verificar `ProductAttributeMetadata` em `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml` quanto a campos obrigatórios.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   Após adicionar o plug-in, as alterações são sincronizadas com os serviços da loja conectados durante a próxima sincronização agendada. Para enviar as atualizações imediatamente, use o seguinte comando da CLI para iniciar o processo de sincronização manualmente.

   ```
   bin/magento saas:resync --feed=productattributes
   ```
