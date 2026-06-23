---
title: Sincronização de dados
description: Revise os dados do catálogo que estão sendo sincronizados da sua fonte de dados do Commerce para  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
TQID: https://experienceleague.adobe.com/ZTMFkch-YNS-CUgCdadmg1kemA8ORXQ7KGCEkI7d-Yw
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: c7633056caec2fcec318f8ebcc9664cfc7b3b9b4
workflow-type: tm+mt
source-wordcount: 484
ht-degree: 0%

---

# Sincronização de dados

A página **Sincronização de Dados** exibe uma visão geral do status de sincronização dos dados do produto transferidos de sua fonte de dados (seu catálogo Commerce existente, sistema PIM (Gerenciamento de Informações do Produto), sistema ERP (Planejamento de Recursos Empresariais) etc.) para o [!DNL Adobe Commerce Optimizer].

A página **Sincronização de Dados** fornece informações valiosas sobre a disponibilidade de dados de produtos para a sua vitrine eletrônica, garantindo que eles possam ser exibidos imediatamente aos seus compradores.

A página **Sincronização de Dados** está localizada em *Configuração* > **Sincronização de dados**.

![Sincronização de Dados](../assets/data-sync.png)

A página **Sincronização de Dados** contém os seguintes campos:

| Campo | Descrição |
| --- | --- |
| Origem do catálogo | Local específico dos dados sincronizados. |
| [!DNL Catalog Service] | Exibe a última atualização de sincronização, o total de produtos recebidos, um campo de pesquisa e uma tabela dos produtos sincronizados para [!DNL Catalog Service]. |
| Descoberta de produto | Exibe a última atualização de sincronização, o total de produtos recebidos, um campo de pesquisa e uma tabela dos produtos sincronizados para Pesquisa. |
| Recommendations | Exibe a última atualização de sincronização, o total de produtos recebidos, um campo de pesquisa e uma tabela dos produtos sincronizados para o Recommendations. |
| Produtos recebidos nas últimas 3 horas | Exibe o número de produtos que foram transferidos da origem do catálogo para [!DNL Adobe Commerce Optimizer] nas últimas três horas. Se você fizer atualizações pouco frequentes no catálogo, esse valor será frequentemente zero. |
| Total de produtos no catálogo | Reflete o número total de produtos de catálogo disponíveis para [!DNL Adobe Commerce Optimizer]. |
| Produtos sincronizados | Fornece detalhes sobre os produtos sincronizados com o [!DNL Adobe Commerce Optimizer]. Por padrão, essa tabela é classificada por &quot;Última atualização&quot;. Para localizar um produto específico, use o campo **[!UICONTROL Search by Name or SKU]**. |

## Lista de produtos sincronizados

Para ver os detalhes de um produto sincronizado no formato JSON, clique no ícone de código ![Link de código](../assets/data-sync-details.png) na linha do produto da tabela de produtos sincronizados.

![Detalhes do produto sincronizado](../assets/synced-products.png)

## Ressincronizar dados do catálogo

Se você não vir produtos específicos na página **Sincronização de Dados**, precisará iniciar uma ressincronização a partir do sistema upstream. No entanto, lembre-se de que uma ressincronização pode aumentar a carga dos recursos de hardware. No entanto, a ressincronização do catálogo pode ser necessária nos seguintes cenários:

- Quando são feitas alterações significativas no catálogo de produtos, como adicionar novos produtos, atualizar detalhes do produto ou modificar categorias

- Se você observar discrepâncias ou problemas de desempenho na exibição dos dados do produto em suas lojas

>[!IMPORTANT]
>
>O tempo necessário para concluir a sincronização varia de acordo com o tamanho do catálogo e o volume de dados atualizados.

## Verifique se a sincronização de dados está funcionando

Para projetos que usam o Adobe Commerce como fonte de dados de upstream por meio do Adobe Commerce Optimizer Connector, é possível monitorar o processo de exportação de dados e iniciar operações de ressincronização na página Status de sincronização do feed de dados. Para obter detalhes, consulte [Verificar se a sincronização de dados está funcionando](../../aco-connector/data-sync-manage.md#verify-that-the-data-sync-is-working) na documentação do _Adobe Commerce Optimizer Connector_.

## Tópicos relacionados

- [Adobe Commerce Optimizer Connector](../../aco-connector/overview.md){target="_blank"}

