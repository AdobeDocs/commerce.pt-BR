---
title: '[!DNL SaaS Data Export Guide]'
description: Saiba mais sobre como usar a extensão  [!DNL data export]  para serviços SaaS do Adobe Commerce que sincroniza dados entre o Adobe Commerce e os serviços Commerce conectados.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Guia do [!DNL SaaS Data Export]

[!DNL SaaS data export] sincroniza dados entre uma instância do Adobe Commerce e o Commerce Services conectado. Ao adicionar o Live Search, as Recomendações de Produto ou o Serviço de Catálogo a uma instalação do Adobe Commerce, a extensão [!DNL Data export] é instalada automaticamente.

A exportação de dados SaaS coleta e exporta vários tipos de dados, chamados de _feeds_, que agregam tipos específicos de informações. Dependendo dos serviços Commerce instalados, os feeds de exportação de dados SaaS incluem:

- **Feeds de entidade de catálogo** agregam dados de produto. Os dados incluem produtos, atributos de produto, preços de produto, variações de produto, categorias, permissões de categoria e permissões de produto.
- O **feed de Escopos** agrega dados para grupos de clientes, sites, lojas e visualizações de loja.
- O **feed de Ordem de Venda** agrega dados de pedidos, incluindo suas entidades relacionadas, como faturas, remessas, avisos de crédito e assim por diante.
- O **feed de Inventário MultisSource** agrega dados sobre os itens de status do estoque do estoque.

A exportação de dados SaaS é fornecida como uma extensão PHP. Ela é compatível com vários métodos para iniciar e gerenciar o processo de sincronização de dados.

- **Sincronização manual do Administrador ou da linha de comando**

   - O [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/data-transfer/data-dashboard) no Administrador do Commerce fornece uma exibição gráfica do status de sincronização. Você pode usar o painel para executar uma ressincronização completa (_sincronização completa_) de todos os feeds. No entanto, a Adobe recomenda apenas executar uma sincronização completa na primeira vez que você conecta o Adobe Commerce a um serviço do Commerce. Consulte [Processo de sincronização](data-synchronization.md).

   - A [ferramenta de linha de comando do Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) fornece comandos para sincronizar feeds específicos e inclui opções adicionais para personalizar o processamento do feed.

- **Sincronização automatizada com trabalhos cron**

   - [Sincronização de dados parciais](data-synchronization.md#partial-synchronization-with-cron-jobs) — Os trabalhos do Cron acionam uma sincronização de dados parcial quando um usuário administrador do Commerce atualiza uma entidade. O processo de exportação de dados envia apenas essas atualizações para os serviços conectados da Commerce. O processo de sincronização parcial é baseado no mecanismo MView e não requer nenhuma ação do usuário administrador ou do integrador de sistema.

   - [Nova tentativa automática para erros de sincronização](data-synchronization.md#failed-items-sync-for-error-recovery)—Os trabalhos do Cron acionam uma nova tentativa automática do processo de sincronização quando ocorrem erros durante o processo de sincronização de dados.

- **Exportar agendamento e desempenho**

   - Desenvolvedores e integradores de sistemas podem estimar o tempo necessário para a exportação de dados SaaS sincronizar dados entre o Adobe Commerce e os serviços conectados. Essa estimativa pode ajudar a agendar o processamento da exportação de dados para evitar a interrupção do site. Consulte [Estimar volume de dados e tempo de transmissão](estimate-data-volume-sync-time.md).

   - Nos casos em que a sincronização precisa ocorrer mais rapidamente, a exportação de dados do SaaS fornece opções de personalização para melhorar o desempenho do processamento da exportação. Consulte [Melhorar o desempenho da exportação de dados](customize-export-processing.md).

- **Rastrear e solucionar problemas de atividades de exportação de dados**—Use os logs de exportação de dados e de exportação de saas para revisar o status da sincronização e as cargas do feed durante o processo de sincronização e indexação. Consulte [Logs e solução de problemas](troubleshooting-logging.md).
