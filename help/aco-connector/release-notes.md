---
title: Notas de versão do [!DNL Adobe Commerce Optimizer Connector]
description: Saiba mais sobre as  [!DNL Adobe Commerce Optimizer Connector] notas de versão, incluindo novos recursos, correções de erros e problemas conhecidos para sincronização e exportação de catálogos.
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# Notas de versão do Adobe Commerce Optimizer Connector

Essas notas de versão descrevem todas as versões do [!DNL Adobe Commerce Optimizer Connector] e incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção de um problema](../assets/fix.svg) Correções e melhorias
![Problema conhecido](../assets/bug.svg) Problemas conhecidos

## Versões de 2026

### Versão 1.0.13

_6 de maio de 2026_

![Correção](../assets/fix.svg) **Melhoria das [!DNL Adobe Commerce Optimizer Connector] instruções de configuração** - Atualização da página de configuração [!DNL Adobe Commerce Optimizer] no Administrador do Commerce para vincular ao _[!DNL Adobe Commerce Optimizer Connector]Guia de Integração_.
<!--COMOPT-1922-->

![Correção](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]aprimoramento de metadados** - O [!DNL Adobe Commerce Optimizer Connector] agora inclui sua versão instalada no cabeçalho de metadados. Essa melhoria permite que as equipes identifiquem rapidamente qual versão do conector está em uso durante a solução de problemas ou os compromissos de suporte.<!--MDEE-1323-->

### Versão 1.0.12

_2 de abril de 2026_

![Novo](../assets/new.svg) **Adição de suporte ao feed de Categorias no comando `saas:resync`**-Agora é possível atualizar e exibir facilmente os dados de categoria mais recentes usando o comando da CLI `saas:resync`:

```terminal
bin/magento saas:resync --feed=categories
```

### Versão 1.0.11

_10 de março de 2026_

![Correção de um problema](../assets/fix.svg) que bloqueava o acesso à página de configuração [!DNL Commerce Services Connector] dos menus do Administrador do Commerce **[!UICONTROL System]** e **[!UICONTROL Configuration]** quando o [!DNL Adobe Commerce Optimizer Connector] estava instalado em uma instância [!DNL Adobe Commerce].  Agora, você pode acessar a página de configuração [!DNL Commerce Services Connector] quando ambas as extensões estiverem instaladas. <!--MDEE-1322-->


### Versão 1.0.10

_9 de março de 2026_

![Correção](../assets/fix.svg) Se você acessar a página **[!UICONTROL Data Feed Sync Status]** antes de concluir a configuração do conector, agora você será redirecionado automaticamente para a página de configuração do conector. Esse fluxo guiado garante que a instalação do conector seja concluída e ajuda a evitar erros causados pela falta de configurações que poderiam resultar em itens de status com falha ou incompletos.<!--MDEE-1296-->

### Versão v1.0.9

_1º de março de 2026_

Versão de disponibilidade geral do [!DNL Adobe Commerce Optimizer Connector].

>[!NOTE]
>
>Se você participou do programa Beta para o [!DNL Adobe Commerce Optimizer Connector] e tem uma versão anterior da extensão instalada, atualize para a versão de disponibilidade geral para receber as atualizações mais recentes.
