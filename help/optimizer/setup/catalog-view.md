---
title: Exibição de catálogo
description: Saiba o que são exibições de catálogo e como criá-las para organizar o catálogo de produtos por estrutura de negócios, políticas e preços.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 0%

---


# Exibições de catálogo para serviços de merchandising

As visualizações de catálogo são a base dos Serviços de merchandising da Adobe Commerce Optimizer, permitindo que você organize seu catálogo de produtos por estrutura de negócios, políticas e preços. Esse modelo de dados flexível oferece suporte a várias marcas, unidades de negócios e cenários em vários idiomas, mantendo a eficiência operacional.

## O que são Exibições de catálogo?

As exibições de catálogo definem como o catálogo de produtos é organizado e exibido. Eles atuam como filtros que determinam:

- **Quais produtos são visíveis** com base na estrutura comercial (marcas, regiões, revendedores)
- **Que preços são mostrados** por meio de catálogos de preços vinculados
- **Como os produtos são filtrados** usando políticas (atributos como marca, modelo, categoria)
- **Que fonte de catálogo é usada** com base em atributos como localidade

Considere as exibições de catálogo como diferentes &quot;lentes&quot; pelas quais os clientes veem seu catálogo. Por exemplo:

- A exibição do catálogo do revendedor pode mostrar somente os produtos disponíveis para esse revendedor específico
- Uma exibição de catálogo regional pode mostrar produtos e preços específicos de uma área geográfica
- A exibição do catálogo de marcas pode mostrar apenas produtos de uma marca específica

## Criar uma exibição de catálogo

Nesta seção, você cria uma exibição de catálogo, selecione uma [política](policies.md) e um [catálogo de preços](pricebooks.md).

Antes de criar uma visualização de catálogo, verifique se você tem:

- [Políticas criadas](policies.md) para definir filtros de produto

- [Catálogos de preços assimilados](pricebooks.md) para preços

1. No menu esquerdo, vá para _Configuração da loja_ e clique em **[!UICONTROL Catalog views]**.

1. Clique em **[!UICONTROL Create catalog view]**. &#x200B;

1. Configure os detalhes de exibição do catálogo:

   - **Nome** — Digite o nome da exibição do catálogo, por exemplo `Celport`. &#x200B;
   - **Origens do catálogo** — Selecione a origem do catálogo (localidade), por exemplo `en-US`.
   - **Políticas** — use o menu suspenso para selecionar as políticas relevantes. Por exemplo, &quot;Marca&quot;, &quot;Modelo&quot;. &#x200B;Verifique se você já [criou uma política](policies.md).

1. Selecione o catálogo de preços a ser vinculado à exibição do catálogo.

   - **Usar todos os catálogos de preços disponíveis**-Essa opção extrai dados de preços de todos os catálogos de preços disponíveis.
   - **Permitir somente catálogos de preços selecionados**-Essa opção exibe a caixa de diálogo **Adicionar catálogos de preços permitidos**, onde é possível selecionar qual catálogo de preços específico usar para a exibição do catálogo.
   - **Desabilitar preço**-Esta opção não está disponível no momento.

1. Clique em **[!UICONTROL Add]** para criar a exibição de catálogo com as políticas e os catálogos de preços vinculados.

A página Exibições de catálogo é atualizada para exibir a nova exibição de catálogo.&#x200B;

Após concluir essas etapas, a exibição do catálogo agora está configurada para exibir produtos e preços com base nas fontes e políticas selecionadas.

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

**2. Catálogo de Base Unificada**
Os dados assimilados criam um catálogo base unificado no pipeline de dados do Serviço de catálogo. Essa única fonte elimina a duplicação de dados nas unidades de negócios.

**3. Exibições de Catálogo**
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
