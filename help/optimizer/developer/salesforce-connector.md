---
title: Salesforce Commerce Connector
description: Saiba mais sobre o [!DNL Commerce Optimizer SFCC Connector] que fornece um ponto de partida para a integração do Salesforce Commerce B2C com o [!DNL Adobe Commerce Optimizer] para sincronizar dados de catálogo e implementar e personalizar o conector para oferecer suporte a operações comerciais.
role: Admin, Developer
source-git-commit: f3da99ec4d2c518748d0911d6cf5d2d89ab45a47
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Salesforce Commerce Connector for Adobe Commerce Optimizer

Baseado na tecnologia App Builder da Adobe, o [!DNL Commerce Optimizer Salesforce Commerce Connector] permite a transferência e o gerenciamento ininterruptos de dados de catálogo do Salesforce Commerce Cloud B2C para o [!DNL Adobe Commerce Optimizer]. Ele conecta ambas as plataformas, mantendo as informações, os preços e as atualizações do produto em sincronia, sem necessidade de uma nova plataforma.

Pronto para uso, o conector oferece recursos confiáveis de sincronização de dados e a flexibilidade para personalizar workflows de acordo com as necessidades da sua empresa.

## Principais recursos

* **Sincronização de dados do catálogo:** envie dados do produto (incluindo variantes, tabelas de preços e estruturas) do Salesforce Commerce B2C para o Adobe Commerce Optimizer para manter as vitrines e os aplicativos orientados por experiência atualizados.
* **Sincronização de Preço:** importe e gerencie dados de preço diretamente do Salesforce Commerce B2C.
* **Suporta vários tipos de dados:** Sincronize produtos, preços e estruturas de catálogo para refletir configurações complexas de merchandising.

* **Fluxos de Trabalho de Sincronização Flexíveis**
   * **Sincronizações Agendadas:** Automatize atualizações usando o agendamento de trabalhos cron; não é necessário nenhum esforço manual.
   * **Atualizações sob Demanda:** acione instantaneamente atualizações no nível de SKU para alterações, correções ou inicializações de produtos urgentes.

* **Compilado para Extensibilidade**
   * Usa pontos de extremidade personalizados [Salesforce Commerce B2C API](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html) (SCAPI) para compatibilidade e fácil adaptação a casos de uso exclusivos ou avançados.
   * Dimensionável de acordo com seus negócios - comece com a sincronização de catálogos e preços e, em seguida, estenda os fluxos de trabalho para oferecer suporte a integrações adicionais ou lógica de negócios.
   * Configurar e evoluir workflows sem reconstruir as integrações principais.

>[!NOTE]
>
>O conector é projetado especificamente para o Salesforce Commerce Cloud B2C. Ele não é compatível com os produtos B2B ou D2C da Salesforce, que são criados em diferentes pilhas de tecnologia.

## Quem se beneficia com o Salesforce Connector?

O [!DNL Salesforce Commerce Connector] é ideal para:

* **Clientes B2C atuais do Salesforce Commerce Cloud** aprimorando os recursos de vitrine
* **Organizações multimarcas** que exigem recursos avançados de merchandising e personalização em várias lojas
* **Empresas que buscam melhorias de desempenho** através do Edge Delivery Services da Adobe para obter experiências de vitrine mais rápidas
* **Empresas com estruturas de preços complexas** sincronizando catálogos de preços sofisticados e preços locais específicos
* **Clientes do AEM** gerenciando catálogos de produtos do Salesforce Commerce B2C ao usar a loja da Adobe Commerce com o Edge Delivery Services
* **Varejistas com requisitos de várias localidades** sincronizando informações de produtos localizadas em mercados e idiomas

## Casos de uso

O conector é compatível com vários casos de uso importantes:

### Assimilação de dados do catálogo e exibição da loja

Este caso de uso principal demonstra o fluxo de dados completo do Salesforce Commerce B2C para a loja da Adobe Commerce:

1. **Assimilação inicial do catálogo:** carregue em massa todo o catálogo de comércio da Salesforce, incluindo produtos simples com variantes, catálogos de preços e informações de preços.
1. **Atualizações delta automatizadas:** sincronize automaticamente as atualizações de produtos da interface do Salesforce Commerce Catalog Management para [!DNL Commerce Optimizer].
1. **Integração com a loja:** Exiba dados de catálogo sincronizados na sua loja do Adobe Commerce Edge Delivery Service usando as [!DNL Commerce Optimizer] APIs da loja.
1. **Atualizações em tempo real** Veja as informações atualizadas do produto (nomes, preços, descrições) imediatamente na sua loja depois de fazer alterações no Salesforce.

### Gerenciamento de produtos em várias localidades

Aproveite os recursos de localização do Salesforce Commerce B2C:

* Sincronizar versões localizadas de campos de texto de produto (nomes, descrições) do Salesforce Commerce B2C para locais diferentes.
* Mapeie os conceitos de localidade do Salesforce 1:1 com [!DNL Commerce Optimizer] localidades.
* Suporte a vários ciclos de assimilação de produtos para locais diferentes.
* Mantenha a consistência entre catálogos de produtos globais.

## Arquitetura e componentes

O [!DNL SFCC Connector] fornece uma camada de integração robusta entre uma instância B2C do Salesforce Commerce e [!DNL Commerce Optimizer]. O conector opera por meio de uma série de ações de sincronização que transferem dados de catálogo, catálogos de preços e informações do produto.

1. **Extração de Dados** — Autentique com a instância B2C do Salesforce Commerce e extraia dados do catálogo usando APIs SCAPI personalizadas.
1. **Transformação de Dados** — Transforme dados de produto para corresponder ao modelo de dados e aos requisitos de esquema do [!DNL Commerce Optimizer].
1. **Assimilação de dados**—Transmita com segurança os dados transformados para [!DNL Commerce Optimizer] usando o SDK ACO TypeScript.
1. **Integração com a Loja**—Os dados sincronizados ficam disponíveis através das APIs [!DNL Commerce Optimizer] para experiências com a loja.

O diagrama a seguir ilustra o fluxo de dados de alto nível da integração:

![Arquitetura do Salesforce Commerce Connector](../assets/sfcc_starter_kit.png){zoomable="yes"}

### Componentes-chave

O [!DNL Commerce Optimizer SFCC Connector] consiste em vários componentes principais:

* **Aplicativo App Builder do Starter Kit SFCC do ACO** - Fornece funções sem servidor que lidam com a sincronização de dados entre o SFCC e o Adobe Commerce Optimizer.
* **Cartucho SFCC personalizado** - Cartucho necessário que estende a instância do Salesforce Commerce Cloud com as APIs necessárias para a extração de dados.
* **Interface do usuário de Gerenciamento** - Interface da Web para monitorar o status de sincronização e gerenciar operações do conector.


### Processo de sincronização

O conector é compatível com vários modos de sincronização.

| Modo de sincronização | Descrição |
|-----------|-------------|
| **Sincronização de Site Completa** | Executa uma sincronização abrangente de todos os produtos, catálogos de preços e preços para o site e localidades do Salesforce Commerce Cloud configurados. Isso inclui <ul><li>metadados e atributos do produto</li><li>estrutura e categorias do catálogo</li><li>catálogos de preços</li><li>informações sobre preços</li><li>dados de produtos com várias localidades</li></ul> |
| **Sincronização Delta** | Recupera e sincroniza apenas as alterações feitas em produtos Salesforce e dados de preço desde a última sincronização, garantindo atualizações eficientes e oportunas.<br>A sincronização delta é executada automaticamente de acordo com um agendamento (padrão: a cada hora) para manter a atualização dos dados. |
| **Opções de Sincronização Direcionadas** | Fornece recursos de sincronização granular: <ul><li>**Sincronização do Catálogo de Preços** sincroniza somente informações do catálogo de preços</li><li>A **Sincronização de Metadados** atualiza os metadados do produto e as definições de atributo</li><li>A **Sincronização de Produto Específico** sincroniza produtos individuais por SKU</li></ul> |

## Considerações importantes

Ao planejar sua implementação, considere estes fatores principais:

### Mapeamento de dados e atributos

* **Atributos pesquisáveis:** o Salesforce Commerce B2C define atributos pesquisáveis por meio da interface do usuário, que a API não expõe. Use o [[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) para configurar manualmente esses atributos pesquisáveis no Adobe Commerce Optimizer.
* **Mapeamento de atributos:** planeje o mapeamento de atributos de produto B2C do Salesforce Commerce para [!DNL Commerce Optimizer] metadados com base nos requisitos da sua empresa.
* **Campos pesquisáveis padrão:** o conector torna automaticamente os atributos principais (`name`, `description`, `ID`) pesquisáveis por padrão.

### Escopo de Sincronização

* **Seleção do site:** o Salesforce Commerce B2C tem um conceito de sites aos quais os catálogos se anexam. Durante a sincronização completa, selecione o site do Salesforce a ser sincronizado.
* **Gerenciamento de localidade:** cada localidade do Salesforce Commerce resulta em um ciclo de assimilação de produto separado em [!DNL Commerce Optimizer].
* **Volume de dados:** Considere o tamanho do catálogo e a frequência de sincronização ao planejar a implementação.

## Monitoramento e gerenciamento

Depois de instalado e configurado, o [!DNL Commerce Optimizer SFCC Connector] fornece recursos abrangentes de monitoramento e gerenciamento do [!DNL SFCC to ACO Sync Panel]:

![Interface do usuário de Gerenciamento do Salesforce Commerce Connector](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

A URL para esta interface é fornecida depois de implantar o [!DNL Commerce Optimizer SFCC Connector Starter Kit] no projeto do App Builder.

Os principais recursos incluem:

* **Rastreamento do Status de Sincronização:** Monitore o status e os carimbos de data/hora de todas as operações de sincronização.
* **Validação da Conectividade:** Teste as conexões com o Salesforce Commerce Cloud e o Adobe Commerce Optimizer.
* **Validação de dados do produto:** verifique se os dados sincronizados do produto aparecem corretamente na loja.
* **Log de Erros e Solução de Problemas**: os logs de erros para solução de problemas podem ser acessados por meio da CLI do App Builder.
* **Gerenciamento de estado:** controle o progresso da sincronização e evite conflitos com o gerenciamento de estado interno.

## Código Source e recursos de desenvolvimento

O [!DNL Commerce Optimizer SFCC Connector] é de código aberto e está disponível para personalização. Os repositórios principais incluem:

* **[Kit Inicial SFCC do ACO](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** - Aplicativo e documentação do conector principal.
* **[Cartuchos SFCC de ACO](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - Cartucho SFCC necessário para integração com a API.
* **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** - SDK para integração com o Adobe Commerce Optimizer.

Esses repositórios fornecem código-fonte completo, documentação detalhada e exemplos para implementar e personalizar o conector.

## Próximas etapas

Pronto para integrar os dados do Salesforce Commerce Cloud ao Adobe Commerce Optimizer? Comece revisando o guia detalhado de implementação no [repositório do Starter Kit SFCC do ACO](https://github.com/adobe-commerce/aco-sfcc-starter-kit) e verifique se você tem os pré-requisitos necessários em vigor.
