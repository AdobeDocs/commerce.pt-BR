---
title: Adicionar arquivos aos produtos
description: Saiba como anexar arquivos como PDFs, manuais e folhas de dados a produtos usando atributos de produto do tipo arquivo no [!DNL Adobe Commerce as a Cloud Service].
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Adicionar arquivos aos produtos

O [!DNL Adobe Commerce as a Cloud Service] oferece suporte ao [tipo de entrada de atributo de produto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"} do &quot;Arquivo&quot;, que permite aos comerciantes anexar arquivos, como PDFs, manuais, certificados e folhas de dados, diretamente aos produtos. Os arquivos são armazenados no armazenamento de mídia do Amazon S3 e podem ser acessados por meio da loja usando o GraphQL ou por meio de integrações usando a REST API.

Há três maneiras de fazer upload de arquivos para atributos de arquivo de produto:

* [Interface do Administrador](#upload-files-through-the-admin) - Faça upload dos arquivos manualmente na página de edição do produto.
* [REST API](#upload-through-the-rest-api) - Carregar arquivos por meio da REST API usando URLs pré-assinadas S3.
* [Importação de produto](#upload-through-product-import) - Importe arquivos em massa fornecendo URLs externas em CSV.

## Pré-requisitos

Antes de fazer upload dos arquivos, você deve criar um atributo de arquivo e atribuí-lo a um conjunto de atributos.

* [Criar um atributo de arquivo](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - Definir **[!UICONTROL Catalog Input Type for Store Owner]** como **[!UICONTROL File]**.

* [Atribuir o atributo a um conjunto de atributos](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} - Arraste o novo atributo de arquivo para o grupo desejado.

* Configure os tipos e o tamanho de arquivo permitidos na configuração dos [Atributos de Arquivo do Produto](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes).

## Fazer upload de arquivos por meio do Administrador

Depois de [criar um atributo de arquivo](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} e atribuí-lo a um conjunto de atributos, você pode carregar arquivos diretamente da página de edição do produto.

1. Na barra lateral _Admin_, vá para **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Abra o produto que deseja editar.

1. Localize o campo de atributo de arquivo e clique em **[!UICONTROL Upload]** para selecionar um arquivo.

![Botão Carregar arquivo no Administrador](./assets/upload-file.png){width="600" zoomable="yes"}

1. Clique em **[!UICONTROL Save]**.

Para substituir um arquivo, exclua o arquivo existente e faça upload de um novo arquivo. O arquivo carregado é armazenado no armazenamento de mídia do Amazon S3.

## Fazer upload por meio da API REST

Use o [Fluxo de URL pré-assinado do S3](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"} para carregar arquivos de forma programática por meio da API REST. Esse processo funciona para atributos de arquivo de produto da mesma maneira que para outros tipos de mídia, como imagens de categoria e arquivos de atributos do cliente.

O processo tem quatro etapas:

1. Chame `POST V1/media/initiate-upload` com o nome do arquivo e `media_resource_type` para obter atributos do arquivo do produto.
1. Use a URL pré-assinada retornada para `PUT` o arquivo diretamente para o Amazon S3.
1. Ligue para `POST V1/media/finish-upload` para confirmar o carregamento.
1. Atribua a chave retornada ao atributo de arquivo do produto por meio de `PUT /V1/products/{sku}`, transmitindo a chave como o valor de [atributo personalizado](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/).

## Upload por meio da importação do produto

Você pode anexar arquivos a produtos em massa usando a [API de importação](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} ou a interface de importação de administrador. Os atributos do arquivo de produto só oferecem suporte à importação de URLs externos, o que segue a mesma abordagem do [Método 2 para importação de imagem de produto](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}. O Commerce baixa o arquivo do URL fornecido e o salva no armazenamento de mídia S3.

>[!NOTE]
>
>Não há suporte no [!DNL Adobe Commerce as a Cloud Service] para a importação de arquivos de um caminho de servidor local (Método 1) porque não há acesso direto ao sistema de arquivos.

### Forneça o URL em uma coluna dedicada

Use o código do atributo como o cabeçalho da coluna CSV e o URL completo como o valor. Por exemplo, se o código do atributo for `file_upload`, o CSV terá esta aparência:

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### Fornecer a URL em `additional_attributes`

Como alternativa, inclua o atributo de arquivo na coluna `additional_attributes`:

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

Em ambos os casos, a URL deve estar acessível publicamente e a extensão e o tamanho do arquivo devem estar em conformidade com as [limitações configuradas](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}.

## Recuperar arquivos por meio do GraphQL

Em [!DNL Adobe Commerce as a Cloud Service], o ponto de extremidade [&#x200B; do &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}GraphQL do Serviço de Catálogo fornece dados do produto. Os atributos de arquivo aparecem no campo `attributes` em `ProductView`, com o `value` contendo a URL pública completa para o arquivo:

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

A resposta inclui o atributo de arquivo com seu URL público:

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>Esta consulta requer os cabeçalhos `Magento-Website-Code` e `Magento-Store-View-Code`. Para obter mais informações, consulte a [consulta de produtos do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}.

## Recuperar arquivos por meio da API REST

Ao recuperar um produto por meio da [REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} (`GET /V1/products/{sku}`), os atributos de arquivo aparecem na matriz `custom_attributes` com o nome de arquivo como o valor:

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
