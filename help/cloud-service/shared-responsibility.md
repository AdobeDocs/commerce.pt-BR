---
title: Responsabilidade compartilhada
description: Saiba mais sobre as responsabilidades de segurança de cada parte envolvida em seu projeto do Adobe Commerce as a Cloud Service.
role: Admin, Architect, Leader
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Segurança de responsabilidade compartilhada e modelo operacional

O Adobe Commerce as a Cloud Service é um serviço sob demanda que depende de um modelo operacional e de segurança de responsabilidade compartilhada. Essas responsabilidades são compartilhadas entre a Adobe e os clientes. Cada parte tem uma responsabilidade distinta pela segurança e operação do aplicativo Adobe Commerce.

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
| Aplicação de patches a serviços de suporte (por exemplo, Nginx ou MySQL) | RA | |
| Definir regras de WAF de origem de back-end | RA | |
| Definição de regras WAF de CDN de back-end | RA | |
| Implantação de regras do WAF da plataforma de back-end | RA | |
| Implantação de regras WAF de CDN de back-end | RA | |
| Correção de bugs principais no Adobe Commerce as a Cloud Service | RA | I |
| Lançamento de patches de infraestrutura do Adobe Commerce as a Cloud Service | RA | |
| Dimensionamento (infraestrutura) | RA | |
| Dimensionamento (aplicativo principal) | RA | |
| Integração de aplicativos externos | | RA |
| Instalação de aplicativos do App Builder | | RA |
| Teste de desempenho de todos os aplicativos App Builder | | RA |
| Definição de temas e design de aplicativos personalizados do App Builder | | RA |
| Configurar DNS de back-end | RA | I |
| Integração da CDN de back-end | RA | I |
| Suporte à CDN de back-end | RA | I |
| Obter um provedor de DNS de back-end | RA | |
| Provisionamento dos ambientes de produção e sandbox | A | R |
| Acesso ao Dynamics para Adobe Commerce na infraestrutura em nuvem | R | C |
| Resolvendo problemas de segurança do cliente de back-end | RA | I |
| Resolvendo problemas de segurança da CDN de back-end | RA | |
| Auxiliar a Adobe na pesquisa de segurança (verificações/auditorias) | RA | |
| Executando verificações ASV de PCI | RA | I |
| Remediando verificações de PCI da infraestrutura Adobe Commerce | R | |
| Gerenciamento de segredos de SO e plataforma | RA | |
| Monitorar logs de segurança de back-end | RA | |
| Controle do suporte e do acesso do cliente | A | R |
| Teste e documentação anuais do plano de DR da Adobe e backup e restauração | RA | |
| Teste e documentação anuais do plano de recuperação de desastres | RA | |
| Depuração e isolamento de problemas | R | R |
| Suporte oportuno ao processo de depuração e isolamento de problemas | R | R |
| Publicação de atualizações e patches no Adobe Commerce Core | RA | I |
| Instalação de atualizações e patches no Adobe Commerce Core | RA | I |
| Qualidade do aplicativo principal do Adobe Commerce | RA | |
