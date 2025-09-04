---
title: Adicionar classe de imposto, conjunto de atributos e atributos de inventário
description: Saiba como estender os dados de feed do produto para incluir atributos para classificação de imposto, conjunto de atributos e configurações avançadas de inventário
role: Admin, Developer
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: 6abfeca68ab67fb11493f78440e09408479e1535
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Adicionar classe de imposto, conjunto de atributos e atributos de inventário

O módulo Atributos extras de produto do Adobe Commerce estende os feeds de dados do produto. Ele inclui atributos de produto adicionais das configurações de produto do Adobe Commerce:

* [Classificação de imposto](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Conjunto de atributos](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Inventário](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

Uma vez instalado, o módulo funciona automaticamente. Ele captura e exporta os atributos adicionais durante a sincronização do produto. Nenhuma configuração adicional é necessária.

## Principais benefícios

* **Aprimoramento automático**: enriquece feeds de produtos com classe de imposto, conjunto de atributos e atributos de inventário
* **Integração perfeita**: fornece contexto essencial para sistemas e serviços externos
* **Configuração zero**: funciona imediatamente após a instalação
* **Atualizações em tempo real**: sincroniza automaticamente com as alterações do produto

## Recursos e atributos exportados

O módulo adiciona três atributos adicionais aos seus feeds de dados de produtos existentes:

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. Informações da classe de imposto (`ac_tax_class`)

**Propósito**: fornece informações de classificação de imposto para cada produto

**Formato dos dados**: valor da cadeia de caracteres que contém o nome da classe de imposto

**Exemplo de saída**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**Casos de uso**:

Quando você exporta dados da classe de imposto para os serviços de catálogo Commerce, esses dados ficam disponíveis para aplicativos que suportam:

* Relatório de conformidade fiscal
* Integração com serviços de cálculo de impostos externos
* Categorização de produtos para sistemas de contabilidade

### &#x200B;2. Informações de conjunto de atributos (`ac_attribute_set`)

**Propósito**: identifica qual conjunto de atributos está atribuído a cada produto

**Formato dos dados**: valor da cadeia de caracteres que contém o nome do conjunto de atributos

**Exemplo de saída**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**Casos de uso**:

Quando você exporta dados do conjunto de atributos para os serviços de catálogo da Commerce, ele ativa recursos avançados de gerenciamento de produtos em sistemas externos. Esses recursos incluem:

* Identificação do modelo de produto
* Gerenciamento e organização do catálogo
* Integração de sistema de terceiros que requer o contexto do conjunto de atributos

### &#x200B;3. Dados avançados de inventário (`ac_inventory`)

**Propósito**: Fornece configurações de gerenciamento de estoque para cada produto

**Formato de dados**: cadeia de caracteres codificada em JSON contendo configuração de inventário

**Campos incluídos**:

* `manageStock` (booleano): se o gerenciamento de estoque está habilitado
* `cartMinQty` (flutuante): quantidade mínima permitida no carrinho de compras
* `cartMaxQty` (flutuante): quantidade máxima permitida no carrinho de compras
* `backorders` (cadeia de caracteres): política de backorder. O valor é um dos seguintes:
   * `"no"`: Nenhuma ordem pendente permitida
   * `"allow"`: Permitir quantidade abaixo de 0
   * `"allow_notify"`: Permitir quantidade abaixo de 0 e notificar o cliente
* `enableQtyIncrements` (booleano): se os incrementos de quantidade estão habilitados
* `qtyIncrements` (flutuante): valor de incremento de quantidade necessário

**Exemplo de saída**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**Casos de uso**:

Quando você exporta dados de inventário para serviços de catálogo da Commerce, ele ativa recursos avançados de gerenciamento de inventário em sistemas externos. Esses recursos incluem:

* Integração do sistema Inventory management
* Regras de validação do carrinho de compras
* Otimização do processo de atendimento do pedido
* Personalização da experiência do cliente

## Aprimoramento do feed de exportação de dados

O módulo de Atributos de produto adicionais aprimora os feeds de produto existentes. Ele integra os novos dados do atributo automaticamente.

* **Feed de produtos** (`products`): aprimorado com os três atributos adicionais

   * Adiciona os atributos `ac_tax_class`, `ac_attribute_set` e `ac_inventory` a cada registro de produto
   * Mantém os dados originais do produto inalterados
   * Mantém a compatibilidade com versões anteriores de consumidores de feed existentes

* **Feed de atributos de produto** (`productAttributes`): aprimorado com metadados de atributo para os novos atributos

   * Registra automaticamente metadados para os três novos atributos no feed `productAttributes`
   * Fornece detalhes de configuração do atributo (tipos de dados, configurações de visibilidade e assim por diante)
   * Ajuda os sistemas externos a entender o novo esquema de atributo

## Instalar a extensão

**Requisitos**

* PHP 8.1, 8.2, 8.3 ou 8.4
* Adobe Commerce 2.4.4+
* [Extensão do Adobe Commerce Data Export](manage-extension.md#update-a-module-to-a-specific-version), versão 103.4.11 ou posterior
* Acesso ao [repo.magento.com](https://repo.magento.com)

  Para gerar chaves e obter os direitos necessários, consulte [Obter suas chaves de autenticação](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Para instalações na nuvem, consulte o [Guia de Infraestrutura do Commerce na Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/develop/authentication-keys).
* Acesso à linha de comando do servidor de aplicativos do Adobe Commerce.

### Etapas de instalação

Adicionar o módulo `adobe-commerce/module-extra-product-attributes` usando o Composer:

```shell
composer require adobe-commerce/module-extra-product-attributes
```

Para ver as etapas detalhadas de instalação, consulte os guias a seguir:

* [Instalar extensão no Adobe Commerce na Infraestrutura em Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [Instalar Adobe Commerce de extensão no local](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extension)

## Sincronizar dados do produto

Após a reimplantação, a instância do Adobe Commerce exporta os dados adicionais automaticamente durante a sincronização do produto. Você também pode usar os comandos da CLI do `resync` para sincronizar imediatamente.

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Solução de problemas

**Falta atributos adicionais nos produtos:**

* Verifique se o módulo está instalado e ativado corretamente
* Execute os comandos resync para atualizar os dados do produto
* Verificar se os produtos têm atribuições válidas de classe de imposto e conjunto de atributos

**Os dados de inventário parecem incorretos:**

* Verifique se as configurações de inventário estão definidas corretamente no Administrador
* Verificar substituições de inventário específicas do site
* Verifique se o [módulo Inventory management](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/guide-overview) está funcionando corretamente

Para obter mais detalhes, consulte o [Guia do Inventory management](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/guide-overview) na *Documentação do Comerciante da Adobe Commerce*.

**Questões de desempenho:**

* Monitorar o desempenho do processo de exportação após a instalação
* Considere o agendamento de ressincronizações durante períodos de tráfego baixo

### Registro e depuração

O módulo registra erros de exportação e avisos no sistema de registro padrão do Commerce. Se você encontrar problemas durante a sincronização do produto, verifique os logs de exportação de dados.

Para obter detalhes, consulte [Revisar logs e solucionar problemas](troubleshooting-logging.md).

