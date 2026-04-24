---
title: Responsabilidade compartilhada
description: Saiba mais sobre as responsabilidades de segurança de cada parte envolvida em seu projeto [!DNL Adobe Commerce Optimizer] do.
role: Admin, Developer, Leader
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Segurança de responsabilidade compartilhada e modelo operacional

>[!BEGINSHADEBOX]

As tabelas de resumo a seguir usam o modelo RACI para mostrar as responsabilidades de segurança compartilhadas entre a Adobe e os clientes.

**R** — Responsável
**A** — Responsável
**C** — Consultado
**I** — Informado

>[!ENDSHADEBOX]

| Tarefa | Adobe | Cliente |
| --- | --- | --- |
| Aplicação de patches de infraestrutura do Adobe Commerce | RA | |
| Aplicação de patches aos serviços de suporte | RA | |
| Definir regras de WAF de origem de back-end | RA | |
| Definição de regras WAF de CDN de back-end | RA | |
| Implantação de regras do WAF da plataforma de back-end | RA | |
| Implantação de regras WAF de CDN de back-end | RA | |
| Correção de erros em [!DNL Adobe Commerce Optimizer] | RA | I |
| Liberando [!DNL Adobe Commerce Optimizer]patches de infraestrutura | RA | |
| Dimensionamento (infraestrutura) | RA | I |
| Integração de aplicativos externos | | RA |
| Instalação de aplicativos do App Builder | | RA |
| Teste de desempenho de todos os aplicativos App Builder | | RA |
| Definição de temas e design de aplicativos personalizados do App Builder | | RA |
| Configurar DNS de back-end | RA |  |
| Integração da CDN de back-end | RA |  |
| Suporte à CDN de back-end | RA |  |
| Obter um provedor de DNS de back-end | RA | |
| Provisionamento dos ambientes de produção e sandbox | A | R |
| Acessando o Dynamics para [!DNL Adobe Commerce Optimizer] | R | C |
| Resolvendo problemas de segurança do cliente de back-end | RA | I |
| Resolvendo problemas de segurança da CDN de back-end | RA | |
| Auxiliar a Adobe na pesquisa de segurança (verificações/auditorias) | RA | |
| Executando verificações ASV de PCI | RA | I |
| Remediando verificações de PCI de infraestrutura [!DNL Adobe Commerce Optimizer] | R | |
| Gerenciamento de segredos de SO e plataforma | RA | |
| Monitorar logs de segurança de back-end | RA | |
| Controle do suporte e do acesso do cliente | A | R |
| Teste e documentação anuais do plano de DR da Adobe e backup e restauração | RA | |
| Teste e documentação anuais do plano de recuperação de desastres | RA | |
| Depuração e isolamento de problemas | R | R |
| Suporte oportuno ao processo de depuração e isolamento de problemas | R | R |
| Instalando atualizações e patches em [!DNL Adobe Commerce Optimizer] | RA | I |
| Qualidade do Aplicativo [!DNL Adobe Commerce Optimizer] Principal | RA | |
