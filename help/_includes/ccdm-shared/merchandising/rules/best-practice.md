---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
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

Use as [regras de supressão de pesquisa](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules) somente quando as consultas do comprador correspondentes precisarem retornar zero produtos, e não quando os produtos precisarem de uma classificação diferente.

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

## Pesquisar práticas recomendadas de supressão e casos de uso {#search-suppression-best-practices}

Uma regra de supressão de pesquisa bloqueia os resultados de consultas que correspondem a suas condições, para que a loja exiba uma página de resultados de pesquisa com zero produtos. O editor de regras não fornece uma pré-visualização das regras de supressão. Use a condição mais restrita que atenda à restrição e siga [Criar e gerenciar regras de supressão de pesquisa](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules). Depois que a regra se tornar ativa, verifique as pesquisas correspondentes e não correspondentes na loja. Verifique a apresentação sem resultados real da loja.

| Caso de uso | Configuração sugerida | O que verificar |
| --- | --- | --- |
| Conformidade normativa para pesquisa | Determine o escopo da regra para a exibição de catálogo afetada e corresponda aos termos de pesquisa restritos. | Confirme os termos com a equipe de conformidade. A supressão de pesquisa por si só não impede o acesso por meio da navegação de categoria, páginas de merchandising, recomendações ou URLs diretas do produto. |
| Restrições de marca | Usar **Consulta contém** quando um nome de marca restrito deve ser bloqueado em consultas mais longas. | Depois que a regra se tornar ativa, verifique as consultas não relacionadas da loja que contêm texto semelhante para evitar a supressão de pesquisas legítimas. |
| Impedir que um termo de pesquisa específico retorne resultados | Use **A consulta** para obter uma frase exata que não deve retornar nenhum produto. | Verifique separadamente as frases relacionadas. Uma condição de correspondência exata não bloqueia todas as consultas que contenham essa frase. |
| Restrições em prefixos ou sufixos de consulta | Usar **Consulta começa com** ou **Consulta termina com** quando o local do texto restrito for importante. | Depois que a regra se tornar ativa, verifique as consultas da loja com o texto no início, no meio e no fim para confirmar o escopo desejado. |
| Restrições temporárias de pesquisa | Defina uma data de início e término para uma restrição de tempo limitado. | Confirme a programação e o status ativado e verifique se a regra ainda é necessária após o término da restrição. |

- Dê um nome descritivo a cada regra e registre o motivo da restrição em sua descrição.
- Revise as condições de consulta antes de publicar as alterações. Depois que a regra se tornar ativa, verifique as consultas da loja que devem ser bloqueadas e as consultas que ainda devem retornar produtos. Os resultados da consulta em cache podem levar até 15 minutos para serem atualizados.
- Revise o estado sem resultados da loja e verifique se os compradores têm uma maneira útil de continuar navegando, como revisar a consulta ou navegar para uma categoria, onde suportado pela loja.
- Não use a supressão de consultas como um substituto para exclusões no nível do produto. Para excluir produtos entre resultados de pesquisa, sugestões de pesquisa e preenchimento automático, use exclusões manuais ou **Eventos de Merchandising baseados em atributos** com uma ação **Ocultar** na **regra de pesquisa padrão**.
- Revise as regras de supressão ativas regularmente. Desative as regras que não são mais necessárias ou edite-as e publique-as quando as restrições forem alteradas.
