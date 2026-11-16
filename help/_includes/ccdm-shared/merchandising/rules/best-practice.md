---
source-git-commit: 4032a0871d0a9b129ad870c93f62a2a7596ea8b7
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Práticas recomendadas das regras de merchandising

Para otimizar a conversão e a receita, implemente **regras de pesquisa** efetivas, uma **regra de listagem padrão** forte e **[regras de categoria](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types)**. Ajuste classificações usando dados de vendas, estoque, promoções e [classificação inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking).

É crucial estabelecer uma **regra padrão** bem-pensada. Sua [regra padrão](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#default-rule) determina como os resultados da pesquisa são classificados inicialmente quando nenhuma regra de pesquisa mais específica se aplica, o que melhora a probabilidade de descoberta e compra. Analise-o regularmente para que ele acompanhe as necessidades e campanhas do comprador.

## Dicas para otimizar as regras de pesquisa

- Fixar ou impulsionar produtos com altos volumes de vendas ou atividade de vendas recente.
- Priorize produtos com altas classificações e análises positivas.
- Verifique se os itens em estoque estão classificados acima.
- Priorize levemente os produtos com margens de lucro mais altas sem comprometer a relevância.
- Destaque os produtos que estão à venda ou que fazem parte de promoções especiais.
- Defina regras de pesquisa durante os períodos de promoção ou de vendas automaticamente usando o intervalo de datas durante o período de promoção.
- Personalize os resultados da pesquisa com base no comportamento individual do comprador usando [classificação inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking), como &quot;recomendado para você&quot;, &quot;mais visto&quot; e assim por diante.
- Quando uma estratégia inteligente diferente de **Nenhuma** for selecionada, ajuste o **[Aumento de classificação inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** por regra e valide em **Testar sua regra** antes de publicar.
- Sempre use o painel &quot;Testar a regra&quot; para visualizar como sua estratégia de classificação inteligente afeta os resultados reais da pesquisa para consultas diferentes.

## Dicas para regras de categoria

- Use as [regras de categoria](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types) em **páginas de categoria** de tráfego alto ou margem alta, em que a ordem com curadoria é importante tanto quanto a pesquisa, por exemplo, coleções sazonais ou departamentos em destaque.
- Alinhe a **classificação inteligente** (por exemplo, tendência, mais visualizada) com a forma como os compradores navegam nessa categoria; as páginas de categoria não usam o texto de consulta de pesquisa da mesma forma que as regras de pesquisa. Consulte [Classificação inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking). Para métodos inteligentes diferentes de **Nenhum**, use **[Aumento inteligente de classificação](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** e pré-visualização de categoria para ajustar a intensidade comportamental dessa regra de categoria.
- Aplique o **pin**, **boost** e **bury** de forma consistente com o plano de campanha; lembre-se de que as posições manuais geralmente se aplicam somente quando o comprador usa a **classificação padrão** para a lista. Consulte [Classificação manual](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#manual-ranking).
- Visualize no fluxo de regras da **categoria** no editor e valide na loja após a publicação, a mesma disciplina usada para o painel &quot;Testar sua regra&quot; na pesquisa.
