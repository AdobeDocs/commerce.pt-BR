---
title: Adicionar atributos de produto dinamicamente
description: Saiba como adicionar atributos de produto personalizados ao feed de exportação de dados de forma dinâmica durante o processo de sincronização de dados.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# Adicionar atributos de produto dinamicamente

Você pode estender atributos de produto sem registrá-los no [!DNL Adobe Commerce] criando um plug-in para adicionar os atributos durante o processo de sincronização de dados.

>[!NOTE]
>
>A melhor maneira de estender atributos de produto é [adicioná-los a [!DNL Adobe Commerce]](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [[!DNL API Mesh] com o [!DNL Catalog Service]](../catalog-service/mesh.md) para estender o esquema [!DNL Catalog Service] [!DNL GraphQL].

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
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   Após adicionar o plug-in, as alterações são sincronizadas com os serviços da loja conectados durante a próxima sincronização agendada. Para enviar as atualizações imediatamente, use o seguinte comando da CLI para iniciar o processo de sincronização manualmente.

   ```shell
   bin/magento saas:resync --feed=products
   ```

## Declarar metadados de atributo de produto personalizado

Se você criar dinamicamente um atributo de produto personalizado e quiser usá-lo para exibição, pesquisa ou filtragem nos serviços da loja, adicione os metadados do atributo de produto para configurar o comportamento da loja.

1. Atualize o [arquivo de configuração de injeção de dependência](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) para definir o plug-in para os metadados de atributo de produto.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Crie o plug-in para o seguinte provedor `Magento\CatalogDataExporter\Model\Provider\ProductMetadata`.

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
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
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

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [Estender e personalizar os feeds de exportação de dados SaaS](extensibility-and-customizations.md)
> * [Sincronizar feeds usando a CLI do Commerce](data-export-cli-commands.md)
> * [Como a sincronização funciona](sync-overview.md) — Saiba mais sobre modos de sincronização e ressincronização agendada vs. manual.
> * [Revisar logs e solucionar problemas](troubleshooting/logging.md)
