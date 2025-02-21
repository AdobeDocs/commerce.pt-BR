---
title: Integração e instalação
description: Saiba como instalar o [!DNL Catalog Service]
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Integração e instalação

Instale o Serviço de Catálogo para solicitar e receber dados do produto de uma instância do Commerce usando a [API GraphQL do Serviço de Catálogo](https://developer.adobe.com/commerce/services/graphql/catalog-service/). O Serviço de catálogo é fornecido como um metapackage de compositor no repositório repo.magento.com.

>[!NOTE]
>
>Se sua instância do Commerce usa o Live Search ou as Recomendações de produto, o Serviço de catálogo será instalado ou atualizado automaticamente quando você integrar ou atualizar esses serviços. Para obter detalhes, consulte as instruções de instalação do [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) e do [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).



## Requisitos do sistema

**Requisitos de software**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3
- Compositor: 2.x

**Plataformas com suporte**

- Adobe Commerce na infraestrutura em nuvem: 2.4.4+
- Adobe Commerce no local: 2.4.4+

## Endpoints

[!DNL Catalog Service] tem dois pontos de extremidade disponíveis para integração:

- Sandbox (`https://catalog-service-sandbox.adobe.io/graphql`) — usada para teste e validação antes de entrar em funcionamento
- Produção (`https://catalog-service.adobe.io/graphql`) — usada para tráfego direto para comerciantes e sites da Commerce

Todas as instâncias de teste do Commerce usam o ponto de extremidade da sandbox.

Execute todos os testes de carga no endpoint da sandbox. Antes de começar o teste de carregamento, envie um [Tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para que a equipe de Serviços possa antecipar o tráfego adicional do servidor.

## Instalação e configuração

Para começar a usar o [!DNL Catalog Service] for Adobe Commerce, siga estas etapas:

- Instalar a extensão Serviço de Catálogo (`magento/catalog-service`)
- Configurar o serviço e a exportação de dados
- Acessar o serviço

### Instalar a extensão Serviço de Catálogo

>[!BEGINSHADEBOX]

**Pré-requisito**

- Acesse [repo.magento.com](https://repo.magento.com) para instalar a extensão. Para geração de chaves e obtenção dos direitos necessários, consulte [Obter suas chaves de autenticação](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Para instalações na nuvem, consulte o [Guia de Infraestrutura do Commerce na Nuvem](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Acesso à linha de comando do servidor de aplicativos do Adobe Commerce.

>[!ENDSHADEBOX]

Instale a versão mais recente da extensão (`magento/catalog-service`) do Catalog Services em uma instância do Adobe Commerce que esteja executando o Adobe Commerce versão 2.4.4 ou posterior. O Serviço de Catálogo é entregue como um metapackage de compositor do repositório [repo.magento.com](https://repo.magento.com).

>[!BEGINTABS]

>[!TAB Infraestrutura em nuvem]

Use este método para instalar o [!DNL Catalog Service] para uma instância do Commerce Cloud.

1. Na estação de trabalho local, altere para o diretório do projeto do Adobe Commerce na infraestrutura em nuvem.

   >[!NOTE]
   >
   >Para obter informações sobre o gerenciamento local de ambientes de projeto do Commerce, consulte [Gerenciamento de ramificações com a CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) no _Guia do Usuário do Adobe Commerce na Infraestrutura da Nuvem_.

1. Confira a ramificação de ambiente para atualizar usando a CLI da Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Adicione o módulo Serviço de Catálogo.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Atualizar dependências de pacote.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Confirmar e enviar alterações de código para os arquivos `composer.json` e `composer.lock`.

1. Adicione, confirme e envie por push as alterações de código dos arquivos `composer.json` e `composer.lock` para o ambiente de nuvem.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   A ação de enviar as atualizações para o ambiente de nuvem inicia o [processo de implantação da nuvem do Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) para aplicar as alterações. Verifique o status da implantação no [log de implantação](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB No local]

Use este método para instalar o [!DNL Catalog Service] para uma instância local.

1. Use o Composer para adicionar o módulo Serviço de catálogo ao seu projeto:

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Atualize as dependências e instale a extensão:

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Atualizar o Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Limpe o cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >Em alguns casos, especialmente ao implantar na produção, você pode evitar a limpeza do código compilado, pois pode levar algum tempo. Certifique-se de fazer backup do sistema antes de fazer qualquer alteração.

>[!ENDTABS]

### Configurar o serviço e a exportação de dados

Após instalar o [!DNL Catalog Service], conclua as tarefas a seguir para integrar o serviço de Catálogo à sua instância do Adobe Commerce. Essa integração permite a sincronização de dados e a comunicação entre a instância do Commerce, o Serviço de catálogo e outros serviços de suporte. A sincronização de dados é realizada pela [extensão de Exportação de Dados SaaS](../data-export/overview.md).

1. Configure o [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) especificando as chaves de API e selecionando um Espaço de Dados SaaS.

   A configuração do Commerce Services Connector é um processo único necessário para usar serviços da Adobe Commerce, como o Serviço de catálogo, o Live Search e as Recomendações de produto. Se você já tiver configurado o conector para outro serviço, ignore esta etapa.

1. Execute uma sincronização de dados inicial no [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   A sincronização inicial pode levar de alguns minutos a horas, dependendo do tamanho do catálogo. Você pode monitorar o status de sincronização no painel de Gerenciamento de dados. Após a sincronização inicial, o Catálogo exporta dados do produto de forma contínua para manter os serviços atualizados.

   >[!NOTE]
   >
   >Você também pode iniciar a sincronização inicial a partir da linha de comando usando a Commerce CLI. Consulte [Sincronização inicial](../data-export/data-export-cli-commands.md#initial-sync) no _Guia de exportação de dados SaaS_.

Para garantir que a exportação de catálogo esteja sendo executada corretamente:

- [Confirme se os trabalhos cron estão em execução](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Verifique se os indexadores estão sendo executados do [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) ou usando o comando `bin/magento indexer:info` da CLI do Commerce.
- Verifique se os indexadores `Catalog Attributes Feed, Product Feed, Product Overrides Feed` e `Product Variant Feed` estão definidos como `Update by Schedule`.

### Monitorar e solucionar problemas de sincronização de dados

Com o Administrador do Commerce, é possível monitorar o processo de sincronização usando o [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Use a [CLI do Commerce](../data-export/data-export-cli-commands.md#troubleshooting) e os logs para gerenciar e solucionar problemas do processo.

### Acessar o serviço

A API do GraphQL [!DNL Catalog Service] pode ser acessada do ponto de extremidade ` https://catalog-service.adobe.io/graphql` usando comandos POST em HTTPS.

Em suas consultas do GraphQL, você deve especificar vários cabeçalhos HTTP, incluindo a chave de API pública adicionada à configuração do Adobe Commerce Services Connector no Administrador. Para obter detalhes, consulte a documentação do [Storefront Services GraphQL](https://developer.adobe.com/commerce/services/graphql/).

### Configuração do firewall

Para permitir [!DNL Catalog Service] por meio de um firewall, adicione `commerce.adobe.io` ao arquivo de inclui na lista de permissões.

## Serviço de catálogo e API Mesh

A [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permite que os desenvolvedores integrem APIs privadas ou de terceiros e outras interfaces com produtos da Adobe usando o Adobe IO.

Consulte o tópico [[!DNL Catalog Service] e Malha de API](mesh.md) para obter detalhes sobre instalação e configuração.

## Painel de gerenciamento de dados

Para obter mais informações sobre a sincronização de dados do [!DNL Catalog Service], consulte o [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).
