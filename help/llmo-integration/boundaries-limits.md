---
title: Limites e limites de integração
description: Saiba mais sobre os limites de escopo para catálogos de terceiros, a cobertura de correção automática, os pré-requisitos de rastree, as considerações de escala corporativa e as restrições de acesso beta restritas para o LLM Optimizer com Commerce.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Limites e limites de integração

>[!IMPORTANT]
>
>O acesso a essa integração é restrito. Entre em contato com o Gerente técnico de conta para obter mais detalhes.

Use este tópico para definir expectativas para o que a integração do [!DNL Adobe Commerce] e do [!DNL Adobe LLM Optimizer] pode automatizar, onde você permanece responsável e quais restrições ainda estão evoluindo.

## Limitações do catálogo de terceiros {#third-party-catalog}

Quando o catálogo **não** estiver em [!DNL Adobe Commerce]:

- O LLM Optimizer ainda pode identificar problemas e sugerir melhorias usando dados de catálogo espelhados ou importados, dependendo da configuração.
- **Correção automática direta** na plataforma de comércio do comerciante não é o mesmo que gravar no catálogo de origem do comerciante. Você pode precisar de um catálogo espelhado, exportação/importação ou automação de parceiros para aplicar as alterações.

Para catálogos hospedados pela Commerce, as atualizações de nome e descrição aprovadas são enviadas para o sistema de registro do Commerce. Consulte [Usar LLM Optimizer com Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Escala e limites técnicos {#scale-limits}

Catálogos grandes e contagens altas de URL podem rastrear, analisar e implantar padrões de borda.

## Rastree e legibilidade de bot {#crawling}

Insights significativos de catálogo e PDP presumem que **bots relevantes para LLM podem acessar** as URLs importantes para você e que as páginas estão estruturadas de forma que a análise automatizada seja confiável. As regras de robôs, a autenticação, o bloqueio geográfico e a personalização pesada podem reduzir a cobertura.

## Tópicos relacionados

- [Visão geral da integração](overview.md)
- [Conectar o Adobe Commerce ao LLM Optimizer](get-started/connect-to-llmo.md)
- [Usar o LLM Optimizer com o Adobe Commerce](get-started/use-llmo-with-commerce.md)
