---
title: Executar uma migração de dados em massa
description: Saiba como configurar e executar uma migração de dados em massa de um Adobe Commerce PaaS ou instância local para o Adobe Commerce as a Cloud Service com a CLI.
feature: Cloud
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
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
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 2802
ht-degree: 0%

---

# Executar uma migração de dados em massa

{{bulk-data-early-access}}

Este guia é uma referência operacional passo a passo para executar uma migração de dados de uma instalação local ou PaaS do [!DNL Adobe Commerce] para o [!DNL Adobe Commerce as a Cloud Service] usando a ferramenta de migração de dados em massa. Os valores reais de configuração e os detalhes específicos do ambiente variam de acordo com a sua configuração.

Antes de começar, confirme se você concluiu cada item da [lista de verificação de preparação do cliente](readiness-checklist.md) e verificou o acesso à API com o [guia de acesso ao serviço de migração](cdms-access.md).

>[!NOTE]
>
>Como parte do pacote de distribuição da ferramenta, é fornecida uma documentação técnica abrangente que abrange a arquitetura da ferramenta, o projeto interno, a estrutura de transformação de dados e a estrutura de teste de integridade.

## Pré-requisitos

- O **[!DNL Docker]** e o **[!DNL Docker Compose]** devem estar instalados no computador em que você executa a migração.
- O usuário que está executando a migração deve ter permissão para executar os comandos `docker` e `docker compose` (ou os `docker-compose` herdados). Em [!DNL Linux], o usuário deve estar no grupo `docker`. Em [!DNL macOS] e [!DNL Windows], [!DNL Docker Desktop] deve estar em execução e acessível. A CLI de migração invoca [!DNL Docker] repetidamente e erros de permissão bloqueiam a execução.
- A configuração principal deve ser consistente entre a origem e o destino antes de executar a migração. Os dados de configuração principais, como configurações de armazenamento e configuração do sistema, não são migrados por essa ferramenta. Configure no destino de maneira independente e alinhe-o com a origem antes da migração.

## Configurar o pacote de ferramentas

Configurar o ambiente para a migração de dados em massa:

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. Extrair o conteúdo de `ccsaas-migration-tools.tar.gz`.

1. Execute todos os comandos da pasta `ccsaas-migration-tools` extraída, onde `bin/console` está.

1. Verifique se a pasta é gravável para logs, cache, [!DNL Composer] e arquivos gerados.

   Altere a propriedade de todos os arquivos e subpastas nesse diretório para o usuário do sistema operacional que executa a migração, para que a ferramenta possa ler e gravar de forma consistente. Por exemplo, em [!DNL Linux]: `chown -R <user>:<group> <project-root>`.

1. Crie os arquivos `.env` e `.my.cnf` na raiz do projeto copiando os arquivos de exemplo (`.example.env` para `.env` e `.my.cnf.example` para `.my.cnf`) e preencha os valores descritos nas seções a seguir.

### Exemplo de arquivos de configuração

Os arquivos `.example.env` e `.my.cnf.example` na raiz do repositório são o ponto de partida para a sua configuração. Copie cada arquivo para seu nome de trabalho e preencha os valores necessários.

| Exemplo de arquivo | Copiar para | O que ele cobre |
| --- | --- | --- |
| `.example.env` | `.env` | Lista anotada de todas as variáveis de ambiente com suporte: desempenho, CDMS, IMS, SaaS de destino, autenticação de URLs de origem, OAuth e valores de PaaS opcionais (`MAGENTO_CLOUD_CLI_TOKEN` quando `id=` está definido em `.my.cnf`). Lista completa de variáveis disponível no arquivo `.env`. |
| `.my.cnf.example` | `.my.cnf` | Referencie `[section]` layouts para locais [!DNL MySQL] e PaaS (`id=project:environment`). O nome `[section]` deve corresponder a `SOURCE_CONNECTION_NAME` em `.env`. Os campos incluem `user`, `password`, `host`, `port`, `database` e `id=` para PaaS. |

## Configurar o arquivo de ambiente

O arquivo `.env` na raiz do projeto é a configuração de migração e extração. Ele orienta o pipeline da CLI, incluindo URLs de origem e de destino, OAuth, a conexão remota do CDMS, autenticação SaaS e IMS e outros switches.

>[!NOTE]
>
>Não inclua barras em URLs. Por exemplo, use `https://example.com` em vez de `https://example.com/`.

Edite o arquivo `.env` e defina pelo menos os seguintes valores corretamente. Para obter a lista completa de variáveis com suporte, consulte as anotações em linha em `.example.env`.

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Configurar credenciais do OAuth de origem

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

Esses quatro valores assinam solicitações da ferramenta de migração para as APIs do armazenamento de origem. Para obtê-los, abra o [!UICONTROL Admin] de origem e vá para [!UICONTROL **Sistema**] > [!UICONTROL **Extensões**] > [!UICONTROL **Integrações**]. Crie ou abra uma integração e copie os valores em `.env`:

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Definir o token da CLI da nuvem

>[!NOTE]
>
>Isso se aplica somente às instâncias de origem [!DNL Adobe Commerce on Cloud]. A ferramenta detecta o tipo de origem automaticamente de `.my.cnf`. Se a seção `SOURCE_CONNECTION_NAME` contiver uma linha `id=` (por exemplo, `id=project:production`), a origem será [!DNL Adobe Commerce on Cloud] e `MAGENTO_CLOUD_CLI_TOKEN` será necessário. Para fontes locais sem `id=`, esse token não é necessário e a configuração do túnel é ignorada.

1. Vá para `https://accounts.magento.cloud` e entre.

1. Clique na imagem do seu perfil e selecione [!UICONTROL **Configurações da conta**].

1. Vá para a seção [!UICONTROL **Tokens de API**].

1. Selecione [!UICONTROL **Criar um token de API**], dê a ele um nome descritivo e copie o token gerado.

1. Definir o token em `.env`:

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>Se esta for a primeira vez que você usa a CLI da nuvem, também é necessário adicionar sua chave pública SSH à sua conta. Consulte o [Guia de conexões seguras](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para obter instruções.

### Alinhar configurações de administração do Commerce

Antes da migração, verifique se as configurações a seguir estão consistentes entre a origem e o destino.

>[!NOTE]
>
>Para garantir uma migração sem problemas, o [!DNL Adobe] recomenda que você torne todas as configurações principais na instância de destino consistentes com a origem.

### Configurar credenciais SaaS e IMS do público-alvo

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

Estas são as configurações de IMS e API [!DNL Adobe Commerce as a Cloud Service] para o destino. Você precisa da ID do locatário, da ID da organização, das credenciais de servidor para servidor do IMS OAuth e do host IMS correto para o seu ambiente. Coordene com sua equipe da Adobe a organização, o locatário e o acesso ao perfil. Não tente inferir ou estimar valores sensíveis.

#### Gerar credenciais IMS

Use o [Adobe Developer Console](https://developer.adobe.com/console/). Você precisa de acesso de [!UICONTROL Developer] ou [!UICONTROL Admin] na organização da Adobe para criar projetos. Um logon básico de usuário não é suficiente para adicionar APIs.

1. Crie um projeto ou abra um existente e selecione [!UICONTROL Add API].

1. Escolha [!UICONTROL **Adobe Commerce as a Cloud Service**] e continue.

1. Selecione [!UICONTROL **OAuth Server-to-Server**] como o tipo de autenticação e continue.

1. Selecione o perfil de produto que sua equipe do Adobe espera para este locatário e selecione [!UICONTROL **Salvar API configurada**].

1. Na barra lateral do projeto, abra [!UICONTROL **Servidor para Servidor OAuth**] (ou [!UICONTROL **Credenciais**]) e copie a ID do cliente e o segredo do cliente para `.env` como `ADOBE_IMS_CLIENT_ID` e `ADOBE_IMS_CLIENT_SECRET`.

O ponto de extremidade do token IMS (`ADOBE_IMS_URL`) deve corresponder ao ambiente da credencial.

| Nível | `ADOBE_IMS_URL` típico |
| --- | --- |
| Controle de qualidade ou preparo | `https://ims-na1-stg1.adobelogin.com` |
| Pré-produção ou produção | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>`na1` nessas URLs representa a região onde a instância de destino é provisionada. Substitua-o pelo identificador de região apropriado se sua instância estiver provisionada em uma região diferente.

`ADOBE_IMS_META_SCOPES` deve corresponder aos escopos provisionados nessa credencial. O arquivo `.example.env` inclui a cadeia de caracteres de escopo separada por vírgulas completa como uma referência. Altere-o somente se a Adobe instruir o.

#### Mapear credenciais de [!DNL Adobe I/O] para o arquivo de ambiente

Em [!DNL Developer Console], os valores de servidor para servidor OAuth são apresentados como uma ID de cliente e um segredo de cliente, correspondendo à seguinte estrutura JSON:

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

Mapeie-os para `.env` (exemplo de espaços reservados):

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

Os hosts da API SaaS diferem entre pré-produção e produção. `TARGET_INSTANCE_REST_URL` e `TARGET_INSTANCE_GRAPHQL_URL` devem usar o mesmo ambiente de API do Commerce que sua migração, seja pré-produção ou produção. Não misture um nível com o CDMS ou locatário do outro nível.

| Ambiente | Host típico em `TARGET_INSTANCE_*_URL` |
| --- | --- |
| Pré-produção ou sandbox | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| Produção | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>`na1` nessas URLs representa a região onde a instância de destino é provisionada. Substitua-o pelo identificador de região apropriado se sua instância estiver provisionada em uma região diferente.

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

Para hosts SaaS de produção, substitua `na1-sandbox` por `na1` em ambas as URLs `TARGET_INSTANCE_*`. Use o `ADOBE_IMS_URL` correspondente para essa camada, conforme mostrado na tabela anterior.

### Definir o endpoint do CDMS

Aponte a ferramenta de migração para o host da API do CDMS que corresponde ao ambiente para o qual você está migrando. Defina `CDMS_HOST` (e normalmente `CDMS_PORT=443`) em `.env`. Use um host, seja de pré-produção ou de produção, não ambos.

| Ambiente | Quando usar | `CDMS_HOST` |
| --- | --- | --- |
| Pré-produção | Execuções de pré-produção ou estilo sandbox, CDMS de não produção | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| Produção | Migração ou transferência de produção em tempo real | `https://commerce-data-migration-service-prod-external.adobe.io` |

Defina ou remova o comentário do bloco que corresponde à sua execução:

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### Definir o código de armazenamento

`STORE_CODE` é o código de exibição de repositório usado pela ferramenta de migração para chamadas da API REST da instância de origem, criação de cliente de teste sintético e limpeza de dados. Ele também é enviado como o cabeçalho `x-store-code` durante a fase de carregamento.

O padrão de `STORE_CODE` é `default` em `.example.env`. Verifique se isso corresponde ao código de exibição de armazenamento padrão da instância de origem. Para verificar, na origem [!UICONTROL Admin], vá para [!UICONTROL **Lojas**] > [!UICONTROL **Todas as Lojas**] e verifique a coluna [!UICONTROL **Código**] para a exibição de loja que deve ser usada. Se o código mostrado lá não for `default`, atualize `STORE_CODE` em `.env` para corresponder.

## Configurar o arquivo de conexão de banco de dados

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

O arquivo `.my.cnf` fornece configurações de conexão [!DNL MySQL] para o lado da extração da ferramenta de migração. Crie-o copiando `.my.cnf.example` para `.my.cnf` na raiz do projeto. O nome da seção deve corresponder a `SOURCE_CONNECTION_NAME` em `.env`.

Para uma origem no local ou auto-hospedada:

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>O computador que executa a ferramenta de migração deve ter acesso direto à rede para o banco de dados de origem. A ferramenta não estabelece nem verifica a conectividade local automaticamente. Confirme se o host, a porta e as credenciais podem ser acessados no computador de migração antes de executar qualquer comando de migração.

Para uma origem [!DNL Adobe Commerce on Cloud]:

```ini
[<connection-name>]
id=<project_id>:<environment>
```

O campo `id=` informa à ferramenta que a origem é PaaS e aciona a configuração de túnel usando `MAGENTO_CLOUD_CLI_TOKEN`. Os valores `project_id` e `environment` estão disponíveis em [!DNL Cloud Console] ou pelos comandos `magento-cloud project:list` e `magento-cloud environment:list`.

## Preparar a rede e as instâncias

A Autenticação básica de HTTP na frente do armazenamento pode bloquear o tráfego da API e da ferramenta. Verifique se está desabilitado para a URL de origem usada pela migração ou se os caminhos da ferramenta são permitidos, para que as solicitações REST e GraphQL possam acessar o armazenamento.

### Manter a estabilidade do banco de dados de origem durante a extração

Embora a ferramenta extraia dados do banco de dados de origem, nenhum outro processo deve gravar neles. Gravações simultâneas podem resultar em um instantâneo inconsistente.

- Interrompa o cron na origem e em qualquer agendador do sistema operacional que execute `bin/magento` ou outros gravadores para a janela de extração ou verifique se não é possível executá-los durante a extração.
- Revise outras integrações, como ERP, OMS, PIM, tarefas personalizadas e APIs de terceiros que gravam no mesmo banco de dados. Pausar ou bloquear gravações para a janela de extração para que nada altere as tabelas enquanto a extração é executada.
- Isso complementa o modo de manutenção e o acesso ao túnel ou ao banco de dados. Juntos, eles reduzem o tráfego da loja e da API. Cron e integrações são fontes separadas de gravações que você deve controlar explicitamente.

### Target

Se o catálogo de destino tiver que ser limpo antes da migração, exclua os produtos em [!UICONTROL Admin] em lotes pequenos, por exemplo, 200 de cada vez, para evitar conflitos de catálogo duplicados e tempos limite de exclusão em massa.

## Criar e executar a migração

Trabalhar no diretório extraído do projeto com acesso de gravação.

### Manter a sessão ativa por SSH

Se você se conectar via SSH, uma rede eliminada poderá eliminar seu shell e interromper uma migração longa. O comando GNU `screen` mantém a sessão ativa no servidor:

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

Você também pode usar `tmux` se ele estiver disponível no servidor.

### Criar a imagem do Docker

Crie a imagem [!DNL Docker] usada por `bin/console`, que contém PHP, CLI e dependências. Execute-a antes da primeira execução ou depois de Dockerfile ou alterações na imagem base.

```bash
./bin/console build
```

### Iniciar os serviços de apoio

Inicie os serviços de apoio [!DNL Docker Compose] da ferramenta, como o banco de dados de teste local e, quando habilitado em `.env`, os serviços locais opcionais. Os serviços exatos dependem da sua configuração. Execute isso após uma criação bem-sucedida e antes dos comandos shell, migração ou em fases.

```bash
./bin/console start
```

### Inicialize o contêiner da CLI

Inicie o contêiner da CLI uma vez para que o ponto de entrada possa concluir a configuração, como uma instalação do [!DNL Composer], se necessário, em relação ao projeto montado. Execute-o uma vez antes da primeira migração em um novo ambiente.

```bash
./bin/console shell
exit
```

### Executar a migração

A ferramenta oferece suporte a duas abordagens de migração. Escolha aquele que se adapta ao seu caso de uso.

#### Migração monofásica

Nenhum modo de manutenção é necessário na instância de origem. Execute o pipeline de migração completa com um único comando:

```bash
./bin/console migration
```

O comando executa todas as etapas do pipeline automaticamente, de ponta a ponta, na seguinte ordem.

1. **Verificação de configuração** — valida as variáveis de ambiente e a configuração da ferramenta.
1. **Inicialização do ambiente** — inicia os serviços [!DNL Docker], abre túneis de nuvem (se aplicável) e executa testes de unidade.
1. **Testes de integração e inicialização do CDMS** — executa testes de integração e inicializa a conexão da API do CDMS.
1. **Criar migração** — registra a migração com CDMS e aguarda a análise do esquema de destino. A ID da migração é salva em `.migration_id`.
1. **Geração de dados de teste e testes funcionais** — executa testes funcionais e gera dados de teste sintéticos na origem para verificação de integridade (se habilitada).
1. **Extração de dados** — extrai dados da instância de origem.
1. **Carregar no destino** — carrega os dados extraídos na instância de destino [!DNL Adobe Commerce as a Cloud Service]. As exibições de preparo são limpas na origem e os dados de teste da origem são removidos por meio de REST em paralelo com a carga.
1. **Verificação de integridade de dados** — aciona a verificação de soma de verificação e executa testes de verificação de API locais. Os resultados são registrados e as falhas não interrompem o pipeline.
1. **Limpeza de dados de teste no destino** — remove os dados de teste sintético da instância de destino.
1. **Resultados do processo** — gera um resumo da migração e, opcionalmente, baixa artefatos do armazenamento.

Use essa opção quando nenhuma janela de manutenção for necessária, o que é típico para execuções secas completas, ambientes de desenvolvimento ou sandbox ou qualquer migração em que a origem possa permanecer ativa durante a extração.

>[!WARNING]
>
>Não use essa opção quando uma origem congelada for necessária, por exemplo, qualquer migração de produção em que novos pedidos ou alterações de dados não devam ocorrer durante a extração. Em vez disso, use a migração em fases. Não use esse comando como uma etapa dentro do fluxo de trabalho de manutenção em fases.

#### Migração multifásica com modo de manutenção

O modo de manutenção é necessário na instância de origem para garantir a consistência dos dados durante a extração. A migração é dividida em fases distintas que devem ser executadas em ordem.

>[!NOTE]
>
>Duas CLIs diferentes estão envolvidas. Os comandos `./bin/console` são executados da raiz do projeto da ferramenta de migração. Os comandos `bin/magento maintenance:*` são executados no servidor de aplicativos [!DNL Adobe Commerce] de origem, por meio de SSH para a raiz de instalação ou por meio de [!UICONTROL Admin]. A ferramenta não emite comandos de manutenção do [!DNL Magento] em seu nome.

| Fase | Quem executa | Estado do Source |
| --- | --- | --- |
| 1. `migration:before-maintenance` | Ferramenta | Live — ainda não habilita a manutenção |
| &#x200B;2. Habilitar modo de manutenção | Manual | Transição para congelado |
| 3. `migration:during-maintenance` | Ferramenta | Congelado — não desative a manutenção durante esta fase |
| &#x200B;4. Desabilitar modo de manutenção | Manual (condicional) | Transição da instância de origem de volta para o modo ativo |
| &#x200B;5. `migration:cleanup` (opcional) | Ferramenta | Em tempo real — deve estar fora de manutenção |

**Fase 1 — Antes da manutenção (a origem está ativa)**

Executar enquanto a instância de origem está ativa e aceitando tráfego. O acesso REST e GraphQL à origem deve estar totalmente disponível. Não ative o modo de manutenção antes que esta fase seja concluída.

Retorne à raiz do servidor e execute:

```bash
./bin/console migration:before-maintenance
```

1. **Verificação de configuração** — valida as variáveis de ambiente e a configuração da ferramenta.
1. **Inicialização de ambiente** — inicia serviços [!DNL Docker], abre túneis de nuvem PaaS (se aplicável) e executa testes de unidade.
1. **Testes de integração e inicialização do CDMS** — executa testes de integração e inicializa a conexão da API do CDMS.
1. **Criar migração** — registra a migração com CDMS e aguarda a análise do esquema de destino. A ID da migração é salva em `.migration_id`.
1. **Testes funcionais** — executa testes funcionais em relação à origem ativa.
1. **Geração de dados de teste** — cria clientes e pedidos de teste sintético na origem para verificação de integridade (se habilitada).

**Fase 2 — Habilitar modo de manutenção (manual)**

Ative o modo de manutenção na origem e pause todas as atividades que gravam ou afetam o banco de dados, incluindo trabalhos agendados, integrações de terceiros, processamento de pedidos e sincronização de ativos de mídia.

No servidor do Commerce de origem (instalar raiz), execute:

```bash
bin/magento maintenance:enable
```

**Fase 3 — Durante a manutenção (a origem está congelada)**

Execute com a instância de origem no modo de manutenção. A origem deve permanecer congelada por toda a duração desta fase. Não desabilite o modo de manutenção até que a **Fase 3** seja concluída com êxito.

```bash
./bin/console migration:during-maintenance
```

1. **Configuração de túnel da nuvem** — para instâncias de origem [!DNL Adobe Commerce on Cloud], reabre túneis da nuvem e verifica a conectividade do banco de dados. Ignorado automaticamente para instâncias locais.
1. **Extração de dados** — extrai dados da instância de origem congelada.
1. **Limpeza do modo de exibição de preparo** — remove os modos de exibição de preparo da origem usando uma conexão direta com o banco de dados (segura no modo de manutenção).
1. **Carregar no destino** — carrega os dados extraídos na instância de destino [!DNL Adobe Commerce as a Cloud Service] e aguarda a conclusão.
1. **Verificação de integridade de dados** — aciona a verificação de soma de verificação CDMS e executa testes de verificação de API locais. Os resultados são registrados e as falhas não interrompem o pipeline.
1. **Limpeza de dados de teste no destino** — remove os dados de teste sintético da instância de destino.
1. **Resultados do processo** — gera um resumo da migração e, opcionalmente, baixa artefatos do armazenamento.

**Fase 4 — Desabilitar modo de manutenção (manual, condicional)**

Essa fase desativa o modo de manutenção, reativando o tráfego para a instância de origem. Esta etapa é necessária antes de executar a fase de limpeza, pois a limpeza se comunica com a origem por meio de REST e falha com `HTTP 503` se o modo de manutenção ainda estiver ativo.

No servidor Commerce de origem, execute:

```bash
bin/magento maintenance:disable
```

**Fase 5 — Limpeza (opcional, a origem deve estar ativa)**

Remova os clientes e pedidos de teste sintético criados na **Fase 1** da instância de origem por meio do REST. Esta fase pode ser executada somente após o modo de manutenção ser desabilitado.

>[!NOTE]
>
>Ignorar esta fase se `SKIP_TEST_DATA_CREATION=true` estiver definido em `.env`, porque nenhum dado de teste foi criado.

Retorne à raiz do servidor e execute:

```bash
./bin/console migration:cleanup
```

1. **Configuração da conexão do banco de dados** — para instâncias de origem [!DNL Adobe Commerce on Cloud], reabre túneis de nuvem. Para instâncias locais, estabelece e verifica a conectividade direta com o banco de dados.
1. **Limpeza do Source REST** — remove clientes e pedidos de teste sintético da origem por meio da API REST.

## Retomar ou executar novamente uma migração

A ferramenta de migração acompanha o progresso usando um arquivo `.migration_id` na raiz do projeto. Esse arquivo é criado automaticamente quando uma nova migração é iniciada e registra o identificador de migração atual.

### Retomar após uma falha

Se uma execução de migração falhar ou for interrompida, execute novamente o mesmo comando para retomar da última etapa bem-sucedida (extração, carregamento ou verificação) em vez de reiniciar do zero. As etapas já concluídas são ignoradas automaticamente.

>[!IMPORTANT]
>
>Ao retomar a fase `migration:during-maintenance`, a origem deve permanecer no modo de manutenção durante todo o processo. Se a origem tiver sido retirada da manutenção ou os dados tiverem sido alterados entre execuções, a migração retomada poderá produzir resultados inconsistentes.

### Iniciar uma nova migração

Para descartar uma execução anterior e iniciar uma migração completamente nova, exclua o arquivo `.migration_id` antes de iniciar a próxima migração:

```bash
rm .migration_id
```

Se `.migration_id` existir e a migração anterior já tiver sido concluída, a ferramenta imprimirá uma mensagem informando que a migração já foi concluída e aconselhará você a excluir o arquivo.

## Revisar logs e depurar

Todos os logs de migração são gravados no diretório `logs/` na raiz do projeto e são organizados em subdiretórios com carimbo de data e hora:

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log` é o log principal de orquestração de pipeline. Se uma etapa falhar, ela mostrará qual script foi encerrado com um código diferente de zero e o porquê.
- Logs por etapa, como `09b_run_load.log` e `11_verify_data_integrity_local.log`, contêm saída detalhada para cada fase.
