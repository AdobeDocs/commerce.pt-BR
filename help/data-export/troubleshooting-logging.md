---
title: Revisar logs e solucionar problemas
description: Saiba como solucionar erros [!DNL data export] usando os logs de exportação de dados e exportação de saas.
feature: Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Revisar logs e solucionar problemas

A extensão [!DNL data export] fornece logs para rastrear processos de sincronização e coleta de dados.

## Logs

Os logs estão disponíveis no diretório `var/log` no servidor de aplicativos do Commerce.

| nome do log | filename | descrição |
|-----------------| ----------| -------------|
| Log de exportação de dados SaaS | `commerce-data-export.log` | Fornece informações sobre atividades de exportação de dados, como eventos de entidade e acionadores de ressincronização completa.  Cada registro de log tem uma estrutura específica e fornece informações sobre o feed, a operação, o status, o tempo decorrido, a ID do processo e o chamador. |
| Log de erros de exportação de dados SaaS | `data-export-errors.log` | Fornece mensagens de erro e rastreia erros que ocorrem durante o processo de sincronização de dados. |
| Log de exportação SaaS | `saas-export.log` | Fornece informações sobre os dados enviados para os serviços SaaS da Commerce. |
| Log de erros de exportação SaaS | `saas-export-errors.log` | Fornece informações sobre erros que ocorrem ao enviar dados para os serviços SaaS da Commerce. |

Se você não vir os dados esperados para um serviço do Adobe Commerce, use os logs de erro da extensão de exportação de dados para determinar onde o problema ocorreu. Além disso, é possível estender registros com dados adicionais para rastreamento e solução de problemas. Consulte [Logon estendido](#extended-logging).

### Formato do log

Cada registro de log tem a seguinte estrutura.

```
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elaspsed from script run>",
   "pid": "<proccess id who executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>A string baseada em JSON é aprimorada para facilitar a leitura.

A tabela a seguir descreve os tipos de operação que podem ser registrados nos logs.

| Operação | Descrição | Exemplo do chamador |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| sincronização completa | A sincronização completa coleta e envia todos os dados para o SaaS de um determinado feed. | `bin/magento saas:resync --feed=products` |
| reindexação parcial | A sincronização parcial coleta e envia dados para o SaaS somente para entidades atualizadas em um determinado feed. Este log só estará presente se existirem entidades atualizadas. | `bin/magento cron:run --group=index` |
| tentar novamente os itens com falha | Reenvia itens de um determinado feed para o SaaS se a operação de sincronização anterior falhou devido a um erro de aplicativo ou servidor do Commerce. Este log só estará presente se houver itens com falha. | `bin/magento cron:run --group=saas_data_exporter` (qualquer grupo cron &quot;*_data_exporter&quot;) |
| sincronização completa (herdada) | Sincronização completa para um determinado feed no modo de exportação herdado. | `bin/magento saas:resync --feed=categories` |
| reindexação parcial (herdado) | Envia entidades atualizadas para o SaaS para um determinado feed no modo de exportação herdado. Este log só estará presente se existirem entidades atualizadas. | `bin/magento cron:run --group=index` |
| sincronização parcial (herdada) | Envia entidades atualizadas para o SaaS para um determinado feed no modo de exportação herdado. Este log só estará presente se existirem entidades atualizadas. | `bin/magento cron:run --group=saas_data_exporter` (qualquer grupo cron &quot;*_data_exporter&quot;) |


### Exemplos de registro

Durante uma ressincronização completa, o progresso é rastreado e registrado a cada 30 segundos por padrão. Este é um exemplo de entrada de log.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

Neste exemplo, os valores `status` fornecem informações sobre a operação de sincronização:

- **`"Progress 2/5"`** indica que 2 de 5 iterações foram concluídas. O número de iterações depende do número de entidades exportadas.
- **`"processed: 200"`** indica que 200 itens foram processados.
- **`"synced: 100"`** indica que 100 itens foram enviados para SaaS. Espera-se que `"synced"` não seja igual a `"processed"`. Veja um exemplo:
   - **`"synced" < "processed"`** significa que a tabela de feed não detectou alterações no item em comparação à versão sincronizada anteriormente. Esses itens são ignorados durante a operação de sincronização.
   - **`"synced" > "processed"`** a mesma id de entidade (por exemplo, `Product ID`) pode ter vários valores em escopos diferentes. Por exemplo, um produto pode ser atribuído a cinco sites. Nesse caso, você pode ter &quot;1 item processado&quot; e &quot;5 itens sincronizados&quot;.

+++ **Exemplo: Log de ressincronização completo para o feed de preço**

```
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## Exibir e solucionar problemas de logs com o New Relic

Se você armazenar logs do Adobe Commerce na New Relic, poderá adicionar regras de análise para melhorar a legibilidade e a experiência de consulta.

1. Faça logon no New Relic.

1. Ir para `Logs => Parsing`.

1. Clique em `Create parsing rule`.

1. Configure a regra de análise adicionando os seguintes valores.

   - **Filtrar logs com base no NRQL**

     `filePath LIKE '%commerce-data-export%.log'`

   - **Regra de análise**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel} %{GREEDYDATA:feed:json}`

Esse exemplo adiciona uma regra que permite consultar logs do New Relic por tipo de feed específico, operação e assim por diante.

**Exemplo de cadeia de caracteres de consulta**—`feed.feed:"products" and feed.status:"Complete"`

## Solução de problemas

Se os dados estiverem ausentes ou incorretos nos Serviços do Comércio, verifique os logs para ver se ocorreu um problema durante a sincronização da instância do Adobe Commerce com a plataforma Commerce Service. Se necessário, use o registro estendido para adicionar mais informações aos registros para solucionar problemas.

- commerce-data-export-errors.log - se ocorreu um erro durante a fase de coleta
- saas-export-errors.log - se um erro ocorreu durante a fase de transmissão

Se você vir erros não relacionados à configuração ou a extensões de terceiros, envie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=en#submit-ticket) com o máximo de informações possível.

### Resolver problemas de sincronização do catálogo {#resolvesync}

Quando você aciona uma ressincronização de dados, pode levar até uma hora para que os dados sejam atualizados e refletidos nos componentes da interface do usuário, como pesquisa em tempo real e unidades de recomendação. Se você ainda vir discrepâncias entre o catálogo e os dados na loja da Commerce, ou se a sincronização do catálogo falhar, consulte o seguinte:

#### Discrepância de dados

1. Exiba a exibição detalhada do produto em questão nos resultados da pesquisa.
1. Copie a saída JSON e verifique se o conteúdo corresponde ao que você tem no catálogo [!DNL Commerce].
1. Se o conteúdo não corresponder, faça uma pequena alteração no produto no catálogo, como adicionar um espaço ou um ponto.
1. Aguarde uma ressincronização ou [acione uma ressincronização manual](#resync).

#### A sincronização não está em execução

Se a sincronização não estiver sendo executada de acordo com um agendamento ou se nada estiver sincronizado, consulte este artigo da [KnowledgeBase](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html).

#### Falha na sincronização

Se a sincronização do catálogo tiver um status de **Falha**, envie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket).

## Logon estendido

Para obter informações de log adicionais, você pode usar variáveis de ambiente para estender logs com dados adicionais para rastreamento e solução de problemas.

Há dois arquivos de log no diretório `var/log/`:

- commerce-data-export-errors.log - se ocorreu um erro durante a fase de coleta
- saas-export-errors.log - se um erro ocorreu durante a fase de transmissão

Você pode usar variáveis de ambiente para estender logs com dados adicionais para rastreamento e solução de problemas.

### Verificar a carga do feed

Inclua a carga do feed no log de exportação do SaaS, adicionando a variável de ambiente `EXPORTER_EXTENDED_LOG=1` quando sincronizar novamente o feed.

```shell script
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

Após a conclusão da operação, a carga do feed estará disponível para revisão no log de exportação do SaaS (`var/.log/saas-export.log`).

### Preservar conteúdo na tabela de índice do feed

Para a extensão de exportação de dados SaaS do Commerce (`magento/module-data-exporter`) 103.3.0 e posterior, os feeds de exportação imediatos mantêm somente os dados mínimos necessários na tabela de índice. Os feeds incluem todos os feeds de status do catálogo e do estoque de estoque.

A preservação de dados de carga útil na tabela de índice não é recomendada em ambientes de produção, mas pode ser útil em um ambiente de desenvolvedor. Inclua a carga do feed no índice adicionando a variável de ambiente `PERSIST_EXPORTED_FEED=1` ao ressincronizar o feed.

```shell script
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### Execute o Profiler para solucionar problemas de desempenho lento

Se o processo de reindexação de um feed específico demorar um tempo excessivo, execute o profiler para coletar dados adicionais que podem ser úteis para a Equipe de suporte.

Execute o profiler adicionando a variável de ambiente `EXPORTER_PROFILER=1` quando você executar o comando reindex.

```
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

Os dados do criador de perfil são armazenados no log de exportação de dados (`var/log/commerce-data-export.log`) no seguinte formato:

```
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```
