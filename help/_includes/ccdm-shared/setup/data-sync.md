---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%
---
A página **Sincronização de Dados** exibe uma visão geral do status de sincronização dos dados do produto transferidos de sua fonte de dados (seu catálogo Commerce existente, o sistema PIM (Gerenciamento de Informações do Produto), o sistema ERP (Planejamento de Recursos Empresariais) etc.) para a camada de dados dos Serviços de Merchandising.

A página **Sincronização de Dados** fornece informações valiosas sobre a disponibilidade de dados de produtos para a sua vitrine eletrônica, garantindo que eles possam ser exibidos imediatamente aos seus compradores.

## Acessar o espaço de trabalho de Sincronização de Dados

A forma como você abre o espaço de trabalho *Sincronização de Dados* depende do produto que você usa:

- **Administrador Do Adobe Commerce** (Adobe Commerce as a Cloud Service)—Selecione *Lojas* > **Sincronização De Catálogo**.
- **Adobe Commerce Optimizer Studio**—Selecione *Configuração de armazenamento* > **Sincronização de Dados**.

![Sincronização de Dados](/help/assets/ccdm-shared/setup/data-sync.png)

A página **Sincronização de Dados** contém os seguintes campos:

| Campo | Descrição |
| --- | --- |
| Origem do catálogo | Local específico dos dados sincronizados. |
| [!DNL Catalog Service] | Exibe a última atualização de sincronização, o total de produtos recebidos, um campo de pesquisa e uma tabela dos produtos sincronizados para [!DNL Catalog Service]. |
| Descoberta de produto | Exibe a última atualização de sincronização, o total de produtos recebidos, um campo de pesquisa e uma tabela dos produtos sincronizados para Pesquisa. |
| Recommendations | Exibe a última atualização de sincronização, o total de produtos recebidos, um campo de pesquisa e uma tabela dos produtos sincronizados para o Recommendations. |
| Produtos recebidos nas últimas 3 horas | Exibe o número de produtos que foram transferidos da origem do catálogo para a camada de dados de Serviços de merchandising nas últimas três horas. Se você fizer atualizações pouco frequentes no catálogo, esse valor será frequentemente zero. |
| Total de produtos no catálogo | Reflete o número total de produtos de catálogo disponíveis na camada de dados Serviços de merchandising. |
| Produtos sincronizados | Fornece detalhes sobre os produtos sincronizados com a camada de dados dos Serviços de merchandising. Por padrão, essa tabela é classificada por &quot;Última atualização&quot;. Para localizar um produto específico, use o campo **[!UICONTROL Search by Name or SKU]**. |

## Lista de produtos sincronizados

Para ver os detalhes de um produto sincronizado no formato JSON, clique no ícone de código ![Link de código](/help/assets/ccdm-shared/setup/data-sync-details.png) na linha do produto da tabela de produtos sincronizados.

![Detalhes do produto sincronizado](/help/assets/ccdm-shared/setup/synced-products.png)

## Ressincronizar dados do catálogo

Se você não vir produtos específicos na página **Sincronização de Dados**, precisará iniciar uma ressincronização a partir do sistema upstream. No entanto, lembre-se de que uma ressincronização pode aumentar a carga dos recursos de hardware. No entanto, a ressincronização do catálogo pode ser necessária nos seguintes cenários:

- Quando são feitas alterações significativas no catálogo de produtos, como adicionar novos produtos, atualizar detalhes do produto ou modificar categorias

- Se você observar discrepâncias ou problemas de desempenho na exibição dos dados do produto em suas lojas

>[!IMPORTANT]
>
>O tempo necessário para concluir a sincronização varia de acordo com o tamanho do catálogo e o volume de dados atualizados.

## Verifique se a sincronização de dados está funcionando

Para projetos que usam o Adobe Commerce como fonte de dados de upstream, você pode monitorar o processo de exportação de dados e iniciar operações de ressincronização na página Status de sincronização do feed de dados. Para obter detalhes, consulte [Monitoramento do status de sincronização do feed de dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status).
