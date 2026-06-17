---
title: Cenários de Solução de Problemas do  [!DNL SaaS Data Export]
description: Saiba como diagnosticar e resolver comportamentos de sincronização inesperados [!DNL SaaS Data Export] causados por configurações incorretas, configurações do indexador ou interpretações incorretas dos resultados de sincronização.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# Solução de problemas de cenários para [!DNL SaaS Data Export]

Esta página descreve comportamentos que você pode observar ao trabalhar com o [!DNL SaaS Data Export], que normalmente são causados por uma configuração incorreta ou interpretação incorreta dos resultados de sincronização. Use as descrições abaixo para identificar a causa raiz e aplicar a resolução apropriada.

## Produto configurável ou em pacote ausente nos serviços da Commerce {#configurable-bundle-missing}

**Problema:** um produto configurável ou em pacote tem o status *Habilitado* em [!DNL Adobe Commerce], mas não é retornado na loja ou é exibido com o status *Desabilitado* nos serviços SaaS da Commerce.

**Causa:** o status efetivo dos produtos compostos depende do status dos produtos derivados, não apenas do status do produto principal. Os serviços SaaS da Commerce refletem esse status calculado:

- **Produtos configuráveis** - pelo menos uma variante de produto deve ser habilitada.
- **Agrupar produtos** - pelo menos um produto deve ser habilitado para cada opção de pacote necessária.

Se essas condições não forem atendidas, o produto principal será tratado como desabilitado mesmo se seu próprio status for definido como *Habilitado*.

**Solução:**

- Para produtos configuráveis, verifique se pelo menos uma variante de produto simples associada está habilitada e atribuída ao site e à exibição de loja corretos.
- Para produtos agrupados, verifique se cada opção de pacote necessária tem pelo menos um produto filho habilitado. Uma opção necessária com todos os filhos desativados faz com que todo o pacote seja tratado como desativado.
- Depois de ativar os produtos secundários apropriados, acione uma ressincronização ou aguarde a próxima sincronização agendada e, em seguida, confirme o status atualizado nos serviços SaaS da Commerce.

## Preços não atualizados após a ativação da regra de preço de catálogo {#prices-not-updated}

**Problema:** Após ativar uma regra de preço de catálogo usando o recurso Atualização Agendada, os preços não são atualizados. O `commerce-data-export.log` mostra `synced: 0` para `prices` feed após a aplicação das atualizações programadas.

**Causa:** uma condição de corrida pode ocorrer entre grupos cron quando as Atualizações Agendadas são usadas para regras de preço de catálogo. O indexador `catalog_data_exporter_product_prices` pode ser executado antes que sua dependência, o índice `catalogrule_product`, tenha terminado a reconstrução. Em consequência, o exportador de preços lê dados obsoletos e não exporta quaisquer alterações.

**Solução:**

A correção imediata para esse problema é uma solução alternativa: configure ambos os grupos cron para serem executados sequencialmente para eliminar a condição de corrida:

1. Vá para **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**.
1. Definir **[!UICONTROL Use Separate Process]** como **[!UICONTROL No]** para ambos:
   - Opções de configuração do Cron para o grupo: **[!UICONTROL index]**
   - Opções de configuração do Cron para o grupo: **[!UICONTROL staging]**
1. Limpe o cache de configuração depois de salvar.

>[!NOTE]
>
>Com ambos os grupos em execução no processo e sequencialmente, uma reindexação completa e lenta bloqueia a execução de preparo até a conclusão. Em catálogos grandes, isso pode atrasar atualizações de preparo.

## Discrepância de dados do catálogo entre [!DNL Adobe Commerce] e serviços conectados {#catalog-data-discrepancy}

**Problema:** Os dados do produto mostrados nos Serviços Commerce conectados (como [!DNL Live Search] ou [!DNL Product Recommendations]) não correspondem aos dados do catálogo em [!DNL Adobe Commerce]. Por exemplo, um nome de produto, preço ou descrição parece desatualizado ou incorreto na loja.

**Causa:** depois que uma ressincronização é acionada, pode levar até uma hora para que os dados sejam atualizados e refletidos nos componentes da interface do usuário. Se a discrepância persistir além dessa janela, talvez o item não tenha sido selecionado pela última sincronização ou a sincronização não tenha detectado uma alteração porque os dados do feed já estavam marcados como atualizados.

**Solução:**

1. Na loja do Commerce, abra os resultados da pesquisa. Em seguida, selecione o produto em questão para abrir a visualização detalhada.
1. Copie a saída JSON e verifique se ela corresponde ao que você tem no catálogo [!DNL Commerce].
1. Se o conteúdo não corresponder, faça uma pequena edição no produto no catálogo, como adicionar um espaço ou um ponto, para forçar a detecção da alteração.
1. Aguarde uma ressincronização ou acione uma ressincronização manual da CLI ou da página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) no Administrador.

Para obter soluções de problemas adicionais de dados de catálogo no [!DNL Product Recommendations], consulte [Solução de problemas do módulo de Recomendações de Produto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce) na Base de Dados de Conhecimento Commerce.

## A sincronização de dados não está sendo executada de acordo com o agendamento {#sync-not-on-schedule}

**Problema:** a sincronização de dados não é executada de acordo com o cronograma ou nenhum item está sendo sincronizado apesar das alterações no produto em [!DNL Adobe Commerce].

**Causa:** as causas mais comuns são trabalhos cron não executados ou indexadores não configurados no modo **[!UICONTROL Update by Schedule]**.

**Solução:**

- [Confirme se os trabalhos cron estão em execução](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verifique se os indexadores dos seguintes feeds estão definidos como **[!UICONTROL Update by Schedule]**: Atributos do Catálogo, Produto, Substituições de Produto e Variante de Produto. Verifique a partir de [[!UICONTROL Index Management]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) no Administrador do Commerce ou usando a CLI: `bin/magento indexer:show-mode | grep -i feed`.

## A sincronização do catálogo tem um status Falha {#catalog-sync-failed}

**Problema:** a sincronização do catálogo mostra o status **Falha** na página **[!UICONTROL Data Feed Sync Status]**.

**Causa:** Erro irrecuperável durante a coleta de dados ou a fase de envio. Causas comuns incluem problemas de autenticação de API, erros de rede ou falhas de validação de dados.

**Solução:**

1. Revise os logs de erro da exportação de dados para obter detalhes sobre a falha. Consulte [Revisar logs e solucionar problemas](logging.md) para ver o formato do log e as opções de log estendidas:
   - `var/log/commerce-data-export-errors.log` para erros durante a coleta de dados.
   - `var/log/saas-export-errors.log` para erros durante o envio de dados.
1. Se o erro não estiver relacionado à configuração ou a uma extensão de terceiros, [envie um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) com as entradas de log relevantes.

## O registro mostra mensagens de &quot;operação ignorada - processo bloqueado&quot; {#process-locked}

**Problema:** O arquivo `commerce-data-export.log` contém entradas semelhantes às seguintes:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**Causa:** Esse é um comportamento esperado, não um erro. A mensagem é exibida quando uma sincronização parcial acionada por cron tenta ser executada enquanto uma reindexação completa ou `saas:resync` já está em andamento. A extensão [!DNL SaaS Data Export] usa um mecanismo de bloqueio de feed para evitar operações de sincronização simultâneas conflitantes.

**Solução:**

Nenhuma ação é necessária. Quando o processo em execução for concluído e liberar o bloqueio, a próxima execução do cron selecionará e sincronizará todas as alterações pendentes. Para obter detalhes sobre como o mecanismo de bloqueio funciona, consulte [Mecanismo de bloqueio de feed para Exportação de Dados SaaS](../feed-lock-mechanism.md).

>[!MORELIKETHIS]
>
> - [Revisar logs e solucionar problemas](logging.md)
> - [Referência de códigos de log](log-codes-reference.md)
> - [Mecanismo de bloqueio de feed para Exportação de Dados SaaS](../feed-lock-mechanism.md)
