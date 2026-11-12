---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%
---
As políticas definem filtros que são aplicados aos produtos em uma exibição de catálogo. Eles ajudam a adaptar a variedade de produtos retornados a uma loja ou canal. Isso garante que o conteúdo correto seja entregue ao destino certo. Por exemplo, lojas físicas, marketplaces e canais de publicidade como Google, Facebook e Instagram.

As políticas usam atributos de produto, como marca, modelo ou categoria de peça, para adaptar os dados do catálogo às necessidades dos negócios. &#x200B;

## Acessar o espaço de trabalho Políticas

A forma como você abre o espaço de trabalho *Políticas* depende do produto que você usa:

- **Administrador do Adobe Commerce** (Adobe Commerce as a Cloud Service)—Selecione *Catálogo* > **Políticas**.
- **Adobe Commerce Optimizer Studio**—Selecione *Configuração de armazenamento* > **Políticas**.

## Filtros

Os filtros definem condições baseadas em atributos que determinam quais produtos correspondem a uma política. Quando associada a uma exibição de catálogo, uma política ajuda a adaptar os produtos retornados para essa exibição. Use atributos de produto, operadores e valores para definir as condições correspondentes.

### Partes de um filtro

Um filtro é composto das seguintes partes:

| Parte | Descrição | Exemplo |
|---|---|---|
| **Atributo** | O atributo de produto usado para filtragem. | `part_category` |
| **Operador** | A condição aplicada ao atributo. | `IN`, `EQUALS`, `CONTAINS` |
| **Origem do valor** | Especifica se os valores são `STATIC` ou `TRIGGER`. | `STATIC` [Saiba mais](#value-source-types) |
| **Valor** | Os valores específicos que atendem à condição. | `brakes, suspension` |

### Exemplo

Um filtro em `part_category` usando o operador `IN` com valores `brakes` e `suspension` corresponde a produtos cujo `part_category` é um dos valores.

### Tipos de origem de valor

Há dois tipos de fontes de valor: **STATIC** e **TRIGGER**.

As políticas com uma **origem de valor** de **ESTÁTICA** são consideradas políticas universais. As políticas universais definem a experiência de um site como um todo. Isso significa que a exibição de catálogo sempre executa essa política. A execução da política não depende da interação do usuário da loja.

As políticas com uma **Origem de valor** de **ACIONADOR** são chamadas de políticas exclusivas. Isso significa que a exibição de catálogo executa essa política somente quando o acionador é especificado no cabeçalho da chamada de API. Na loja, isso significa que as informações são exibidas com base no que o comprador seleciona. Por exemplo, na imagem a seguir, há dois menus suspensos: **Marca** e **Modelo**.

![Acionar a fonte de valor na loja](/help/assets/ccdm-shared/setup/policy-trigger.png)

A **Marca** e o **Modelo** são acionadores definidos:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Se o comprador clicar no menu suspenso Modelo, o cabeçalho da chamada de API conterá `AC-Policy-Model`, que está configurado para mostrar apenas produtos específicos à política `AC-Policy-Model`.

### Acionadores de cabeçalho HTTP de vários valores {#multi-value-http-header-triggers}

Uma política de gatilho que usa o tipo de transporte `HTTP_HEADER` pode receber vários valores em um único cabeçalho. Os valores devem ser separados por vírgulas e o operador de filtro deve ser `IN`. Cada valor é tratado como uma correspondência aceitável. Os valores são avaliados com a semântica `OR`.

Por exemplo, um filtro de política usando `IN` com o seguinte cabeçalho:

```
AC-Policy-Vehicle: UNIVERSAL,veh-bolt-mammoth-limited-2025
```

corresponde a produtos cujo atributo `vehicle` é `UNIVERSAL` ou `veh-bolt-mammoth-limited-2025`.

Enquanto um operador de filtro de `EQUALS`, `GREATER_THAN_EQUAL` ou `LESS_THAN_EQUAL` é rejeitado com um erro de validação.

#### Notas de sintaxe

- O nome do cabeçalho corresponde ao nome do acionador configurado, por exemplo `AC-Policy-Vehicle`.
- Vírgulas separam valores individuais dentro do cabeçalho. Quando o mesmo cabeçalho `AC-Policy-_Name_` aparece mais de uma vez, seus valores são combinados em um único valor de cabeçalho separado por vírgulas
- O operador de filtro é `IN`.
- Um filtro de política com **Origem do valor** definida como `TRIGGER`.
- Um gatilho cujo **Tipo de transporte** é `HTTP_HEADER`.

## Criar política

Nesta seção, você cria uma nova regra. A política pode ser **ESTÁTICA** ou **ACIONADOR**.

### Criar uma política STATIC

1. No espaço de trabalho **[!UICONTROL Policies]**, clique no botão **[!UICONTROL Add Policy]**.

   Uma nova página é aberta para que você preencha os detalhes da política. &#x200B;

1. Insira o nome da política, por exemplo &quot;Categorias de peças Celport&quot;.

1. Clique no botão **[!UICONTROL Add Filter]**.

   Uma caixa de diálogo é aberta para que você adicione detalhes do filtro.

1. Adicione os detalhes do filtro. Por exemplo:

   1. **Atributo** - Insira um atributo do catálogo. Por exemplo, &quot;part_category&quot;. Esse nome deve corresponder exatamente ao nome do atributo no catálogo.
   1. **Operador** - Escolha o operador. Por exemplo, **IN**. &#x200B;
   1. **Value Source** - Selecione **STATIC**. &#x200B;
   1. **Valor** - Insira um valor da definição de atributo especificada anteriormente. Por exemplo, insira &quot;freios&quot; para criar um filtro para peças de freios.
   1. Para salvar o valor, pressione **Enter**.

      Se a política tiver sido projetada para filtrar por vários valores, insira cada valor separadamente.

1. Clique no botão **[!UICONTROL Save]** na caixa de diálogo de detalhes do filtro. &#x200B;

1. Clique no ícone do menu (...) ao lado do filtro criado e selecione **Habilitar**. Aqui, você também pode **Editar**, **Desabilitar** ou **Excluir** o filtro.

   A coluna **Status** mostra um ícone verde e a palavra &quot;Habilitado&quot;.

1. Clique no botão **[!UICONTROL Save]** para salvar a nova política.&#x200B; Se o botão não estiver ativo, verifique se o nome da política foi adicionado clicando no ícone de lápis ao lado de **Nova Política**.

1. Para verificar sua nova política, clique na seta para trás para retornar ao espaço de trabalho **[!UICONTROL Policies]**.

### Criar uma política de ACIONADOR

1. No espaço de trabalho **[!UICONTROL Policies]**, clique no botão **[!UICONTROL Add Policy]**.

   Uma nova página é aberta para que você preencha os detalhes da política. &#x200B;

1. Insira o nome da política, por exemplo &quot;Categorias de peças Celport&quot;.

1. Clique no botão **[!UICONTROL Add Trigger]**.

   A caixa de diálogo **Detalhes do acionador** é exibida.

1. Insira um nome para o acionador, como **AC-Policy-Brand**.

1. Selecione o **Tipo de transporte**. **HTTP_HEADER** é o único tipo aceito no momento.

1. Clique no botão **[!UICONTROL Save]** para salvar o acionador.

1. Clique no botão **[!UICONTROL Add Filter]**.

   Uma caixa de diálogo é aberta para que você adicione detalhes do filtro.

1. Adicione os detalhes do filtro. Por exemplo:

   1. **Atributo** - Insira um atributo do catálogo. Por exemplo, &quot;part_category&quot;. Esse nome deve corresponder exatamente ao nome do atributo no catálogo.
   1. **Operador** - Escolha o operador. Por exemplo, **IN**. &#x200B;
   1. **Value Source** - Selecione **TRIGGER**. &#x200B;
   1. **Valor** - Insira o nome do acionador criado anteriormente (**AC-Policy-Brand**).

   No momento da configuração, o filtro faz referência ao acionador configurado. No tempo de execução, o cabeçalho da solicitação de API fornece o valor ou os valores avaliados por esse filtro.

1. Clique no botão **[!UICONTROL Save]** na caixa de diálogo de detalhes do filtro. &#x200B;

1. Clique no ícone do menu (...) ao lado do filtro criado e selecione **Habilitar**. Aqui, você também pode **Editar**, **Desabilitar** ou **Excluir** o filtro.

   A coluna **Status** mostra um ícone verde e a palavra &quot;Habilitado&quot;.

1. Clique no botão **[!UICONTROL Save]** para salvar a nova política.&#x200B; Se o botão não estiver ativo, verifique se o nome da política foi adicionado clicando no ícone de lápis ao lado de **Nova Política**.

1. Para verificar sua nova política, clique na seta para trás para retornar ao espaço de trabalho **[!UICONTROL Policies]**.

Seguir essas etapas cria a política que pode ser vinculada a uma exibição de catálogo para controlar a visibilidade do produto.
