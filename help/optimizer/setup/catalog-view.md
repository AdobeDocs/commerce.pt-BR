---
title: Exibições do catálogo
description: Saiba o que são exibições de catálogo e como criá-las para organizar o catálogo de produtos por estrutura de negócios, políticas e preços.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente ao Adobe Commerce as a Cloud Service e a projetos [!DNL Adobe Commerce Optimizer] (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 76c1b81c-b456-4334-89bd-6027308cbc47
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
nudge: true
source-git-commit: d081e975b03805a0f46d5194f8c3cd46e3c86839
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
# Exibições de catálogo para Serviços de merchandising

{{$include /help/_includes/ccdm-shared/setup/catalog-view.md}}

## Gerenciar exibições do catálogo

Use estas instruções para gerenciar exibições de catálogo:

- [Criar exibição de catálogo](#create-a-catalog-view) — Defina o nome, a origem do catálogo, as políticas e o catálogo de preços. Em seguida, [especifique a exibição do catálogo para recomendações e regras de descoberta de produtos](#specify-catalog-views-for-recommendations-and-product-discovery-rules), revise [camadas de catálogo](#catalog-layers) que substituem atributos de produto ou [torne a exibição do catálogo privada](#make-a-catalog-view-private).
- [Editar uma exibição de catálogo](#edit-a-catalog-view)—Atualize suas configurações de fontes, políticas, catálogo de preços e proteção.
- [Excluir uma exibição de catálogo](#delete-a-catalog-view) — Remova uma exibição de catálogo desnecessária.
- [Exibir detalhes de exibição do catálogo](#view-catalog-view-details)—Examine a configuração de exibição do catálogo na tabela Exibições do catálogo.

### Criar uma exibição de catálogo

Antes de criar uma visualização de catálogo, prepare os seguintes itens conforme necessário:

- Uma [origem do catálogo](catalog-sources.md)
- [Políticas](policies.md) que definem filtros de produto
- [Camadas do catálogo](catalog-layer.md) se precisar substituir atributos do produto
- [Catálogos de preços](pricebooks.md) para os preços exibidos na exibição
- [Chaves de acesso restrito](restricted-access-keys.md) se você deseja criar uma exibição de catálogo privado

#### Configuração

Nesta seção, você cria uma exibição de catálogo, selecione uma [política](policies.md) e um [catálogo de preços](pricebooks.md).

1. No menu esquerdo, vá para **[!UICONTROL Store setup]** e clique em **[!UICONTROL Catalog views]**.

1. Clique em **[!UICONTROL Create catalog view]**. &#x200B;

1. Configure os detalhes de exibição do catálogo:

   - **Nome** — Digite o nome da exibição do catálogo, por exemplo `Celport`. &#x200B;
   - **Origens do catálogo** — Selecione a [origem do catálogo](catalog-sources.md), por exemplo `en-US`.
   - **Camadas do catálogo** — Revise as camadas e a prioridade assimiladas.
   - **Políticas** — use o menu suspenso para selecionar as políticas relevantes. Por exemplo, &quot;Marca&quot;, &quot;Modelo&quot;. &#x200B;Verifique se você já [criou uma política](policies.md).

1. Selecione o catálogo de preços a ser vinculado à exibição do catálogo.

   - **Usar todos os catálogos de preços disponíveis**—Esta opção extrai dados de preços de todos os catálogos de preços disponíveis.
   - **Permitir somente catálogos de preços selecionados**—Esta opção exibe a caixa de diálogo **Adicionar catálogos de preços permitidos**. Use esta caixa de diálogo para selecionar qual catálogo de preços específico usar para a exibição do catálogo.
   - **Somente catálogo de preços** — Selecione esta opção se somente um catálogo de preços se aplicar. Essa opção é necessária se você quiser configurar uma exibição de catálogo privado, que pode fazer referência a apenas um catálogo de preços. Consulte [Restrição de catálogo de preços em exibições de catálogo privado](private-catalog-view.md#price-book-restriction-on-private-catalog-views).
   - **Desabilitar preço**—Esta opção não está disponível no momento.

   >[!NOTE]
   >
   >Uma ID de catálogo de preços controla quais preços são solicitados. Ele não restringe o acesso à exibição do catálogo. Para restringir o acesso, habilite a Proteção de Catálogo para criar uma [exibição de catálogo privado](private-catalog-view.md).

1. (Opcional) Alterne **[!UICONTROL Catalog Protection]** para **[!UICONTROL Enabled]** para restringir os dados desta exibição de catálogo aos clientes com um token assinado válido. Consulte [Proteger uma exibição de catálogo](private-catalog-view.md#protect-a-catalog-view) para obter etapas de configuração.

1. Clique em **[!UICONTROL Add]** para criar a exibição de catálogo com as políticas e os catálogos de preços vinculados.

A página Exibições de catálogo é atualizada para exibir a nova exibição de catálogo.&#x200B;

Após concluir essas etapas, a exibição do catálogo agora está configurada para exibir produtos e preços com base nas fontes e políticas selecionadas.

#### Especificar exibições de catálogo para recomendações e regras de descoberta de produtos

Você pode especificar uma exibição de catálogo ao [criar unidades de recomendação](../merchandising/recommendations/create.md) ou [regras de merchandising](../merchandising/rules/add.md).

#### Camadas do catálogo

As camadas de catálogo permitem substituir atributos de produto selecionados sem alterar os dados do catálogo de origem. Use camadas para personalizar nomes, descrições, imagens, links ou metadados para uma exibição de catálogo.

Consulte [Camadas do catálogo](catalog-layer.md).

#### Tornar uma exibição de catálogo privada

Por padrão, uma visualização de catálogo é pública para aplicativos clientes que podem acessar a API de merchandising do GraphQL. Para restringir o acesso, configure uma exibição de catálogo privado habilitando **[!UICONTROL Catalog Protection]**.

Para saber como proteger uma exibição de catálogo e verificar se o acesso é imposto, consulte [Exibições de catálogo privado](private-catalog-view.md).

### Editar uma exibição de catálogo

1. No espaço de trabalho **[!UICONTROL Catalog views]**, localize a exibição do catálogo.
1. Para abrir o menu de ações, selecione (**[!UICONTROL ...]**).
1. Selecione **[!UICONTROL Edit]** para acessar o editor de exibição de catálogo.
1. Atualize o nome, as fontes de catálogo, as políticas, as informações do catálogo de preços e as configurações de **[!UICONTROL Catalog Protection]** (incluindo chaves de acesso restrito atribuídas), conforme necessário.
1. Clique em **[!UICONTROL Save]**.

### Excluir uma exibição de catálogo

1. No espaço de trabalho **[!UICONTROL Catalog views]**, localize a exibição do catálogo.
1. Para abrir o menu de ações, selecione (**[!UICONTROL ...]**).
1. Selecione **[!UICONTROL Delete]**.
1. Confirme a exclusão.

   Quando a caixa de diálogo de confirmação for exibida, clique em **[!UICONTROL Delete]**.

### Exibir detalhes de exibição do catálogo

Esta opção fornece uma maneira rápida de ver todos os parâmetros de exibição do catálogo, permanecendo na tabela **[!UICONTROL Catalog views]**.

No espaço de trabalho **[!UICONTROL Catalog views]**, selecione o ![ícone de informações](/help/assets/ccdm-shared/recommendations/info-icon.png) para uma exibição de catálogo para exibir seus detalhes de configuração.

![Detalhes de exibição do catálogo](../assets/catalog-view-details.png)

Aqui, você pode ver os detalhes de configuração da visualização do catálogo, como:

- ID da Visualização
- Nome
- Origens do catálogo
- Políticas
- Data de criação
- Dados modificados

Algumas dessas configurações são necessárias à medida que você configura sua loja ou usa a API de assimilação de dados.
