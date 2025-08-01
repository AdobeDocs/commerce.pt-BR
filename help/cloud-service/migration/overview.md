---
title: Migrar para  [!DNL Adobe Commerce as a Cloud Service]
description: Saiba como migrar para o  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Architect
source-git-commit: 2ecf5e0960b2e63cc95016e8ee5509b3c475de13
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 0%

---

# Migrar para [!DNL Adobe Commerce as a Cloud Service]

O [!DNL Adobe Commerce as a Cloud Service] fornece um guia abrangente para desenvolvedores que estão fazendo a transição de uma implementação existente do Adobe Commerce PaaS para a nova oferta do Adobe Commerce as a Cloud Service (SaaS). O Adobe Commerce as a Cloud Service representa uma mudança significativa para um modelo SaaS totalmente gerenciado e sem versão, oferecendo desempenho aprimorado, escalabilidade, operações simplificadas e maior integração com a Adobe Experience Cloud mais ampla.

>[!NOTE]
>
>Para obter mais informações sobre as ferramentas de migração, consulte a [Ferramenta de Migração de Dados em Massa](./bulk-data.md).

## Compreender a mudança - comparação entre PaaS e SaaS

**Principais diferenças**

* [!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."} **PaaS (Atual)**: o comerciante gerencia o código do aplicativo, as atualizações, os patches e a configuração da infraestrutura no ambiente hospedado da Adobe. [Modelo de responsabilidade compartilhada](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility) para serviços (MySQL, Elasticsearch e outros).
* [!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} **SaaS (Novo - [!DNL Adobe Commerce as a Cloud Service])**: o Adobe gerencia totalmente o aplicativo principal, a infraestrutura e as atualizações. Os comerciantes se concentram na personalização por meio de pontos de extensibilidade (APIs, App Builder, SDKs de interface do usuário). O código do aplicativo principal está bloqueado.

**Implicações arquitetônicas**

* **Plataforma sem versão**: atualizações contínuas significam que não há mais atualizações de versão principais para o núcleo.
* **Microsserviços e API-first**: maior dependência de APIs para extensibilidade e integração.
* **Headless por padrão (opcional)**: forte suporte para vitrines dissociadas (por exemplo, vitrines para a Commerce alimentadas pela Edge Delivery Services).
* **Edge Delivery Services**: impacto no desempenho e na implantação do front-end.

**Novos conceitos e ferramentas**
* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) e [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
* Provisionamento de autoatendimento com o [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Caminhos de migração

O [!DNL Adobe Commerce as a Cloud Service] oferece suporte a vários caminhos de migração, dependendo da linha do tempo, da loja e das personalizações.

Como alternativa a uma migração completa, o [!DNL Adobe Commerce as a Cloud Service] oferece suporte a uma migração em fases, usando Commerce Optimizer ou uma abordagem incremental.

* **Migração incremental** — Essa abordagem envolve a migração de dados, personalizações e integrações em estágios. Essa abordagem é ideal para grandes comerciantes com muitas personalizações que desejam fazer a transição gradual de suas personalizações e dados complexos para [!DNL Adobe Commerce as a Cloud Service] em seu próprio ritmo.

![migração incremental](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—Esta abordagem permite a migração iterativa, usando o Commerce Optimizer como uma fase de transição para mover personalizações e dados complexos para o [!DNL Adobe Commerce as a Cloud Service] no seu próprio ritmo. A Commerce Optimizer fornece acesso a Serviços de merchandising viabilizados por Exibições e políticas de catálogo, Commerce Storefront viabilizada pela Edge Delivery e Visualizações de produto viabilizadas pela AEM Assets.

![migração iterativa](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migração completa** — Essa abordagem envolve a migração de todos os dados, personalizações e integrações de uma só vez. Essa abordagem é ideal para comerciantes menores com poucas personalizações que desejam fazer a transição rápida para o [!DNL Adobe Commerce as a Cloud Service].

A tabela a seguir fornece uma visão geral do processo de migração para diferentes vitrines e configurações:

|                    | Loja LUMA | PWA Storefront | Commerce Storefront ativado por Edge Delivery | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migração de dados | Obrigatório | Obrigatório | Obrigatório | Obrigatório |
| Loja | Migrar para a Commerce Storefront habilitada pela Edge Delivery | Migrar para a Commerce Storefront habilitada pela Edge Delivery ou manter | Sem impacto | Sem impacto |
| API Mesh | Criar nova malha | Criar uma nova malha ou reconfigurar uma malha existente | Criar uma nova malha ou reconfigurar uma malha existente | Criar uma nova malha ou reconfigurar uma malha existente |
| Integrações | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração |
| Personalizações | Mover para App Builder e API Mesh | Mover para App Builder e API Mesh | Mover para App Builder e API Mesh | Mover para App Builder e API Mesh |
| Gerenciamento do Assets | Migração necessária se estiver usando o OOTB | Migração necessária se estiver usando o OOTB | Migração necessária se estiver usando o OOTB | Migração necessária se estiver usando o OOTB |
| Extensões | Migrar para o App Builder | Migrar para o App Builder | Migrar para o App Builder | Migrar para o App Builder |

Conforme indicado na tabela, as mitigações para cada migração consistirão em:

* **Migração de dados**—Usando a [ferramenta de migração](./bulk-data.md) fornecida para migrar dados da sua instância existente para o [!DNL Adobe Commerce as a Cloud Service].
* **Storefront** — as Storefront da Commerce existentes alimentadas pela Edge Delivery e as lojas headless não exigem mitigação, mas as lojas Luma exigem migração para a Commerce Storefront alimentada pela Edge Delivery. As vitrines da PWA Studio podem ser migradas para a Commerce Storefront com a tecnologia da Edge Delivery ou mantidas em seu estado atual. A Adobe fornecerá aceleradores para auxiliar na migração da loja.
* **[Malha de API](https://developer.adobe.com/graphql-mesh-gateway)**—Crie uma nova malha ou modifique a existente. A Adobe fornecerá malhas pré-configuradas para auxiliar nesse processo.
* **Integrações** — Todas as integrações precisam aproveitar o [kit inicial de integração](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) ou a [[!DNL Adobe Commerce as a Cloud Service] API REST](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Personalizações** — Todas as personalizações devem ser movidas para o App Builder e para a API Mesh.
* **Gerenciamento do Assets**—Todo o gerenciamento de ativos requer migração. Se você já estiver usando o AEM Assets, não será necessário migrar.
* **Extensões** — Todas as extensões em andamento precisam ser recriadas como extensões fora do processo. Até o final de 2025, a Adobe fornecerá acesso às nossas extensões mais populares para minimizar os tempos de compilação.

## Fases de migração

As fases a seguir descrevem as etapas e considerações necessárias para a migração para o [!DNL Adobe Commerce as a Cloud Service].

### Avaliação e planejamento antes da migração

Essa fase é essencial para minimizar os riscos e estabelecer um caminho de migração claro e identificar problemas antes que eles surjam.

**Descoberta e auditoria do ambiente atual**

**Análise de codebase:**

* Identificar todos os módulos personalizados, temas e substituições.
* Analise as modificações do código principal e determine quais precisarão ser refatoradas como parte da migração.
* Avalie extensões de terceiros e determine a compatibilidade com o [!DNL Adobe Commerce as a Cloud Service]. Existem alternativas compatíveis com SaaS ou você precisa criar integrações de API personalizadas ou aplicativos App Builder?
* Identifique qualquer código ou funcionalidade obsoleta que não será migrada.

**Auditoria de dados:**

* Avalie o tamanho e a complexidade do banco de dados.
* Identificar dados ou tabelas não utilizados para limpeza.
* Revise os processos existentes de importação/exportação de dados.

**Revisão de integrações:**

* Listar todos os sistemas externos integrados ao Adobe Commerce (ERP, CRM, PIM, gateways de pagamento, provedores de envio, OMS e quaisquer outros sistemas).
* Avalie os métodos de integração (API, scripts personalizados e outros métodos).
* Avaliar a compatibilidade com a abordagem de API First de [!DNL Adobe Commerce as a Cloud Service] e o App Builder.

**Benchmarks de desempenho:**

* Documente as pontuações atuais do Lighthouse, os tempos de carregamento da página e os KPIs (indicadores-chave de desempenho), que fornecem uma linha de base para medir as melhorias pós-migração.

**Revisão da configuração de segurança:**

* Avalie quaisquer regras personalizadas do WAF, listas de permissões de IP e outras configurações de segurança.

**Definir escopo e estratégia de migração:**

* **Migração em fases vs. de uma só vez:** Avalie os prós e os contras de cada abordagem.
* **Identificar processos comerciais principais:** Priorize as funcionalidades que devem ser migradas primeiro, como:
   * Regras complexas de preços
   * Regras de negócios personalizadas aplicadas antes que um pedido seja feito ou processado oficialmente
   * Cálculos de imposto complexos
   * Validações de endereço
   * Lógica personalizada acionada depois que um pedido é feito
* **Loja headless vs. monolítica:** Ponto de decisão para desenvolvimento de nova loja ou adaptação de vitrines existentes.
* **Estratégia de integração:** determine como as integrações existentes serão reorganizadas (API Mesh, App Builder, API direta).
* **Estratégia de migração de dados:** determine se você pretende migrar usando dados históricos completos, dados parciais ou nenhum dado migrado.

**Preparação e treinamento da equipe:**

* Familiarize-se com [!DNL Adobe Commerce as a Cloud Service] conceitos, fluxos de trabalho de desenvolvimento e novas ferramentas.
* Participe do treinamento prático com Adobe App Builder, Edge Delivery Services e [!DNL Adobe Commerce as a Cloud Service] pipelines de implantação.

**Configuração e provisionamento do ambiente:**

* Provisionar os ambientes de sandbox e desenvolvimento do [!DNL Adobe Commerce as a Cloud Service] com o Commerce Cloud Manager.

### Fases de migração incremental

**Refatoração e externalização estratégicas**

Essa fase consiste no núcleo da migração, com foco na adaptação de sua base de código para o paradigma nativo em nuvem [!DNL Adobe Commerce as a Cloud Service]. Isso envolve a adoção estratégica de novos serviços da Adobe e a remoção da lógica personalizada da plataforma principal do Commerce.

#### &#x200B;1. Migrar personalizações e extensões &quot;em andamento&quot; para o App Builder

Esta é uma fase crucial para atingir um &quot;núcleo bloqueado&quot; e uma solução que não se torna obsoleta, central para a filosofia de arquitetura do [!DNL Adobe Commerce as a Cloud Service].

* **Externalizar lógica complexa para o App Builder**: analisar módulos personalizados existentes e extensões de terceiros dentro da sua base de código PaaS. Para uma lógica de negócios complexa, integrações sob medida ou microsserviços que não exigem manipulação direta e em andamento do modelo de dados principal do Commerce, alterne-os e recompile-os como aplicativos sem servidor no Adobe Developer App Builder.
* **Aproveite a API Mesh**: para cenários que exigem dados de vários sistemas de back-end (por exemplo, seu back-end PaaS Commerce, ERP, CRM e microsserviços personalizados do App Builder), implemente uma camada de API Mesh no App Builder. Isso consolida APIs diferentes em um único endpoint GraphQL de alto desempenho consumido por sua nova loja ou outros serviços, simplificando a busca complexa de dados.
* **Arquitetura orientada por eventos**: utilize o Adobe I/O Events para acionar ações do App Builder com base em eventos que ocorrem em sua instância do PaaS (por exemplo, atualizações de produtos, registros de clientes, alterações de status de pedidos) ou outros sistemas conectados. Isso promove a comunicação assíncrona, reduz o acoplamento rígido e melhora a resiliência do sistema.

**Benefício**: esta etapa reduz significativamente a dívida técnica associada a personalizações profundamente incorporadas, acelera consideravelmente a transição da sua instância do Commerce para o [!DNL Adobe Commerce as a Cloud Service], melhora a escalabilidade e a implantabilidade independente da lógica personalizada e promove ciclos de desenvolvimento mais rápidos para extensões.

#### &#x200B;2. Adote serviços de merchandising da Adobe Commerce com base em SaaS e integre os dados do catálogo

Este é um ponto de integração inicial crítico com duas opções relacionadas ao gerenciamento de dados de catálogo:

>[!BEGINTABS]

>[!TAB Opção 1 - Serviço SaaS de catálogo existente]

**Aproveite o serviço SaaS do catálogo existente integrado ao back-end PaaS**

Esta opção serve como uma etapa de transição, com base em uma integração existente em que o back-end do PaaS preenche uma instância existente do serviço SaaS do Adobe Commerce com dados do [serviço de catálogo](../../catalog-service/guide-overview.md), do [live search](../../live-search/overview.md) e das [recomendações de produto](../../product-recommendations/overview.md).

* **Sincronização de dados do catálogo**: certifique-se de que a instância do Adobe Commerce PaaS continue a sincronizar dados de produtos e catálogos com o serviço SaaS do catálogo Adobe Commerce existente. Normalmente, isso depende de conectores ou módulos estabelecidos na instância do PaaS. O serviço SaaS de catálogo permanece como a fonte oficial para funções de pesquisa e merchandising, derivando seus dados do back-end do PaaS.
* **API Mesh para otimização**: embora a loja headless (no Edge Delivery Services) e outros serviços possam consumir dados diretamente do serviço SaaS do catálogo, a Adobe recomenda usar a API Mesh (no App Builder). A API Mesh pode unificar APIs do serviço SaaS de catálogo com outras APIs necessárias do back-end do PaaS (por exemplo, verificações de inventário em tempo real do banco de dados transacional ou atributos de produto personalizados não totalmente replicados para o serviço SaaS de catálogo) em um único endpoint GraphQL com bom desempenho. Isso também permite armazenamento em cache, autenticação e transformação de resposta centralizados.
* **Integrar o Live Search e as Recomendações de Produto**: Configurar os serviços SaaS do Live Search e das Recomendações de Produto para [assimilar dados do catálogo](https://experienceleague.adobe.com/en/docs/commerce/live-search/install#configure-the-data) diretamente do seu serviço SaaS do Catálogo do Adobe Commerce existente, que por sua vez é preenchido pelo seu back-end PaaS.

**Benefício**: fornece um caminho mais rápido para uma loja headless e recursos de merchandising SaaS avançados, aproveitando um serviço SaaS de catálogo existente e operacional e seu pipeline de integração com seu back-end PaaS. No entanto, ela mantém a dependência do back-end PaaS para a fonte de dados do catálogo principal e não fornece os recursos de agregação de várias fontes inerentes ao novo Modelo de dados de catálogo combinável. Essa opção é um trampolim válido para uma arquitetura de composição mais completa.

>[!TAB Opção 2 - Modelo de Dados de Catálogo Combinável]

**Adotar o novo Modelo de Dados de Catálogo de Composição (CCDM)**

Essa é a abordagem estratégica e que não se torna obsoleta para aproveitar o Adobe Commerce Optimizer. O CCDM fornece um serviço de catálogo flexível, escalável e unificado projetado para agregação de dados de várias fontes e comercialização dinâmica.

* **Assimilação e unificação de dados**
   * Comece assimilando dados de produto e catálogo da instância do Adobe Commerce PaaS existente (e/ou outros sistemas PIM/ERP) no novo Modelo de dados de catálogo combinável (CCDM).
   * Mapeie atributos de produto existentes para o esquema flexível do CCDM. Priorize os dados críticos do produto para a assimilação inicial.
   * Estabeleça pipelines de dados robustos para sincronização contínua. Isso pode envolver:
      * **Orientado por eventos** (por meio do App Builder): utilize o Adobe I/O Events da sua instância do PaaS para acionar aplicativos Adobe App Builder disponíveis publicamente ou personalizados. Esses aplicativos transformam e enviam alterações de dados (criar, atualizar e excluir) para o CCDM por meio de suas APIs.
      * **Assimilação em lote**: para grandes cargas iniciais ou atualizações periódicas em massa, use transferências de arquivos seguras (por exemplo, CSV ou JSON) para uma área de preparo, processadas pelos serviços de assimilação do Adobe Experience Platform (AEP) no CCDM.
      * **Integração da API direta** (com a orquestração do App Builder): para cenários mais complexos, o App Builder pode agir como uma camada de orquestração, fazendo chamadas de API diretas para o back-end do PaaS, transformando os dados e enviando-os para o CCDM.
* **Exibição de catálogo e definição de política**: configure exibições de catálogo (agrupamentos lógicos para apresentação de catálogo exclusiva, como exibições de loja, regiões e segmentos B2B/B2C) e defina políticas (conjuntos de regras para apresentação de produto, filtragem e merchandising) no CCDM. Isso permite o controle dinâmico sobre os sortimentos de produtos e a lógica de exibição por exibição de catálogo.
* **Integrar o Live Search e as Recomendações de Produto**: depois que os dados do catálogo estiverem presentes no CCDM, integre os serviços Adobe Live Search e Recomendações de Produto com base em SaaS. Eles aproveitam a IA do Adobe Sensei e os modelos de aprendizado de máquina para relevância de pesquisa superior e recomendações personalizadas, consumindo dados diretamente da CCDM.

**Benefício**: ao abstrair o gerenciamento de catálogos e a descoberta em serviços CCDM e SaaS associados, você obtém melhor desempenho, obtém recursos de merchandising orientados por IA, descarrega significativamente as operações de leitura de seu back-end herdado e habilita um &quot;peel-off&quot; robusto da experiência de topo de funil.

>[!ENDTABS]

#### &#x200B;3. Crie sua vitrine no Edge Delivery Services

Com pipelines de dados de merchandising estabelecidos e personalizações externalizadas, o foco muda para a criação de um front-end de alto desempenho.

* **Configuração inicial**: configure seu projeto usando o modelo da vitrine da Adobe Commerce Store para o Edge Delivery Services. Isso fornece um front-end headless fundamental criado com tecnologias modernas da Web.
* **Conectar-se a serviços de catálogo e à API em Malha**: sua Loja do Commerce consumirá dados principalmente por meio de APIs da GraphQL:
   * **Opção 1**: do serviço SaaS de catálogo existente (por meio da API Mesh) para obter informações sobre o produto e regras de merchandising.
   * **Opção 2**: do CCDM para informações sobre produtos e regras de merchandising.
   * No API Mesh, para quaisquer dados orquestrados do back-end herdado (instância PaaS) ou serviços personalizados do App Builder (por exemplo, inventário em tempo real, atributos de produto personalizados e exibição de pontos de fidelidade).
* **Migração de conteúdo (AEM Services)**: Migre seu conteúdo estático existente (por exemplo, páginas &quot;Sobre nós&quot;, postagens de blog e banners de marketing) para o AEM Services, que capacita a Commerce Storefront. Aproveite os recursos de criação de conteúdo do AEM e verifique se os ativos estão otimizados para o Edge Delivery Services.
* **Desenvolver componentes principais da interface do usuário**: crie componentes críticos da interface do usuário para páginas de detalhes do produto (PDPs), páginas de listagem de produtos (PLPs) e páginas de conteúdo geral usando componentes de entrada do Edge Delivery Services e componentes personalizados do React/Vue. Priorizar os fluxos comerciais principais.
* **Integração com o carrinho/check-out existente**: inicialmente, a loja da Edge Delivery Services orquestrará uma entrega para seu Adobe Commerce PaaS (ou outra plataforma de terceiros) existente para gerenciamento e check-out do carrinho. Normalmente, isso envolve:
   * **Redirecionamento**: redirecionando o usuário para o carrinho nativo da plataforma herdada e fazendo check-out das URLs, transmitindo os identificadores de sessão e carrinho necessários.
   * **Interação direta com a API** (com a orquestração do App Builder): criação de componentes personalizados de carrinho e interface de check-out dentro do Edge Delivery Services que interagem diretamente com o carrinho do back-end do PaaS e as APIs de check-out. Isso geralmente envolve o App Builder as a Backend-for-Frontend (BFF) para orquestrar chamadas para vários serviços de back-end (por exemplo, carrinho de PaaS, gateways de pagamento e calculadoras de envio).

**Benefício**: proporciona uma experiência de vitrine extremamente rápida, otimizada para SEO e altamente flexível. Essa fase contribui diretamente para uma experiência superior do cliente e estabelece a base para a inovação futura de front-end.

#### &#x200B;4. Migração de dados (processo em fases)

A migração de dados é um processo crítico e multifacetado que é executado simultaneamente com a refatoração e o desenvolvimento da loja, garantindo a consistência e a integridade dos dados.

* **Limpar e otimizar dados existentes**: antes de qualquer migração em larga escala, execute limpeza, eliminação de duplicação e validação abrangentes de dados no banco de dados PaaS existente. Essa etapa proativa é crucial para minimizar a transferência de problemas de dados herdados e garantir a qualidade dos dados no novo ambiente.

**Migrações de dados em massa**

A migração de dados em massa envolve fazer um despejo de dados completo da instância do Adobe Commerce PaaS, transformar esse conjunto de dados inteiro e importá-lo para o Adobe Commerce as a Cloud Service de uma só vez. Normalmente, esse método é usado para a população inicial de dados.

* **Disponibilidade de ferramentas**: as [ferramentas de migração de dados em massa](./bulk-data.md) dedicadas para uso do cliente em migrações de dados em massa primárias do Commerce estarão disponíveis por solicitação em meados de julho de 2025. Se os clientes precisarem de assistência com a migração de dados em massa antecipadamente, o Adobe poderá facilitar a transferência de dados em seu nome, mediante solicitação.

* **Processo**:
   * **Exportação de dados completa**: extraia um conjunto de dados completo da sua instância do Adobe Commerce PaaS (por exemplo, produtos, categorias, contas de clientes, dados históricos de pedidos, blocos estáticos e conteúdo da página).
   * **Transformação de dados**: aplique as transformações necessárias para alinhar os dados extraídos com os requisitos de esquema dos novos componentes do Adobe Commerce as a Cloud Service, incluindo o Modelo de Dados de Catálogo Combinável (CCDM), se adotado, e quaisquer outros serviços ou bancos de dados relevantes da Adobe. Isso pode envolver scripts personalizados ou ferramentas especializadas de mapeamento de dados.
   * **Importação inicial**: importe o conjunto de dados completo transformado nos respectivos componentes do Adobe Commerce as a Cloud Service. Para dados de produto e categoria, isso preenche o serviço de catálogo escolhido (CCDM ou SaaS de catálogo existente). Para dados de clientes e pedidos, isso preenche o back-end transacional ou os serviços associados.
   * **Validação**: valide rigorosamente os dados importados para garantir integridade, precisão e consistência em todos os novos sistemas.

**Migrações de dados iterativos**

As migrações de dados iterativos se concentram na sincronização de alterações incrementais e deltas da instância PaaS de origem para os novos componentes do Cloud Service, garantindo a atualização dos dados antes e depois da transferência.

* **Disponibilidade de ferramentas**: as ferramentas especificamente projetadas para migrações de dados iterativos estarão disponíveis no segundo semestre de 2025.

* **Processo**:
   * **Identificação delta**: estabeleça mecanismos para identificar alterações (criações, atualizações e exclusões) em conjuntos de dados críticos no ambiente PaaS desde a última sincronização. Isso pode envolver captura de dados de alteração (CDC), comparações de carimbo de data e hora ou acionadores baseados em eventos.
   * **Sincronização contínua**: implemente mecanismos robustos para a sincronização contínua e incremental de dados do seu ambiente PaaS para os novos componentes do Cloud Service (por exemplo, CCDM e back-end transacional). Isso é fundamental para manter a atualização dos dados e minimizar o tempo de inatividade durante a transferência.
   * **Eventos de alavancagem**: utilize a Adobe I/O Events quando possível para acionar ações do App Builder para atualizações em tempo real ou quase em tempo real da sua instância do PaaS para os novos serviços. Por exemplo, uma atualização de produto no PaaS pode acionar um evento que atualize a entrada correspondente no CCDM.
   * **Atualizações orientadas por API**: para dados que não são orientados por eventos, use chamadas de API agendadas (por meio do App Builder ou outras plataformas de integração) para extrair alterações do PaaS e enviá-las para os novos sistemas.
   * **Manipulação e monitoramento de erros**: implemente uma manipulação, um log e um monitoramento de erros robustos para todos os pipelines de dados iterativos para garantir que a integridade dos dados seja mantida durante todo o processo.

### Pós-migração e operações contínuas

**Transferência e ativação de DNS:**

* Planeje cuidadosamente a transferência de DNS com o mínimo de tempo de inatividade.
* Monitore a integridade e o desempenho do site imediatamente após o lançamento.

**Operações pós-inicialização:**

**Encerrando ambiente PaaS:**

* Arquive ou exclua com segurança instâncias e dados antigos do PaaS após o período de validação.

**Fluxo de trabalho de desenvolvimento em andamento:**

* Adote a natureza sem versão do [!DNL Adobe Commerce as a Cloud Service], que tem pequenas implantações contínuas em vez de grandes atualizações.
* Utilize o Cloud Manager para gerenciar ambientes e implantações.
* Aproveite o App Builder para estender a funcionalidade sem afetar o núcleo.

**Monitoramento, desempenho e segurança:**

* Monitore continuamente o desempenho do site, erros e registros de segurança.
* Utilize os recursos de segurança integrados da Adobe e siga as práticas recomendadas.

**Treinamento e documentação:**

* Treine novos desenvolvedores e usuários empresariais na plataforma e nos fluxos de trabalho do [!DNL Adobe Commerce as a Cloud Service].
* Mantenha documentação interna atualizada para integrações e processos personalizados.
