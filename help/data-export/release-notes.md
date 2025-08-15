---
title: Notas de versão do [!DNL SaaS Data Export Extension]
description: As informações da versão mais recente do  [!DNL Data Export Extension] para Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: 0722458a67a945b13d2cb27d8848d58d909aea35
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 0%

---

# Notas de versão da extensão [!DNL SaaS Data Export]

Essas notas de versão descrevem as versões mais recentes da extensão [!DNL SaaS data export]. O suporte é fornecido para a versão principal atual lançada. As notas de versão para versões mais antigas são fornecidas para referência.

As atualizações incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos


>[!NOTE]
>
>A extensão de exportação de dados SaaS é uma coleção de módulos instalados automaticamente com o Live Search, o Product Recommendations e o Catalog Service. Você pode verificar a versão instalada em seu sistema usando o Composer. Em alguns casos, você pode querer atualizar a extensão de exportação de dados no seu sistema para coletar correções ou novos recursos sem atualizar a versão do Serviço do Commerce.

## Versão principal atual

## Versão 103.4.8

![Correção](../assets/fix.svg) corrigido um problema em que os feeds de preço do produto não eram regenerados quando um produto era excluído ou quando o SKU do produto era alterado.<!--MDEE-1125-->
![Correção](../assets/fix.svg) Processamento de atualização de produto aprimorado para garantir que as alterações sejam refletidas com precisão ao atualizar um produto recém-criado com o mesmo SKU de um produto excluído anteriormente. A sincronização do produto agora usa corretamente as IDs do produto atualizadas, garantindo uma exportação de dados precisa e confiável.<!--MDEE-1126-->
![Correção](../assets/fix.svg) Corrigido um problema no qual o Serviço de Catálogo retornava dados de variante desatualizados para produtos configuráveis, garantindo que os eventos de atualização de produto fossem publicados após as exclusões de atributos.<!--MDEE-1127-->

## Versão 103.4.8

![Novo](../assets/new.svg) Foram adicionadas informações de preço de camada ao feed de preços. <!--MDEE-1070-->
![Correção](../assets/fix.svg) A extensão Exportador de Dados agora exporta corretamente os preços de seleção de pacotes no escopo do site, garantindo que os preços da loja reflitam valores precisos com base na configuração &quot;Escopo do Preço de Catálogo&quot;.<!--MDEE-1115-->
![Correção](../assets/fix.svg) Anteriormente, os produtos eram sincronizados com um status `lowStock=true` incorreto ao usar o Inventory management (Inventory management de várias origens) com configuração de limite. Esse problema foi corrigido para garantir um relatório preciso de estoque baixo.<!--MDEE-1113-->

## Versão 103.4.7

![Correção](../assets/fix.svg) Remoção de tabelas obsoletas que armazenavam permissões de categoria para produtos. <!--MDEE-1065-->

## Versão 103.4.6

![Correção](../assets/fix.svg) Exporte dados de produto baixáveis do Adobe Commerce usando o atributo `ac_downloadable` para usar com o Adobe Commerce Optimizer. <!--MDEE-1043-->
![Correção](../assets/fix.svg) Correção de erro crítico de instalação para a versão 2.4.4 do Adobe Commerce. <!--MDEE-1074-->

## Versão 103.4.5

A ![nova](../assets/new.svg) exportação de dados SaaS agora oferece suporte ao tipo de produto `giftcard` da Adobe Commerce. No feed de dados, os produtos de cartão-presente são exportados como produtos simples com o tipo de atributo de produto `ac_giftcard`. <!--MDEE-1042-->
![Correção](../assets/fix.svg) Relatórios de erros de exportação de dados aprimorados. Os logs agora incluem mensagens de erro mais detalhadas, incluindo detalhes técnicos originais para facilitar a depuração e o rastreamento de erros. <!--MDEE-1064-->

## Versão 103.4.4

![Novo](../assets/new.svg) Adicionou uma mensagem de aviso que é exibida quando o argumento `cleanup-feed` é adicionado ao comando da CLI `saas:resync`. A opção `--cleanup-feed` deve ser usada com cuidado e somente em cenários específicos, como após a limpeza do ambiente ou com a opção `--dry-run`. Usá-lo em outros casos pode levar à perda de dados e a problemas de sincronização. <!--MDEE-1047-->
![Correção](../assets/fix.svg) adicionou o `x-request-id` da resposta do servidor para melhorar a rastreabilidade. <!--MDEE-1041-->
![Correção](../assets/fix.svg) Corrigido um problema no qual o status de sincronização não era salvo para todo o lote de feeds, o que resultava em ressincronização desnecessária. <!--MDEE-1049-->
![Correção](../assets/fix.svg) Corrigido um problema no qual todos os feeds do lote de feeds eram ignorados durante a sincronização se um feed contivesse um erro. <!--MDEE-976-->
![Correção](../assets/fix.svg) Suporte adicionado para dimensões no indexador de permissões de categoria. <!--MDEE-654-->

## Versão 103.4.3

![Correção](../assets/fix.svg) Resolveu um problema em que os produtos eram ignorados durante o processo de exportação de dados devido à falta de atributos EAV. <!--MDEE-970-->

## Versão 103.4.2

![Correção](../assets/fix.svg) Adicionada a capacidade de coletar cargas de entidade no `saas-export.log` ao executar a ressincronização de teste usando o comando `saas:resync --dry-run` com a variável de ambiente `EXPORTER_EXTENDED_LOG=1`. <!--MDEE-1023-->

## Versão 103.4.1

![Correção](../assets/fix.svg) Adicionou um prefixo às chaves de cache QueryXml para evitar conflitos de nomenclatura com outros módulos. <!--MDEE-1019-->

## Versão 103.4.0

![Correção](../assets/fix.svg) O feed de substituições do produto não envia mais permissões se o produto não estiver atribuído a uma categoria.<!--MDEE-449-->

## Versão 103.3.21

![Correção](../assets/new.svg) Adicionada a funcionalidade para sincronizar parcialmente os feeds do `products`, `productOverrides` e `productAttributes` com base em uma lista especificada de SKUs de produtos. Use a nova funcionalidade adicionando a opção `--by-ids` ao comando da CLI resync: <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![Correção](../assets/fix.svg) Reduziu possíveis problemas de compatibilidade com o PHP 8.4 ao solucionar funcionalidades obsoletas. <!--MDEE-1002-->

## Versão 103.3.20

![Correção](../assets/fix.svg) Corrigiu erros `BulkException` não rastreáveis em `cron.log`, melhorando as mensagens de erros relacionados a falhas no trabalho cron de Exportação de Dados de Catálogo.<!--MDEE-966-->
![Correção](../assets/fix.svg) Desempenho aprimorado do processo de ressincronização de produtos em instâncias com um alto número de exibições de loja. <!--MDEE-974-->

## Versão 103.3.19

![Correção](../assets/fix.svg) atualizou a extensão de exportação de dados para melhorar a extensibilidade dos feeds. <!--MDEE-936-->
![Correção](../assets/fix.svg) O processador de exportação de dados agora verifica o status do indexador antes de uma ressincronização completa para evitar perda acidental de dados na tabela de feed.

## Versão 103.3.18

![Correção](../assets/fix.svg) As atualizações de preparo das entidades de produto e categoria agora são acionadas corretamente nas atualizações de dados da Exportação de Dados.<!--MDEE-963-->

## Versão 103.3.17

![Correção](../assets/fix.svg) Compatibilidade adicionada para PHP 8.4. <!--MDEE-941-->

## Versão 103.3.16

![Correção](../assets/fix.svg) Os valores de opção podem estar vazios para produtos configuráveis para várias exibições de loja. <!--MDEE-926-->

## Versão 103.3.15

![Correção](../assets/fix.svg) Operação estável garantida de testes de integração em configurações mais antigas. <!--MDEE-869-->
![Correção](../assets/fix.svg) Parar de propagar opções de atributo desnecessárias. <!--MDEE-882-->
![Correção](../assets/fix.svg) Corrigida a mensagem de erro enviada ao log de exportação de dados quando a serialização de dados falhava. <!--MDEE-913-->
![Correção](../assets/fix.svg) Melhorou a confiabilidade de atualizações de produtos simples com cobertura de teste adicional. <!--MDEE-886-->

## Versão 103.3.14

![Correção](../assets/fix.svg) O indexador exportador agora mantém o status correto para indexadores dependentes. Anteriormente, esses índices eram invalidados incorretamente e exigiam verificações e validação adicionais que retardavam o desempenho da indexação. <!--MDEE-866-->

## Versão 103.3.13

![Correção](../assets/fix.svg) Desempenho aprimorado do processo de sincronização de dados ao adicionar um cache local para dados de opções de atributo.<!--MDEE-864-->

## Versão 103.3.12

![Correção](../assets/fix.svg) Resolveu um problema que aumentava o tempo de sincronização de produtos simples e virtuais. <!--MDEE-861-->

## Versão 103.3.11

![Correção](../assets/fix.svg) O serviço de exportação de dados agora envia dados de preço especiais para produtos de pacote como uma porcentagem, corrigindo um problema anterior em que foi enviado como um preço final. <!--MDEE-854-->
![Correção](../assets/fix.svg) Atualizou a implementação do monólogo para compatibilidade com o Monólogo 3. <!--MDEE-858-->

## Versão 103.3.10

![Correção](../assets/fix.svg) Correção de várias filtragens de análise para o feed de opções personalizadas do produto. <!--MDEE-842-->
![Correção](../assets/fix.svg) Feeds inválidos não são reenviados até que o valor de hash do feed seja alterado.<!--MDEE-848-->

## Versão 103.3.9

![Correção](../assets/fix.svg) Quando uma entidade é excluída, o sinalizador `deleted` agora é propagado para os feeds de serviço de escopo do site (`scopesWebsite`) e grupo de clientes (`scopesCustomerGroup`).<!--MDEE-839-->

## Versão 103.3.8

![Correção](../assets/fix.svg) As opções de configuração desabilitadas não são mais exportadas como opções ativas.<!--MDEE-812-->
![Correção](../assets/fix.svg) As opções e os valores são atualizados em um produto configurável quando alterações são feitas em um produto filho. <!--MDEE-835-->
![Novo](../assets/new.svg) adição da capacidade de incluir dados de atributos do sistema adicionais no feed de atributos do produto.

## Versão 103.3.7

![Correção](../assets/fix.svg) Remoção de dependências desnecessárias do módulo InventoryDataExporter.
![Correção](../assets/fix.svg) Alteradas as versões necessárias dos módulos de inventário incluídos no módulo CatalogInventoryDataExporter para oferecer suporte à versão 2.4.4 do Adobe Commerce.

## Versão 103.3.6

![Correção](../assets/fix.svg) Corrigidos bloqueios que ocorriam durante a reindexação do feed no modo de vários threads. Agora as consultas são separadas em operações Inserir e Atualizar.
![Correção](../assets/fix.svg) Otimizou a consulta de preços para catálogos grandes com muitos sites.
![Novo](../assets/new.svg) Lógica de repetição adicionada para executar novamente transações com falha quando ocorrem bloqueios.

## Versão 103.3.5

![Correção](../assets/fix.svg) Definir dependência para a versão de exportação de dados compatível mais recente para o módulo comum SaaS.

![Correção](../assets/fix.svg) Substituiu a instância `ScopeConfig` por `ServiceConfigInterface` para dar suporte a diferentes configurações de serviço.

## Versão 103.3.4

![Correção](../assets/fix.svg) Adicionado suporte para log de auditoria de transferência de dados, adicionando um mecanismo para despachar um evento `data_sent_outside` sempre que os dados forem transmitidos da instância do Commerce para um serviço do Commerce <!--MDEE-785-->

## Versão 103.3.3

A ![nova](../assets/new.svg) exportação de dados SaaS agora armazena em cache os atributos Entity-Attribute-Value (EAV) para a consulta de metadados do atributo.

![Correção](../assets/fix.svg) Corrigido um problema no qual o feed do `InventoryStockStatus` não era salvo na tentativa caso o produto fosse excluído.

## Versão 103.3.2

![Correção](../assets/fix.svg) Corrigido um problema no qual o campo `modifiedAt` não estava presente nos feeds de entidades removidos.

## Versão 103.3.1

![Correção](../assets/fix.svg) Corrigido um problema que fazia com que uma mensagem `Invalid Template File` fosse exibida durante a reindexação do feed de produtos quando o Page Builder estava instalado.

## Versão 103.3.0

![Novo](../assets/new.svg) tabelas de feeds de exportação imediata migradas para a estrutura unificada:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Novo](../assets/new.svg) migrou os feeds de catálogo e inventário para a solução de exportação imediata.

![Novo](../assets/new.svg) cron-jobs de feed de exportação imediata renomeados para `*_feed_resend_failed_items`.

![Novo](../assets/new.svg) renomeou feeds de exportação imediatos, IDs de exibição de indexador e tabelas de log de alterações.
- tabelas de feed (e IDs de exibição do indexador):
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- alterar nomes de tabela de log - Segue o mesmo padrão de nomenclatura das tabelas de feed, mas os nomes de tabela de log de alteração adicionam um sufixo `_cl`.  Por exemplo `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
Se você tiver um código personalizado que faça referência a qualquer uma dessas entidades, atualize as referências com os novos nomes para garantir que seu código continue a funcionar corretamente.

![Correção](../assets/fix.svg) Defina o campo `modified_at` nos dados de feed somente para feeds que o exijam.

![Correção](../assets/fix.svg) Modifique a consulta `productAttributes` para recuperar apenas atributos do produto.

## Versão 103.2.6

![Correção](../assets/fix.svg) Corrigido um problema que impedia que os feeds fossem reindexados quando as tabelas tinham um prefixo.

## Versão 103.2.5

![Correção](../assets/fix.svg) Otimizou a consulta de preço.

## Versão 103.2.4

![Correção](../assets/fix.svg) Corrigido o status incorreto do Stock que era exibido para um produto quando o Commerce Inventory management estava habilitado.

## Versão 103.2.3

![Corrigir](../assets/fix.svg) preços especiais no nível do site fixo.
![Correção](../assets/fix.svg) Adicionou mutex para todos os feeds processados.


## Versão 103.2.2

![Correção](../assets/fix.svg) Feeds aprimorados na estratégia de agrupamento para catálogos grandes. A tabela de lotes agora é preenchida com um número limitado de IDs para reduzir o uso da memória.

![Correção](../assets/fix.svg) Eliminou a dependência forte do CommerceInventoryDataExporter para módulos MSI.

![Corrigir](../assets/fix.svg) Logs `commerce-data-exporter` aprimorados para coletar mais informações e organizar por diferentes estágios de exportação.

## Versão 103.2.1

- Versão atualizada lançada.

## Versão 103.2.0

- Adição da sincronização de dados de vários threads para produtos e preços.
