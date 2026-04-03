---
title: Notas de versão do [!DNL Adobe Commerce Optimizer Connector]
description: As informações da versão mais recente do  [!DNL Adobe Commerce Optimizer Connector] para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Notas de versão do Adobe Commerce Optimizer Connector

Essas notas de versão descrevem todas as versões do [!DNL Adobe Commerce Optimizer Connector] e incluem:

![Novos](../assets/new.svg) Novos recursos
![Problema corrigido](../assets/fix.svg) Correções e melhorias
![Problema conhecido](../assets/bug.svg) Problemas conhecidos

## Versões de 2026

### Versão 1.0.12

_2 de abril de 2026_

![Novo](../assets/new.svg) **Adição de suporte ao feed de Categorias no comando `saas:resync` **-Agora é possível atualizar e exibir facilmente os dados de categoria mais recentes usando o comando da CLI `saas:resync`:

```terminal
bin/magento saas:resync --feed=categories
```

_10 de março de 2026_

![Correção de um problema](../assets/fix.svg) que bloqueava o acesso à página de configuração do Commerce Services Connector a partir dos menus do Commerce Admin System e Configuração quando o Adobe Commerce Optimizer Connector estava instalado em uma instância do Commerce.  Agora, você pode acessar a página de configuração do Commerce Services Connector quando ambas as extensões estiverem instaladas. <!--MDEE-1322-->


### Versão v1.0.10

_9 de março de 2026_

![Correção](../assets/fix.svg) Se você acessar a página Status de sincronização do feed de dados antes de concluir a configuração do Conector, agora você é redirecionado automaticamente para a página Configuração do conector. Esse fluxo guiado garante que a instalação do Conector seja concluída e ajuda a evitar erros causados pela falta de configurações que poderiam resultar em itens de status com falha ou incompletos.<!--MDEE-1296-->

### Versão v1.0.9

_1º de março de 2026_

Versão de disponibilidade geral do Adobe Commerce Optimizer Connector.

>[!NOTE]
>
>Se você participou do programa Beta para o Adobe Commerce Optimizer Connector e tem uma versão anterior da extensão instalada, atualize para a versão de disponibilidade geral para receber as atualizações mais recentes.

