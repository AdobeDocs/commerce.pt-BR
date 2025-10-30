---
title: Adicionar facetas
description: Saiba como adicionar atributos de produto filtráveis como [!DNL Live Search] facetas.
exl-id: 80559107-2b2d-411f-8c32-99ff024e7a09
source-git-commit: 15afc6fcd1e6783640dc3980ee06290e017abf37
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Adicionar facetas

Qualquer atributo de produto filtrável pode ser usado como uma faceta. O painel *Adicionar aspectos* lista os aspectos atuais e facilita a atribuição de atributos de produto adicionais como aspectos. Durante esse processo de três etapas, um atributo é escolhido para ser usado como uma faceta, as propriedades são editadas, se necessário, e as alterações são publicadas na loja.

![Adicionar aspectos](assets/facets-add.png)

## Etapa 1: adicionar uma faceta

1. No Administrador, vá para **Marketing** > SEO e pesquisa > **[!DNL Live Search]**.
1. Na guia *Faceting*, clique em **Adicionar facetas**.
1. Na lista *Adicionar aspectos*, cada atributo disponível tem um ![Botão Adicionar](assets/btn-add.png) separado. Conclua uma das opções a seguir:

   * Na lista *Atributos de faceta*, escolha o atributo de produto que você deseja usar como faceta e clique em **Adicionar**.
   * Para localizar um atributo de produto específico, insira os primeiros caracteres do nome do atributo na caixa *Pesquisar*. Em seguida, clique em **Adicionar**.

     Para configurar os intervalos e agrupamentos de facetas de preços, consulte [Configurações](settings.md). Para saber mais, vá para [Tipos de facetas](facets-type.md).
A faceta é adicionada à parte inferior da lista *Facetas Dinâmicas* e o botão *Publicar alterações* fica disponível.

1. Se a faceta que você deseja adicionar não puder ser encontrada, vá para **Lojas** > Atributos > **Produto** e verifique se o atributo tem as [propriedades necessárias](facets.md) para ser usado como uma faceta. Se necessário, atualize as seguintes propriedades da loja do atributo:

   * **[!UICONTROL Use in Search]** -  `Yes`
   * **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
   * **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

1. Quando solicitado, atualize o cache.

   A faceta ficará disponível na loja na próxima vez que o catálogo for sincronizado com [!DNL Live Search]. Se a faceta não estiver disponível após duas horas, consulte [Sincronizar dados do catálogo](install.md#synchronize-catalog-data).

## Etapa 2: Editar propriedades da faceta (Opcional)

1. Para editar as propriedades da faceta, clique em **Mais** (![Mais seletor](assets/btn-more.png)) opções na coluna à direita.
1. No menu, clique em **Editar**. Em seguida, ajuste as seguintes propriedades, conforme necessário.

   * Rótulo - ([Headless](facets-type.md) somente) Insira o rótulo de facetas que você deseja usar.
   * Tipo de classificação - As facetas são classificadas alfabeticamente para todas as [!DNL Commerce] lojas. Para implementações headless, os aspectos podem ser classificados em ordem alfabética ou por contagem. Opções: alfabética, contagem (somente headless)
   * Valor máximo - Insira o número máximo de valores de facetas exibidos na loja. Entradas válidas: 0 - 100; Padrão: 8

1. Quando terminar, clique em **Salvar**.

   ![Editar facetas](assets/facet-edit.png)

1. Para fixar a faceta na parte superior da lista *Filtros*, clique no pino cinza (![Seletor de pinos](assets/btn-pin-gray.png)).
1. Para alterar a ordem da faceta fixada, clique no ícone **Mover** (![Mover seletor](assets/btn-move.png)) e arraste a linha para uma nova posição na seção *Facetas fixadas*.

## Etapa 3: publicar alterações

1. Quando a faceta estiver concluída, clique em **Publicar alterações**.
1. Aguarde até que a faceta apareça no armazenamento.
Se a faceta não estiver disponível após duas horas, consulte [Verificar exportação](install.md#synchronize-catalog-data) nas instruções de instalação.

## Descrições dos campos

| Campo | Descrição |
|--- |--- |
| Rótulo | (Somente [Headless](facets-type.md)) O [rótulo de faceta](facets-type.md) que está visível na loja pode ser editado para manter a consistência com a sua marca. |
| Tipo de classificação | O método usado para [classificar](facets-type.md) facetas. Todas as [!DNL Commerce] vitrines classificam os aspectos somente em ordem alfabética. Implementações headless também podem classificar por `Count`. Opções:<br />Alfabético - Classifica aspectos em ordem alfabética.<br />Contagem - (Somente headless) Classifica facetas com base no número de correspondências encontradas. |
| Valor máximo | O número máximo de valores que podem ser exibidos na loja para cada faceta. Os aspectos que representam um intervalo de valores são distribuídos uniformemente. Entradas válidas: 0 - 100; Padrão: 8 |

### Controles

| Controle | Descrição |
|--- |--- |
| ![Seletor de pinos](assets/btn-pin-blue.png) | Fixa ou desfixa uma faceta na parte superior da lista *Filtros*. |
| ![Mais seletor](assets/btn-more.png) | Exibe um menu de mais ações que podem ser aplicadas à faceta selecionada. Opções: Editar, Excluir |
| ![Mover seletor](assets/btn-move.png) | Use o ícone *Mover* para arrastar uma faceta fixada para outro local na seção *Facetas fixadas*. |
