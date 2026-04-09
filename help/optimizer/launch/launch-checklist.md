---
title: Lista de verificação do Launch
description: Saiba como validar a configuração, a vitrine, o SEO, a CDN, as integrações, a segurança, a análise e os testes para a produção do  [!DNL Adobe Commerce Optimizer] .
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# Lista de verificação de inicialização

Use esta lista de verificação para verificar se o projeto de produção [!DNL Adobe Commerce Optimizer] está configurado, testado e pronto para ser iniciado. Trabalhe cada seção com sua equipe e rastreie a conclusão em seu próprio plano de projeto ou rastreador. Para obter os recursos do produto e as áreas de interface do usuário mencionadas abaixo, consulte a [[!DNL Adobe Commerce Optimizer] documentação](../overview.md).

## Caso de uso e arquitetura {#use-case}

Use esta lista de verificação ao fornecer uma experiência B2C que combina o [!DNL Adobe Commerce Optimizer] e o Edge Delivery Services (EDS) com uma instância existente do Adobe Commerce na nuvem.

A solução geralmente inclui estes componentes:

- **Nuvem** — O Adobe Commerce na Nuvem gerencia dados de catálogo, clientes, ativos e fluxos de compra (check-out, gerenciamento de pedidos, envio etc.).
- O **Otimizer**—[!DNL Adobe Commerce Optimizer] fornece experiências de merchandising.
- **Storefront** — A Adobe Commerce Storefront no Edge Delivery Services fornece a interface do usuário.
- **Serviços de terceiros**—Pagamento, remessa e provedores de impostos.
- **App Builder**—Extensibilidade.
- **Malha de API**—Solicitar roteamento.

## Verificar o Adobe Commerce na nuvem {#verify-cloud}

Confirme se o ambiente do Adobe Commerce na nuvem está pronto para produção.

▢ A instância da nuvem está [provisionada](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project).
▢ Os dados de teste e fictícios foram removidos da instância.
▢ Dados de produção carregados na instância.
▢ Você conhece o [ponto de extremidade do GraphQL](https://developer.adobe.com/commerce/webapi/graphql/).
▢ A instância atende aos requisitos de [pronto para inicialização](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist).

## Verificar instância do Commerce Optimizer {#verify-optimizer}

Confirme se a instância de produção [!DNL Adobe Commerce Optimizer] está configurada corretamente.

▢ A instância de produção está ativa. Consulte [Introdução](../get-started.md) para saber como provisioná-lo.
▢ A instância está na região correta.
▢ O tipo de ambiente é Produção.
▢ Você sabe a ID da organização, a ID do cliente, a URL de assimilação e a URL da Commerce Optimizer. Consulte [Introdução](../get-started.md).
▢ Os limites e limites configurados correspondem aos valores confirmados pelo Adobe Customer Technical Advisor (CTA).
▢ Os artefatos de teste e os dados fictícios foram removidos da instância.

## Verificar site da loja {#verify-storefront-site}

Confirme se o site da loja do Edge Delivery Services existe e se o acesso é restrito.

▢ O site da loja existe. Consulte [Criar uma vitrine](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/).
▢ Você sabe o nome do site.
▢ Somente pessoas autorizadas têm [permissão para publicar](https://tools.aem.live/tools/user-admin/index.html).
▢ Somente pessoas autorizadas têm [permissão para criar](https://docs.da.live/administrators/guides/permissions).

## Verificar a integração da Cloud e do Otimizer {#cloud-optimizer-integration}

Confirme se o Adobe Commerce na nuvem e o [!DNL Adobe Commerce Optimizer] trocam dados corretamente.

### No Adobe Commerce

Conclua essas verificações no projeto na nuvem.

▢ O conector do Commerce Optimizer está [instalado e configurado](../../aco-connector/get-started.md).
▢ O comando da CLI `aco:conf:show` confirma a conexão com a instância do Commerce Optimizer de produção. A ID da organização, a ID do cliente, o URL de assimilação e o URL da Commerce Optimizer correspondem à produção.
▢ Os escopos de sincronização na [Configuração de exportação](../../aco-connector/get-started.md) correspondem aos seus requisitos.
▢ [Status de sincronização do feed de dados](../../aco-connector/get-started.md) confirma a exportação de dados da instância da nuvem.

### No Commerce Optimizer

Conclua essas verificações na interface do usuário do [!DNL Adobe Commerce Optimizer].

▢ O [painel de sincronização de dados](../setup/data-sync.md) mostra os dados recebidos. Produtos, preços e atributos são exibidos para o Serviço de catálogo, Descoberta de produtos e Recomendações.
▢ [Catálogos de preços](../setup/pricebooks.md) são criados automaticamente a partir de grupos de clientes na Nuvem.
▢ [Exibições de catálogo](../setup/catalog-view.md) existem e você conhece suas IDs.
▢ [Políticas](../setup/policies.md) existem e você conhece suas IDs.
▢ [Facetas](../merchandising/facets/overview.md) estão configuradas.
▢ [Sinônimos](../merchandising/synonyms/overview.md) estão configurados.
▢ [Regras de merchandising](../merchandising/rules/overview.md) estão configuradas.
▢ [Preço facetado e idioma de pesquisa](../settings.md) correspondem às suas necessidades quando você usa esses recursos.
▢ [Recomendações de produto](../merchandising/recommendations/create.md) existem e se comportam conforme esperado na visualização.
▢ [Pesquisar dados de desempenho](../manage-results/search-performance.md) aparece no *Administrador*.
▢ [Dados de desempenho do Recommendations](../manage-results/recommendation-performance.md) aparecem no *Administrador*.

## Verificar a integração da loja e da nuvem {#storefront-cloud-integration}

Confirme se a loja lê a partir do endpoint correto do Adobe Commerce GraphQL.

### No Adobe Commerce

▢ Pacotes de compatibilidade da Storefront estão [instalados](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).

### Na loja

▢ A configuração `commerce-core-endpoint` da vitrine aponta para o seu [ponto de extremidade do Cloud GraphQL](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
▢ Se você usar a API Mesh como proxy para o Cloud GraphQL, `commerce-core-endpoint` apontará para o ponto de extremidade da API Mesh em vez do ponto de extremidade do Cloud GraphQL.

## Verificar a integração da loja e do Otimizer {#storefront-optimizer-integration}

Confirme as configurações do Commerce Optimizer na configuração da loja.

▢ Sua loja usa as [configurações corretas do Commerce Optimizer](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
▢ `adobe-commerce-optimizer` é `true`.
▢ `commerce-endpoint` aponta para o ponto de extremidade de produção do Commerce Optimizer GraphQL ou para o ponto de extremidade da API Mesh ao usar a API Mesh.
▢ `headers.cs.AC-view-ID` contém a ID de exibição do catálogo da instância do Commerce Optimizer de produção.

## Verificar serviços de terceiros na nuvem {#third-party-services}

Confirme as integrações que são executadas em seu sistema de comércio de host (não em [!DNL Adobe Commerce Optimizer]).

▢ **Pagamentos:** O gateway de pagamento está ativo e foi testado (Stripe, PayPal, Adyen, etc.).
▢ **Envio:** as conexões da API de envio funcionam (UPS, FedEx e assim por diante).
▢ **Remessa:** A plataforma de preenchimento está conectada e testada (por exemplo, ShipStation).
▢ **Imposto:** A integração do cálculo de impostos está validada (Avalara, TaxJar, etc.).
▢ **Imposto:** A sincronização do software de contabilidade funciona (QuickBooks e assim por diante).
▢ **Inventário:** PIM, ERP ou integração de gerenciamento de inventário testada e sincronizada.
▢ **Arquitetura:** o sistema de comércio host controla o pagamento, a remessa, os impostos e o inventário (não [!DNL Adobe Commerce Optimizer]).
▢ **Arquitetura:** API Mesh e App Builder permanecem em sincronia entre o sistema de comércio host e o [!DNL Adobe Commerce Optimizer].
▢ **Email:** A entrega de emails transacionais funciona (confirmação de pedidos, envio e assim por diante).
▢ **Email:** Os modelos de email correspondem à sua marca e usam links corretos.

## Verificar o App Builder e a API Mesh {#app-builder-mesh}

Confirme a configuração de extensibilidade para produção.

### App Builder

▢ O espaço de trabalho de produção inclui todas as configurações e serviços necessários.
▢ O aplicativo de produção passa no teste em cenários de compilação.
▢ Os limites e limites do produto foram revisados e confirmados com base na [descrição do produto Adobe Developer App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} e nas [configurações e limitações do sistema App Builder](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
▢ O aplicativo de produção usa pontos de extremidade de produção do App Builder.
▢ extensões personalizadas do painel *Admin* são implantadas no espaço de trabalho de produção.

### API Mesh

▢ Configurações e origens estão prontas para produção.

### Eventos

▢ Adobe I/O Events estão configurados e as assinaturas estão verificadas.

## Finalizar experiência da loja {#finalize-storefront}

Comportamento de conteúdo polonês, SEO, desempenho, segurança e CDN antes do lançamento.

### Conteúdo e criação

Confirme o fluxo de trabalho de criação e os componentes da loja.

▢ A revisão da [lista de verificação de ativação do AEM/EDS](https://www.aem.live/docs/go-live-checklist) foi concluída.
▢ A origem de criação é baseada em documento ou Editor Universal (e configurada).
▢ O conteúdo é publicado usando o ciclo visualizar → publicar.
▢ Controle de qualidade de conteúdo e design concluído no domínio `.aem.live`.
▢ Um favicon está configurado e é distribuído corretamente pelo site.
▢ da.live e os visuais de produto usam [credenciais dedicadas ](https://docs.da.live/administrators/guides/permissions) configuradas.
▢ Os drop-ins (carrinho, check-out, PDP, PLP, autenticação, conta) foram [personalizados](../storefront.md) e testados.
A marca da Loja ▢ reflete os tokens de design CSS, tipografia e cores.

### SEO e indexação

Confirme metadados, URLs e comportamento do rastreo.

▢ Metadados de título de documento estão presentes para páginas principais (especialmente PDPs e PLPs). Consulte [metadados de SEO](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} na documentação da _Adobe Commerce Storefront_.
▢ PDPs incluem [metadados e dados estruturados](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (por exemplo, JSON-LD).
Os formatos de URL do produto ▢ são consistentes (por exemplo, `domain/product-name`).
▢ URLs personalizadas redirecionam para URLs canônicas.
▢ O projeto inclui `robots.txt` que permite a indexação onde apropriado, faz referência a mapas de site e bloqueia caminhos que você não deseja indexar (por exemplo, `/drafts`).
▢ [Redirecionar](https://www.aem.live/docs/redirects) arquivos abrangem as alterações de URL da migração (por exemplo, após a remoção de `.html`).
O Mapa do site ▢ existe e é enviado ao Console de Pesquisa da Google conforme necessário.
▢ URLs canônicas retornam o status `2xx` (não `3xx` ou `4xx`).
▢ Sites multilíngues incluem `hreflang` marcas no mapa de site.
▢ O relatório de cobertura do Console de Pesquisa da Google está atualizado.

### Pré-renderização

Confirme a renderização do lado do servidor onde você a ativa.

▢ A pré-renderização está ativada para páginas principais. Consulte [Pré-renderização do AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} na documentação da _Adobe Commerce Storefront_.
As URLs ▢ usam minúsculas, portanto, a pré-renderização não quebra links.
▢ A origem do HTML inclui metadados e conteúdo de corpo que confirmam que a pré-renderização funciona.
As Localidades ▢ mostram as páginas traduzidas corretas onde aplicável.
▢ A marcação de HTML adicional está [configurada](https://www.aem.live/docs/redirects) conforme necessário.

### Desempenho e monitoramento

Confirme as linhas de base de desempenho e a fiação de análise.

▢ Sua loja segue as [práticas recomendadas de desempenho](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} na documentação da _Adobe Commerce Storefront_.
▢ (Opcional) O Google Analytics e o Google Tag Manager estão configurados.
A implementação do ▢ [Eventos da vitrine](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) é válida e os dados aparecem nos painéis do [!DNL Live Search] e do [!DNL Product Recommendations] no *Administrador* do Adobe Commerce.
▢ O parâmetro de análise `environment` na [configuração do Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} é `"Testing"` durante o desenvolvimento e `"Production"` na ativação. Consulte [Instrumentação do Analytics](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}.
▢ As pontuações do Lighthouse atendem às suas metas (por exemplo, `100` em páginas-chave), dadas as orientações sobre este tópico.

### Segurança e acesso

Confirme permissões e segredos.

▢ Permissões apropriadas estão configuradas para conteúdo do DA e sites do EDS. Consulte [Permissões do DA.live](https://da.live/docs/administration/permissions) e [Configuração de autenticação para criação](https://www.aem.live/docs/authentication-setup-authoring).
▢ A integração dos visuais de produto foi provisionada. Consulte [Visão geral sobre acesso ao AEM Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
▢ Os links para redefinição de senha em modelos de email correspondem à configuração do Edge Delivery Services. Consulte as Perguntas frequentes da loja: [O que devo fazer se meus links de modelo de email forem desfeitos após migrar para o Edge Delivery Services ou Helix?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
▢ As chaves de produção para integrações e provedores de pagamento estão em vigor.
▢ Domínios são resolvidos e webhooks de back-end funcionam.

### CDN e armazenamento em cache

Confirme o comportamento da CDN, DNS e cache.

▢ A configuração da CDN usa o ponto de extremidade de produção do GraphQL (`yourproject.com/graphql`) para extensões e scripts do Sidekick (por exemplo, geração de mapa de site e o importador de imagem).
▢ Quando você usa o Adobe Commerce Fastly, um token de limpeza CDN está disponível e a [configuração do site](https://tools.aem.live/tools/cdn-setup/index.html) inclui `authToken` e `serviceId`.
A ▢ [configuração de CDN](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} valida o armazenamento em cache e a invalidação.
▢ Para [configurações de vários armazenamentos](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}, as solicitações do Serviço de Catálogo e do [!DNL Live Search] incluem um buster de cache específico do armazenamento (por exemplo, um parâmetro de consulta ou uma regra CDN).
▢ A invalidação por push funciona de ponta a ponta (publique uma alteração e, em seguida, verifique no domínio de produção).
O TTL DNS ▢ é baixo o suficiente antes da transferência.
▢ registros DNS A e CNAME estão corretos para todos os domínios e nomes de host.
▢ O certificado SSL/TLS é provisionado e verificado para o domínio de produção.
▢ `www` e redirecionamentos de apex se comportam corretamente.

## Segurança e conformidade {#security-compliance}

Confirme a postura de segurança e as tarefas de conformidade.

▢ **SSL:** um certificado SSL/TLS confiável está instalado.
▢ **SSL:** HTTPS é imposto em todo o site.
▢ **Acesso:** As senhas padrão de *Administrador* foram alteradas e uma política de senha forte está em vigor. Consulte [!DNL Adobe Commerce Optimizer] [Gerenciamento de usuários e identidades](../user-management.md).
▢ **Acesso:** A URL do *Administrador* não é a padrão.
▢ **Acesso:** A autenticação de dois fatores está habilitada para todos os usuários *Administrador*.
▢ **Acesso:** nenhum usuário administrador inativo ou não utilizado está associado ao projeto.
▢ **Firewall:** O WAF (Firewall de Aplicativo Web) está configurado e verificado.
▢ **PCI:** O teste de inserção de segurança na produção (escopo PCI) foi concluído.
▢ **Verificação:** A Ferramenta de Verificação de Segurança do Adobe está registrada e uma verificação inicial está concluída.
▢ **Acesso:** o CORS permite somente origens aprovadas.
▢ **Conformidade:** O [modelo de responsabilidade compartilhada](../shared-responsibility.md) para [!DNL Adobe Commerce Optimizer] está atualizado e define claramente a Adobe em relação às responsabilidades do cliente.
▢ **Conformidade:** Os requisitos de política de privacidade, consentimento de cookie e GDPR ou CCPA foram verificados.

## Analytics e monitoramento {#analytics-monitoring}

Confirme a medição e as linhas de base.

▢ **RUM:** O RUM (Monitoramento de Usuário Real) é instrumentado para comparação antes e depois.
▢ **Analytics:** a coleta de dados do Adobe Experience Platform está configurada (se aplicável).
▢ **Analytics:** verificado se as marcas MarTech são acionadas no nome de host de produção.
▢ **Analytics:** as análises de linha de base estão documentadas; flutuações pós-lançamento (exibições de página, taxa de rejeição, etc.) são esperadas.
▢ **Eventos:** O rastreamento de conversão funciona de ponta a ponta (adicionar ao carrinho → check-out → confirmação).

## Testes {#testing}

Confirme a qualidade antes e depois do lançamento.

▢ **Funcional:** Os fluxos principais funcionam de ponta a ponta: navegar → pesquisar → filtrar → adicionar ao carrinho → check-out → criação de conta.
▢ **Funcional:** gateways de pagamento aceitam transações reais e de teste.
▢ **Funcional:** trabalho de posicionamento de pedidos, email de confirmação e rastreamento de pedidos.
▢ **Funcional:** as opções de envio e os cálculos de impostos estão precisos.
▢ **Funcional:** cupons, descontos e programas de fidelidade se comportam conforme esperado.
▢ **UAT:** O teste de aceitação de usuário foi concluído no preparo e na produção.
▢ **Desempenho:** os testes de carga e tensão foram concluídos e o Adobe CTA ou CSE tem os resultados.
▢ **Desempenho:** o tempo de carregamento da página é de menos de três segundos na área de trabalho e em dispositivos móveis.
▢ **Desempenho:** as pontuações do Lighthouse atendem aos destinos em páginas-chave (por exemplo, através do PageSpeed Insights).
▢ **Desempenho:** imagens, scripts e ativos estão otimizados.
▢ **Compatibilidade:** Chrome, Firefox, Safari e Edge se comportam conforme esperado.
▢ **Compatibilidade:** layouts responsivos funcionam em dispositivos móveis, tablets e área de trabalho.
▢ **Compatibilidade:** o desempenho é aceitável em 3G, 4G e Wi-Fi.
▢ **Acessibilidade:** uma auditoria de acessibilidade foi concluída (WCAG, leitor de tela, navegação pelo teclado).
▢ **Funcional:** um plano de monitoramento 404 pós-lançamento está em vigor.
▢ **UAT:** Existe um plano de reversão que passa no teste se ocorrerem problemas na inicialização.

## Dia de lançamento e pós-lançamento {#launch-post-launch}

Confirme as tarefas de comunicação, suporte e acompanhamento.

▢ **Coordenação do lançamento:** o Adobe tem sua data de lançamento confirmada; a CTA foi notificada por email.
▢ **Suporte:** O número de linha direta P1 foi registrado: US (+1) 800-497-0335, em seguida, pressione 6 para Commerce.
▢ **Suporte:** sua equipe foi treinada para abrir um tíquete de suporte **antes** de ligar para a linha direta P1.
▢ **Pós-lançamento:** verifique as pontuações do Lighthouse no domínio de produção.
▢ **Pós-inicialização:** Monitore o Google Search Console para erros de indexação e rastrea.
▢ **Pós-inicialização:** Monitore relatórios 404 e adicione redirecionamentos para URLs herdadas de alto tráfego.
▢ **Pós-lançamento:** Confirme os dados de MarTech e de análise na produção.
▢ **Pós-lançamento:** Peça à sua CTA, CSE ou AM para habilitar o monitoramento de alto nível do SLA.
▢ Existe um plano de recuperação de desastres que passa no teste.
▢ Um processo está em vigor para rastrear e atualizar pacotes padronizados e de extensão para as versões atuais.
