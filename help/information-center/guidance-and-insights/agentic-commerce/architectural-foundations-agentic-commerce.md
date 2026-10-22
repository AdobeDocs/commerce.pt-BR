---
title: Projetar uma plataforma Commerce para compradores e agentes de IA
description: Saiba como criar uma plataforma de comércio que sirva compradores humanos e agentes de IA de uma única fonte de verdade, desde o design de catálogos e o MCP até a telemetria.
role: Developer, Leader
recommendations: noCatalog
autotag-review: '2026-10-20T20:32:40.424Z'
TQID: 'https://experienceleague.adobe.com/ub4oTxr4IfLGgqqz0S1npY-sn0FZb3mKq-GdjD9eDjI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
    internal-label: Data quality
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%
---

# Criar uma plataforma de comércio para compradores e agentes de IA

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Retrato de Surya Lamech" src="../../assets/guidance-and-insights/agentic-commerce-author-avatar-slamech.png" width="96"><br><strong>Surya Lamech</strong><br><em>Gerente Principal de Marketing do Produto</em></td>
</tr>
</table>

![Ilustração de exemplo de uma plataforma de comércio agênico na qual os agentes de IA e humanos interagem com uma única fonte de verdade](../../assets/guidance-and-insights/agentic-commerce-hero.png "Os fundamentos arquitetônicos de uma plataforma de comércio agênico")

*Criando uma plataforma comercial onde os agentes de IA e humanos interagem com uma única fonte de verdade.*

O Commerce está passando por uma mudança estrutural. Os clientes não dependem mais apenas de mecanismos de pesquisa ou de frentes de loja de navegação para explorar suas opções. Em vez disso, eles estão se voltando para interfaces alimentadas por LLM, assistentes baseados em bate-papo e ferramentas de compras agenciais para fazer perguntas, comparar produtos entre varejistas e acelerar a tomada de decisões no estágio inicial.

Essas interfaces são mecanismos eficientes para detecção, treinamento e comparação. Eles ajudam os clientes a esclarecer necessidades, avaliar compensações e restringir opções mais rapidamente do que a navegação tradicional.

No entanto, quando chega a hora de concluir uma compra, os clientes ainda preferem predominantemente lojas confiáveis e sites de propriedade da marca, onde a segurança de pagamento, a transparência de atendimento e o serviço pós-compra são bem compreendidos. A conversão permanece ancorada em ambientes em que a confiança já foi estabelecida.

É importante notar que a IA não desaparece nesta fase. Quando os clientes chegam à loja de uma marca, a IA corporativa pode aprimorar a experiência guiando a seleção do produto, personalizando as recomendações em tempo real, respondendo às objeções, agrupando itens complementares e simplificando a finalização da compra. Nesses ambientes confiáveis, a IA se torna um acelerador de conversão, melhorando as taxas de conclusão e aumentando o valor médio de pedido.

Para competir nesse novo cenário, as empresas precisam de uma base comercial **estruturada, controlada e otimizada para o consumo humano e de agentes**. A Adobe Commerce foi criada para essa mudança, e os princípios abaixo descrevem o que é necessário para estar realmente pronto para o agente.

## Uma arquitetura comercial criada para dois públicos-alvo

![Diagrama mostrando vitrines e aplicativos para humanos à esquerda e assistentes de chat e agentes autônomos à direita, ambos desenhando a partir de um Commerce Core central de produtos, preços, inventário, promoções, carrinho e check-out que é exposto por meio de APIs e MCP](../../assets/guidance-and-insights/agentic-commerce-foundational-model.png){width="800" zoomable="yes"}

*O que os clientes veem e o que os agentes consomem permanecem consistentes, precisos e sob a marca.*

A pilha de comércio moderna deve agora atender a dois públicos igualmente importantes: pessoas e agentes de IA. Experiências voltadas para o ser humano, como vitrines e aplicativos, continuam sendo essenciais para o engajamento, a expressão da marca e a construção da fidelidade do cliente. Mas ao lado deles há uma superfície voltada para o agente em rápida expansão: terminais legíveis por máquina que fornecem LLMs e agentes autônomos com fatos estruturados, conteúdo governado e recursos transacionais.

Os agentes têm melhor desempenho ao trabalhar com dados limpos e estruturados fornecidos por APIs previsíveis, em vez de tentar interpretar o JavaScript ou inferir regras de negócios a partir de camadas de apresentação. Isso significa que as especificações do produto, os preços, a disponibilidade e a lógica promocional devem existir como recursos endereçáveis expostos por meio de APIs e interfaces padronizadas, como servidores MCP. Quando as superfícies voltadas para humanos e agentes são provenientes da mesma fonte subjacente de verdade, as marcas garantem que o que os clientes veem e o que os agentes consomem permaneçam consistentes, precisos e na marca.

Essa arquitetura de superfície dupla é a base do comércio agêntico.

## Um catálogo projetado para raciocínio de máquina

![Diagrama que mostra entidades de produto estruturadas (SKUs, atributos, variantes, pacotes, preços e disponibilidade) moldadas por camadas e políticas de catálogo e, em seguida, entregues por meio de exibições de catálogo a uma loja de marcas, marketplace, feed de parceiros, aplicativo móvel e IA ou superfície de agente](../../assets/guidance-and-insights/agentic-commerce-agent-interaction.png){width="800" zoomable="yes"}

*Uma fonte controlada da verdade, formada por canal sem nunca bifurcar os dados do produto.*

O catálogo é o núcleo do comércio agênico. Ele deve ser estruturado para máquinas, orientado para conformidade e flexível o suficiente para suportar toda a gama de interações humanas e de agentes. O modelo de catálogo da Adobe Commerce criado com base em exibições de catálogo, políticas, camadas e entidades de produto estruturadas foi projetado para esse futuro.

As exibições de catálogo definem onde e como os dados do produto são expostos, seja para uma vitrine, um marketplace, um feed de parceiro ou uma superfície de IA. Cada visualização pode ter suas próprias regras de disponibilidade de produto, preço e visibilidade de atributo, garantindo que as informações certas cheguem ao consumidor ou agente certo. As camadas de catálogo permitem enriquecer os dados do produto para canais específicos sem modificar os dados do produto de origem. As políticas controlam a qualificação do cliente, a lógica do inventário, os preços e as restrições de conformidade. Combinadas, as empresas têm controle preciso sobre quais dados de catálogo um agente pode acessar ou agir.

## Os MCPs são a linguagem comum para agentes

![Diagrama que mostra os assistentes de compras, os agentes de suporte e as ferramentas de desenvolvedor enviando solicitações por meio do Protocolo de Contexto de Modelo, que inclui o MCP do Commerce e o MCP do desenvolvedor, para recursos da Adobe Commerce, como criação de carrinho, check-out, pagamentos, inventário e promoções e devoluções](../../assets/guidance-and-insights/agentic-commerce-reference-stack.png){width="800" zoomable="yes"}

*O MCP padroniza como os agentes solicitam ações na intenção natural, e o Adobe Commerce as executa como ações determinísticas controladas.*

Para que o Commerce Agentic funcione de ponta a ponta, as plataformas de comércio eletrônico devem suportar protocolos padronizados que permitam aos agentes executar ações com segurança, como criação de carrinho, início de finalização, orquestração de pagamentos, validação de inventário, promoções e devoluções.

Por meio do suporte nativo para o protocolo de contexto de modelo (MCP), o Adobe estrutura e expõe os recursos de comércio de uma maneira que os LLMs podem interpretar de forma consistente. O MCP padroniza como os dados do produto, as regras de negócios e o contexto transacional são apresentados aos LLMs, garantindo que os agentes possam argumentar sobre eles de forma confiável, enquanto as empresas mantêm o controle e o controle. Com o Commerce MCP, as empresas podem criar experiências agênticas personalizadas, como assistentes de compras, criação de carrinho de agente, agentes de suporte e muito mais.

O MCP para desenvolvedores traz recursos de desenvolvimento alimentados por IA que permitem que as equipes estendam rapidamente a funcionalidade da plataforma e implantem componentes de vitrine combináveis. Ao incorporar as fontes de conhecimento, a documentação e as práticas recomendadas da plataforma da Adobe diretamente no fluxo de trabalho de desenvolvimento, o MCP do desenvolvedor ajuda novos desenvolvedores a se integrarem mais rapidamente e a se tornarem produtivos desde o primeiro início. Ele gera código que segue padrões comprovados de arquitetura, é fácil de manter e atende aos padrões de qualidade exigidos pelo comércio corporativo. O resultado é um caminho acelerado da ideia à produção, dando às empresas a velocidade para experimentar, iterar e enviar recursos de comércio à frente dos concorrentes.

A Adobe também está comprometida com o suporte a protocolos de comércio agênico, como o ACP (Agentic Commerce Protocol) e o UCP (Universal Commerce Protocol), permitindo a descoberta de produtos e interações transacionais seguras baseadas em padrões entre agentes e sua loja.

Ao adotar protocolos abertos em vez de integrações pontuais, o Adobe garante que as interações comerciais sejam controladas, determinísticas e seguras e, ao mesmo tempo, permite um novo modelo de envolvimento agente-comerciante, no qual agentes confiáveis podem realizar transações diretamente de acordo com políticas claramente definidas.

## Telemetria e otimização contínua

Em um ecossistema mediado por IA, a telemetria se torna a vantagem estratégica. As empresas precisam de visibilidade sobre como sua marca é representada nos LLMs, como os agentes representam seu conteúdo com precisão, como o tráfego indicado pelo agente é convertido e onde surgem problemas de governança ou conformidade. Eles também precisam de telemetria operacional que acompanhe a execução do agente e a detecção de anomalias em interações do agente.

O Adobe oferece visibilidade sobre como seus produtos aparecem em LLMs, aprimora os dados do produto com IA e aumenta a legibilidade dos dados pelo LMS. Ao adicionar contexto significativo ao catálogo, os LLMs não apenas detectam seus produtos com precisão, mas também entendem o que são, para quem são e por que são importantes para os clientes.

Além disso, as páginas de detalhes do seu produto que foram otimizadas para consumo humano geralmente podem ter dados invisíveis para os agentes. Esses dados podem estar ocultos por trás de modais, configuradores e páginas vinculadas. Os agentes podem não entender totalmente as categorias, os pacotes e as variantes do produto. A Adobe pode identificar essas informações críticas ausentes e implantá-las como JSON-LD na borda, para que os agentes possam obter todos os dados relevantes do produto.

Através desta telemetria constante e otimização marcas podem garantir a máxima visibilidade e manter-se competitivas em todos LLMs.

## Por que isso é importante

O comércio eletrônico não está mais restrito a vitrines e resultados de pesquisa. Os LLMs e os agentes autônomos cada vez mais mediam a descoberta, a avaliação e as transações. Essa mudança muda a mecânica da visibilidade, a dinâmica do controle e os fundamentos da confiança. As marcas vencedoras arquitetarão uma base nativa em IA.

## Orientação relacionada

* [Exibições de catálogo](/help/optimizer/setup/catalog-view.md)
* [Camadas do catálogo](/help/optimizer/setup/catalog-layer.md)
* [Políticas](/help/optimizer/setup/policies.md)
* [Ferramentas de desenvolvedor de codificação de IA para o Adobe Commerce App Builder](/help/cloud-service/migration/coding-tools.md)
* [APIs do Commerce](../../apis/commerce-apis.md)
* [Lista de reprodução do Commerce Developer Agent](https://experienceleague.adobe.com/en/playlists/commerce-developer-agent)—Assista a vídeos técnicos sobre como configurar e usar o Commerce Developer Agent.
