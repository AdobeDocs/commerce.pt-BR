---
title: Responsabilidade compartilhada
description: Saiba mais sobre as responsabilidades de segurança de cada parte envolvida em seu projeto [!DNL Adobe Commerce as a Cloud Service] do.
role: Admin, Architect, Leader
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Segurança de responsabilidade compartilhada e modelo operacional

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] é um serviço sob demanda que depende de um modelo operacional e de segurança de responsabilidade compartilhada. Essas responsabilidades são compartilhadas entre a Adobe e os clientes. Cada parte tem uma responsabilidade distinta pela segurança e operação do aplicativo Adobe Commerce.

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
| Correção de bugs principais em [!DNL Adobe Commerce as a Cloud Service] | RA | I |
| Liberando patches de infraestrutura do [!DNL Adobe Commerce as a Cloud Service] | RA | |
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
