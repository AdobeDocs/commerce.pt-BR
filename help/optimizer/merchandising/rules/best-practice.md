---
title: Práticas recomendadas das regras de merchandising
description: Saiba mais sobre as práticas recomendadas para implementar regras de merchandising para páginas de pesquisa, listagens padrão e categoria.
role: Admin, Developer
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Práticas recomendadas das regras de merchandising

Para otimizar a conversão e a receita, implemente **regras de pesquisa** efetivas, uma **regra de listagem padrão** forte e **[regras de categoria](add.md#rule-types)** (beta). Ajuste classificações usando dados de vendas, estoque, promoções e [classificação inteligente](add.md#intelligent-ranking).

É crucial estabelecer uma **regra padrão** bem-pensada. Sua [regra padrão](overview.md#default-rule) determina como os resultados da pesquisa são classificados inicialmente quando nenhuma regra de pesquisa mais específica se aplica, o que melhora a probabilidade de descoberta e compra. Analise-o regularmente para que ele acompanhe as necessidades e campanhas do comprador.

## Dicas para otimizar as regras de pesquisa

- Fixar ou impulsionar produtos com altos volumes de vendas ou atividade de vendas recente.
- Priorize produtos com altas classificações e análises positivas.
- Verifique se os itens em estoque estão classificados acima.
- Priorize levemente os produtos com margens de lucro mais altas sem comprometer a relevância.
- Destaque os produtos que estão à venda ou que fazem parte de promoções especiais.
- Defina regras de pesquisa durante os períodos de promoção ou de vendas automaticamente usando o intervalo de datas durante o período de promoção.
- Personalize os resultados da pesquisa com base no comportamento individual do comprador usando [classificação inteligente](add.md#intelligent-ranking), como &quot;recomendado para você&quot;, &quot;mais visto&quot; e assim por diante.
- Sempre use o painel &quot;Testar a regra&quot; para visualizar como sua estratégia de classificação inteligente afeta os resultados reais da pesquisa para consultas diferentes.

## Dicas para regras de categoria

>[!IMPORTANT]
>
>As regras de categoria estão na versão beta.

- Use as [regras de categoria](add.md#rule-types) em **páginas de categoria** de tráfego alto ou margem alta, em que a ordem com curadoria é importante tanto quanto a pesquisa, por exemplo, coleções sazonais ou departamentos em destaque.
- Alinhe a **classificação inteligente** (por exemplo, tendência, mais visualizada) com a forma como os compradores navegam nessa categoria; as páginas de categoria não usam o texto de consulta de pesquisa da mesma forma que as regras de pesquisa. Consulte [Classificação inteligente](add.md#intelligent-ranking).
- Aplique o **pin**, **boost** e **bury** de forma consistente com o plano de campanha; lembre-se de que as posições manuais geralmente se aplicam somente quando o comprador usa a **classificação padrão** para a lista. Consulte [Classificação manual](add.md#manual-ranking).
- Visualize no fluxo de regras da **categoria** no editor e valide na loja após a publicação, a mesma disciplina usada para o painel &quot;Testar sua regra&quot; na pesquisa.
