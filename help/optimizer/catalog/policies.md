---
title: Políticas
description: Saiba como usar políticas para filtrar dados em um canal para garantir que os dados sejam enviados para o destino correto.
hide: true
recommendations: noCatalog
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Políticas

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

As políticas são filtros de acesso a dados contidos em canais que refinam ainda mais os dados entregues a cada canal. As políticas garantem que o conteúdo correto seja enviado ao destino certo. Por exemplo, lojas físicas, mercados, pipelines de anúncios (Google, Facebook, Instagram) em pontos de venda.

As políticas são baseadas em atributos de produto, como marca, modelo ou categoria de peça, e são usadas para adaptar os dados do catálogo de forma a atender às necessidades específicas dos negócios. &#x200B;

## Filtros

Filtros são o mecanismo em uma política que impõe a segmentação de catálogo. Os filtros permitem que as empresas personalizem vitrines e canais para conjuntos de produtos específicos com base nas necessidades operacionais. Use critérios como atributos de produto, operadores e valores para definir uma regra ou condição que indique quais produtos estão incluídos ou excluídos em um canal ou vitrine.

### Partes de um filtro

Um filtro é composto pelas seguintes partes:

| Parte | Descrição | Exemplo |
|---|---|---|
| **Atributo** | O atributo de produto usado para filtragem. | `part_category` |
| **Operador** | A condição aplicada ao atributo. | `IN`, , `EQUALS``CONTAINS` |
| **Valor fonte** | Especifica se os valores são `STATIC` ou `TRIGGER`. | `STATIC` |
| **Valor** | Os valores específicos que atendem à condição. | `brakes, suspension` |

### Exemplo

Um filtro com o atributo `part_category`, um operador de `IN` e valores `brakes, suspension` garante que apenas produtos categorizados como freios e suspensão sejam incluídos na política.

### Tipos de origem de valor

Há dois tipos de fontes de valor: **STATIC** e **TRIGGER**.

As políticas com uma **origem de valor** de **ESTÁTICA** são consideradas políticas universais. As políticas universais definem a experiência de um site como um todo. Isso significa que o canal sempre executará essa política. Em outras palavras, a execução dessa política não se baseia em nenhuma interação do usuário na loja.

As políticas com uma **Origem de valor** de **ACIONADOR** são chamadas de políticas exclusivas. Isso significa que o canal executará essa política somente quando o acionador for especificado no cabeçalho da chamada de API. Na loja, isso significa que as informações são exibidas com base no que o comprador seleciona. Por exemplo, na imagem a seguir, há dois menus suspensos: **Marca** e **Modelo**.

![Acionar a fonte de valor na loja](../assets/policy-trigger.png)

A **Marca** e o **Modelo** são acionadores definidos:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Se o comprador clicar no menu suspenso **Marca**, o cabeçalho da chamada de API conterá `AC-Policy-Brand`, que está configurado para mostrar apenas produtos específicos à política `AC-Policy-Brand`.

## Criar política

Nesta seção, você cria uma nova regra. A política pode ser **ESTÁTICA** ou **ACIONADOR**.

### Criar uma política STATIC

1. No menu esquerdo, abra a seção **[!UICONTROL Catalog]** e clique em **[!UICONTROL Policies]**.

1. Clique no botão **[!UICONTROL Add Policy]**.

   Uma nova página é aberta para que você preencha os detalhes da política. &#x200B;

1. Insira o nome da política, por exemplo &quot;Categorias de peças Celport&quot;.

1. Clique no botão **[!UICONTROL Add Filter]**.

   Uma caixa de diálogo é aberta para que você adicione detalhes do filtro.

1. Adicione os detalhes do filtro. Por exemplo:

   1. **Atributo** - Insira um atributo do catálogo. Por exemplo, &quot;part_category&quot;. Esse nome deve corresponder exatamente ao nome do atributo no catálogo.
   1. **Operador** - Escolha o operador. Por exemplo, **IN**. &#x200B;
   1. **Value Source** - Selecione **STATIC**. &#x200B;
   1. **Valor** - Insira o(s) valor(es) no atributo especificado anteriormente. Por exemplo, &quot;freios, suspensão&quot;. &#x200B;Esses nomes devem corresponder exatamente aos nomes dos valores do atributo especificado anteriormente.

1. Clique no botão **[!UICONTROL Save]** na caixa de diálogo de detalhes do filtro. &#x200B;

1. Clique nos pontos de ação (...) ao lado do filtro criado e selecione **Habilitar**. Aqui, você também pode **Editar**, **Desabilitar** ou **Excluir** o filtro.

   A coluna **Status** mostra um ícone verde e a palavra &quot;Habilitado&quot;.

1. Clique no botão **[!UICONTROL Save]** para salvar a nova política.&#x200B; Se o botão não estiver ativo, verifique se o nome da política foi adicionado clicando no ícone de lápis ao lado de **Nova Política**.

1. Para verificar sua nova política, volte para a lista de políticas clicando na seta para trás. &#x200B;Você verá sua nova política listada.

### Criar uma política de ACIONADOR

1. No menu esquerdo, abra a seção **[!UICONTROL Catalog]** e clique em **[!UICONTROL Policies]**.

1. Clique no botão **[!UICONTROL Add Policy]**.

   Uma nova página é aberta para que você preencha os detalhes da política. &#x200B;

1. Insira o nome da política, por exemplo &quot;Categorias de peças Celport&quot;.

1. Clique no botão **[!UICONTROL Add Trigger]**.

   A caixa de diálogo **Detalhes do acionador** é exibida.

1. Insira um nome para o acionador, como **AC-Policy-Brand**.

1. Selecione o **Tipo de transporte**. **HTTP_HEADER** é o único tipo aceito no momento.

1. Clique no botão **[!UICONTROL Save]** para salvar o acionador.

1. Clique no **[!UICONTROL Add Filter]** botão.

   Uma caixa de diálogo é aberta para você adicionar detalhes do filtro.

1. Adicione os detalhes do filtro. Por exemplo:

   1. **** Atributo - Insira um atributo do catálogo. Por exemplo, &quot;part_categoria&quot;. Este nome deve corresponder exatamente ao nome do atributo no catálogo.
   1. **Operador** - Escolha o operador. Por exemplo, **IN**.
   1. **Valor Origem** - Selecione Acionador ****.
   1. **** Valor - Insira o nome do acionador que você criou anteriormente (**AC-Policy-Brand**).

1. Clique na **[!UICONTROL Save]** botão na caixa de diálogo de detalhes do filtro.

1. Clique nos pontos de ação (...) ao lado do filtro criado e selecione **Ativar**. A partir daqui você também **pode Editar**, **Desativar** ou **Excluir** filtro.

   A coluna **Status** mostra um ícone verde e a palavra &quot;Habilitado&quot;.

1. Clique no botão **[!UICONTROL Save]** para salvar a nova política.&#x200B; Se o botão não estiver ativo, verifique se o nome da política foi adicionado clicando no ícone de lápis ao lado de **Nova Política**.

1. Para verificar sua nova política, volte para a lista de políticas clicando na seta para trás. &#x200B;Você verá sua nova política listada.

Ao seguir essas etapas, a política será criada e estará pronta para ser vinculada a um canal para controlar a visibilidade do produto.
