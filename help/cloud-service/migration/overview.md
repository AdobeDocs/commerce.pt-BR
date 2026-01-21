---
title: Migrar para [!DNL Adobe Commerce as a Cloud Service]
description: Aprenda a migrar para [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a Adobe Systems Comércio como Cloud Service e somente projetos Adobe Systems Comércio Optimizer (infraestrutura SaaS gerenciados Adobe Systems)."
role: Developer
level: Intermediate
source-git-commit: af56d52f98a83310b858f82f16693f5323c1b962
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 0%

---

# Migrar para [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] Fornece um guia abrangente para desenvolvedores que transitam de uma Adobe Systems existente Comércio implementação PaaS para os novos Adobe Systems Comércio as a Cloud Service (SaaS). Adobe Systems Comércio como Cloud Service representa uma mudança significativa para um modelo SaaS totalmente gerenciado e sem versão, oferecendo melhor desempenho, escalabilidade, operações simplificadas e uma integração mais rigorosa com o mais [!DNL Adobe Experience Cloud]amplo.

>[!NOTE]
>
>Para obter mais informações sobre ferramentas de migração, consulte a [Ferramenta](./bulk-data.md) de migração de dados em massa.

## Entendendo a mudança - comparando PaaS e SaaS

**Principais diferenças**

* [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a Adobe Systems Comércio em projetos da Cloud (infraestrutura PaaS gerenciada por Adobe Systems) e somente projetos no local."} **PaaS (Atual)**: o Merchant gerencia aplicativo código, atualizações, correções, configuração de infraestrutura dentro do ambiente hospedado da Adobe Systems. [Modelo de responsabilidade](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/security-and-compliance/shared-responsibility) compartilhado para serviços (MySQL, Elasticsearch e outros).
* [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a Adobe Systems Comércio como Cloud Service e somente projetos Adobe Systems Comércio Optimizer (infraestrutura SaaS gerenciados Adobe Systems)."} **SaaS (Novo - [!DNL Adobe Commerce as a Cloud Service])**: Adobe Systems gerencia completamente as principais aplicativo, infraestrutura e atualizações. Os comerciantes se concentram na personalização por meio de pontos de extensibilidade (APIs, App Builder, SDKs de interface do usuário). O código do aplicativo principal está bloqueado.

**Implicações arquitetônicas**

* **Plataforma** sem versão: atualizações contínuas significam que não há mais atualizações de versão importantes para o núcleo.
* **Microservices e API primeiro**: maior dependência de APIs para extensibilidade e integração.
* **Sem per cabeçalho por padrão (opcional)**: suporte forte para vitrines dissociadas (por exemplo, Comércio storefront fornecida pelos Serviços de entrega do Edge).
* **Serviços de entrega de** borda: impacto no desempenho front-end e no implantação.

**Novo de ferramentas e conceitos**

* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) e [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=pt-BR)
* Provisionamento de autoatendimento com o [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Caminhos de migração

O [!DNL Adobe Commerce as a Cloud Service] oferece suporte a vários caminhos de migração, dependendo da linha do tempo, da loja e das personalizações.

Como alternativa a uma migração completa, o [!DNL Adobe Commerce as a Cloud Service] oferece suporte a uma migração em fases, usando Commerce Optimizer ou uma abordagem incremental.

* **Migração incremental** — Essa abordagem envolve a migração de dados, personalizações e integrações em estágios. Essa abordagem é ideal para grandes comerciantes com muitas personalizações que desejam fazer a transição gradual de suas personalizações e dados complexos para [!DNL Adobe Commerce as a Cloud Service] em seu próprio ritmo.

![migração incremental](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**—Esta abordagem permite a migração iterativa, usando o Commerce Optimizer como uma fase de transição para mover personalizações e dados complexos para o [!DNL Adobe Commerce as a Cloud Service] no seu próprio ritmo. A Commerce Optimizer fornece acesso aos Serviços de merchandising fornecidos pelas Exibições e políticas do catálogo, pela Commerce Storefront fornecida pela Edge Delivery e pelo [!DNL Product Visuals powered by AEM Assets].

![migração iterativa](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migração completa** — Essa abordagem envolve a migração de todos os dados, personalizações e integrações de uma só vez. Essa abordagem é ideal para comerciantes menores com poucas personalizações que desejam fazer a transição rápida para o [!DNL Adobe Commerce as a Cloud Service].

A tabela a seguir fornece uma visão geral do processo de migração para diferentes vitrines e configurações:

|                    | Loja LUMA | PWA Storefront | Comércio de armazenamento fornecido pela entrega do edge | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migração de dados | Necessário | Necessário | Necessário | Obrigatório |
| Loja | Migrar para a Commerce Storefront habilitada pela Edge Delivery | Migrar para a Commerce Storefront habilitada pela Edge Delivery ou manter | Nenhum impacto | Sem impacto |
| API Mesh | Criar nova malha | Construa nova malha ou reconfigure a existente | Construa nova malha ou reconfigure a existente | Construa nova malha ou reconfigure a existente |
| Integrações | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração | Aproveitar o kit inicial de integração |
| Personalizações | Mover para aplicativo Builder > Malha da API | Mover para aplicativo Builder > Malha da API | Mover para aplicativo Builder > Malha da API | Mover para aplicativo Builder > Malha da API |
| Gerenciamento de Assets | Migração necessária se estiver usando OOTB | Migração necessária se estiver usando OOTB | Migração necessária se estiver usando OOTB | Migração necessária se estiver usando OOTB |
| Extensões | Migrar para o Aplicativo Builder | Migrar para o Aplicativo Builder | Migrar para o Aplicativo Builder | Migrar para o Aplicativo Builder |

Conforme indicado na tabela, as mitigações para cada migração consistirão em:

* **Migração de dados**—Usando a [ferramenta de migração](./bulk-data.md) fornecida para migrar dados da sua instância existente para o [!DNL Adobe Commerce as a Cloud Service].
* **Storefront - Storefronts** Comércio existentes acionadas pela Edge Delivery e vitrines sem cabeça não exigem atenuação, mas as vitrines Luma exigem a migração para Comércio Storefront acionada pela Edge Delivery. PWA Studio vitrines podem ser migradas para Comércio Storefront fornecida pela Edge Delivery ou mantidas em seu estado atual. Adobe Systems fornecerá aceleradores para ajudar na migração da vitrine.
* **[Malha](https://developer.adobe.com/graphql-mesh-gateway)** da API - Criar uma nova malha ou modificar a existente. Adobe Systems fornecerá malhas pré-configuradas para ajudar nesse processo.
* **Integrações**: todas as integrações precisam usar o kit[&#x200B; inicial da &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)integração ou a [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Personalizações** — Todas as personalizações devem ser movidas para o aplicativo Builder e a Malha de API.
* **Gerenciamento do Assets**—Todo o gerenciamento de ativos requer migração. Se você já estiver usando o [!DNL AEM Assets], não há necessidade de migrar.
* **Extensões** — Todas as extensões em andamento precisam ser recriadas como extensões fora do processo. Até o final de 2025, a Adobe fornecerá acesso às nossas extensões mais populares para minimizar os tempos de compilação.

## Fases de migração

As fases a seguir descrevem as etapas e considerações necessárias para a migração para o [!DNL Adobe Commerce as a Cloud Service].

### Avaliação e planejamento antes da migração

Esta fase é crítico para minimizar riscos e estabelecer um caminho de migração claro e identificar problemas antes que eles ocorram.

**Descoberta e auditoria do ambiente atual**

**Análise de codebase:**

* Identificar todos os módulos personalizados, temas e substituições.
* Analise as modificações do código principal e determine quais precisarão ser refatoradas como parte da migração.
* Avalie as extensões de terceiros e determine a compatibilidade com [!DNL Adobe Commerce as a Cloud Service]. Existem alternativas compatíveis com o SaaS ou você precisa criar integrações personalizadas de API ou aplicativos aplicativo Builder?
* Identifique qualquer código ou funcionalidade obsoleto que não será migrado.

**Auditoria de dados:**

* Avalie o tamanho e a complexidade do banco de dados.
* Identifique dados ou tabelas não usados para limpar.
* Revise os processos existentes de importação/exportação de dados.

**Revisão de integrações:**

* Listar todos os sistemas externos integrados com Adobe Systems Comércio (ERP, CRM, PIM, gateways de pagamento, provedores de envio, OMS e qualquer outro sistema).
* Avalie os métodos de integração (API, scripts personalizados e outros métodos).
* Avalie a compatibilidade com [!DNL Adobe Commerce as a Cloud Service]a abordagem da API e o Construtor de aplicativo.

**Benchmarks de desempenho:**

* Documente as pontuações atuais do Lighthouse, os tempos de carregamento da página e os KPIs (indicadores-chave de desempenho), que fornecem uma linha de base para medir as melhorias pós-migração.

**Revisão da configuração de segurança:**

* Avalie quaisquer regras WAF personalizadas, incluis na lista de permissões de IP e quaisquer outras configurações de segurança.

**Definir escopo e estratégia de migração:**

* **Migração entre fases e tudo ao mesmo tempo:** avalie os prós e contras de cada abordagem.
* **Identificar processos comerciais principais:** Priorize as funcionalidades que devem ser migradas primeiro, como:
   * Regras complexas de preços
   * Regras de negócios personalizadas aplicadas antes de uma solicitar ser oficialmente colocada ou processada
   * Cálculos fiscais complexos
   * Validações de endereço
   * Lógica personalizada acionada depois que um pedido é feito
* **Loja headless vs. monolítica:** Ponto de decisão para desenvolvimento de nova loja ou adaptação de vitrines existentes.
* **Estratégia de integração:** determine como as integrações existentes serão reorganizadas (API Mesh, App Builder, API direta).
* **Estratégia de migração de dados:** determine se você pretende migrar usando dados históricos completos, dados parciais ou nenhum dado migrado.

**Preparação e treinamento da equipe:**

* Familiarize-se com [!DNL Adobe Commerce as a Cloud Service] conceitos, fluxos de trabalho de desenvolvimento e novas ferramentas.
* Participe de treinamento práticos com a Adobe Systems aplicativo Builder, Edge Delivery Services e [!DNL Adobe Commerce as a Cloud Service] pipelines implantação.

**Configuração e provisionamento do ambiente:**

* Provisione os [!DNL Adobe Commerce as a Cloud Service] ambientes de segurança e desenvolvimento com o Gerenciador de Commerce Cloud.

### Fases de migração incremental

**Refatoração e externalização estratégicas**

Esta fase consiste no núcleo da migração, com foco em adaptar sua base de códigos ao [!DNL Adobe Commerce as a Cloud Service] paradigma nativo nuvem. Isso envolve a adoção estrategicamente de novos serviços de Adobe Systems e a mudança da lógica personalizada para fora da plataforma principal Comércio.

#### &#x200B;1. Migre personalizações e extensões &quot;em processo&quot; para o aplicativo Builder

Trata-se de uma fase crucial para alcançar um &quot;núcleo bloqueado&quot; e sua solução à prova de futuro, central para a [!DNL Adobe Commerce as a Cloud Service] filosofia arquitetônica.

* **Externalize lógica complexa para aplicativo Builder**: analise módulos personalizados existentes e extensões de terceiros dentro de sua base de código do PaaS. Para integrações complexas de lógica de negócios ou microsserviços sob medida que não requerem manipulação direta e em processo dos principais Comércio modelo de dados, refator e reinserção como aplicativos sem servidor dentro do Adobe Systems Developer aplicativo Builder.
* **Aproveite a malha** de API: para cenários que exigem dados de vários sistemas de back-end (por exemplo, seus paas Comércio back-end, ERP, CRM e microsserviços personalizados aplicativo Builder), implementar uma camada de Malha de API dentro aplicativo Builder. Isso consolida APIs díspares em um único terminal GraphQL performante consumido pela sua nova vitrine ou outros serviços, simplificando a obtenção de dados complexos.
* **Arquitetura** orientada por eventos: utilize Adobe Systems Eventos de E/S para acionar ações do aplicativo Builder com base em eventos que ocorrem em sua instância PaaS (por exemplo, atualizações de produtos, registros do cliente, solicitar alterações de status) ou outros sistemas conectados. Isso promove a comunicação assíncrona, reduz o acoplamento apertado e aumenta a resiliência do sistema.

**Benefício**: esta etapa reduz significativamente a dívida técnica associada a personalizações profundamente incorporadas, acelera consideravelmente a transição da sua instância do Commerce para o [!DNL Adobe Commerce as a Cloud Service], melhora a escalabilidade e a implantabilidade independente da lógica personalizada e promove ciclos de desenvolvimento mais rápidos para extensões.

#### &#x200B;2. Adote serviços de merchandising da Adobe Commerce com base em SaaS e integre os dados do catálogo

Este é um ponto de integração inicial crítico com duas opções relacionadas ao gerenciamento de dados de catálogo:

>[!BEGINTABS]

>[!TAB Opção 1 - Serviço SaaS de catálogo existente]

**Aproveite o serviço de SaaS de catálogo existente integrado ao backend PaaS**

Essa opção serve como uma etapa transitória, baseada em uma integração existente no qual o back-end do PaaS preenche uma instância existente do serviço Adobe Systems Comércio SaaS com dados do serviço de [catálogo, &#x200B;](../../catalog-service/guide-overview.md)pesquisa[&#x200B; ativos e recomendações](../../live-search/overview.md) de [produtos.](../../product-recommendations/overview.md)

* **Sincronização** de dados do catálogo: certifique-se de que sua Adobe Systems Comércio Instância PaaS continue sincronizando dados de produtos e catálogos com o serviço Adobe Systems Comércio SaaS existente. Normalmente, isso depende de conectores ou módulos estabelecidos no instância PaaS. O serviço Catalog SaaS continua a ser a fonte autoritária para funções de pesquisa e merchandising, derivando seus dados do backend PaaS.
* **Malha de API para otimização**: enquanto a vitrine sem cabeça (no Edge Delivery Services) e outros serviços poderiam consumir diretamente dados do serviço catalog SaaS, Adobe Systems recomenda altamente o uso da Malha de API (no aplicativo Builder). A Malha de API pode unificar APIs do serviço Catalog SaaS com outras APIs necessárias do back-end do PaaS (por exemplo, verificações inventário em tempo real do banco de dados transacional ou de atributos de produtos personalizados não totalmente replicados para o serviço Catalog SaaS) em um único terminal GraphQL executante. Isso também permite armazenamento em cache centralizados, autenticação e transformação de resposta.
* **Integrar o Live Search e as Recomendações de Produto**: Configurar os serviços SaaS do Live Search e das Recomendações de Produto para [assimilar dados do catálogo](https://experienceleague.adobe.com/pt-br/docs/commerce/live-search/install#configure-the-data) diretamente do seu serviço SaaS do Catálogo do Adobe Commerce existente, que por sua vez é preenchido pelo seu back-end PaaS.

**Benefício**: fornece um caminho mais rápido para uma loja headless e recursos de merchandising SaaS avançados, aproveitando um serviço SaaS de catálogo existente e operacional e seu pipeline de integração com seu back-end PaaS. No entanto, ela retém a dependência do backend PaaS para o catálogo principal fonte de dados e não fornece os recursos de agregação de várias fontes inerentes ao novo Modelo de dados do catálogo composável. Essa opção é um trampolim válido para uma arquitetura de composição mais completa.

>[!TAB Opção 2 - Modelo de dados do catálogo compatível]

**Adotar o novo modelo de dados do catálogo composável (CCDM)**

Essa é a abordagem estratégica e que não se torna obsoleta para aproveitar o Adobe Commerce Optimizer. O CCDM fornece um serviço de catálogo unificado, flexível, dimensionável e projetado para agregação de dados de várias fontes e merchandising dinâmicos.

* **Assimilação e unificação de dados**
   * Comece assimilando dados de produto e catálogo da instância do Adobe Commerce PaaS existente (e/ou outros sistemas PIM/ERP) no novo Modelo de dados de catálogo combinável (CCDM).
   * Mapeie atributos de produto existentes para o esquema flexível do CCDM. Priorize os dados críticos do produto para a assimilação inicial.
   * Estabeleça pipelines de dados robustos para sincronização contínua. Isso pode envolver:
      * **Orientado** por eventos (por meio do aplicativo Builder): utilize Adobe Systems Eventos de E/S da sua instância PaaS para acionar aplicativos Adobe Systems do Construtor aplicativo disponíveis publicamente ou personalizados. Esses aplicativos transformam e empurram as alterações de dados (criem, atualizem e excluam) para o CCDM por meio de suas APIs.
      * **Em lote ingestão**: Para grandes cargas iniciais ou atualizações periódicas em massa, use transferências seguras de arquivos (por exemplo, CSV ou JSON) para uma área de preparo, processada por serviços de ingestão de Adobe Experience Platform (AEP) no CCDM.
      * **Integração** direta da API (com orquestração do aplicativo Builder): para cenários mais complexos, o aplicativo Builder pode atuar como uma camada de orquestração, fazer chamadas diretas de API para o back-end do PaaS, transformá-los e enviá-los para o CCDM.
* **Catalogar visualização e definição** política: configurar exibições de catálogos (agrupamentos lógicos para apresentação exclusiva de catálogos, como armazenamento exibições, regiões e segmentos B2B/B2C) e definir políticas (conjuntos regra para apresentação de produtos, filtragem e merchandising) no CCDM. Isso permite o controle dinâmico sobre sortimentos de produtos e lógica de exibição por visualização de catálogo.
* **Integre o Live Search e o Product recomendações**: uma vez que os dados do catálogo estão presentes no CCDM, integre os serviços live Search e recomendações produtos baseados em SaaS da Adobe Systems. Essas usar Adobe Systems AI AI e modelos de aprendizado de máquina para relevância pesquisa superior e recomendações personalizadas, consumindo dados diretamente do CCDM.

**Benefício**: ao abstrair o gerenciamento e a descoberta de catálogos no CCDM e serviços associados ao SaaS, você obtê melhor desempenho, ganha recursos de merchandising orientados por IA, descarrega significativamente as operações de leitura do seu back-end legado e permite uma &quot;peel-off&quot; robusta do funil experiência.

>[!ENDTABS]

#### &#x200B;3. Crie sua vitrine nos serviços de entrega do Edge

Com merchandising pipelines de dados estabelecidos e personalizações externalizadas, o focalizar muda para a construção de seu frontend de alto desempenho.

* **Configuração inicial**: configure seu projeto usando o modelo da vitrine da Adobe Commerce Store para o Edge Delivery Services. Isso fornece um front-end headless fundamental criado com tecnologias modernas da Web.
* **Conectar-se a serviços de catálogo e à API em Malha**: sua Loja do Commerce consumirá dados principalmente por meio de APIs da GraphQL:
   * **Opção 1**: do serviço SaaS de catálogo existente (por meio da Malha da API) para informações sobre produtos e merchandising regras.
   * **Opção 2**: do CCDM para informações de produtos e regras de merchandising.
   * Da Malha da API para quaisquer dados orquestrados do seu back-end herdado (PaaS instância) ou de serviços personalizados aplicativo Builder (por exemplo, inventário em tempo real, atributos de produto personalizados e pontos de fidelidade são exibidos).
* **Migração de conteúdo (AEM Services)**: Migre seu conteúdo estático existente (por exemplo, páginas &quot;Sobre nós&quot;, postagens de blog e banners de marketing) para o AEM Services, que capacita a Commerce Storefront. Aproveite os recursos de criação de conteúdo do AEM e verifique se os ativos estão otimizados para o Edge Delivery Services.
* **Desenvolva componentes principais interface: crie crítico componentes usuário de interface para páginas de detalhes do produto (PDPs), páginas** de listagem de produtos (PLPs) e páginas de conteúdo gerais usando componentes suspensos do Edge Delivery Services e componentes personalizados do React/Vue. Priorize os fluxos principais de comércio.
* **Integração com carrinho/checkout** existentes: Inicialmente, a vitrine dos Serviços de Entrega de Edge orquestrará uma entrega para as Adobe Systems Comércio PaaS (ou outra plataforma de terceiros) para carrinho gerenciamento e check-out. Normalmente, isso envolve:
   * **Redirecionamento**: redirecionando o usuário para os URLs de carrinho nativo e checkout da plataforma herdada, passando a sessão necessária e os identificadores carrinho.
   * **Interação direta com a API** (com a orquestração do App Builder): criação de componentes personalizados de carrinho e interface de check-out dentro do Edge Delivery Services que interagem diretamente com o carrinho do back-end do PaaS e as APIs de check-out. Isso geralmente envolve o App Builder as a Backend-for-Frontend (BFF) para orquestrar chamadas para vários serviços de back-end (por exemplo, carrinho de PaaS, gateways de pagamento e calculadoras de envio).

**Benefício**: proporciona uma experiência de vitrine extremamente rápida, otimizada para SEO e altamente flexível. Essa fase contribui diretamente para uma experiência superior do cliente e estabelece a base para a inovação futura de front-end.

#### &#x200B;4. Migração de dados (processo em fases)

A migração de dados é um processo crítico e multifacetado que é executado simultaneamente com a refatoração e o desenvolvimento da loja, garantindo a consistência e a integridade dos dados.

* **Limpe e otimize os dados** existentes: antes de qualquer migração em larga escala, execute dados abrangentes limpeza, desduplicação e validação no banco de dados PaaS existente. Essa etapa proativa é crucial para minimizar a transferência de problemas de dados herdados e garantir a qualidade dos dados nas novas ambiente.

**Migrações de dados em massa**

A migração de dados em massa envolve obter um dump de dados completo da sua Adobe Systems Comércio instância PaaS, transformar todo esse conjunto de dados e importá-lo em Adobe Systems Comércio como um Cloud Service de uma só vez. Normalmente, esse método é usado para a população inicial de dados.

* **Disponibilidade de** ferramentas: ferramentas[&#x200B; dedicadas &#x200B;](./bulk-data.md)de migração de dados em massa para uso do cliente em Comércio migrações de dados em massa estarão disponíveis até solicitação no primeiro trimestre de 2026. Se os clientes precisarem de assistência com a migração de dados em massa previamente, Adobe Systems pode facilitar a transferência de dados em seu nome solicitação.

* **Processo**:
   * **Exportação** completa de dados: Extract uma conjunto de dados completa da Adobe Systems Comércio instância PaaS (por exemplo, produtos, categorias, contas do cliente, dados de solicitar históricos, blocos estáticos e página conteúdo).
   * **Transformação de dados**: aplique as transformações necessárias para alinhar os dados extraídos com os requisitos de esquema dos novos componentes do Adobe Commerce as a Cloud Service, incluindo o Modelo de Dados de Catálogo Combinável (CCDM), se adotado, e quaisquer outros serviços ou bancos de dados relevantes da Adobe. Isso pode envolver scripts personalizados ou ferramentas especializadas de mapeamento de dados.
   * **Importação inicial**: importe o conjunto de dados completo transformado nos respectivos componentes do Adobe Commerce as a Cloud Service. Para dados de produto e categoria, isso preenche o serviço de catálogo escolhido (CCDM ou SaaS de catálogo existente). Para dados de clientes e pedidos, isso preenche o back-end transacional ou os serviços associados.
   * **Validação**: valide rigorosamente os dados importados para garantir integridade, precisão e consistência em todos os novos sistemas.

**Migrações de dados iterativos**

As migrações de dados iterativos se concentram na sincronização de alterações incrementais e deltas da instância PaaS de origem para os novos componentes do Cloud Service, garantindo a atualização dos dados antes e depois da transferência.

* **Disponibilidade de ferramentas**: as ferramentas especificamente projetadas para migrações de dados iterativos estarão disponíveis em 2026.

* **Processo**:
   * **Identificação delta**: estabeleça mecanismos para identificar alterações (criações, atualizações e exclusões) em conjuntos de dados críticos no ambiente PaaS desde a última sincronização. Isso pode envolver captura de dados de alteração (CDC), comparações de carimbo de data e hora ou acionadores baseados em eventos.
   * **Sincronização** contínua: implemente mecanismos robustos para sincronização contínua e incremental de dados da sua ambiente PaaS com os novos componentes Cloud Service (por exemplo, CCDM e back-end transacional). Isso é fundamental para manter o frescor dos dados e minimizar o tempo de inatividade durante o corte.
   * **Aproveitar os eventos**: utilize eventos de E/S Adobe Systems, quando possível, para acionar ações aplicativo Construtor para atualizações em tempo real ou quase em tempo real do seu instância PaaS para os novos serviços. Por exemplo, uma atualização de produto no PaaS pode acionar uma evento que atualiza a entrada correspondente no CCDM.
   * **Atualizações orientadas por API: para dados que não são evento orientados** por evento, use chamadas de API agendadas (por meio do aplicativo Builder ou outras plataformas de integração) para obter alterações do PaaS e enviá-las para os novos sistemas.
   * **Erro manuseio e monitoramento**: implemente tratamento, fazendo logon e monitoramento robustos de todos os pipelines de dados iterativos para garantir que a integridade dos dados seja mantida durante todo o processo.

### Pós-migração e operações contínuas

**Transferência e ativação de DNS:**

* Planeje cuidadosamente a transferência de DNS com o mínimo de tempo de inatividade.
* Monitore a integridade e o desempenho do site imediatamente após o lançamento.

**Operações de Post-iniciar:**

**Descontinuação do ambiente PaaS:**

* Arquive ou exclua com segurança instâncias e dados antigos do PaaS após o período de validação.

**Fluxo de trabalho de desenvolvimento em andamento:**

* Adote a natureza sem versão do [!DNL Adobe Commerce as a Cloud Service], que tem pequenas implantações contínuas em vez de grandes atualizações.
* Utilize o Cloud Manager para gerenciar ambientes e implantações.
* Aproveite o App Builder para estender a funcionalidade sem afetar o núcleo.

**Monitoramento, desempenho e segurança:**

* Monitor continuamente desempenho do site, erros e logs de segurança.
* Utilize os recursos incorporados de segurança da Adobe Systems e siga as práticas recomendadas.

**Treinamento e documentação:**

* Treine novos desenvolvedores e usuários empresariais na [!DNL Adobe Commerce as a Cloud Service] plataforma e no workflows.
* Mantenha a documentação interna atualizada para integrações e processos personalizados.
