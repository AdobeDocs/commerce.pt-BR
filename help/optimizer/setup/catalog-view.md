---
title: Exibição de catálogo
description: Saiba o que são exibições de catálogo e como criá-las para organizar o catálogo de produtos por estrutura de negócios, políticas e preços.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 1210
ht-degree: 0%

---

# Exibições de catálogo para serviços de merchandising

As exibições de catálogo são a base dos Serviços de Merchandising do [!DNL Adobe Commerce Optimizer], permitindo que você organize o catálogo de produtos por estrutura de negócios, políticas e preços. Esse modelo de dados flexível oferece suporte a várias marcas, unidades de negócios e cenários em vários idiomas, mantendo a eficiência operacional.

## O que são Exibições de catálogo?

As exibições de catálogo definem como o catálogo de produtos é organizado e exibido. Eles atuam como filtros que determinam:

- **Quais produtos são visíveis** com base na estrutura comercial (marcas, regiões, revendedores)
- **Que preços são mostrados** por meio de catálogos de preços vinculados
- **Como os produtos são filtrados** usando políticas (atributos como marca, modelo, categoria)
- **Que [origem do catálogo](catalog-sources.md) é usada** com base em atributos como localidade

Considere as exibições de catálogo como diferentes &quot;lentes&quot; pelas quais os clientes veem seu catálogo. Por exemplo:

- A exibição do catálogo do revendedor pode mostrar somente os produtos disponíveis para esse revendedor específico
- Uma exibição de catálogo regional pode mostrar produtos e preços específicos de uma área geográfica
- A exibição do catálogo de marcas pode mostrar apenas produtos de uma marca específica

## Criar uma exibição de catálogo

Nesta seção, você cria uma exibição de catálogo, selecione uma [política](policies.md) e um [catálogo de preços](pricebooks.md).

Antes de criar uma visualização de catálogo, verifique se você tem:

- [Políticas criadas](policies.md) para definir filtros de produto.

- [Definiu camadas de catálogo](catalog-layer.md) para definir variantes de seus produtos.

- [Catálogos de preços assimilados](pricebooks.md) para preços.

1. No menu esquerdo, vá para _Configuração da loja_ e clique em **[!UICONTROL Catalog views]**.

1. Clique em **[!UICONTROL Create catalog view]**. &#x200B;

1. Configure os detalhes de exibição do catálogo:

   - **Nome** — Digite o nome da exibição do catálogo, por exemplo `Celport`. &#x200B;
   - **Origens do catálogo** — Selecione a [origem do catálogo](catalog-sources.md), por exemplo `en-US`.
   - **Camadas do catálogo**-Revise as camadas e a prioridade assimiladas.
   - **Políticas** — use o menu suspenso para selecionar as políticas relevantes. Por exemplo, &quot;Marca&quot;, &quot;Modelo&quot;. &#x200B;Verifique se você já [criou uma política](policies.md).

1. Selecione o catálogo de preços a ser vinculado à exibição do catálogo.

   - **Usar todos os catálogos de preços disponíveis**-Essa opção extrai dados de preços de todos os catálogos de preços disponíveis.
   - **Permitir somente catálogos de preços selecionados**-Essa opção exibe a caixa de diálogo **Adicionar catálogos de preços permitidos**, onde é possível selecionar qual catálogo de preços específico usar para a exibição do catálogo.
   - **Desabilitar preço**-Esta opção não está disponível no momento.

1. Clique em **[!UICONTROL Add]** para criar a exibição de catálogo com as políticas e os catálogos de preços vinculados.

A página Exibições de catálogo é atualizada para exibir a nova exibição de catálogo.&#x200B;

Após concluir essas etapas, a exibição do catálogo agora está configurada para exibir produtos e preços com base nas fontes e políticas selecionadas.

### Especificar exibições de catálogo para recomendações e regras de descoberta de produtos

Você pode especificar uma exibição de catálogo ao [criar unidades de recomendação](../merchandising/recommendations/create.md) ou [regras de merchandising](../merchandising/rules/add.md).

## Camadas do catálogo

As camadas de catálogo permitem modificar os dados do produto em uma exibição de catálogo sem alterar os dados de origem originais. As camadas aplicam alterações a atributos específicos do produto, como nome, descrição, imagens, links e metadados, criando uma camada na parte superior do catálogo base. Os dados originais do produto permanecem intactos, permitindo personalizar produtos com segurança e reverter alterações a qualquer momento.

Casos de uso comuns para camadas de catálogo incluem:

- **Otimização de SEO**—Substitua metatítulos e descrições do produto com base nas recomendações de IA do [Sites Optimizer](../manage-results/opportunities.md)
- **Campanhas sazonais** — Atualize temporariamente nomes de produtos, descrições ou imagens para promoções
- **Personalização regional**—Exibir informações de produto diferentes com base na localização geográfica ou no idioma
- **Teste A/B**—Teste diferentes apresentações de produtos para otimizar as taxas de conversão
- **Gerenciamento de várias marcas**—Personalize atributos de produto para diferentes exibições de catálogos de marcas

Para saber mais sobre como criar, gerenciar e priorizar camadas de catálogo, consulte [Camadas de catálogo](catalog-layer.md).

## Gerenciar exibição de catálogo

Siga estas instruções para atualizar ou exibir as propriedades de exibições de catálogo existentes.

### Editar exibição de catálogo

1. No espaço de trabalho *Exibições de catálogo*, localize a exibição de catálogo na grade que você deseja editar e clique em **...** para abrir o menu de ações.
1. Clique em **Editar** para acessar o editor de exibição de catálogo.
1. Atualize o nome, as origens do catálogo, as políticas e as informações do catálogo de preços conforme necessário.
1. Salve as alterações.

### Excluir exibição de catálogo

1. No espaço de trabalho *Exibições de catálogo*, localize a exibição de catálogo na grade que você deseja editar e clique em **...** para abrir o menu de ações.
1. Clique em **Excluir**.

   Quando a caixa de diálogo de confirmação for exibida, clique em **[!UICONTROL Delete]**.

### Exibir detalhes

Esta opção fornece uma maneira rápida de ver todos os parâmetros de exibição de catálogo, permanecendo na tabela *Exibições de catálogo*.

No espaço de trabalho *Exibições de catálogo*, localize a exibição de catálogo na grade que você deseja editar e clique no ![ícone de informações](../assets/info-icon.png).

![Detalhes de exibição do catálogo](../assets/catalog-view-details.png)

Aqui, você pode ver os detalhes de configuração da visualização do catálogo, como:

- ID da Visualização
- Nome
- Origens do catálogo
- Políticas
- Data de criação
- Dados modificados

Algumas dessas configurações são necessárias à medida que você configura sua loja ou usa a API de assimilação de dados.

## Visão geral da arquitetura

As exibições de catálogo são parte da estrutura de Serviços de merchandising que substitui a estrutura de site, loja e loja usada nas bases da Adobe Commerce por um modelo mais flexível:

Arquitetura ![[!DNL Merchandising Services]](../assets/merchandising-svcs-architecture.png)

### Como funciona

**1. Assimilação de dados**
Os dados do catálogo do PIM, ERP e outros sistemas são assimilados na estrutura de serviços de merchandising. Cada SKU contém informações de local e atributos de produto que mapeiam para exibições de catálogo, políticas e locais. Para obter mais informações sobre a assimilação de dados, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/).

**2. Catálogo de base unificada**
Os dados assimilados criam um catálogo base unificado no pipeline de dados do Serviço de catálogo. Essa única fonte elimina a duplicação de dados nas unidades de negócios.

**3. Exibições do catálogo**
Várias exibições de catálogo representam unidades de negócios diferentes (por exemplo, &quot;Texas Retail&quot;, &quot;Texas Retail Seasonal&quot;). Locais, políticas e catálogos de preços podem ser compartilhados entre exibições de catálogo para maior flexibilidade.

**4. Entrega multicanal**
Os dados de catálogo filtrados são entregues para vários destinos, incluindo lojas Edge Delivery Services, marketplaces, plataformas de publicidade e microlojas personalizadas. Para obter mais informações sobre a entrega de dados do catálogo, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/).

### Componentes principais

| Componente | Finalidade | Exemplo |
|---|---|---|
| **Exibição de catálogo** | Unidade de negócios ou canal de distribuição | Rede de revendedores, Loja regional |
| **Política** | Filtro de produto com base em atributos | Marca, modelo, categoria |
| **Localidade** | Configuração de idioma/região | en-US, fr-CA, es-MX |
| **Catálogo de Preços** | Estrutura de preços | Varejo, Atacado, Funcionário |

### Fluxo de dados

1. **Assimilar** - Dados de produto de sistemas PIM/ERP
2. **Processo** - Aplicar exibições de catálogo, políticas e preços
3. **Entrega** - Veicula o catálogo filtrado em vitrines, marketplaces etc.

## Principais recursos

| Recurso | Benefício |
|---|---|
| **Catálogo de Base Única** | Eliminar a duplicação de dados em unidades de negócios |
| **Preços flexíveis** | Vários catálogos de preços por SKU para diferentes segmentos de clientes |
| **Escalável** | Gerencie mais de 200 milhões de SKUs com eficiência |
| **Multicanal** | Oferece catálogos para vitrines, mercados e plataformas de publicidade |
| **Atualizações em tempo real** | Atualize rapidamente os dados do catálogo para promoções e campanhas |

## Casos de uso

### Conglomerado multimarcas

**Desafio**: gerenciar várias marcas, países e idiomas<br>
**Solução**: catálogo único com exibições de catálogo para cada combinação de marca/região

### Revendedor de peças automotivas

**Desafio**: 3.000 revendedores com os mesmos produtos, mas com preços diferentes<br>
**Solução**: um catálogo com exibições de catálogo e catálogos específicos de revendedores

### Retailer com vários locais

**Desafio**: preços e inventário diferentes por localização<br>
**Solução**: exibições de catálogo baseadas em localização com políticas específicas de região

>[!INFO]
>
>Para obter informações detalhadas sobre a assimilação e a entrega de dados do catálogo, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/).

## Veja mais aqui

- [Fontes do catálogo](catalog-sources.md) - Defina o escopo autoritativo de produtos, atributos e categorias para comportamento de pesquisa, filtro e classificação
- [Camadas do catálogo](catalog-layer.md) - Saiba como modificar dados do produto sem alterar a origem original
- [Políticas](policies.md) - Criar políticas para filtrar produtos nas exibições de catálogo
- [Catálogos de preços](pricebooks.md) - Gerenciar estruturas de preços para diferentes segmentos de clientes
