---
title: Adicionar sinônimos
description: Adicione  [!DNL Live Search] sinônimos para melhorar a resposta às solicitações de pesquisa.
exl-id: 2dc535ea-35a3-45a8-8171-901005223cc9
source-git-commit: 6dcfd0a54e6a6814b7f5708e0c221452b8af4537
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Adicionar sinônimos

Aumente o engajamento do cliente adicionando sua própria lista com curadoria de sinônimos do [!DNL Live Search]. [!DNL Live Search] pode gerenciar até 200 sinônimos por exibição de loja.

![[!DNL Live Search] sinônimos](assets/synonym-workspace.png)

## Etapa 1: adicionar um sinônimo

1. No Administrador, vá para **Marketing** > SEO e pesquisa > **[!DNL Live Search]**.
1. Para vários armazenamentos, defina o **Escopo** para a [exibição de armazenamento](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) onde as configurações de sinônimo se aplicam.
1. Clique na guia **Sinônimos**.
1. Clique no botão **Adicionar sinônimos**.

## Etapa 2: definir o sinônimo por tipo

Siga as instruções para o [tipo de sinônimo](synonyms-type.md) que você deseja criar.

### Sinônimo de bidirecional

1. Aceite a opção padrão **Bidirecional**.

   ![Adicionar sinônimo bidirecional](assets/synonym-add-two-way.png)

1. Digite o termo ou frase **Palavra-chave** que deve ser correspondida.
1. Insira os termos de **Expansão** que você deseja adicionar como sinônimos para a palavra-chave. Separe vários termos com uma vírgula.
Neste exemplo, a palavra-chave a ser correspondida é &quot;calças&quot; e o conjunto de termos de expansão é &quot;calças, calças&quot;.

   ![Exemplo de sinônimo bidirecional](assets/synonym-add-two-way-example.png)

1. Quando terminar, clique em **Salvar**.
O conjunto de sinônimos aparece na lista com uma seta bidirecional entre cada termo, o que significa que os termos são intercambiáveis.

   ![Sinônimo bidirecional](assets/synonym-two-way.png)

### Sinônimo unidirecional

1. Clique no tipo de sinônimo **Unidirecional**.

   ![Adicionar sinônimo unidirecional](assets/synonym-add-one-way.png)

1. Insira os termos da **Palavra-chave** e da **Expansão**. Separe vários termos com uma vírgula.

   ![Exemplo de sinônimo unidirecional](assets/synonym-add-one-way-example.png)

   Neste exemplo, a palavra-chave é &quot;calças&quot; e os termos de expansão unidirecional &quot;capris, peddle-pushers&quot; são um subconjunto de &quot;calças&quot;, mas com um significado específico.

1. Quando terminar, clique em **Salvar**.
O conjunto de sinônimos aparece na lista com uma seta unidirecional apontando dos termos de expansão para a palavra-chave para indicar que os termos são subconjuntos da palavra-chave. Um sinal de mais separa cada termo de expansão.

   ![Sinônimo unidirecional](assets/synonym-one-way.png)

## Etapa 3: publicar alterações

1. Quando seus sinônimos estiverem completos, clique em **Publicar alterações**.
1. Aguarde até duas horas para que suas atualizações fiquem disponíveis na loja.

## Descrições de campo

| Campo | Descrição |
|--- |--- |
| [Tipo](synonyms.md) | Determina se os sinônimos têm o mesmo significado que a palavra-chave ou se são um subconjunto da palavra-chave. Opções:<br />Bidirecional (padrão) - Termos que têm o mesmo significado que a palavra-chave e retornam os mesmos resultados de pesquisa<br />Unidirecional - Termos que são um subconjunto da palavra-chave. Sinônimos unidirecionais retornam uma lista mais restrita de produtos específicos. |
| Palavra-chave | Uma palavra que é comumente associada a uma seleção de produtos em seu catálogo. |
| Expansão | Termos adicionais que têm o mesmo significado ou significado semelhante à palavra-chave. |
