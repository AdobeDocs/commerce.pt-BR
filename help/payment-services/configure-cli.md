---
title: Configuração da linha de comando
description: Após a instalação, você pode configurar o [!DNL Payment Services] usando a Interface de Linha de Comando (CLI).
role: Admin, Developer
level: Intermediate
feature: Payments, Checkout, Configuration, Integration
exl-id: bb59bd49-6ecd-4ef1-a6b9-e1e93db04bf6
source-git-commit: 24622b8a20b8cd95e13a68df6e0929206ffbb06b
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Configuração da linha de comando

Após instalar o [!DNL Payment Services], você poderá configurá-lo facilmente a partir do [na página inicial](payments-home.md) ou por meio da CLI (Interface de Linha de Comando).

## Configurar exportação de dados

[!DNL Payment Services] combina dados de pedidos exportados de [!DNL Magento Open Source] e [!DNL Adobe Commerce] com dados de pagamentos agregados de provedores de pagamentos para criar relatórios úteis. A extensão [!DNL Payment Services] usa indexadores para coletar com eficiência todos os dados necessários para os relatórios.

Para saber mais sobre os dados usados nos relatórios [!DNL Payment Services], consulte [Relatório de status do pagamento da ordem](order-payment-status.md#data-used-in-the-report).

### Configurar cron em [!DNL Magento Open Source]

Se quiser usar um modo de índice `BY SCHEDULE` em [!DNL Magento Open Source], você deve configurar o cron. Consulte [Configurar e executar o cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs).

### Definir indexadores

Os dados do pedido são exportados e mantidos no Serviço de Pagamento, usando um dos dois modos de índice: `ON SAVE` (padrão) ou `BY SCHEDULE` (recomendado).

Os índices a seguir são para [!DNL Payment Services]:

| Código | Nome | Descrição |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | Feed de Ordem de Venda | Cria um índice de dados do pedido |
| `sales_order_status_data_exporter` | Feed de Status da Ordem de Venda | Cria índice de dados de status de ordens de venda |
| `store_data_exporter` | Feed de lojas | Cria um índice de dados de armazenamento |

Para alterar o modo de índice dos três indexadores, execute:

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>Se você não especificar nenhum indexador em seu comando, todos os indexadores serão atualizados com o mesmo valor. Se quiser alterar um indexador específico, você deve listá-lo no comando.

Para saber mais sobre como alterar manualmente o modo de um indexador, consulte [Configurar indexadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"} na documentação do desenvolvedor. Para saber como alterá-lo no Administrador, consulte [Gerenciamento de índice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"} no guia do usuário principal.

### Reindexar dados manualmente

Você pode reindexar os dados manualmente, em vez de esperar que eles aconteçam automaticamente. Consulte [Reindex](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"} em [Manage the Indexers](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"} para obter mais informações.

Quando o modo `BY SCHEDULE` é definido, o sistema rastreia entidades alteradas e o trabalho cron atualiza o índice dessas entidades com base em um agendamento definido. Consulte [Executar cron a partir da linha de comando](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run) em [Configurar e executar cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)) para saber como disparar manualmente a indexação usando trabalhos cron.

### Enviar dados reindexados para o serviço de pagamento

Depois que os dados forem indexados, eles serão enviados automaticamente para [!DNL Payment Services]. Você também pode acionar manualmente o processo de envio de dados indexados com este comando:

```bash
bin/magento saas:resync --feed [feedName]
```

Use as seguintes opções de comando:

| Comando | Descrição |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | Executa uma reindexação do feed especificado e o envia para o serviço correspondente |
| `bin/magento saas:resync --no-reindex` | Ignora a indexação e envia dados não sincronizados dos índices |

O parâmetro `--feed` permite especificar qual feed você deseja enviar:

| Feed | Descrição |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | Feed de pedidos no modo de Produção |
| `paymentServicesOrdersSandbox` | Feed de pedidos no modo Sandbox |
| `paymentServicesOrderStatusesProduction` | Status dos pedidos no modo Produção |
| `paymentServicesOrderStatusesSandbox` | Status dos pedidos no modo Sandbox |
| `paymentServicesStoresProduction` | Lojas no modo de produção |
| `paymentServicesStoresSandbox` | Lojas no modo Sandbox |

Todos os dados necessários para os relatórios são enviados para [!DNL Payment Services] automaticamente se o cron estiver configurado e instalado. Você também pode acionar manualmente o processo de envio de dados cron para [!DNL Payment Services].

```bash
bin/magento cron:run --group payment_services_data_export
```

Para saber mais sobre indexação e indexadores, consulte o tópico [Gerenciar os indexadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) na documentação do desenvolvedor.

## Configurar escopo via CLI

[!DNL Payment Services] permite que comerciantes usem [várias contas do PayPal](settings.md#use-multiple-paypal-accounts). Agora, você pode alterar os escopos dessas contas via CLI.

Para definir o escopo para o nível `website`, execute:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

Para definir o escopo para o nível `store`, use:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> Se você quiser alterar o escopo para o nível de armazenamento, contate o representante de vendas [!DNL Payment Services].

Ao alterar o escopo, limpe o cache para mostrar as alterações:

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## Configurar processamento L2/L3

O [!DNL Payment Services] pode processar dados de nível 2 e nível 3 de transações de pagamento com cartão para fornecer informações adicionais aos comerciantes.

>[!WARNING]
>
> A integração com o processamento de Nível 2 e Nível 3 com o PayPal está disponível somente para comerciantes dos EUA. Consulte [processamento de pagamento](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} na documentação do desenvolvedor do PayPal para obter mais informações.

Se quiser usar os dados de processamento L2/L3 para [!DNL Payment Services], ou se tiver dúvidas, entre em contato com o gerente de conta do [!DNL Payment Services].

Para saber mais sobre o processamento L2 e L3 usado em [!DNL Payment Services], consulte [Processamento de Nível 2 e Nível 3](levels-card-payment-transactions.md).
