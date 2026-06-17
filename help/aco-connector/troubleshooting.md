---
title: Solucionar problemas do(a) [!DNL Adobe Commerce Optimizer Connector]
description: Saiba como solucionar problemas de [!DNL Adobe Commerce Optimizer Connector] credencial, sincronização de catálogo e exportação de escopo de integrações do  [!DNL Adobe Commerce] PaaS.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
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
source-wordcount: 331
ht-degree: 0%

---

# Solucionar problemas do [!DNL Adobe Commerce Optimizer Connector]

Use este guia para diagnosticar e resolver problemas comuns com o [!DNL Adobe Commerce Optimizer Connector] durante a instalação inicial, a sincronização do feed de catálogo e a configuração de exportação de escopo. As seções abaixo abordam validação de credencial e locatário, falhas de sincronização de dados e diagnóstico [!DNL SaaS Data Export] relacionado.

## Falha na validação de credenciais ou locatário

Se `aco:config:init` falhar durante a validação de credencial:

- Execute o comando da CLI `bin/magento aco:config:show` [!DNL Adobe Commerce] para verificar os valores armazenados.
- Confirme se a ID do locatário pertence à organização IMS usada para obter as credenciais.
- Confirme se o cliente OAuth tem os escopos necessários para o serviço de assimilação [!DNL Adobe Commerce Optimizer] (consulte [Obter Credenciais de IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)).

## Dados não sincronizados

**Verificar detalhes do erro no nível do item:**

Consulte [Verificar se a sincronização de dados está funcionando](./data-sync-manage.md#verify-that-the-data-sync-is-working) para obter as etapas para abrir o **[!UICONTROL Data Feed Sync Status]** no Administrador do Commerce. Selecione o feed com falha para visualizar os detalhes do erro por item.

Pontos principais sobre o tratamento de erros:

- **400 erros** não são repetidos. Inspecione o conteúdo em busca de campos obrigatórios malformados ou ausentes. Consulte [Mapeamento de campos para feeds de conector](reference/field-mapping.md) para obter o formato esperado.
- **5xx erros** são automaticamente repetidos pelo trabalho cron `*_resend_failed_items` (é executado a cada 5 minutos).

**Verificar configuração do escopo:**

Se o problema afetar apenas uma origem de catálogo específica (código de exibição de loja) ou catálogo de preços, verifique se a exibição correspondente do site ou da loja tem a sincronização desativada. Consulte [Personalizar a configuração de exportação de escopos do Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration).

**Quando resolvido:**

Os feeds de conector mostram um status de sucesso no **[!UICONTROL Data Feed Sync Status]**, e os produtos, preços e atributos esperados aparecem na página **[!UICONTROL Data Sync]** do [!DNL Commerce Optimizer].

## Configuração incorreta e interpretação de resultados

Para obter um catálogo de comportamentos específicos causados por uma configuração incorreta ou interpretação incorreta dos resultados de sincronização, como produtos ausentes, preços incorretos ou lacunas de dados em nível de escopo, consulte [Cenários de solução de problemas](troubleshooting/troubleshooting-scenarios.md).

## Diagnóstico [!DNL SaaS Data Export]

Para obter os diagnósticos de nível inferior do [!DNL SaaS Data Export], incluindo locais de log e comandos de ressincronização de feed, consulte o [[!DNL SaaS Data Export] guia de solução de problemas](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}.
