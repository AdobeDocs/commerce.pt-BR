---
title: Merchandising de categoria
description: Use o  [!DNL Live Search] Merchandising por categoria para ter uma experiência de compra mais rápida.
gourl: ls_catalog_merchandising
exl-id: b2645096-aafc-4d68-8adc-ab5410a9dfb6
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
TQID: https://experienceleague.adobe.com/2omWXwNttfwW04upO-QlQlRa41w9vgpdlPOYVFOX7-4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 1143
ht-degree: 0%

---

# Merchandising de categoria

O merchandising por categoria permite que os proprietários de lojas apliquem [!DNL Live Search] [regras](rules.md) de classificação inteligente a categorias e subcategorias de produtos.

Este vídeo é uma introdução ao Merchandising por categoria.

>[!VIDEO](https://video.tv.adobe.com/v/3424617)

O recurso é acessado no Administrador em **Marketing** > SEO e pesquisa > **[!DNL Live Search]** > **Merchandising de categorias**.

>[!NOTE]
>
>O Merchandising por categoria está disponível com [!DNL Live Search] [3.0.0 ou superior](release-notes.md). Se você vir o espaço de trabalho Categoria de merchandising, mas ele não estiver preenchido com dados, atualize o módulo [!DNL Live Search].

![Espaço de trabalho de merchandising da categoria](assets/category_workspace.png)

A exibição de Merchandising por categoria mostra regras de categoria definidas, com colunas para:

* Categoria
* Estratégia de classificação
* Classificação herdada
* Última atualização
* Ação

Você pode pesquisar uma categoria ou subcategoria no campo &quot;Pesquisar por categoria&quot;.

## Estratégias de classificação

O Merchandising por categoria usa os mesmos tipos de classificação que com [produtos individuais](rules-workspace.md).
Há dois tipos de classificação: Inteligente e Manual.

**A classificação inteligente** aproveita a análise de dados comportamentais de vitrine pela [Adobe AI](https://business.adobe.com/ai.html) para classificar todos os produtos nas categorias escolhidas por um determinado algoritmo. Depois de escolher uma classificação Inteligente, a ordem específica dos produtos será alterada com o tempo, à medida que o [!DNL Adobe AI] reanalisar os dados subjacentes de forma contínua. Por exemplo, os principais produtos de tendências mudam automaticamente com o tempo, à medida que as preferências do comprador mudam.
Os métodos de classificação inteligente são:

* Mais comprados: classifica os produtos de acordo com a frequência com que os compradores os compraram nos sete dias anteriores.
* Mais adicionados ao carrinho: classifica os produtos de acordo com a frequência com que os compradores os adicionaram ao carrinho nos sete dias anteriores.
* Mais visualizados: classifica os produtos de acordo com a frequência com que os compradores os visualizaram nos sete dias anteriores.
* Recomendado para você: com base no comportamento anterior e atual de cada comprador no local, o classifica os produtos de acordo com a probabilidade de o comprador interagir com cada um.
* Tendências: classifica os produtos por retomadas recentes de popularidade com base nas visualizações.
* Nenhum: classifica os produtos de acordo com sua ordem padrão.


Para ajustar a intensidade com que os sinais de comportamento afetam a ordem do produto para qualquer método de classificação inteligente, exceto **Nenhum**, defina **[!UICONTROL Intelligent Ranking Boost]** no editor de regras. Para obter detalhes sobre padrões, limites, comportamento de visualização e como o aumento se compara à **Classificação manual**, consulte [Aumento inteligente de classificação](rules-add.md#intelligent-ranking-boost).

**A classificação manual** permite que os usuários substituam a ordem de classificação automática de produtos definindo regras manuais de fixação, reforço, enterramento e ocultação.

## Classificação herdada

Como comerciante, selecione todas as categorias de roupas femininas para classificar por &quot;tendência&quot;. Isso inclui as subcategorias &quot;Calças femininas&quot;, &quot;Camisas femininas&quot; e &quot;Acessórios femininos&quot;. As categorias para homens não devem ser afetadas. Você pode usar classificações herdadas para fazer isso.

Ao selecionar um método de classificação inteligente para uma categoria ou subcategoria que tenha subcategorias, você pode ativar a opção **Aplicar classificações inteligentes a subcategorias**. Isso aplica o método de classificação a todas as subcategorias.

Essas subcategorias agora herdam essa regra da categoria principal (&quot;Sim&quot; na coluna Classificação herdada). Na coluna Ação, as únicas opções disponíveis são **Editar Regra** e **Exibir Detalhes**. A opção **Excluir** está desabilitada para regras herdadas em subcategorias. Excluir a herança de subcategoria requer desfazer a herança da categoria principal.

Cada categoria ou subcategoria pode ter até uma classificação inteligente aplicada de cada vez. Também pode ter uma ou mais classificações manuais aplicadas simultaneamente.

Se você aplicar uma classificação Inteligente a uma categoria e habilitar [!UICONTROL Apply intelligent ranking to subcategories], a classificação Inteligente da categoria substituirá qualquer classificação Inteligente já aplicada às suas subcategorias.

![Lista de subcategorias substituída](assets/category_overwite_subs.png){width="700"}

Se você clicar em **Exibir tudo**, uma caixa de diálogo será aberta com detalhes das alterações propostas.

![Detalhes das alterações de classificação](assets/category_overwrite.png)

Ao adicionar uma classificação inteligente diretamente a uma categoria que tem uma classificação inteligente herdada, a herança é substituída pela nova classificação inteligente.

Ao excluir a classificação Inteligente da categoria, a herança é restabelecida.
Em ambos os cenários, qualquer classificação manual é mantida.

Se você remover uma classificação inteligente de uma categoria enquanto [!UICONTROL Apply intelligent ranking to subcategories] estiver habilitado, somente as classificações inteligentes herdadas por suas subcategorias serão removidas. Quaisquer classificações manuais permanecem porque não são herdadas.

Será exibida uma caixa de diálogo explicando quais subcategorias herdadas são afetadas por quaisquer alterações feitas em uma categoria de nível superior.

![Caixa de diálogo modal de alterações de classificação](assets/category_overwrite_modal.png){width="1200"}

## Criar uma regra de categoria

Para criar uma regra de categoria:

1. Clique no botão **Adicionar regra**.
1. No modo de exibição _Selecionar Categoria_, clique nas categorias e subcategorias.
1. Marque a caixa de seleção para selecionar a categoria que deseja classificar.
1. Clique em **Aplicar**.

   ![Selecione uma categoria](assets/category_select.png)

1. Na exibição _Adicionar regra de categoria_, selecione o método de classificação inteligente que deseja aplicar à categoria.
A Página de Visualização de Categoria mostra os resultados reais da classificação selecionada, usando os dados do [!DNL Live Search].
1. Clique em **Salvar e publicar** para salvar a regra.

![Selecione o método de classificação inteligente](assets/category_ranking.png)

O serviço [!DNL Live Search] processa a regra e a ativa no armazenamento quando concluído.

## Modificar uma regra de categoria

Para modificar uma regra existente:

1. Clique em **...** na coluna Ação e escolha **Editar**.
1. Na exibição de regra Editar Categoria, faça as alterações necessárias e clique em **Salvar e Publicar**.

As alterações são refletidas no armazenamento quando [!DNL Live Search] processou a alteração.

## Excluir uma regra de categoria

Para excluir uma regra de categoria:

1. Clique em **...** na coluna Ação e escolha **Excluir**.
1. No modal _Excluir regra_, selecione **Excluir** para remover a regra ou **Cancelar** para cancelar a ação.

## Classificação manual

A classificação manual permite substituir a ordem do produto determinada pelas regras de Classificação inteligente (se houver) e controlar manualmente onde os produtos aparecem nos resultados.

Eventos são ações que modificam os resultados da pesquisa quando condições definidas são atendidas. Uma classificação manual pode ter até 25 eventos.

* Aumentar: move um produto para cima nos resultados da pesquisa.
* Enterro: move um produto para baixo nos resultados da pesquisa.
* Fixar um produto: move um produto para uma posição específica nos resultados.
* Ocultar um produto: exclui um produto dos resultados da pesquisa.

Criar uma classificação manual:

1. Configure uma regra de classificação Inteligente para uma categoria conforme descrito acima.

   Os resultados da consulta aparecem na exibição de Página de categoria de visualização. Ele usa seus dados reais do Live Search para visualizar os resultados.

1. Clique e arraste um produto na exibição da Página Visualizar categoria. Arraste e solte-o na posição desejada. Os campos Produto e Posição são automaticamente preenchidos no painel Eventos.

Você também pode clicar no ícone de pino para bloquear um produto no local atual. Use o menu de contexto de reticências para &quot;Fixar na parte superior&quot; ou &quot;Fixar na parte inferior&quot;.

Para adicionar um evento manualmente:

1. Em Classificação Manual, clique no menu **Selecionar um evento** e escolha um evento a ser realizado quando as condições associadas forem atendidas.
1. Insira o nome do produto que você deseja que seja afetado. Os produtos são sugeridos à medida que você digita.
1. Para vários eventos, escolha outros eventos que deseja acionar quando as condições forem atendidas.

>[!NOTE]
>
>As regras são aplicadas quando uma categoria específica é aberta na loja e uma regra existe para essa categoria. Para regras de merchandising por categoria, a ordem de classificação padrão é &quot;Classificar por: Posição&quot;. Se um comprador alterar a ordem de classificação, todos os produtos ocultos, fixados e enterrados não serão mais classificados.
