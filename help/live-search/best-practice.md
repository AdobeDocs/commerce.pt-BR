---
title: Práticas recomendadas do [!DNL Live Search]
description: Conheça as práticas recomendadas para implementar o [!DNL Live Search] em sua loja.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 0%

---

# Práticas recomendadas

Este artigo ajuda os merchandisers a aprimorar a funcionalidade de pesquisa do site, garantindo uma experiência perfeita e eficiente do comprador que maximize as taxas de conversão. Seguindo as estratégias descritas, você aprenderá a implementar recursos de pesquisa avançada e a refinar continuamente sua ferramenta de pesquisa para obter o desempenho ideal com o Adobe Commerce [!DNL Live Search].

Há vários fatores principais que determinam a relevância e a eficácia dos resultados da pesquisa:

- Dados de produtos bem estruturados garantem que os algoritmos de pesquisa possam corresponder de forma eficaz os produtos às consultas. Dados de produtos de baixa qualidade resultam em resultados de pesquisa relevantes insuficientes. Para afetar diretamente o sucesso de sua estratégia de merchandising:
   - Configure os atributos corretos como pesquisáveis com seu peso correspondente.
   - Verifique se os dados nesses atributos são relevantes.
- Uma experiência de pesquisa bem projetada cria confiança com os clientes e inspira confiança de que encontrarão o que precisam.
- As regras de pesquisa são críticas, pois podem elevar a visibilidade de determinados produtos com base em popularidade, novos concorrentes, critérios promocionais ou qualquer outra estratégia de merchandising para atender aos requisitos da sua empresa.
- A navegação facetada permite que os compradores refinem sua pesquisa e obtenham resultados relevantes rapidamente.

Para gerenciar o [!DNL Live Search], vá para **Marketing** > *SEO e Pesquisa* > **[!DNL Live Search]** no Administrador do Adobe [!DNL Commerce]. 

## Otimizar a funcionalidade de pesquisa

Nesta seção, você aprenderá a otimizar sua funcionalidade de pesquisa usando recursos como preenchimento automático para fornecer sugestões em tempo real, como tipo de comprador, sinônimos e ortografias, para garantir que os compradores encontrem produtos mesmo que usem palavras diferentes, facetas para permitir que os compradores restrinjam os resultados de pesquisa e redirecionem os compradores automaticamente de uma consulta de pesquisa para uma página específica.

### Preenchimento automático

O recurso de autocompletar, também conhecido como type-ahead ou autosuggestions, é um recurso de pesquisa interativa que exibe dinamicamente sugestões para os compradores à medida que eles inserem seus termos de pesquisa. Isso ajuda os compradores a encontrar produtos de maneira rápida e fácil, oferecendo sugestões em tempo real com base em suas informações.

O widget [!DNL Live Search] [[!DNL popover]](storefront-popover.md) habilita as opções de preenchimento automático de pesquisa para sugerir produtos populares. Com cada caractere digitado pelo comprador, o popover é atualizado com produtos sugeridos e imagens em miniatura dos principais resultados da pesquisa.

[!DNL Live Search] começa a retornar resultados quando o usuário digita dois caracteres. Para uma correspondência parcial, o número máximo de caracteres por palavra é 20. O número de caracteres em uma consulta &quot;pesquisar ao digitar&quot; não é configurável.

Saiba mais sobre o widget [popover](storefront-popover.md).

### Sinônimos e erros ortográficos

O Live Search gerencia erros ortográficos por padrão. Você pode configurar sinônimos para incluir palavras que os compradores podem usar que diferem das palavras especificadas em seu catálogo. Você não quer perder uma venda porque alguém está procurando um &quot;sofá&quot;, enquanto seu produto está listado como um &quot;sofá&quot;. Você pode capturar uma ampla variedade de termos de pesquisa inserindo todas as palavras possíveis que os clientes podem usar para encontrar seus produtos. Você pode [definir sinônimos como unidirecionais ou bidirecionais](synonyms-add.md#step-2-define-the-synonym-by-type) para melhorar os resultados.

#### Dicas para otimizar sinônimos

- Mapeie os nomes de marcas e abreviações para seus nomes completos, por exemplo &quot;HP&quot; para &quot;Hewlett-Packard&quot; e apelidos de produtos comuns, por exemplo &quot;iPhone&quot; para &quot;Apple iPhone&quot;.
- Inclua jargões específicos do setor e termos que os compradores podem usar alternadamente, por exemplo &quot;tênis&quot; e &quot;tênis de corrida&quot;.
- Atualize regularmente a lista de sinônimos com base em novas tendências de pesquisa, adições de produtos e comportamento do comprador.
- Teste a eficácia dos mapeamentos de sinônimos analisando os resultados da pesquisa e o feedback do comprador. Refine mapeamentos para melhorar a precisão e a relevância.

Saiba mais sobre sinônimos:

- [Tipos de sinônimos](synonyms-type.md)
- [Criar sinônimos](synonyms-add.md)
- [Gerenciar sinônimos](synonyms-manage.md)
- [Suporte de idioma](settings.md#language)

### Facetas

A funcionalidade de filtro e faceta é um componente crítico do site [!DNL Commerce], projetada para aprimorar a experiência do comprador permitindo que ele restrinja os resultados da pesquisa e localize produtos com mais eficiência. Essa funcionalidade ajuda os compradores a classificar grandes catálogos de itens aplicando critérios específicos, tornando o processo de compra mais rápido, fácil e satisfatório. Ao implementar filtros e facetas eficazes e fáceis de comprar, você pode ajudar os clientes a encontrar exatamente o que precisam de maneira rápida e eficiente, aumentando, em última análise, as taxas de satisfação e conversão.

Para configurar um atributo de produto como uma faceta, ele deve ter as seguintes [propriedades definidas](facets-add.md#step-1-add-a-facet):

- **[!UICONTROL Use in Search]** -  `Yes`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

#### Dicas para otimizar aspectos

- Determine os atributos mais relevantes e úteis para seus produtos, como título, categoria, marca, faixa de preços, cor e tamanho, e defina-os como [facetas dinâmicas](facets-type.md). 
- Defina e classifique atributos de produto que sejam consistentes em todo o catálogo e altamente relevantes para seus produtos, a fim de melhorar a relevância e os recursos de filtragem para seus compradores.
- Verifique se os rótulos de facetas são fáceis de entender e nomeados de forma consistente em todo o site. Por exemplo, use &quot;Intervalo de preços&quot; em vez de &quot;Custo&quot;.
- Evite sobrecarregar os compradores, limitando o número de facetas às mais importantes. Muitas opções podem causar fadiga de decisão. Por padrão, [!DNL Live Search] está limitado a no máximo 100 atributos configurados como facetas e 30 compartimentos retornados em cada faceta. Saiba mais sobre [limitações de facetas](boundaries-limits.md#facets). 
- Permite que os compradores selecionem vários critérios de filtro simultaneamente para refinar os resultados. Por exemplo, permitir que os compradores selecionem as cores &quot;Vermelho&quot; e &quot;Azul&quot;.
- Exiba o número de produtos disponíveis ao lado de cada opção de faceta para dar aos compradores uma ideia dos resultados de pesquisa que eles podem esperar.
- Implemente seções de facetas recolhíveis para manter a interface limpa e gerenciável, especialmente em dispositivos móveis.
- Permita que os compradores redefinam facilmente facetas individuais ou todos os filtros selecionados para iniciar uma nova pesquisa.

Saiba mais sobre aspectos:

- [Tipos de facetas](facets-type.md)
- [Adicionar facetas](facets-add.md)
- [Gerenciar facetas](facets-manage.md) (editar, fixar uma faceta, excluir, publicar)
- [Faceting de preço](settings.md#price-faceting)

### Redirecionamentos de pesquisa

Um redirecionamento de pesquisa permite redirecionar automaticamente os compradores de uma consulta de pesquisa para uma página específica. Os redirecionamentos de pesquisa podem melhorar a experiência do comprador e orientar os clientes para o conteúdo mais relevante, como uma página de produto, categoria, página de aterrissagem ou um conjunto personalizado de resultados de pesquisa. Os redirecionamentos de pesquisa ajudam a simplificar a experiência de compra e garantir que os compradores encontrem o que estão procurando de forma rápida e eficiente.

Casos de uso recomendados para configurar redirecionamentos de pesquisa:

- **Produtos ou Categorias Populares** - Redirecione os compradores para uma página ou categoria de produto específica quando eles procurarem por termos comuns ou populares. Por exemplo, a pesquisa de &quot;iPhone&quot; pode redirecionar diretamente para a página de categoria do iPhone ou para uma página de modelo específica.

- **Campanhas promocionais** - Durante eventos ou vendas promocionais, redirecione termos de pesquisa relevantes para páginas de aterrissagem que destacam ofertas especiais ou produtos em destaque.

- **Pesquisas de marca** - Quando os compradores procurarem um nome de marca, redirecione-os para a página dedicada da marca na qual todos os produtos dessa marca estão listados.

- **Descontinuação de produto** - Se um produto for descontinuado, você poderá redirecionar as pesquisas desse produto para produtos semelhantes ou para a nova versão do produto.

Sempre teste os redirecionamentos de pesquisa para garantir que estejam funcionando corretamente e levando às páginas mais relevantes. Monitore continuamente seu desempenho e faça os ajustes necessários.

Saiba como [gerenciar redirecionamentos de pesquisa](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/catalog/search/search-terms).

## Melhorar relevância dos resultados da pesquisa

Esta seção discute como melhorar a relevância dos resultados da pesquisa implementando regras de pesquisa eficazes e usando metadados de produto para garantir que atributos precisos e detalhados sejam pesquisáveis.

### Imagens

Certifique-se de que os produtos secundários dos produtos configuráveis tenham imagens com as funções corretas. Ter produtos principais ou secundários pode fazer com que o resultado da pesquisa não tenha imagens.

>[!NOTE]
>
>As imagens nos resultados da pesquisa podem ser diferentes, dependendo do termo de pesquisa. Se o termo de pesquisa determinar que um produto secundário é mais relevante, as imagens do produto secundário serão usadas em vez das imagens do produto principal.

### Pesquisar regras

Para otimizar sua taxa de conversão e receita, você deve implementar regras de pesquisa eficazes. Ajuste classificações de produtos com base em dados de vendas, níveis de estoque e promoções com o [Pesquisar merchandising](rules.md).

É crucial estabelecer uma regra de pesquisa padrão bem planejada. Sua [regra padrão](rules.md#default-rule) determina como os resultados da pesquisa são classificados e exibidos inicialmente para os compradores, melhorando sua experiência geral e aumentando a probabilidade de compra. O monitoramento e o ajuste regulares dessa regra garantem que ela continue a atender às necessidades e aos objetivos de negócios do comprador de maneira eficaz.

#### Dicas para otimizar as regras de pesquisa

- Fixar ou impulsionar produtos com altos volumes de vendas ou atividade de vendas recente.
- Priorize produtos com altas classificações e análises positivas.
- Verifique se os itens em estoque estão classificados acima.
- Priorize levemente os produtos com margens de lucro mais altas sem comprometer a relevância.
- Destaque os produtos que estão à venda ou que fazem parte de promoções especiais.
- Defina regras de pesquisa durante os períodos de promoção ou de vendas automaticamente usando o intervalo de datas durante o período de promoção.
- Personalize os resultados da pesquisa com base no comportamento individual do comprador usando [classificação inteligente](rules-add.md#intelligent-ranking), como &quot;recomendado para você&quot;, &quot;mais visto&quot; e assim por diante. Para adaptar o comportamento do comprador, você deve garantir que o evento seja implementado corretamente. Para os comerciantes da Luma, o evento está disponível e pronto para uso. Para implementações headless ou personalizadas, você deve [implementar um evento](events.md) com base nas suas necessidades específicas.

Saiba mais sobre regras de pesquisa:

- [Espaço de trabalho de merchandising](rules-workspace.md#set-the-scope)
- [Requisitos](rules.md#requirements)
- [Regra de pesquisa padrão](rules.md#default-rule)
- Gerenciar regras de pesquisa
   - [Criar](rules-add.md)
   - [Editar, exibir, excluir](rules-manage.md)
- Coleção de dados
   - [[!DNL Live Search] eventos](events.md)
   - [Coletor de Eventos da Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)
   - [Eventos do GitHub Commerce](https://github.com/adobe/commerce-events/tree/main/examples) 

### Aproveitar os metadados do produto

Verifique se atributos de produto precisos e detalhados estão [configurados como pesquisáveis](workspace.md#set-attributes-as-searchable). Observe que os atributos SKU, nome e categoria podem ser pesquisados por padrão e não podem ser excluídos da pesquisa. Para obter melhores resultados, não use espaços nas SKUs.

Para aumentar a relevância da pesquisa, atribua um peso a cada atributo pesquisável. Atributos com um peso maior devem aparecer mais altos nos resultados da pesquisa. A classificação por relevância é afetada por vários critérios, como peso da pesquisa. Isso significa que, às vezes, os atributos com menor peso de pesquisa ainda podem ter mais relevância do que os atributos com maior peso de pesquisa. Outros critérios podem incluir o número de correspondências em qualquer atributo, a posição do termo de pesquisa encontrado e a estrutura geral do texto antes e depois de um termo de pesquisa.

Verifique se cada produto tem conteúdo relevante em cada atributo pesquisável. Não é recomendável definir um atributo como pesquisável se ele tiver grandes quantidades de conteúdo, o que pode reduzir a relevância dos resultados da pesquisa.

Saiba mais sobre atributos de produto para pesquisa:

- [Definir atributos como pesquisáveis](workspace.md#set-attributes-as-searchable)
- [Atribuir peso aos atributos](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## Monitorar resultados da pesquisa

Para otimizar os resultados da pesquisa com o [!DNL Live Search], monitore os KPIs (Indicadores-chave de desempenho) relevantes, como consultas exclusivas, posição média dos cliques, taxas de click-through, taxa de conversão e taxa de resultados zero para entender como os compradores interagem com a funcionalidade da pesquisa. Esses dados o orientam a atualizar e refinar regularmente as regras de pesquisa.

Você pode monitorar esses KPIs no [!DNL Live Search] [Espaço de trabalho de desempenho](performance.md), onde encontra as seguintes métricas: 

- **Pesquisas Exclusivas** - A contagem de consultas de pesquisa distintas executadas no site [!DNL Commerce]. Cada pesquisa única é contada apenas uma vez, mesmo que seja repetida várias vezes pelo mesmo comprador ou por compradores diferentes. Essa métrica ajuda você a entender a diversidade de termos de pesquisa usados por clientes e fornece insights sobre quais produtos ou informações os compradores estão procurando. O rastreamento de pesquisas exclusivas permite:

   - Identifique tendências de pesquisa populares e itens pesquisados com frequência.
   - Detecte possíveis lacunas no catálogo ou conteúdo do produto.
   - Otimize sua funcionalidade de pesquisa adicionando [sinônimos](synonyms.md), criando ou atualizando regras de pesquisa.

- **Posição média do clique** - Indica que a posição média dos resultados da pesquisa clicados pelos compradores após executar uma consulta de pesquisa no site. Essa métrica fornece insights sobre a relevância e a eficácia dos resultados da pesquisa.

  Uma posição de clique média mais baixa (mais próxima a 1) sugere que os compradores encontrem resultados relevantes rapidamente, indicando que sua estratégia de pesquisa é eficaz. Ele ajuda você a entender o comportamento do comprador e a distância que ele está disposto a percorrer para encontrar o produto desejado. Se a posição média dos cliques for alta, isso poderá indicar que os resultados mais relevantes não estão aparecendo na parte superior, o que exige uma revisão e otimização da estratégia de pesquisa.

- **Taxa de Click-Through (CTR)** - Mede a porcentagem de compradores que clicam em um resultado de pesquisa após executar uma consulta de pesquisa. Um CTR alto indica que os resultados da pesquisa são relevantes e atraentes para os compradores, pois eles estão clicando nos resultados encontrados. O monitoramento da CTR pode ajudar a identificar áreas que precisam ser melhoradas. Baixo CTR pode sugerir que os resultados da pesquisa não correspondem à intenção do comprador, solicitando a necessidade de refinar as regras de pesquisa, aprimorar os dados do produto ou melhorar a apresentação do resultado.

- **Índice de conversão** - Indica a eficácia do recurso de pesquisa na promoção de vendas e na realização de metas comerciais. Ele reflete a eficácia geral da funcionalidade de pesquisa para atender às necessidades do comprador e facilitar uma experiência de compra tranquila. Uma alta taxa de conversão indica que os resultados da pesquisa são altamente relevantes e persuasivos, levando os compradores a concluir as compras. Se o índice de conversão for baixo, ele poderá sugerir problemas com relevância de pesquisa, disponibilidade de produto ou a jornada geral do comprador, desde a pesquisa até a compra.

- **Nenhum resultado** - Mede a porcentagem de consultas de pesquisa no site [!DNL Commerce] que não retorna resultados. Essa métrica é essencial para entender com que frequência as pesquisas dos compradores não são bem-sucedidas e pode fornecer insights sobre possíveis lacunas no catálogo de produtos ou na configuração de pesquisa. Uma alta taxa de resultados zero pode frustrar os compradores, resultando em uma experiência de compra ruim e em potencial perda de clientes. Ele pode indicar produtos ou categorias ausentes no catálogo que os compradores estão procurando, orientando as decisões de inventário e de listagem de produtos.

  Para reduzir a taxa de resultados zero, é possível:

   - Ofereça termos de pesquisa alternativos ou relacionados, como [sinônimos](synonyms.md), quando nenhuma correspondência exata for encontrada.
   - Forneça aos compradores sugestões relacionadas ou alternativas quando a pesquisa não produzir resultados definindo redirecionamentos de pesquisa.
   - Revise regularmente consultas com zero resultados para identificar padrões e fazer os ajustes necessários no catálogo de produtos e nas configurações de pesquisa.

- **Resultados Populares** - Podem melhorar significativamente os resultados da pesquisa alinhando-os às preferências e comportamentos do comprador.

Você pode usar esses dados de métrica para otimizar a funcionalidade de pesquisa das seguintes maneiras:

- Implemente regras para classificar automaticamente os produtos populares em posições mais altas nos resultados da pesquisa. Os produtos frequentemente clicados ou comprados podem ter prioridade para aparecer no topo. Prepare manualmente listas de produtos populares para consultas de pesquisa específicas e verifique se esses itens são exibidos de forma destacada.
- Destaque os produtos que estão em tendência ou que tiveram um pico de popularidade recentemente. Isso pode ser particularmente eficaz durante eventos sazonais, feriados ou períodos promocionais. Para isso, use a classificação inteligente que melhor se adapta ao seu caso de uso e às necessidades da empresa ao configurar uma regra de pesquisa.
- Destaque os filtros ou aspectos populares, caso os compradores filtrem com frequência por determinadas marcas ou intervalos de preço, torne essas opções mais proeminentes fixando esses aspectos e classificando-os de acordo.
- Quando uma pesquisa produzir zero resultado, use os dados de resultados populares para sugerir produtos alternativos ou categorias relacionadas que tenham alto engajamento do comprador.
- Analise termos de pesquisa populares e dados de produtos para identificar palavras-chave importantes. Otimize os atributos pesquisáveis do seu produto com essas palavras-chave para melhorar a relevância da pesquisa.
- Analise regularmente os dados de seus resultados para entender as tendências em constante mudança, as preferências e o comportamento do comprador, identificar os principais termos de pesquisa e detectar problemas. Use este loop de comentários para refinar e melhorar continuamente suas regras de pesquisa e ofertas de produtos

Para obter os dados corretos no relatório [!DNL Live Search], você deve garantir que o evento seja implementado corretamente. Para os comerciantes da Luma, o evento está disponível e pronto para uso. Para implementações headless ou personalizadas, você deve [implementar um evento](events.md) com base nas suas necessidades específicas.
