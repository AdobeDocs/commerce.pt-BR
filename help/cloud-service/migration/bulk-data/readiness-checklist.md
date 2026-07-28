---
title: Lista de verificação de prontidão do cliente
description: Saiba como se preparar para uma migração de dados em massa para o Adobe Commerce as a Cloud Service com uma lista de verificação de disponibilidade que abrange engajamento, máquina, origem e destino.
feature: Cloud
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c32adafa-ed01-4b31-997e-2413013911b0id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# Lista de verificação de preparação do cliente

{{bulk-data-early-access}}

Use esta lista de verificação para se preparar para uma migração de dados de uma instância do [!DNL Adobe Commerce on Cloud] ou local para o [!DNL Adobe Commerce as a Cloud Service] usando a ferramenta de migração de dados em massa.

A ferramenta de migração é distribuída como parte do processo de contrato do Commerce Deployment Engineering (CDE). O acesso à ferramenta é restringido por um contrato CDE assinado e não está disponível ao público.

Esta lista de verificação abrange o que você precisa ter em vigor antes que a ferramenta seja compartilhada ([Estágio 1](#stage-1-before-tool-access)) e o que você precisa pronto para começar a configuração e a execução assim que tiver a ferramenta ([Estágio 2](#stage-2-before-running-the-migration)). Analise essa lista de verificação com a equipe do Adobe antecipadamente, pois alguns itens exigem coordenação da Adobe.

## Estágio 1: antes do acesso à ferramenta

Conclua ou confirme o seguinte antes de fornecer a ferramenta e a documentação de migração.

- **Compromisso do CDE** — Um contrato de Engenharia Implantada da Commerce assinado deve estar em vigor. O acesso à ferramenta é concedido na fase de assinatura de oferta do ciclo de vida do CDE. Fale com a equipe do Adobe.
- **Questionário de escopo concluído** — Um questionário de escopo é concluído durante a Descoberta do CDE para validar se a migração é viável com os recursos atuais da ferramenta e para avaliar o espaço físico e a complexidade dos dados. Certifique-se de que isso esteja concluído com sua equipe do Adobe antes de prosseguir.
- **Nenhum dado HIPAA confirmado** — A instância de origem não deve conter dados regulados por HIPAA. Confirme antes de continuar.
- **Endereços IP fornecidos** — forneça à sua equipe do Adobe a lista de endereços IP estáticos a partir dos quais a ferramenta de migração será executada. Isso é necessário para que o acesso à rede seja configurado no Adobe.
- **Instância de destino provisionada** — A instância de destino [!DNL Adobe Commerce as a Cloud Service] deve ser provisionada antes do início da migração. Coordene com a equipe do Adobe para confirmar se a instância está pronta.

## Etapa 2: antes de executar a migração

Depois de ter acesso à ferramenta, prepare os seguintes itens antes de começar a configuração e a execução.

### Máquina de migração

A ferramenta de migração é executada em uma máquina controlada por você, como uma caixa de salto dedicada. Esta máquina deve atender aos seguintes requisitos.

- **[!DNL Docker]e [!DNL Docker Compose] instalados** — A ferramenta é baseada em [!DNL Docker]. O `docker` e o `docker compose` (ou o `docker-compose` herdado) devem estar instalados e funcionando no computador de migração.
- **[!DNL Docker]permissões de execução** — O usuário executando a migração deve ter permissão para executar comandos [!DNL Docker]. Em [!DNL Linux], o usuário deve estar no grupo `docker`. Em [!DNL macOS] e [!DNL Windows], [!DNL Docker Desktop] deve estar em execução e acessível.
- **Diretório de trabalho gravável** — O diretório onde a ferramenta de migração é extraída deve ser totalmente gravável pelo usuário de migração. A ferramenta grava logs, cache, [!DNL Composer] dependências e arquivos gerados durante a execução.
- **Espaço em disco suficiente** — garanta espaço livre em disco adequado para dados extraídos, [!DNL Docker] imagens e saída de log. Os requisitos de espaço variam dependendo do tamanho do banco de dados de origem.
- **Fontes locais: conectividade direta de banco de dados do computador de migração** — Para instâncias de origem locais, o computador de migração deve ter acesso direto de rede ao banco de dados de origem. A ferramenta não estabelece automaticamente a conectividade com o banco de dados local. Confirme se o host, a porta e as credenciais podem ser acessados no computador de migração antes de executar qualquer comando de migração.
- **CLI da Nuvem instalada e chave SSH registrada** — Para instâncias de origem [!DNL Adobe Commerce on Cloud], a [CLI da Nuvem](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) deve estar instalada no computador de migração. Sua chave pública SSH também deve estar registrada em sua conta. Consulte o [Guia de conexões seguras](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para obter instruções.

### Instância do Source

- **APIs de repositório do Source acessíveis** — As APIs REST e GraphQL do repositório de origem devem ser acessíveis no computador de migração. Certifique-se de que nenhuma Autenticação básica de HTTP ou restrição de rede bloqueie o tráfego da API para o URL de origem.
- **Credenciais do Source OAuth** — a ferramenta de migração usa o OAuth para autenticar com o armazenamento de origem. Crie ou confirme uma integração na origem [!UICONTROL **Admin**] ([!UICONTROL **System**] > [!UICONTROL **Extensions**] > [!UICONTROL Integrations]) e tenha a chave do consumidor, o segredo do consumidor, o token de acesso e o segredo do token de acesso prontos.
- **Fontes do PaaS: Token da API da Magento Cloud** — Gere um token de API [!DNL Cloud] a partir das [configurações da conta da nuvem](https://accounts.magento.cloud) em [!UICONTROL **Configurações de conta**] > [!UICONTROL **Tokens de API**]. Necessário somente quando a origem é uma instância [!DNL Adobe Commerce on Cloud].
- **Credenciais do banco de dados Source** — (Somente no local) Tenha os detalhes de conexão do banco de dados de origem [!DNL MySQL] prontos para configuração: nome de `host`, `port`, `user`, `password` e `database`.
- **Capacidade de pausar o cron** — Você deve conseguir parar o cron na instância de origem durante a extração de dados para impedir gravações simultâneas.
- **Capacidade de pausar integrações e trabalhos em segundo plano** — Quaisquer integrações de terceiros (ERP, OMS, PIM), trabalhos agendados ou processos em segundo plano que gravam no banco de dados de origem devem ser pausados para a janela de extração.
- **Capacidade de habilitar e desabilitar o modo de manutenção** — (Somente migração em fases) Se você executar uma migração em fases com uma janela de manutenção, deverá habilitar e desabilitar o modo de manutenção na instância de origem.

### Instância de destino

- **ID de locatário e ID de organização confirmadas** — Obtenha `TARGET_TENANT_ID` e `TARGET_ORG_ID` da sua equipe da Adobe antes da configuração.
- **Credenciais de servidor para servidor OAuth do IMS** — Necessárias para que a ferramenta de migração se autentique no destino. Gerado por meio da [Adobe Developer Console](https://developer.adobe.com/console/). Você precisa de acesso de [!UICONTROL Developer] ou [!UICONTROL Admin] à sua organização da Adobe, pois o acesso básico de usuário não é suficiente para criar credenciais. Coordene com a equipe do Adobe o perfil de produto correto a ser selecionado e tenha a ID de cliente (`ADOBE_IMS_CLIENT_ID`) e o segredo do cliente (`ADOBE_IMS_CLIENT_SECRET`) prontos.
- **URL do ponto de extremidade do CDMS** — Fornecido pela equipe da Adobe. Não tente inferir esse valor. Você precisa do endpoint de pré-produção para migrações de sandbox e teste e do endpoint de produção para migrações de transferência ao vivo.
- **Configuração principal alinhada entre origem e destino** — Os dados de configuração principais, como configurações de armazenamento e configuração do sistema, não são migrados pela ferramenta. Configure-o manualmente no destino para corresponder à origem antes da migração.
- **Repositórios B2B: recursos B2B configurados de forma consistente** — Se a origem for um repositório habilitado para B2B, verifique se as configurações relevantes de [!UICONTROL Admin] B2B estão configuradas de forma consistente na origem e no destino antes da migração. Consulte o [guia de migração](migration-guide.md) para obter as configurações específicas necessárias.

### Planejamento de migração

- **Abordagem de migração decidida** — antes de começar, determine qual abordagem se adapta ao seu caso de uso.
  - Migração monofásica - Nenhum modo de manutenção necessário. Adequa-se a ambientes secos, de desenvolvimento ou de sandbox, ou a qualquer migração em que a origem possa permanecer ativa durante a extração.
  - Migração multifásica - O modo de manutenção é obrigatório. É necessária uma migração de várias fases para migrações de produção em que a origem deve ser congelada durante a extração, para garantir a consistência dos dados.
- **Janela de manutenção planejada** — Aplica-se somente a migrações de várias fases. Planeje e comunique a janela de manutenção com antecedência. A instância de origem não está disponível para usuários finais durante as fases de extração e carregamento.
- **Código de exibição de repositório confirmado** — Identifique o código de exibição de repositório (`STORE_CODE`) na instância de origem. O padrão é `default`, mas deve corresponder ao código real em [!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]. Um código de armazenamento incorreto pode afetar as operações de dados durante a migração.

Após confirmar todos os itens, você estará pronto para verificar o acesso ao serviço com o [guia de acesso ao serviço de migração](cdms-access.md) e, em seguida, iniciar as etapas de configuração e execução no [guia de migração](migration-guide.md).
