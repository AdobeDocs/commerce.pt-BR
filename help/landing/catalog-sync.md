---
title: Sincronização de catálogo
description: Saiba como exportar dados do produto do  [!DNL Commerce] servidor para o [!DNL Commerce Services].
feature: Catalog Management, Data Import/Export, Catalog Service
exl-id: 99f96b93-b036-490c-8c57-40463a0de365
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Sincronização de catálogo

>[!NOTE]
>
> O Painel de sincronização do catálogo agora é o Painel de gerenciamento de dados. Este painel renovado agora dá suporte a [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+ e [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+. Os clientes podem obter o Painel de gerenciamento de dados atualizando para a versão mais recente de um desses serviços. Leia mais sobre isso na documentação do [Painel de gerenciamento de dados](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html). Este tópico atual permanece para os usuários que ainda não atualizaram e ainda têm o painel Sincronização de catálogo.

O Adobe Commerce usa indexadores para compilar dados de catálogo em tabelas. O processo é automaticamente acionado por [eventos](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html#events-that-trigger-full-reindexing), como uma alteração no preço de um produto ou no nível do estoque.

O serviço de Sincronização de Catálogo move os dados do produto de uma instância do [!DNL Adobe Commerce] para a plataforma do [!DNL Commerce Services] continuamente para manter os dados atualizados. Por exemplo, o [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) exige as informações atuais do catálogo para retornar com precisão as recomendações com nomes, preços e disponibilidade corretos. Use o painel _Sincronização de Catálogo_ para observar e gerenciar o processo de sincronização ou a interface de linha de comando para disparar uma sincronização de catálogo e reindexar os dados do produto para consumo por [!DNL Commerce Services]. Consulte [Referência de interface de linha de comando](../data-export/data-export-cli-commands.md) no Guia _Exportação de dados SaaS_.

## Acesso ao painel Sincronização do catálogo

Para acessar o painel Sincronização de Catálogo, selecione **Sistema** > _Transferência de Dados_ > **Sincronização de Catálogo**.

Com o painel **Sincronização de Catálogo**, você pode:

- Exibir o status da sincronização (**Em Andamento**, **Êxito**, **Falha**)
- Exibir o número total de produtos sincronizados
- Pesquisar produtos sincronizados para exibir seu estado atual
- Pesquise o catálogo da loja por nome, SKU etc.
- Exibir detalhes do produto sincronizado no JSON para ajudar a diagnosticar uma discrepância de sincronização
- Reiniciar o processo de sincronização

### Última sincronização

Relata um status de sincronização de:

- **Sucesso** - Exibe a data e a hora em que a sincronização foi bem-sucedida e o número de produtos atualizados
- **Falha** - Exibe a data e a hora em que a sincronização foi tentada
- **Em andamento** - Exibe a data e a hora da última sincronização bem-sucedida

O processo de sincronização de catálogo é executado automaticamente a cada hora. Se você não vir os produtos esperados na loja, ou se os produtos não refletirem as alterações recentes feitas, você pode resolver [problemas de sincronização de catálogo](#resolvesync).

### Produtos sincronizados

Exibe o número total de produtos sincronizados do catálogo do [!DNL Commerce]. Após a sincronização inicial, somente os produtos alterados devem ser sincronizados.

## Ressincronizar {#resync}

Se você precisar iniciar uma ressincronização do catálogo antes que a sincronização agendada por hora ocorra, é possível forçar uma ressincronização.

>[!NOTE]
>
> Forçar uma ressincronização aciona uma ressincronização de todo o catálogo de produtos, o que pode aumentar a carga dos recursos de hardware.

1. No painel _Sincronização de Catálogo_, selecione **Configurações**.

   A página _Configurações de Sincronização do Catálogo_ é exibida.

1. Na seção _Ressincronizar Dados_, clique em [!UICONTROL Resync].

   O [!DNL Commerce] sincroniza seu catálogo durante a próxima janela de sincronização agendada. Dependendo do tamanho do catálogo, essa operação pode levar muito tempo.

## Produtos de catálogo sincronizados

A tabela **Produtos de catálogo sincronizados** exibe as informações a seguir.

| Campo | Descrição |
|---|---|
| ID | Identificador exclusivo do produto |
| Nome | Nome da vitrine do produto |
| Tipo | Identifica o tipo do produto, como simples, configurável ou baixável |
| Última exportação | Data em que o produto foi exportado com êxito do catálogo pela última vez |
| Última modificação | Data da última modificação do produto no catálogo |
| SKU | Exibe a unidade de manutenção de estoque do produto |
| Preço | Preço do produto |
| Visibilidade | Uma configuração de visibilidade do produto conforme definido no catálogo [!DNL Commerce] |

## Resolver problemas de sincronização do catálogo {#resolvesync}

Consulte [Logs e solução de problemas](../data-export/troubleshooting-logging.md#troubleshooting) no _Guia de Exportação de Dados SaaS_.
