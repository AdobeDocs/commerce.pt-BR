---
title: Migrar para  [!DNL Adobe Commerce as a Cloud Service]
description: Saiba como migrar para o  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-06-18T16:12:28.840Z'
TQID: 'https://experienceleague.adobe.com/GmxaQdGKvAIDpZ2jvmlLFSYw0IFQysIMOT0lUnsJBsI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: e03840ea9e0e43a005f385914e8599804383e79d
workflow-type: tm+mt
source-wordcount: 3305
ht-degree: 0%

---

# Migrar para [!DNL Adobe Commerce as a Cloud Service]

Este guia ajuda os desenvolvedores a fazerem a transição do [!DNL Adobe Commerce on Cloud] ou no local para o [!DNL Adobe Commerce as a Cloud Service] (SaaS). Esse modelo SaaS oferece desempenho aprimorado, escalabilidade e integração com o [!DNL Adobe Experience Cloud].

>[!NOTE]
>
>Para obter mais informações sobre ferramentas de migração, consulte a [ferramenta de migração de dados em massa](./bulk-data/migration-tool.md).

## Visão geral

Migrar um repositório [!DNL Adobe Commerce] estabelecido para [!DNL Adobe Commerce as a Cloud Service] é mais do que mover dados. Uma migração real abrange as seguintes áreas:

- Aplicativo - personalizações e extensões criadas para [!DNL Adobe Commerce on Cloud] ou instalações locais
- Dados - catálogos, pedidos, clientes e configuração
- Loja
- Integrações com sistemas externos

[!DNL Adobe Commerce as a Cloud Service] é uma plataforma SaaS sem versão, o que significa que nenhuma dessas áreas pode ser migrada sem adaptá-las. As personalizações são modernizadas nos aplicativos do [!DNL App Builder], as vitrines são recriadas no Edge Delivery Services (EDS), os dados são migrados para o novo locatário do [!DNL Adobe Commerce as a Cloud Service] e as integrações são restabelecidas usando os padrões SaaS.

Em vez de considerar a migração como um único projeto monolítico, a Adobe fornece um fluxo de trabalho de migração integrado que abrange as [três ferramentas de migração](#migration-tools-workflow).

Esse fluxo de trabalho compartilhado consolida a detecção, alinha as equipes de engenharia e de entrega e fornece um plano de migração consistente.

![diagrama do fluxo de migração](../assets/migration-flow.png)

### Comparação de PaaS e SaaS

O [!DNL Adobe Commerce on Cloud] ou local (PaaS) e o [!DNL Adobe Commerce as a Cloud Service] (SaaS) diferem na forma como são gerenciados e como os comerciantes interagem com a plataforma.

**Principais diferenças**

- [!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."}
- **[!DNL Adobe Commerce on Cloud Infrastructure]**: O comerciante gerencia o código do aplicativo, as atualizações, os patches e a configuração da infraestrutura.
- **[!DNL Adobe Commerce]no local**: o comerciante gerencia o código do aplicativo, as atualizações, os patches e a configuração da infraestrutura no ambiente hospedado da Adobe.

  >[!NOTE]
  >
  >[Modelo de responsabilidade compartilhada](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility) para serviços (MySQL, Elasticsearch e outros).

- [!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} **SaaS (Novo - [!DNL Adobe Commerce as a Cloud Service])**: o Adobe gerencia totalmente o aplicativo principal, a infraestrutura e as atualizações. Os comerciantes se concentram na personalização por meio de pontos de extensibilidade (APIs, App Builder, SDKs de interface). O código do aplicativo principal está bloqueado.

**Implicações arquitetônicas**

- **Plataforma sem versão**: atualizações contínuas significam que não há mais atualizações de versão principais para o núcleo.
- **Microsserviços e API-first**: maior dependência de APIs para extensibilidade e integração.
- **Headless por padrão (opcional)**: forte suporte para vitrines dissociadas (por exemplo, vitrines para a Commerce alimentadas pela Edge Delivery Services).
- **Edge Delivery Services**: impacto no desempenho e na implantação do front-end.

**Novas ferramentas e conceitos**

- [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) e [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/)
- [Commerce Optimizer](../../optimizer/overview.md)
- [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/)
- Provisionamento de autoatendimento com o [Commerce Cloud Manager](../getting-started.md#create-an-instance)

### A jornada de migração

Uma migração passa pelas seguintes fases:

- **Avaliar** - Analise a implementação existente e considere o seguinte: personalizações de inventário, integrações, características de vitrine e estruturas de dados. Depois de analisar, crie um roteiro com recomendações de migração, pontuação de complexidade e estimativas de esforço.
- **Modernizar o aplicativo e migrar dados** - Recriar personalizações como [!DNL App Builder] aplicativos ao migrar dados comerciais para o [!DNL Adobe Commerce as a Cloud Service].
- **Modernizar a loja** - Recriar a loja no Edge Delivery Services (EDS) para Commerce.
- **Sobrepor e operar** - Alternar o tráfego para [!DNL Adobe Commerce as a Cloud Service], desativar sistemas herdados e fazer a transição para uma operação em andamento.

A migração geralmente é iterativa, não linear. As empresas podem avaliar vários ambientes, validar recomendações, modernizar de forma incremental e refinar planos de implementação antes da transferência final da produção.

### Fluxo de trabalho das ferramentas de migração

Cada um dos workflows a seguir tem sua própria ferramenta. Use-os juntos para concluir sua migração com a avaliação de migração, que serve como o blueprint comum usado durante a migração.

| Fluxo de trabalho (WRK) | Ferramenta | Descrição |
| --- | --- | --- |
| [Avaliação](#migration-assessment-tool) | **Ferramenta de Avaliação de Migração** | Avaliação orientada por IA da implementação existente que faz o inventário de módulos personalizados, extensões de terceiros, integrações, observações de vitrine, esquema do banco de dados, tabelas personalizadas, recomendações de migração, pontuação de complexidade e estimativas do esforço de modernização. |
| [Modernização de aplicativos e vitrines](#code-and-storefront-migration-commerce-developer-mcp) | **MCP de Desenvolvedor do Commerce** | Modernização do aplicativo Commerce assistida por IA, acelerando a migração de personalizações para o [!DNL App Builder], oferecendo suporte à transformação de vitrine para o Edge Delivery Services (EDS) e orientando desenvolvedores por meio da jornada mais ampla de modernização de aplicativos com implementação revisada e validada pelas equipes de engenharia. |
| [Migração de dados](#data-migration-commerce-data-migration-service) | **Serviço de Migração de Dados do Commerce** | Verificação de extração, carregamento e integridade de dados de catálogo, cliente e pedido no [!DNL Adobe Commerce as a Cloud Service]. |

Estas faixas não são independentes. Usá-los juntos na ordem correta minimiza o retrabalho.

- **Executar a avaliação primeiro** - Executar a avaliação primeiro identifica personalizações sem suporte, estima o esforço de migração, expõe as considerações de migração de dados e destaca as dependências de integração antes de iniciar a implementação. A avaliação torna-se o blueprint de migração usado pela modernização de aplicativos e fluxos de trabalho de migração de dados.
- **Modernização de aplicativos** - O Commerce Developer MCP usa a avaliação de migração para determinar quais personalizações devem ser modernizadas e como. Em seguida, o MCP gera os aplicativos [!DNL App Builder] e componentes de vitrine correspondentes.
- **Migração de dados** - O questionário de escopo da migração de dados captura o escopo, os volumes e as tabelas personalizadas que foram exibidos pela avaliação.
- **Dados personalizados e de terceiros** - Os dados mantidos em tabelas personalizadas por extensões de terceiros são identificados durante a avaliação, mas não são tratados pela migração de dados padrão e exigem uma personalização de [!DNL App Builder].

A modernização do Storefront não é apenas uma migração da interface do usuário. Além de migrar a funcionalidade comercial, você precisa considerar a arquitetura de experiência, a modernização de componentes reutilizáveis, a otimização do desempenho e a adoção de padrões do Edge Delivery Services.

As integrações são avaliadas como parte da avaliação de migração, mas sua implementação varia dependendo do cenário. As integrações podem aproveitar as APIs do [!DNL App Builder], [!DNL API Mesh], Adobe I/O Events e [!DNL Adobe Commerce as a Cloud Service].

Essas ferramentas de migração continuam a expandir e manter um fluxo de trabalho de migração unificado centrado na avaliação da migração.

### Próximas etapas

Quando estiver pronto para migrar, comece criando uma avaliação. A avaliação da migração estabelece o plano após o restante da migração.

A Ferramenta de avaliação de migração e o Commerce Developer MCP usam IA para auxiliar na descoberta, planejamento e implementação. Assim como em qualquer fluxo de trabalho de engenharia, as recomendações e implementações geradas por IA devem ser cuidadosamente revisadas e validadas pela sua equipe como parte dos processos padrão de arquitetura, teste e controle de qualidade.

## Ferramenta de avaliação de migração

Antes de iniciar o desenvolvimento ou a migração, você deve considerar o tamanho da migração e determinar os itens que exigem desenvolvimento. Um armazenamento [!DNL Adobe Commerce] no [!DNL Adobe Commerce on Cloud] ou no local provavelmente tem módulos personalizados, integrações, personalizações de vitrine e estruturas de dados, o que pode não ser óbvio até que alguém analise a implementação. A Ferramenta de avaliação de migração verifica automaticamente sua base de código para identificar esses itens para desenvolvimento.

### Visão geral da avaliação

A Ferramenta de Avaliação da Migração realiza uma avaliação de IA da implementação existente e produz uma avaliação de modernização estruturada e um roteiro de migração do [!DNL Adobe Commerce as a Cloud Service]. Ele também cria uma visão abrangente da migração avaliando personalizações de aplicativos, integrações, estruturas de dados, características da loja e outros detalhes de implementação que influenciam a modernização. Ele transforma a detecção em um processo rápido e repetível que permite avaliar o esforço, o risco e o sequenciamento antes de assumir compromissos.

A avaliação que a Ferramenta de Avaliação da Migração produz não é apenas um relatório. A avaliação se torna um artefato de migração compartilhado que informa o planejamento, a implementação e a validação em todo o ciclo de vida da migração. Como a primeira fase da jornada de migração, suas conclusões abrangem os esforços de modernização de aplicativos e migração de dados que se seguem.

Para obter mais informações sobre o que está incluído em um relatório de avaliação de migração e como usá-lo, consulte [Avaliação de Migração](./assessment.md).

### Etapas de avaliação

Uma avaliação é executada em relação à implementação existente e prossegue por uma série de etapas automatizadas:

- **Inventário** — Cataloga a implementação. Inclui: módulos personalizados, dependências do Composer, extensões de terceiros, configuração, componentes de vitrine (quando aplicável), arquivos, pontos de extensibilidade, eventos, plug-ins, APIs, trabalhos cron, filas, esquema de banco de dados e tabelas de banco de dados personalizadas.
- **Analisar** — Executa uma análise estática para identificar personalizações de repositório, divergências de uma instalação padrão do [!DNL Adobe Commerce] e como essas personalizações interagem no aplicativo.
- **Classificar** — Usa a IA para interpretar cada personalização, resumindo o que ela faz, agrupando recursos relacionados, identificando padrões de implementação e fornecendo recomendações de migração contextual.
- **Mapear e recomendar** — Mapeia cada recurso para seu equivalente [!DNL Adobe Commerce as a Cloud Service], incluindo: recursos padrão, aplicativos [!DNL App Builder] ou serviços da Adobe. Em seguida, a avaliação recomenda um caminho de modernização e avalia a complexidade, as dependências e o esforço de implementação.
- **Relatório** — produz um roteiro exportável para o planejamento da execução da migração, que permite comunicar os riscos às partes interessadas. Também identifica prioridades, dependências, dívida técnica e riscos de implementação.

### Valor de avaliação

O valor de uma avaliação é a quantidade de confiança que você pode ter antes de se comprometer com as especificidades do desenvolvimento. Em vez de estimar uma migração com práticas regulares de definição do escopo, a avaliação fornece uma compreensão da implementação baseada em evidências. Isso inclui quais personalizações são simples de migrar, quais exigem um novo design e quais podem ser completamente removidas. As avaliações rotineiramente revelam funcionalidades obsoletas ou não utilizadas, permitindo que você reduza débitos técnicos.

Cada recomendação inclui evidências de suporte, juntamente com citações de volta à implementação subjacente, o que permite que arquitetos e engenheiros validem durante o planejamento. Como cada avaliação segue a mesma metodologia, é possível comparar várias necessidades de desenvolvimento usando uma estrutura de pontuação e planejamento consistente.

A avaliação não é apenas um ponto de partida. A ferramenta de migração downstream usa os resultados da avaliação para acelerar a implementação e manter a consistência com o plano de migração aprovado. A análise de personalização torna-se o blueprint para a modernização de aplicativos, enquanto a avaliação de dados define o escopo do esforço de migração de dados analisando o tamanho do banco de dados, o inventário de entidades e as tabelas personalizadas.

### Escopo da avaliação

A Ferramenta de avaliação da migração se concentra em entender todo o cenário de migração. Ele analisa módulos personalizados, plug-ins, eventos, APIs, tarefas cron, filas, integrações com sistemas externos, características da loja e o esquema do banco de dados do qual essas personalizações dependem. A avaliação mapeia o que descobre para os recursos [!DNL Adobe Commerce as a Cloud Service] disponíveis e identifica onde a funcionalidade deve ser modernizada usando o [!DNL App Builder] ou reprojetada para a arquitetura SaaS.

A avaliação é mais uma ferramenta de planejamento do que de execução. Ele identifica o que deve ser modernizado, estima a complexidade da implementação e fornece recomendações. As decisões de implementação e a validação da arquitetura permanecem como atividades de colaboração entre a Adobe, os parceiros e as equipes de engenharia do cliente.

Os dados armazenados em tabelas personalizadas por extensões de terceiros são exibidos como uma consideração de migração. A migração de dados padrão não migra esses dados automaticamente. Aplicativos [!DNL App Builder] personalizados podem ser necessários para dar suporte a esses cenários. Consulte o [guia de Migração de Dados](#data-migration-commerce-data-migration-service) para obter mais informações.

A avaliação oferece análise à personalização da loja e aos workflows de migração de dados:

- Migração de código e vitrine — a análise de aplicativos da avaliação torna-se o blueprint do Commerce Developer MCP
- Migração de dados - O inventário de entidades, a análise de características do banco de dados e a análise de tabela personalizada da avaliação estabelecem o escopo do serviço de migração de dados da Commerce.

Também é possível executar novamente as avaliações à medida que seus aplicativos evoluem. Isso permite que suas equipes validem o trabalho de correção, avaliem o progresso da modernização e refine continuamente os planos de migração durante todo o contrato.

### Próximas etapas

Cada migração do [!DNL Adobe Commerce as a Cloud Service] deve começar com uma avaliação. É uma maneira econômica de estabelecer escopo, reduzir incertezas e criar um blueprint de migração compartilhado antes do início da implementação.

Para obter mais informações sobre ferramentas de avaliação e fluxo de trabalho de desenvolvedor downstream, consulte [Adobe Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/).

## Migração de código e vitrine (Commerce Developer MCP)

No [!DNL Adobe Commerce on Cloud] ou no local, as personalizações podem usar PHP em andamento — módulos, plug-ins e observadores de eventos executados dentro do aplicativo. [!DNL Adobe Commerce as a Cloud Service] é uma plataforma SaaS sem versão e esse modelo não se aplica mais. As personalizações são executadas como aplicativos [!DNL Adobe Developer App Builder] fora de processo que se integram ao Commerce por meio de eventos e APIs. Modernizar as personalizações de um armazenamento para essa arquitetura normalmente é o esforço de engenharia mais significativo em uma migração do [!DNL Adobe Commerce as a Cloud Service].

### Visão geral da migração de código

Começando pela avaliação de migração, o Commerce Developer MCP fornece uma experiência conversacional do IDE para a modernização de personalizações herdadas do PHP em aplicativos [!DNL App Builder]. Também fornece assistência para a reconstrução de vitrines no Edge Delivery Services (EDS). Ao consumir diretamente as descobertas da Ferramenta de avaliação de migração, o Commerce Developer MCP mantém a implementação alinhada ao roteiro de migração aprovado, reduzindo a interpretação manual, mantendo a rastreabilidade e garantindo a consistência em todo o processo.

Embora a migração seja o principal caso de uso, o Commerce Developer MCP foi projetado como um agente de desenvolvimento de IA abrangente para [!DNL Adobe Commerce]. O MCP oferece suporte a modernização, novos desenvolvimentos, fluxos de trabalho operacionais e todas as atualizações do [!DNL Adobe Commerce as a Cloud Service]. Esse nível de flexibilidade permite que as equipes continuem criando e estendendo aplicativos Commerce muito tempo após a migração.

### Commerce Developer MCP

Usando os resultados da [avaliação de migração](#migration-assessment-tool), o Commerce Developer MCP transforma as personalizações identificadas em aplicativos [!DNL App Builder] por meio de um fluxo de trabalho de desenvolvimento iterativo. Considere as diretrizes a seguir ao desenvolver usando essas ferramentas:

- **Comece com o blueprint** - O Commerce Developer MCP consome a avaliação de migração, usando suas personalizações, recomendações e prioridades de migração identificadas como base para o planejamento de implementação.

- **Planejar cada personalização** - Para cada personalização, o Commerce Developer MCP desenvolve uma especificação que descreve a arquitetura [!DNL Adobe Commerce as a Cloud Service] recomendada, os padrões de integração necessários e qualquer redesign necessário para transição para um aplicativo fora do processo.

- **Criar de forma colaborativa** - Em vez de gerar código inicialmente, o Commerce Developer MCP auxilia você durante todo o ciclo de vida do desenvolvimento, planejando implementações, discutindo arquitetura, gerando e refinando código, validando padrões recomendados e fornecendo orientação para a implantação. Os desenvolvedores podem refinar iterativamente as implementações geradas por meio da linguagem natural, permitindo que os detalhes do projeto evoluam de forma colaborativa durante todo o esforço de modernização.

  - As implementações geradas são projetadas para acelerar a entrega e, ao mesmo tempo, permanecer totalmente revisáveis, testáveis e extensíveis pelas equipes de engenharia.

- **Integrar e implantar** - O Commerce Developer MCP conecta aplicativos ao Commerce por meio dos padrões de integração apropriados, auxilia nos fluxos de trabalho de implantação e valida implementações em relação aos padrões de arquitetura recomendados antes da implantação, o que melhora a consistência e reduz o esforço duplicado.

  - O Commerce Developer MCP contém o MCP [!DNL Adobe Commerce App Builder], que fornece conhecimento de domínio, padrões de implementação, orientação arquitetônica, conhecimento contextual do produto e práticas de codificação validadas diretamente no fluxo de trabalho de desenvolvimento. Isso garante que as recomendações do MCP permaneçam alinhadas às práticas recomendadas da Adobe, independentemente de os desenvolvedores trabalharem diretamente com o MCP do desenvolvedor do Commerce ou em combinação com outros agentes, como Claude, Cursor ou Copilot.

### Modernização de vitrine eletrônica

No front-end, o MCP do Commerce Developer moderniza [vitrines](https://experienceleague.adobe.com/developer/commerce/storefront/) no Edge Delivery Services (EDS) para Commerce usando a placa-padrão do Adobe Commerce, os Componentes de Entrega e os blocos de EDS.

O Commerce Developer MCP carrega projetos de vitrine existentes com base na matriz do Commerce. Ele moderniza sua loja ao:

- Geração de blocos EDS responsivos
- Geração de dados de página com reconhecimento de Commerce (página inicial, PLP, PDP, carrinho, check-out, conta)
- Composição e extensão de componentes suspensos
- Tradução de designs para implementações de EDS
- Conversão de vitrines monolíticas herdadas em uma arquitetura de blocos EDS combinável

O MCP também auxilia com:

- Modernização de componentes
- Composição em bloco reutilizável
- Otimização de experiência
- Alinhamento com as práticas recomendadas atuais do Edge Delivery Services

### Valor MCP do desenvolvedor

Mover de personalizações do PHP em andamento para aplicativos [!DNL App Builder] de composição representa uma mudança significativa na arquitetura. O Commerce Developer MCP fecha essa lacuna, incorporando o conhecimento do [!DNL Adobe Commerce], os padrões de implementação do [!DNL App Builder] e as práticas recomendadas do produto diretamente no fluxo de trabalho de desenvolvimento.

A inclusão desse contexto melhora a consistência na velocidade de entrega e na qualidade da engenharia. As equipes podem modernizar os aplicativos mais rapidamente e, ao mesmo tempo, produzir implementações que seguem uma orientação de arquitetura consistente.

Ao incorporar padrões de implementação recomendados, o Commerce Developer MCP reduz a dependência de especialistas individuais e ajuda as organizações a dimensionar os esforços de modernização de forma consistente em todos os projetos.

O processo de migração é também uma oportunidade para melhorar a implementação existente. As equipes podem simplificar as personalizações herdadas, desativar funcionalidades obsoletas, adotar recursos SaaS e modernizar a arquitetura do aplicativo em vez de carregar dívidas técnicas históricas.

Como o Commerce Developer MCP consome a avaliação de migração diretamente, todo esforço de modernização mantém a rastreabilidade até a avaliação original, garantindo que a implementação permaneça alinhada ao roteiro de migração aprovado.

O Commerce Developer MCP também promove o design de aplicativos combináveis, incentivando aplicativos [!DNL App Builder] modulares que podem evoluir independentemente, à medida que as necessidades dos negócios mudam.

### Escopo do MCP de desenvolvedor

No back-end, o Commerce Developer MCP moderniza a camada de personalização e integração, transformando módulos PHP, plug-ins e observadores de eventos em aplicativos [!DNL App Builder] e estabelece padrões de integração para conectá-los ao Adobe Commerce. Também acelera o desenvolvimento em check-out, pagamentos e na interface do administrador.

No front-end, o MCP do desenvolvedor do Commerce [moderniza as vitrines do Commerce](#storefront-modernization) no Edge Delivery Services.

O MCP não lida com a migração de dados. Os dados corporativos são migrados por meio do [Serviço de Migração de Dados da Commerce](#data-migration-commerce-data-migration-service). O MCP dá suporte aos aplicativos [!DNL App Builder] necessários quando a lógica de negócios ou as tabelas personalizadas exigem a modernização dos aplicativos.

### Próximas etapas

A modernização do código e da loja começa assim que o roteiro da Ferramenta de avaliação de migração estabelece o escopo e as prioridades da migração.

Para obter mais informações sobre como instalar e usar o MCP, consulte a documentação do [Commerce Developer MCP](https://developer.adobe.com/commerce/extensibility/developer-agent/).

## Migração de dados (Serviço de migração de dados da Commerce)

A migração para o [!DNL Adobe Commerce as a Cloud Service] pode exigir a migração de anos de dados, incluindo: catálogos, pedidos, clientes e configuração.

O Serviço de migração de dados da Commerce substitui uma migração manual por um processo único, repetível e automatizado. Isso torna as migrações complexas de bancos de dados mais previsíveis e eficientes.

### Serviço de migração de dados da Commerce

Uma migração usa um fluxo de trabalho guiado, orientado por uma ferramenta de linha de comando Docker (`./bin/console migration`). Um integrador de sistemas ou operador executa esse fluxo de trabalho no armazenamento de origem.

A migração de dados principais é automatizada, mas a maioria das migrações envolve esquemas, extensões e casos de borda não padrão, razão pela qual todas as migrações começam com uma [avaliação](#migration-assessment-tool) do armazenamento de origem. Após validar as credenciais e a conectividade, registrar a migração e estabelecer uma linha de base de verificação, você pode prosseguir com a migração de dados.

A ferramenta de serviço de migração executa as seguintes etapas de gerenciamento de dados:

1. **Extrair e transformar** — Extrai todos os dados relevantes da origem em paralelo e os remodela para [!DNL Adobe Commerce as a Cloud Service]. Os dados incompatíveis são filtrados e os atributos personalizados e outras estruturas são remapeados.
1. **Carregar** — Transfere os dados extraídos para o Serviço de Migração de Dados do Commerce. O serviço carrega os dados no [!DNL Adobe Commerce as a Cloud Service], recompila os índices e assimila o catálogo.
1. **Verificar** — Compara os dados de origem e de destino no nível do banco de dados. Em seguida, o serviço valida uma amostra de registros em tempo real por meio do GraphQL da loja e das APIs REST do administrador para verificar os dados.
1. **Relatório** — Consolida os resultados de cada etapa em um relatório de migração final.

Esses estágios de movimentação de dados exigem uma janela de manutenção, mas durante a fase de preparação, o armazenamento permanece operacional, mantendo o tempo de inatividade em um mínimo.

### Valor do serviço de migração

O serviço de migração de dados da Commerce preserva a integridade dos dados usando evidências. Cada migração é verificada por meio da comparação dos dados de origem e de destino e da validação de uma amostra de registros em tempo real por meio das APIs. Dados que não são mapeados corretamente para [!DNL Adobe Commerce as a Cloud Service], como atributos personalizados, são filtrados e remapeados automaticamente durante a extração.

O serviço de migração foi projetado para bancos de dados corporativos. A migração de dados é particionada e processada de forma assíncrona, permitindo a migração confiável de catálogos grandes e históricos de pedidos extensos. Várias migrações podem ser executadas em paralelo à medida que o pipeline cresce. Se uma migração for interrompida, ela será retomada da última etapa concluída e as tarefas interrompidas serão detectadas e repetidas automaticamente.

O tempo de inatividade é minimizado das seguintes maneiras:

- A maior parte do trabalho é realizado enquanto a loja permanece ativa, o que significa que apenas o cutover final requer uma janela de manutenção.
- A migração de dados usa leituras e gravações diretas de SQL altamente eficientes e ignora tabelas e registros que não precisam ser migrados.

Como as migrações envolvem a movimentação de dados de produção pela infraestrutura do Adobe, todo o caminho está protegido:

- Todos os uploads são verificados em busca de malware antes de atingir o destino
- A camada de entrada valida tipos de arquivos e bloqueia operações inseguras do banco de dados
- Cada solicitação é autenticada usando o Adobe IMS e a verificação de assinatura de gateway

O serviço de migração de dados da Commerce está ativo na produção mundial e já realizou várias migrações de nível corporativo.

### Dados personalizados e de terceiros

O serviço de migração oferece suporte somente aos dados principais de comércio primários. O serviço de migração não lida com entidades personalizadas de terceiros.

Os dados de terceiros podem ser migrados de acordo com cada caso, o que requer uma personalização correspondente da ferramenta de extração do Docker. Após a criação de ferramentas personalizadas, os dados podem ser extraídos da origem e gravados no [!DNL App Builder] ou no banco de dados de terceiros.

Como cada extensão modela seus dados de forma diferente, um caminho de migração para dados de terceiros só pode ser projetado após determinar o esquema e os locais do armazenamento de origem e de destino. As migrações de dados de terceiros devem ser identificadas antecipadamente para fornecer tempo para definição do escopo.

### Próximas etapas

Quando estiver pronto para migrar, conclua o [questionário de escopo da migração de dados](../assets/data-migration-scoping-questionnaire.xlsx), que requer a topologia de origem, o escopo da entidade, os volumes, as restrições de conformidade, a mecânica de transferência e as [tabelas personalizadas](#custom-and-third-party-data) necessárias para planejar a migração. A conclusão deste questionário permite que a Adobe avalie seu ambiente e planeje uma janela de migração.

Revise a documentação do [Guia da Ferramenta de Migração de Dados em Massa](bulk-data/migration-tool.md) para saber mais sobre o fluxo de trabalho, os dados com suporte e a verificação.

Os integradores de sistemas que preparam um ambiente de origem também podem usar a [CLI da Adobe Commerce Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) padrão e a [Adobe Developer Console](https://developer.adobe.com) para credenciais IMS.
