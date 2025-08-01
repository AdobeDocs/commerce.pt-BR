---
title: Melhore o desempenho da exportação de dados SaaS
description: Saiba como melhorar o desempenho da exportação de dados SaaS para Serviços da Commerce usando um modo de exportação de dados de vários threads.
role: Admin, Developer
exl-id: 7151118c-5e30-44d0-b515-5801a73e44ec
source-git-commit: 9b28da0bf861a266e9d679ba59470f46d9a89c1c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Melhore o desempenho da exportação de dados SaaS

**Modo de exportação de dados de vários threads** acelera o processo de exportação dividindo os dados de feed em lotes e processando-os simultaneamente.

Os desenvolvedores ou integradores de sistema podem melhorar o desempenho usando o modo de exportação de dados de vários segmentos em vez do modo de segmento único padrão. No modo de thread único, não há paralelização do processo de envio do feed. Além disso, devido aos limites padrão definidos, todos os clientes estão restritos a usar apenas um segmento. Na maioria dos casos, não é necessário personalizar a configuração.

## Considerações sobre o uso do modo de vários segmentos

Ao trabalhar com serviços de exportação de dados, você deseja otimizar o desempenho, garantindo uma sincronização precisa.
A Adobe recomenda usar a configuração padrão para assimilação de dados, que normalmente atende aos requisitos de sincronização para comerciantes do Commerce. No entanto, há cenários em que a personalização pode acelerar o tempo de processamento.

Considere os seguintes fatores principais ao decidir se a configuração da exportação de dados deve ser personalizada:

- **Sincronização Inicial** - Avalie o número de produtos e [estime o volume de dados e o tempo de transmissão](estimate-data-volume-sync-time.md) com base na configuração padrão. Pergunte a si mesmo: é possível aguardar essa sincronização de dados inicial após a integração de um serviço do Commerce?

- **Adicionando Novos Modos de Exibição de Loja ou Sites**-Se você planeja adicionar Modos de Exibição de Loja ou Sites com a mesma contagem de produto após a ativação, estime o volume de dados e o tempo de transmissão. Determine se o tempo de sincronização é aceitável com a configuração padrão ou se o processamento de vários threads é necessário.

- **Importações regulares** - Antecipe importações regulares, como atualizações de preços ou alterações de status do estoque. Avalie se essas atualizações podem ser aplicadas dentro de um período de tempo aceitável ou se é necessário um processamento mais rápido.

- **Peso do Produto**-Considere se seus produtos são leves ou pesados. Ajuste o tamanho do lote adequadamente se as descrições ou atributos do produto aumentarem o tamanho do produto.

Lembre-se de que um planejamento criterioso, incluindo a estimativa do volume de dados e do tempo de sincronização, pode frequentemente eliminar a necessidade de personalização. Agende operações de assimilação de feed com base nessas estimativas para atingir resultados ideais.

>[!NOTE]
>
>A Adobe recomenda ter cuidado ao usar o processamento de vários threads. Se você configurar multi-threading para um desempenho mais rápido, poderá acionar as medidas de proteção incluídas dos Serviços Adobe Commerce para evitar o uso indevido do sistema durante a assimilação de dados. Essas medidas de proteção também impedem que os usuários acionem alterações de sincronização que podem sobrecarregar o sistema. Quando as grades de proteção são acionadas, as solicitações são bloqueadas e o sistema retorna erros 429. Se encontrar esses erros, ajuste sua configuração e envie um tíquete de suporte para obter assistência.

## Configurar multi-threading

O modo de vários threads tem suporte para todos os [métodos de sincronização](data-synchronization.md#synchronization-process)—sincronização completa, sincronização parcial e sincronização de itens com falha. Para configurar multi-threading, especifique o número de threads e o tamanho do lote a serem usados durante a sincronização.

- `thread-count` é o número de threads ativados para processar entidades. O padrão `thread-count` é `1`.
- `batch-size` é o número de entidades processadas em uma iteração. O padrão `batch-size` são `100` registros para todos os feeds, exceto o feed de preço. Para o feed de preço, o valor padrão é `500` registros.

Você pode configurar vários threads como uma opção temporária ao executar um comando resync ou adicionando a configuração de vários threads à configuração do aplicativo Adobe Commerce.

>[!NOTE]
>
>Alinhe o desempenho da exportação de dados SaaS com o limite de taxa definido para um cliente no lado do consumidor.

### Configurar multi-threading no tempo de execução

Ao executar um comando de sincronização completa a partir da linha de comando, especifique o processamento de vários threads adicionando as opções `thread-count` e `batch-size` ao comando da CLI.

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

As opções especificadas na linha de comando substituem a configuração de exportação de dados especificada no arquivo `config.php` do aplicativo Adobe Commerce.

### Adicionar multi-threading à configuração do Commerce

Para processar todas as operações de exportação de dados usando multi-threading, os integradores de sistema ou desenvolvedores podem modificar o número de threads e o tamanho do lote para cada feed na configuração do aplicativo do Commerce.

Essas alterações podem ser aplicadas adicionando valores personalizados à [seção do sistema](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system) do arquivo de configuração, `app/etc/config.php`.

**Exemplo: configuração de multithreading para produtos e preços**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
