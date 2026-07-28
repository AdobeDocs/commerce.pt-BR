---
title: Ferramenta Migração de dados em massa
description: Saiba como usar a ferramenta de migração de dados em massa para migrar dados da sua instância existente do Adobe Commerce na nuvem para o  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# Ferramenta de migração de dados em massa

>[!IMPORTANT]
>
>A ferramenta de migração de dados em massa está atualmente em Acesso antecipado. O acesso é fornecido exclusivamente por meio do processo de contrato do Commerce Deployment Engineering (CDE).

A ferramenta de migração de dados em massa permite que os integradores de sistema migrem dados comerciais principais primários de [!DNL Adobe Commerce on Cloud] ou instalações locais para [!DNL Adobe Commerce as a Cloud Service].

A ferramenta de migração de dados em massa é uma CLI do Docker que os integradores de sistema executam em sua própria máquina de migração. Ele se conecta à instância de origem, extrai dados principais de comércio de terceiros, faz upload deles para o serviço de migração da Adobe (Serviço de migração de dados da Commerce) e monitora o progresso até a conclusão.

Todos os comandos são executados localmente, para que você controle quando a migração começa, quando o modo de manutenção é aplicado e quando cada fase é executada.

## Fluxo de trabalho de migração

A ferramenta gerencia os seguintes estágios de ponta a ponta:

- **Extração de dados** — extrai dados principais de comércio da instância de origem ([!DNL Adobe Commerce on Cloud] ou no local).
- **Carregamento de dados** — carrega dados extraídos na instância de destino [!DNL Adobe Commerce as a Cloud Service].
- **Verificação de integridade de dados** — executa verificações automatizadas após a migração, incluindo comparação de API REST e GraphQL e validação de contagem de registros.

>[!NOTE]
>
>Atualmente, a ferramenta de migração de dados em massa é compatível com a migração somente de dados principais de comércio primários. No momento, não há suporte para a migração de dados personalizada. As configurações (configurações de armazenamento, configuração do sistema) não são migradas automaticamente e devem ser definidas na instância de destino independentemente antes da migração.

## Arquitetura

A ferramenta de migração de dados em massa segue uma arquitetura distribuída que permite uma migração de dados segura e eficiente. Esta ferramenta ajuda os integradores de sistemas a migrar dados de um [!DNL Adobe Commerce on Cloud or on-premises instance] existente para o [!DNL Adobe Commerce as a Cloud Service]. Para obter mais informações sobre o processo de migração, consulte a [Visão geral da migração](../overview.md).

A imagem a seguir detalha a arquitetura do e o fluxo de dados completo usando a ferramenta de migração de dados em massa.

![Diagrama da arquitetura da ferramenta de migração de dados em massa mostrando o fluxo de dados de PaaS para SaaS](../../assets/bulk-data-diagram.png){zoomable="yes"}

### Componentes

| Componente | Função |
| --------- | ---- |
| **Ferramenta de migração de dados em massa** | A CLI baseada no Docker que o integrador de sistemas executa na máquina de migração, que orquestra o pipeline completo lendo o esquema e os dados da origem, fazendo upload dos dados extraídos para o serviço de migração da Adobe e promovendo transições de status. |
| **Instância do Source (Commerce na Nuvem ou no local)** | A origem da migração. A ferramenta se conecta por meio de APIs REST e GraphQL e por um túnel SSH ([!DNL Adobe Commerce on Cloud]) ou por uma conexão de banco de dados direta (local) para extração de dados. |
| **API do Serviço de Migração de Dados (CDMS) da Commerce** | API REST gerenciada pela Adobe que registra migrações, coordena transições de estado e fornece endpoints seguros para fazer upload de dados extraídos. A ferramenta de migração se conecta a esta API usando a URL do ponto de extremidade CDMS e as credenciais IMS na sua configuração `.env`. |
| **trabalhador do Serviço de Migração de Dados (CDMS) da Commerce** | Serviço em segundo plano gerenciado pela Adobe que carrega os dados extraídos na instância de destino e executa a verificação de integridade pós-carregamento. |
| **[!DNL Adobe Commerce as a Cloud Service]** | A versão baseada em SaaS do Adobe Commerce e seu destino de migração. Recebe dados carregados e expõe o Catálogo, o Live Search e os serviços de regras de preço usados durante a verificação de integridade. |

### Fluxo de dados

Os dados são movidos pelos componentes na seguinte sequência:

1. A ferramenta de migração de dados em massa lê o esquema do banco de dados e os dados da instância de origem, por meio de um túnel SSH para [!DNL Adobe Commerce on Cloud] ou uma conexão de banco de dados direta para local.
1. A ferramenta registra a migração e faz upload dos dados extraídos por meio da API do CDMS.
1. O trabalhador CDMS carrega os dados no locatário de destino [!DNL Adobe Commerce as a Cloud Service].
1. [!DNL Adobe Commerce as a Cloud Service] assimila os dados de catálogo carregados e compila o índice de catálogo.
1. O trabalhador do Serviço de migração de dados (CDMS) da Commerce verifica os dados carregados por meio da comparação da soma de verificação do banco de dados, REST e GraphQL nos seguintes serviços:

   - **Catálogo** (GraphQL) — dados de produto e categoria.
   - **Live Search** (REST) — correção do índice de pesquisa.
   - **Regras de precificação** (REST) — preço e dados de regra.

1. A ferramenta pesquisa o status da migração em todo o e recupera o relatório de migração final na conclusão.


## Ciclo de vida do compromisso

O acesso à ferramenta de migração de dados em massa é fornecido exclusivamente por meio de um contrato do Commerce Deployment Engineering (CDE). A ferramenta não está acessível publicamente.

O ciclo de vida típico do contrato é:

1. **Descoberta de CÓDIGO** - Conclua a chamada de escopo inicial, avalie a área ocupada e a complexidade dos dados e conclua o questionário de escopo.
1. **Assinatura de Contrato** - O contrato comercial está em vigor e o escopo da migração foi confirmado. Nesse estágio, você receberá acesso à ferramenta de migração.
1. **Coinovação e suporte do CDE** - Trabalhe em conjunto com a Adobe para instalar a ferramenta em seu ambiente e executar migrações de teste.
1. **Ativar** - Execute a migração de substituição de produção e conclua a verificação de integridade de dados.

## Distribuição da ferramenta

A ferramenta é distribuída como parte do compromisso do CDE. Seu representante da Adobe fornece o pacote de ferramentas, que inclui:

- A CLI baseada em Docker e a configuração de build
- Um modelo de configuração `.example.env` com documentação para todas as variáveis de ambiente necessárias
- Documentação técnica abrangente que abrange a arquitetura da ferramenta, a referência de configuração, as estruturas personalizadas de transformação e teste e os guias de solução de problemas

Para obter instruções detalhadas de configuração e operação, consulte a documentação incluída no pacote de distribuição da ferramenta.

## Guias de migração

As páginas a seguir demonstram o ciclo de vida completo da migração, da preparação à execução. Para obter uma compreensão completa do processo de migração, analise-os na seguinte ordem:

1. [Lista de verificação de preparação do cliente](readiness-checklist.md) — Confirme os pré-requisitos de envolvimento, máquina de migração, origem e destino antes de solicitar acesso à ferramenta.
1. [Verificar o acesso ao serviço de migração](cdms-access.md) — Após obter acesso à ferramenta, valide a acessibilidade da rede, a autenticação IMS e a autorização do locatário em relação à API do Serviço de Migração de Dados (CDMS) da Commerce.
1. [Executar uma migração de dados em massa](migration-guide.md) — Configure a ferramenta, prepare a rede e as instâncias e inicie a migração.

Para obter a referência de configuração completa, as estruturas de transformação e teste personalizadas e a orientação para solução de problemas, consulte a documentação incluída no pacote de distribuição da ferramenta.
