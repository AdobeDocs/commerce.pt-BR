---
title: Sincronizar dados com a exportação de dados SaaS
description: Saiba como o  [!DNL SaaS Data Export]  coleta e sincroniza dados entre instâncias do Adobe Commerce e serviços SaaS conectados.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: 55c433f36b122813e8fc9136a7efbb869246b7f5
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Sincronizar dados com a exportação de dados SaaS

Quando você instala um serviço do Commerce que requer exportação de dados, como Serviço de catálogo, Live Search ou Recomendações de produto, uma coleção de módulos de exportação de dados do Saas é instalada para gerenciar o processo de coleta e sincronização de dados.

A exportação de dados SaaS move os dados do produto de uma instância do Adobe Commerce para a plataforma de serviços da Commerce de forma contínua para manter os dados atualizados. Por exemplo, as Recomendações de produto exigem informações atuais do catálogo para retornar com precisão as recomendações com nomes, preços e disponibilidade corretos. Use o [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) para observar e gerenciar o processo de sincronização, ou a interface de linha de comando para disparar uma sincronização e reindexar os dados do produto para consumo pelos Serviços Commerce.

O diagrama a seguir mostra o fluxo de exportação de dados SaaS.

![Coleta de exportação de dados SaaS e fluxo de sincronização para Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Os principais componentes do fluxo de exportação de dados SaaS incluem:

- Módulos de exportação de dados SaaS que coletam os dados para feeds do Adobe Commerce, montam itens de feed, aguardam atualizações e persistem o status do feed.
- Módulos de exportação SaaS que exportam dados, configuram o roteamento e publicam os feeds para serviços conectados.
- O Serviço do Adobe Commerce gerencia o processo de assimilação de dados para validar feeds recebidos e atualizações persistentes nos serviços conectados.

## Modos de sincronização

A exportação de dados SaaS tem dois modos para processar feeds de entidade:

- **Modo de exportação imediata** — Neste modo, os dados são coletados e enviados imediatamente para o Commerce Service em uma única iteração. Esse modo acelera a entrega de atualizações de entidades ao serviço do Commerce e reduz o tamanho do armazenamento das tabelas de feed.

- **Modo de exportação herdado** — Neste modo, os dados são coletados em um único processo. Em seguida, um trabalho cron envia os dados coletados para os serviços de comércio conectados. Nas entradas do log de exportação de dados, os feeds que usam o modo herdado são rotulados como `(legacy)`.

## Tipos de sincronização

A exportação de dados SaaS suporta três tipos de sincronização - sincronização completa, sincronização parcial e nova tentativa de sincronização de itens com falha.

### Sincronização completa

Depois de conectar uma instância do Adobe Commerce ao Commerce Service, execute uma sincronização completa para enviar dados de feed de entidade do Adobe Commerce para o serviço conectado.

>[!NOTE]
>
>A sincronização completa é principalmente para a fase de integração. Evite o uso regular para evitar a sobrecarga do banco de dados. Após a sincronização inicial, as alterações em andamento são sincronizadas automaticamente usando a sincronização parcial.

### Sincronização parcial

Com a sincronização parcial, a exportação de dados SaaS envia automaticamente as atualizações do aplicativo Commerce, como alterações de nome de produto ou atualizações de preço, para os serviços de comércio conectados.

O processo de exportação de dados usa os seguintes trabalhos cron para automatizar a operação de sincronização parcial.

- trabalhos do grupo cron &quot;index&quot;:
   - O trabalho `indexer_reindex_all_invalid` reindexa todos os feeds inválidos. É um trabalho cron padrão do Adobe Commerce.
   - O trabalho `saas_data_exporter` é para feeds de exportação herdados.
   - O trabalho `sales_data_exporter` é específico ao feed de exportação de dados de vendas.

Esses trabalhos são executados a cada minuto.

Para que a sincronização parcial funcione, o aplicativo Commerce requer a seguinte configuração:

- [O agendamento de tarefas está habilitado por meio de trabalhos cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- Todos os indexadores de exportação de dados SaaS estão configurados no modo `Update by Schedule`.

  Na versão de exportação de dados SaaS 103.1.0 e posterior, o modo `Update by Schedule` é habilitado por padrão. Você pode verificar a configuração de índice no servidor usando o comando da CLI do Commerce, `bin/magento indexer:show-mode | grep -i feed`

### Repetir sincronização de Itens com Falha

A sincronização Repetir itens com falha usa um processo separado para reenviar itens que não foram sincronizados devido a erros durante o processo de sincronização, por exemplo, um erro de aplicativo, uma interrupção de rede ou um erro de serviço SaaS. A implementação desta sincronização também se baseia em trabalhos cron.

- `resync_failed_feeds_data_exporter` trabalhos do grupo cron:
   - O trabalho `<feed name>_feed_resend_failed_feeds_items` reenvia itens com falha de sincronização, por exemplo `products_feed_resend_failed_items`.

### Exibir e gerenciar o processo de sincronização

A maioria das atividades de sincronização é processada automaticamente com base na configuração do aplicativo. No entanto, a exportação de dados SaaS também fornece ferramentas para gerenciar o processo.

- Os usuários administradores podem exibir e acompanhar o progresso da sincronização e obter informações sobre os dados no [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

- Desenvolvedores, integradores de sistemas ou administradores com acesso ao servidor de aplicativos do Commerce podem gerenciar o processo de sincronização e os feeds de dados usando a CLI (Command-Line Tool, ferramenta de linha de comando) do Adobe Commerce. Consulte [Gerenciar operações de sincronização usando a CLI do Commerce](data-export-cli-commands.md).

### Verificar a configuração do aplicativo do Commerce

A sincronização parcial e a sincronização de itens com falha de Repetir funcionam somente se a instância do Commerce tiver sido configurada corretamente. Normalmente, a configuração é concluída ao configurar o serviço do Commerce. Se a exportação de dados não estiver funcionando corretamente, verifique a seguinte configuração.

- [Confirme se os trabalhos cron estão em execução](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Verifique se os indexadores estão sendo executados do [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) ou usando o comando `bin/magento indexer:info` da CLI do Commerce.

- Verifique se os indexadores dos seguintes feeds estão definidos como `Update by Schedule`: Atributos do Catálogo, Produto, Substituições de Produto e Variante de Produto. Você pode verificar os indexadores do [Gerenciamento de Índice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) no Administrador ou usando a CLI (`bin/magento indexer:show-mode | grep -i feed`).

### Notificações do gerenciador de eventos para o log de transferência de dados

Na versão 103.3.4 e posterior, a Exportação de dados SaaS despacha o evento `data_sent_outside` quando os dados são enviados da instância do Commerce para os serviços da Adobe Commerce.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>Para obter informações sobre eventos e como se inscrever neles, consulte [Eventos e Observadores](https://developer.adobe.com/commerce/php/development/components/events-and-observers) na Documentação do desenvolvedor do Adobe Commerce.
