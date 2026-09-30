---
title: Suporte para tipos de produtos personalizados na exportação de dados do catálogo SaaS
description: Saiba como o módulo de ativação de catálogo MCP da Commerce Storefront permite que a Exportação de dados SaaS represente tipos de produtos de terceiros não reconhecidos e personalizados como produtos simples em dados de catálogo enviados para o Live Search e o Serviço de catálogo.
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# Suporte para tipos de produtos personalizados na exportação de dados do catálogo SaaS

>[!IMPORTANT]
>
>O suporte para tipos de produtos personalizados está atualmente no **Acesso antecipado** como parte do [!DNL Commerce Storefront MCP]. Este módulo é compatível com o Adobe Commerce versões 2.4.4 e mais recentes. Os requisitos de disponibilidade, empacotamento e instalação estão sujeitos a alterações antes da disponibilidade geral. Para solicitar um convite para este **Acesso antecipado**, envie um email para [commerceeap@adobe.com](mailto:commerceeap@adobe.com). A equipe do Adobe responderá com as próximas etapas e os requisitos de qualificação.

## Visão geral

A [!DNL SaaS Data Export] reconhece os tipos de produtos padrão da Adobe Commerce (simples, configurável, pacote e assim por diante) quando prepara dados de catálogo para os Serviços da Commerce conectados, como o [Live Search](../live-search/overview.md) e o [Serviço de Catálogo](../catalog-service/overview.md). Extensões de terceiros podem apresentar **tipos de produto personalizados** que [!DNL SaaS Data Export] não reconhece nativamente.

O módulo de habilitação de catálogo MCP da Commerce Storefront permite que o [!DNL SaaS Data Export] represente esses tipos de produtos personalizados e não reconhecidos como **produtos simples** na carga do catálogo de saída, para que os compradores que usam o [!DNL Commerce Storefront MCP] possam detectá-los por meio de serviços com base em catálogo.

## Escopo do comportamento

- O módulo de ativação do catálogo MCP da Commerce Storefront não altera o tipo de produto armazenado no Adobe Commerce. Representar um tipo de produto personalizado como um produto simples se aplica somente aos dados de catálogo enviados para [!DNL Live Search] e [!DNL Catalog Service].
- Nenhuma configuração de Admin ou de tempo de execução é necessária. Os tipos do produto padrão continuam a ser exportados normalmente.
- O módulo é direcionado aos tipos de produtos personalizados introduzidos por extensões de terceiros, não aos tipos de produtos padrão do Commerce.

## Instalar o módulo

Para habilitar o módulo de habilitação de catálogo MCP do Commerce Storefront, execute o seguinte na linha de comando:

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## Ressincronizar os dados do catálogo

A instalação do módulo não altera os dados subjacentes do produto no Adobe Commerce, portanto, os itens de tipo de produto personalizado existentes não são reexportados automaticamente. Para aplicar a nova representação de produto simples aos dados de catálogo que já foram sincronizados antes da instalação do módulo, ressincronize manualmente os dados de catálogo. Consulte [Ressincronizar dados manualmente](data-sync-manage.md#manually-resync-data).
