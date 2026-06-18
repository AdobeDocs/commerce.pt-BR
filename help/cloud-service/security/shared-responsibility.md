---
title: Responsabilidade compartilhada
description: Saiba mais sobre as responsabilidades de segurança de cada parte envolvida em seu projeto [!DNL Adobe Commerce as a Cloud Service] do.
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
autotag-review: '2026-06-18T16:19:21.186Z'
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
subfeature_v2:
  - id: d9ced453-36f4-4eb5-b2f3-1d593e32476b
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 0%

---

# Segurança de responsabilidade compartilhada e modelo operacional

[!DNL Adobe Commerce as a Cloud Service] é um serviço sob demanda que depende de um modelo operacional e de segurança de responsabilidade compartilhada. A Adobe e os clientes compartilham essas responsabilidades, com cada parte com responsabilidades distintas para proteger e operar o aplicativo da Adobe Commerce.

>[!BEGINSHADEBOX]

As tabelas de resumo a seguir usam o modelo RACI para mostrar as responsabilidades de segurança compartilhadas entre a Adobe e os clientes.

**R** — Responsável
**A** — Responsável
**C** — Consultado
**I** — Informado

>[!ENDSHADEBOX]

| Tarefa | Adobe | Cliente |
| --- | --- | --- |
| Definir regras de WAF de origem de back-end | RA | |
| Definição de regras WAF de CDN de back-end | RA | |
| Implantando e mantendo [!DNL Adobe Developer App Builder] aplicativos | | RA |
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
