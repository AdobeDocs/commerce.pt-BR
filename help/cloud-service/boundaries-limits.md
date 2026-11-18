---
title: Limites e limites do Adobe Commerce as a Cloud Service
description: Saiba mais sobre limites de licença e limites do sistema do Adobe Commerce as a Cloud Service. Planeje a capacidade, rastreie o uso e evite latência e limitação quando os limites forem excedidos.
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente ao Adobe Commerce as a Cloud Service e a projetos [!DNL Adobe Commerce as a Cloud Service] (infraestrutura SaaS gerenciada pela Adobe)."
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# Limites e limites

[!DNL Adobe Commerce as a Cloud Service] aplica **limites de licença** e **limites do sistema** que definem quanta capacidade o projeto pode usar:

- **Os limites de licença** são baseados na sua capacidade adquirida e podem ser expandidos com a compra de pacotes adicionais.
- **Os limites do sistema** são limites fixos que protegem os recursos do sistema e garantem um desempenho confiável para todos os usuários.

>[!IMPORTANT]
>
> Sua utilização deve permanecer dentro desses limites. Excedê-los pode causar maior latência e limitação de solicitação.

## Solicitar capacidade adicional

Você pode aumentar seus limites de licença comprando os pacotes de licença descritos em [Limites de licença e limites do sistema](#license-limits-and-system-boundaries) ou negociando licenças personalizadas para casos de uso exclusivos. Entre em contato com seu representante de conta da Adobe para discutir suas necessidades.

Em caso de dúvidas sobre os limites do sistema, contate o [Suporte da Adobe](https://experienceleague.adobe.com/home?lang=en#support).

## Evitar problemas de desempenho

Siga estas práticas recomendadas para ficar dentro dos limites e evitar problemas operacionais:

- **Revise seus limites** - Entenda seus [limites de capacidade](#license-limits-and-system-boundaries) antes de iniciar novas vitrines ou campanhas.
- **Rastrear seu uso** - Use painéis de métricas internos ou logs CDN.

## Limites da licença e limites do sistema

As tabelas a seguir resumem os limites de licença e os limites do sistema por área de recurso e incluem informações sobre o uso de licenças adicionais para expandir a capacidade, quando aplicável.

### Limites de ambiente

| **Ambiente** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| **Ambiente de sandbox** | O número de ambientes de sandbox incluídos | 2 por instância | Sim<p>Adicionar uma licença de ambiente adicional por instância</p> |
| **Ambiente de produção** | O número de ambientes de produção incluídos | 1 por instância | Sim<p>Adicionar uma licença de ambiente adicional por instância</p> |

{style="table-layout:auto"}

### Catálogo

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Taxa de assimilação do produto | A quantidade de produtos criados ou atualizados | 1K atualizações por minuto<p>No máximo 100 mil atualizações por dia</p> | Sim<p>Adicionar um pacote de licenças:</p><ul><li>5 mil atualizações por minuto<br>No máximo 500 mil atualizações por dia</li><li>10.000 atualizações por minuto<br>No máximo 1 milhão de atualizações por dia</li></ul><p>A capacidade máxima para assimilação de dados é de 1 milhão de atualizações por dia.</p> |
| Tamanho do conteúdo do produto | A quantidade máxima de dados permitida ao criar, atualizar ou assimilar informações do produto usando a API | 200 KB | Não |
| Categorias | O número de categorias em que os produtos podem ser agrupados | 6,000 | Não |
| Número de produtos | O número de SKUs com suporte no catálogo | 250 mil SKUs | Sim<p>Adicionar pacote de licença do 100K SKU</p> |
| Variantes por produto | O número de variantes de produtos (tamanho, combinações de cores) permitidas por produto | 10 K | Não |
| Visualizações da loja | O número de contextos de exibição de loja (por exemplo, localidades) | 50 | Não |
| SLA para que uma atualização de produto apareça na pesquisa | Tempo para a criação/atualização de um produto aparecer na pesquisa da loja | 10 - 15 minutos | Não |

{style="table-layout:auto"}

### Check-out

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Produtos no carrinho | O número de produtos permitidos por carrinho de compras | 650 | Não |
| Endereços de cliente por conta | O número de endereços de clientes permitidos por conta | 2,000 | Não |
| Regras de preço do carrinho | O número de regras de preço do carrinho que aplicam descontos a itens do carrinho, com base em um conjunto de condições | 100,000 | Não |
| Cupons | O número de códigos de cupom usados com regras de preço do carrinho | 1,000,000 | Não |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals] limites

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Visuais de produto Usuários avançados | Usuário licenciado com recursos completos de gerenciamento de ativos digitais, incluindo ferramentas de IA, [!DNL Adobe Express]/[!DNL Firefly] integrações e compartilhamento de Content Hub, lidando com as principais tarefas do DAM e recursos avançados nativos em nuvem para obter eficiência ideal. | 2 | Sim<p>Atualizar para a licença [!DNL AEM Assets]</p> |
| Usuários do Product Visuals Collaborator | Acesse e trabalhe com ativos por meio da integração do AEM Commerce, crie e edite conteúdo usando o [!DNL Adobe Express] e o [!DNL Firefly] e, se habilitado, aproveite os ativos aprovados por meio do portal do Content Hub. | 2 | Sim<p>Atualizar para a licença [!DNL AEM Assets]</p> |
| Armazenamento de dados Visuals do produto | Espaço de armazenamento alocado para ativos | Armazenamento de 1 TB | Não |
| Uso do Dynamic Media | Tolerância para operações de processamento de mídia dinâmica que inclui:<ul><li>Entrega de imagem</li><li>Imagem inteligente</li><li>Entrega de vídeo</li></ul><p>Para obter detalhes, consulte *Calcular uso do Dynamic Media* abaixo. | Com base na GMV (valor bruto da mercadoria)<p>Alocação mínima: 5 milhões de operações/mês</p> | Sim<ul><li>Licença de compra para operações adicionais</li><li>Atualizar para a licença [!DNL AEM Assets]</li></ul> |
| Entrega de vídeo | Subsídio para entrega ou download de vídeo | 300 vídeos, 1 minuto por vídeo | Sim<p>Atualizar para a licença [!DNL AEM Assets]</p> |
| Geração de ativos | Acesso à IA gerativa [!DNL Adobe Express] e [!DNL Adobe Firefly] para criação de imagens | Nenhum | Adquirir créditos de IA geradores separadamente |

{style="table-layout:auto"}

>[!NOTE]
>
>**Usuários Avançados** podem acessar [!DNL Adobe Express] diretamente ou no [!DNL Adobe Commerce as a Cloud Service].
>
>**Usuários do Collaborator** podem acessar o aplicativo [!DNL Adobe Express] diretamente. O uso é regido pelos [Termos de Licenciamento Específicos do Produto do Adobe Express](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).

>[!BEGINSHADEBOX &quot;Calcular uso do Dynamic Media&quot;]

O uso do Dynamic Media rastreia solicitações de API que entram nos componentes Visuais do Produto em [!DNL Adobe Commerce as a Cloud Service] para facilitar uma das seguintes ações:

- **A entrega de imagem consome uma operação de mídia dinâmica** para cada ocorrência do seguinte:
  - **transformação básica de imagem** de um ativo digital, por exemplo, redimensionamento, escala, conversão de formato, compactação ou operações de recorte.
  - **entrega ou download de imagens estáticas** dos ativos digitais ou representação de ativos digitais (além de vídeo).
- **A entrega de imagens inteligentes consome 20 operações do Dynamic Media** para cada entrega otimizada de um único ativo digital, gerando automaticamente a representação de imagem mais apropriada para o dispositivo e o navegador de um usuário final.
- **A entrega de vídeo consome 20 Operações do Dynamic Media** para uma única entrega ou download de um vídeo, ou para uma variante transformada de um vídeo.

>[!ENDSHADEBOX]

>[!NOTE]
>
>Os limites acima abrangem alocações de capacidade e uso. Para obter a visão geral dos recursos Visuais de Produto e as restrições funcionais, consulte [Visuais de Produto com o AEM Assets](../optimizer/setup/product-visuals.md).

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### Loja do catálogo

A alocação básica para os recursos de vitrine de catálogo é determinada com base no nível GMV (valor de mercadoria bruta). A tabela indica a alocação mínima para cada recurso.

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Taxa de recuperação do catálogo | Número de vezes por mês que uma API de catálogo é chamada por um sistema (vitrine, sistema de transações, ERP ou outro) para recuperar dados do catálogo | Com base no nível de GMV<p>Alocação mínima: 10 milhões/mês</p> | Sim<p>Adicionar 1 milhão de solicitações por mês a pacotes de licenças</p> |
| Solicitações de conteúdo | Solicitações à loja para exibições de página do HTML ou chamadas de API JSON. Contado como 1 exibição de página ou 5 chamadas de API. | Com base no nível de GMV<p>Alocação mínima: 2 milhões por mês</p> | Sim<p>Adicionar um pacote de licença mensal</p> |
| Variações da GenAI da loja | Permissão para a geração de conteúdo baseado em texto | Com base no nível de GMV<p>Alocação mínima: 1 mil variações por mês</p> | Sim<p>Adquirir créditos de IA geradores separadamente</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>A geração de imagem requer uma licença [!DNL Adobe Firefly] provisionada para a mesma organização IMS que [!DNL Adobe Commerce as a Cloud Service].

### Descoberta de produto

Os limites a seguir se aplicam à pesquisa de produtos da loja, à listagem e à configuração de merchandising.

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- |---------------------------------------------------|
| Recuperação de produto | Máximo de SKUs por solicitação do GraphQL [!DNL Catalog Service] ao buscar dados do produto com `products`, `productSearch`, `refineProduct` e `variants`. Dividir solicitações maiores em várias chamadas. | 100 | Não |
| Atributos filtráveis | O número de características do produto (como cor, tamanho, marca ou material) que podem ser ativadas para a navegação em camadas e aspectos | 200 | Não |
| Atributos pesquisáveis | O número de características do produto que podem ser indexadas para pesquisa no catálogo | 200 | Não |
| Atributos classificáveis | O número de características do produto disponíveis como opções de classificação em páginas de pesquisa e categoria. | 50 | Não |
| Profundidade da paginação de pesquisa | Máximo de produtos acessível por meio de paginação de pesquisa (por exemplo, página 100 × 100 produtos/página) | 10 K | Não |
| Facetas | O número de atributos de produto filtráveis (como Marca, Cor, Tamanho, Preço) que podem ser configurados para ajudar os compradores a refinar os resultados da pesquisa e procurar categorias | 100<p>Deve ser um atributo filtrável</p> | Sim<p>Pode aumentar para 500 por meio de solicitação de suporte</p> |
| Opções por faceta | O número de valores de atributo de produto filtráveis que os compradores podem selecionar em uma faceta (por exemplo, &quot;Vermelho&quot;, &quot;Azul&quot; para Cor; &quot;Pequeno&quot;, &quot;Medium&quot; para Tamanho) | 100 | Sim<p>Pode aumentar por meio de solicitação de suporte</p> |

{style="table-layout:auto"}

### Recommendations

Os recursos a seguir estão disponíveis para recomendações de produtos. Alguns recursos disponíveis em outros produtos da Adobe Commerce não têm suporte no [!DNL Adobe Commerce as a Cloud Service].

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** |
| --- | --- | --- | --- |
| Unidades de recomendação ativas | Número de componentes de recomendação ativos na sua loja (como &quot;Clientes também visualizados&quot; ou &quot;Você também pode gostar&quot;) | 50 unidades ativas por tipo de página para Recomendações de produto, com escopo explícito do modelo de catálogo, se necessário | Não |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### Extensibilidade

| **Recurso** | **Descrição** | **Alocação base** | **Expansível?** | **Notas** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacidade para criar extensões e integrações nativas em nuvem | Com base no nível de GMV<p>Alocação mínima: 1 pacote/ano</p> | Sim<p>Adicionar pacotes adicionais</p> | Para obter os limites definidos por pacote, consulte:<ul><li>[descrição do produto App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html).</li><li>[Limitações e configurações do sistema](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) nos *Guias do App Builder Runtime*.</li><li>[Requisitos de armazenamento do App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

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
   * Add-On: 10 × dynamic media packs (1M each)
-->
