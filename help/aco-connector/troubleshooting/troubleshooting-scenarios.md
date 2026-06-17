---
title: Cenários de Solução de Problemas do  [!DNL Adobe Commerce Optimizer Connector]
description: Diagnosticar e resolver comportamento inesperado em  [!DNL Adobe Commerce Optimizer Connector]  causado por erro de configuração ou interpretação dos resultados de sincronização.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---


# Cenários de solução de problemas do [!DNL Adobe Commerce Optimizer Connector]

Esta página descreve comportamentos que você pode observar ao trabalhar com o [!DNL Adobe Commerce Optimizer Connector], que normalmente são causados por uma configuração incorreta ou interpretação incorreta dos resultados de sincronização. Use as descrições abaixo para identificar a causa raiz e aplicar a resolução apropriada.

## O status do feed mostra &quot;Sucesso&quot;, mas os dados não estão visíveis em [!DNL Adobe Commerce Optimizer]

**Problema:** A página **[!UICONTROL Data Feed Sync Status]** relata uma sincronização bem-sucedida, mas os produtos, preços, etc., não estão aparecendo conforme esperado em [!DNL Adobe Commerce Optimizer].

**Causa:** Um status de feed bem-sucedido significa que os dados foram aceitos pelo ponto de extremidade de assimilação, mas não que ele concluiu a propagação por [!DNL Adobe Commerce Optimizer]. A propagação pode levar vários minutos após a assimilação.

**Solução:**

- Aguarde alguns minutos e atualize a exibição [!DNL Adobe Commerce Optimizer].
- Confirme se a ID do locatário configurada no [!DNL Adobe Commerce] corresponde ao ambiente do [!DNL Commerce Optimizer] que você está verificando.
- Verifique se a [origem do catálogo](../../optimizer/setup/catalog-sources.md) (código de exibição de armazenamento) ou catálogo de preços correto está selecionado em [!DNL Commerce Optimizer].

## Os produtos estão ausentes do catálogo exportado

**Problema:** alguns produtos não aparecem em [!DNL Adobe Commerce Optimizer] após uma sincronização completa do catálogo.

**Causa:** Se houver falha na validação dos produtos durante a exportação, eles serão omitidos da sincronização. Os produtos desativados ou não visíveis no catálogo não serão retornados pela API de produtos.

**Solução:**

- Confirme se os produtos afetados estão atribuídos à exibição do site e da loja usada como origem do catálogo.
- Verifique se os produtos estão ativados e definidos com uma visibilidade que inclua listagens de catálogo.
- Revisar detalhes de erro por item para o feed de catálogo em **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

## Preços incorretos ou ausentes em [!DNL Adobe Commerce Optimizer]

**Problema:** os produtos aparecem em [!DNL Adobe Commerce Optimizer], mas não exibem o preço retornado com a [consulta de produtos GraphQL](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}, ou o preço não corresponde ao que está configurado em [!DNL Adobe Commerce].

**Causa:** o feed do catálogo de preços usa um escopo que mapeia para um site e grupo de clientes específicos. Uma configuração incorreta de [exibição de catálogo](../../optimizer/setup/catalog-view.md) pode resultar em preços incorretos ou ausentes.

**Solução:**

- Verifique se o site está configurado para sincronização na configuração de exportação do conector. Consulte [Personalizar a configuração da exportação de dados](../get-started.md#customize-the-commerce-scopes-export-configuration).
- Confirme se a ID do catálogo de preços usada em [!DNL Commerce Optimizer] está presente na configuração da [exibição do catálogo](../../optimizer/setup/catalog-view.md){target="_blank"} usada para executar a consulta de produtos.

## Os dados em [!DNL Adobe Commerce Optimizer] foram substituídos ou modificados inesperadamente após a sincronização

**Problema:** alterações de dados aplicadas diretamente em [!DNL Adobe Commerce Optimizer] por um sistema externo (como um PIM ou ERP) são perdidas ou revertidas depois que o conector executa uma sincronização.

**Causa:** Quando sistemas diferentes de [!DNL Adobe Commerce] gravam diretamente em [!DNL Adobe Commerce Optimizer], por exemplo, um PIM ou outro sistema externo, podem ocorrer conflitos de dados. O conector sincroniza os dados *de uma maneira*, de [!DNL Adobe Commerce] para [!DNL Adobe Commerce Optimizer], e não sincroniza as alterações novamente para [!DNL Adobe Commerce]. Como resultado, dados gravados diretamente em [!DNL Adobe Commerce Optimizer] não são refletidos em [!DNL Adobe Commerce] e podem ser substituídos durante uma sincronização posterior.


**Solução:**

Em vez de gravar modificações de catálogo diretamente em [!DNL Adobe Commerce Optimizer], use [camadas de catálogo](../../optimizer/setup/catalog-layer.md){target="_blank"} para aplicar alterações fora de [!DNL Adobe Commerce]. As camadas de catálogo permitem que sistemas externos enriqueçam ou substituam dados de catálogo em [!DNL Adobe Commerce Optimizer] sem entrar em conflito com a sincronização do conector.

## Solução de problemas comuns do [!DNL SaaS Data Export]

Para problemas relacionados ao [!DNL SaaS Data Export] subjacente que podem afetar o conector, consulte [Cenários de solução de problemas do [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md).
