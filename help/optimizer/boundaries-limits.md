---
title: Limites e limites
description: Compreender [!DNL Adobe Commerce Optimizer] limites e limites para planejar a capacidade e evitar problemas de desempenho.
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 4f238b002d1481126d4fec0a249b7f9ff437248e
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Limites e limites

[!DNL Adobe Commerce Optimizer] tem dois tipos de limites:

- **Limites de licença**—Com base na sua capacidade adquirida; pode ser expandido adquirindo pacotes adicionais.
- **Limites do sistema**—Limites fixos que protegem os recursos do sistema e garantem desempenho confiável para todos os usuários.

Sua utilização deve permanecer dentro desses limites. Excedê-los pode causar maior latência e limitação de solicitação.

## Solicitar capacidade adicional

Os limites de licença podem ser aumentados adquirindo os pacotes de licença descritos na seção [Limites de licença e limites do sistema](#license-limits-and-system-boundaries) ou negociando o licenciamento personalizado para casos de uso exclusivos. Entre em contato com seu representante de conta da Adobe para discutir suas necessidades.

Em caso de dúvidas sobre os limites do sistema, contate o [Suporte da Adobe](https://experienceleague.adobe.com/home?lang=pt-BR#support).

## Evitar problemas de desempenho

Siga estas práticas recomendadas para ficar dentro dos limites e evitar problemas operacionais:

- **Revise seus limites**—Entenda seus [limites de capacidade](#license-limits-and-system-boundaries) antes de iniciar novas vitrines ou campanhas.
- **Rastrear seu uso**—Use painéis de métricas internos ou logs de CDN.

## Limites da licença e limites do sistema

As tabelas a seguir resumem os limites de licença e os limites do sistema por área de recurso e incluem informações sobre a adição de mais licenças para expandir a capacidade, quando aplicável.

### Limites de ambiente

| **Ambiente** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| **Ambiente de sandbox** | O número de ambientes de sandbox incluídos | 2 por instância | Sim<p>Adicionar uma licença de ambiente adicional por instância</p> |
| **Ambiente de produção** | O número de ambientes de produção incluídos | 1 por instância | Licença<p>Adicionar uma licença de ambiente adicional por instância</p> |

{style="table-layout:auto"}

### Catálogo

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Taxa de assimilação do produto | A quantidade de produtos criados ou atualizados | 1K atualizações por minuto<p>No máximo 100 mil atualizações por dia</p> | Sim<p>Adicionar um pacote de licenças:</p><ul><li>5 mil atualizações por minuto<br>No máximo 500 mil atualizações por dia</li> <li>10.000 atualizações por minuto<br>No máximo 1 milhão de atualizações por dia</li></ul><p>A capacidade máxima para assimilação de dados é de 1 milhão de atualizações por dia.</p> |
| Tamanho do conteúdo do produto | A quantidade máxima de dados permitida ao criar, atualizar ou assimilar informações do produto usando a API | 200 KB | Não |
| Variações do catálogo | O número de visualizações de um catálogo que estão disponíveis para os usuários da loja,<p>que são contados como (*Número de Exibições do Catálogo × Número de Catálogos de Preços*)</p> | 100 variações | Sim<p>Adicionar pacote de licenças de 100 variações de catálogo</p> |
| Produtos em uma única origem de catálogo | SKUs compatíveis no catálogo | 250 mil SKUs | Sim<p>Adicionar pacote de licença do 100K SKU</p> |
| Variantes por produto | O número de variantes de produtos (tamanho, combinações de cores) permitidas por produto | 10 K | Não |
| Origens do catálogo | O número de contextos de dados de catálogo (por exemplo, localidades ou fontes de dados como PIMs e ERPs) | 50 | Não |

{style="table-layout:auto"}

### Catálogos de preços

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Catálogos de preços | O número de catálogos de preços permitidos por instância | Com base no número de [Variações de catálogo](#catalog) | Sim<br>Aumentar variações de catálogo |
| Descontos por registro de preço | O número de descontos que podem ser aplicados a um preço de produto em um único catálogo de preços | 10 | Não |

{style="table-layout:auto"}

### Visualizações de produto viabilizadas pelo AEM Assets

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Visuais de produto Usuários avançados | Usuário licenciado com recursos completos de gerenciamento de ativos digitais, incluindo ferramentas de IA, integrações Adobe Express/Firefly e compartilhamento da Content Hub, lidando com as principais tarefas do DAM e recursos avançados nativos em nuvem para obter eficiência ideal. | 2 | Sim<p>Atualizar para a licença do AEM Assets</p> |
| Usuários do Product Visuals Collaborator | Acesse e trabalhe com ativos por meio da integração do AEM Commerce, crie e edite conteúdo usando o Adobe Express e o Firefly e, se ativado, aproveite os ativos aprovados por meio do portal do Content Hub. | 2 | Sim<p>Atualizar para a licença do AEM Assets</p> |
| Armazenamento de dados Visuals do produto | Espaço de armazenamento alocado para ativos | Armazenamento de 1 TB | Não |
| Uso do Dynamic Media | Tolerância para operações de processamento de mídia dinâmica que inclui:<ul><li>Entrega de imagem</li><li>Imagem inteligente</li><li>Entrega de vídeo</li></ul><p>Para obter detalhes, consulte *Calcular uso do Dynamic Media* abaixo. | Baseado em GMV<p>Alocação mínima: 5 milhões de operações/mês</p> | Sim<ul><li>Licença de compra para operações adicionais</li><li>Atualizar para a licença do AEM Assets</li></ul> |
| Entrega de vídeo | Subsídio para entrega ou download de vídeo | 300 vídeos, 1 minuto por vídeo | Sim<p>Atualizar para a licença do AEM Assets</p> |
| Geração de ativos | Acesso à IA gerativa do Adobe Express e do Adobe Firefly para criação de imagens | Nenhum | Adquirir créditos de IA geradores separadamente |

{style="table-layout:auto"}


>[!NOTE]
>
>**Usuários Avançados** podem acessar o Adobe Express diretamente ou no Adobe Commerce Optimizer. **Usuários do Collaborator** podem acessar o aplicativo Adobe Express diretamente. O uso é regido pelos [Termos de Licenciamento Específicos do Produto do Adobe Express Firefly](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


>[!BEGINSHADEBOX &quot;Calcular uso do Dynamic Media&quot;]

O uso do Dynamic Media rastreia as solicitações de API que entram nos componentes Visuais do produto no Adobe Commerce Optimizer para facilitar uma das seguintes ações:

- **A entrega de imagem consome uma operação de mídia dinâmica** para cada ocorrência do seguinte:
   - **transformação básica de imagem** de um ativo digital, por exemplo, redimensionamento, escala, conversão de formato, compactação ou operações de recorte.
   - **entrega ou download de imagens estáticas** dos referidos ativos digitais ou representação de ativos digitais (além de vídeo)
- **A entrega de imagens inteligentes consome 20 operações do Dynamic Media** para cada entrega otimizada de um único ativo digital, gerando automaticamente a representação de imagem mais apropriada para o dispositivo e o navegador de um usuário final.
- **A entrega de vídeo consome 20 Operações do Dynamic Media** para uma única entrega ou download de um vídeo, ou para uma variante transformada de um vídeo.

>[!ENDSHADEBOX]


### Exibições e políticas do catálogo

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Exibições de catálogo | Número de subconjuntos configuráveis do catálogo principal | Com base no número de [Variações de catálogo](#catalog) | Sim<br>Aumentar variações de catálogo |
| Políticas por exibição de catálogo | Número de filtros de dados permitidos | 10 | Não |
| Valores de atributo em uma política | Número de características do produto que podem ser configuradas para filtragem | 100 | Não |

{style="table-layout:auto"}

### Loja do catálogo

A alocação básica dos recursos de vitrine de catálogos é determinada com base na camada GMV. A tabela indica a alocação mínima para cada recurso.

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Taxa de recuperação do catálogo | Número de vezes por mês que uma API de catálogo é chamada por um sistema (vitrine, sistema de transações, ERP ou outro) para recuperar dados do catálogo | Com base no nível de GMV<p>Alocação mínima: 10 milhões/mês</p> | Sim<p>Adicionar 1 milhão de solicitações por mês a pacotes de licenças</p> |
| Solicitações de conteúdo | Solicitações à Commerce Storefront para exibições de página do HTML ou chamadas de API JSON. Contado como 1 exibição de página ou 5 chamadas de API. | Com base no nível de GMV<p>Alocação mínima: 2 milhões/mês</p> | Sim<p>Adicionar um pacote de licença mensal</p> |
| Variações da GenAI da loja | Permissão para a geração de conteúdo baseado em texto | Com base no nível de GMV<p>Alocação mínima: 1 mil variações por mês</p> | Sim<p>Adquirir créditos de IA geradores separadamente</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>A geração de imagem exige uma licença do Adobe Firefly provisionada para a mesma organização IMS que o Adobe Commerce Optimizer.


### Descoberta de produto

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Produtos por solicitação de pesquisa | O número máximo de produtos retornados por página nos resultados da pesquisa | 100 | Não |
| Atributos filtráveis | O número de características do produto (como cor, tamanho, marca ou material) que podem ser ativadas para a navegação em camadas e aspectos | 200 | Não |
| Atributos pesquisáveis | O número de características do produto que podem ser configuradas para uso com o serviço de pesquisa do catálogo de produtos | 200 | Não |
| Atributos classificáveis | O número de características do produto que podem ser configuradas para determinar a ordem dos valores de resultado de pesquisa | 50 | Não |
| Profundidade da paginação de pesquisa | O número máximo de produtos acessíveis por paginação (por exemplo, página 100 × 100 produtos/página) | 10 K | Não |
| Facetas | O número de atributos de produto filtráveis (como Marca, Cor, Tamanho, Preço) que podem ser configurados para ajudar os compradores a refinar os resultados da pesquisa e procurar categorias | 100<p>Deve ser um atributo filtrável</p> | Não |
| Opções por faceta | O número de valores de atributos de produto filtráveis (como &quot;Vermelho&quot;, &quot;Azul&quot; para Cor; &quot;Pequeno&quot;, &quot;Medium&quot; para Tamanho) que os compradores podem selecionar em uma lista | 100 | Sim<p>Pode aumentar por meio de solicitação de suporte</p> |

{style="table-layout:auto"}

### Recommendations

Os recursos a seguir estão disponíveis para recomendações de produtos. Alguns recursos disponíveis em outros produtos da Adobe Commerce não têm suporte no [!DNL Adobe Commerce Optimizer].

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Unidades de recomendação ativas | Número de componentes de recomendação ativos na sua loja (como &quot;Clientes também visualizados&quot; ou &quot;Você também pode gostar&quot;) | 50 | Não |
| Inclusões/exclusões de categoria ou atributo | Filtrar produtos para um conjunto específico que esteja qualificado para recomendações | Não suportado | |

{style="table-layout:auto"}

### Extensibilidade

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** | **Notas** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacidade para criar extensões e integrações nativas em nuvem | Com base no nível de GMV<p>Alocação mínima: 1 pacote/ano</p> | Sim<p>Adicionar pacotes adicionais</p> | Para obter os limites definidos por pacote, consulte:<ul><li>[Descrição de produto do App Builder](https://helpx.adobe.com/br/legal/product-descriptions/adobe-developer-app-builder.html) para limites definidos por pacote.</li><li>[Limitações e configurações do sistema](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) nos *Guias do App Builder Runtime*.</li><li>[Requisitos de armazenamento do App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each) -->
