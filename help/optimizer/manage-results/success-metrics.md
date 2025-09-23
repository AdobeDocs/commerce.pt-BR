---
title: Métricas de sucesso
description: Métricas de sucesso fornecem o insight para as métricas principais de desempenho da sua loja  [!DNL Adobe Commerce Optimizer] .
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
source-git-commit: 497f5e887d987435d57a340ef16fcfa561edc545
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Métricas de sucesso

Esta página fornece uma visão geral das métricas principais de desempenho do armazenamento [!DNL Adobe Commerce Optimizer]. O objetivo é que você entenda rapidamente os resultados da implementação do [!DNL Adobe Commerce Optimizer], depois ajude você e sua equipe a identificar oportunidades de crescimento e a destacar áreas para otimização.

![Relatório de métricas de sucesso](../assets/success-metrics.png)

As métricas no relatório são extraídas dos dados do evento da loja. [Saiba mais](../setup/events/overview.md) sobre os dados de evento coletados.

## Noções básicas sobre suas métricas

O relatório de métricas de sucesso fornece insights acionáveis em cinco áreas principais de desempenho que afetam diretamente os resultados de seus negócios. Cada métrica revela padrões de comportamento do cliente e armazena desempenho que ajudam a descobrir oportunidades e enfrentar desafios. Aproveite esses insights para tomar decisões mais inteligentes e otimizar sua experiência comercial.

**Principais destaques** resume as métricas principais de cada área de desempenho. Use esta seção para identificar rapidamente suas maiores oportunidades de melhoria.

Os principais indicadores de desempenho são:

- **Receita** — Sua métrica financeira principal que mostra o desempenho total das vendas.
- **Conversão** — A porcentagem de visitantes que concluíram compras.
- **Envolvimento** — como os usuários interagem ativamente com o seu site.
- **Aquisição** — a eficácia dos esforços de aquisição de clientes.
- **Taxa de Rejeição** — A porcentagem de visitantes que sai depois de visualizar apenas uma página.

## Gerar um relatório

1. No painel esquerdo, selecione **Métricas de sucesso**.
1. Em **Configuração do Relatório**, especifique o **Intervalo de datas**, **Origem do catálogo**, com base na sua configuração de localidade e **Moeda**.
1. Clique em **[!UICONTROL Apply]**.

   Os **Principais Destaques**, **Receita**, **Conversão**, **Envolvimento**, **Aquisição** e **Taxa de devolução** são atualizações com base na configuração do seu relatório.

1. Clique em **[!UICONTROL Export]** para salvar o relatório como uma PDF.

## Próximas etapas e estratégias de otimização

Use seus dados de métricas de sucesso para identificar oportunidades de melhoria e implementar estratégias de otimização direcionadas. As seções a seguir fornecem orientação específica e acionável para cada área de métrica.

### Otimização da receita

Para a receita, seu objetivo é aumentar o valor total de vendas e o valor médio de pedido.

![Receita das métricas de sucesso](../assets/revenue.png)

#### Estratégias

- **Implementar recomendações alimentadas por IA**: use o mecanismo de recomendação do otimizador para exibir produtos relevantes que impulsionam taxas de conversão mais altas. Implante *os clientes que viram isto também viram* e *Compraram isto, compraram aquilo* tipos de recomendações para aumentar as oportunidades de vendas cruzadas.

- **Criar regras de merchandising**: impulsione produtos de altas margens nos resultados da pesquisa usando [regras de merchandising](../merchandising/rules/overview.md). Fixe itens mais vendidos no topo dos resultados da pesquisa para consultas de alto tráfego.

- **Otimizar a descoberta de produtos**: use [facetas inteligentes](../merchandising/facets/overview.md) para ajudar os clientes a encontrar produtos com mais eficiência, resultando em taxas de conversão mais altas e aumento de receita.

- **Aproveite as oportunidades sazonais**: crie regras de merchandising baseadas em tempo para promover itens sazonais ou promocionais durante os períodos de pico de compras.

### Melhoria do índice de conversão

Para melhorar o índice de conversão, seu objetivo é converter mais visitantes em clientes.

![Taxa de conversão de métricas de sucesso](../assets/conversion-rate.png)

#### Estratégias

- **Otimizar relevância da pesquisa**: implemente [sinônimos](../merchandising/synonyms/overview.md) para garantir que os clientes encontrem o que estão procurando, mesmo com termos de pesquisa diferentes. Use facetas dinâmicas para fornecer opções de filtragem relevantes.

- **Posicionamento de recomendação estratégica**: implante unidades de recomendação em páginas de alto tráfego, como páginas de detalhes do produto e páginas de categoria. Use as recomendações *Mais visualizados* e *Mais comprados* para criar confiança e urgência.

- **Melhore a visibilidade do produto**: use as regras de merchandising para garantir que os produtos com mais vendas e de alta conversão apareçam de forma destacada nos resultados da pesquisa.

- **Tipos de recomendação de teste A/B**: experimente com diferentes tipos e disposições de recomendação para encontrar o que funciona melhor para seu público-alvo.

### Aprimoramento de engajamento

Para aprimorar o engajamento, sua meta é aumentar a interação com o cliente e o tempo no local.

![Engajamento nas métricas de sucesso](../assets/engagement.png)

#### Estratégias

- **Diversificar tipos de recomendação**: Evite mostrar as mesmas recomendações repetidamente. Use uma combinação de *Recomendado para você*, *Tendências* e *Visualizado recentemente* para manter o conteúdo atualizado e envolvente.

- **Implementar pesquisa inteligente**: use facetas dinâmicas orientadas por IA e reclassificação de resultados para adaptar os resultados da pesquisa em tempo real com base no comportamento do comprador.

- **Criar experiências personalizadas**: implante unidades &quot;Recomendado para você&quot; na página inicial e em toda a jornada do cliente para fornecer sugestões personalizadas de produtos.

- **Otimizar experiência de pesquisa**: use sinônimos para melhorar a relevância da pesquisa e garantir que os clientes encontrem o que estão procurando rapidamente.

### Crescimento da aquisição

Para adquirir mais crescimento, seu objetivo é atrair mais clientes novos e melhorar a eficiência da aquisição.

![Aquisição de métricas de sucesso](../assets/acquisition.png)

#### Estratégias

- **Aproveite os dados de desempenho da pesquisa**: use o relatório de [desempenho da pesquisa](../manage-results/search-performance.md) para identificar produtos de tendência e termos de pesquisa populares. Crie regras de merchandising para destacar esses itens.

- **Otimizar o desempenho da recomendação**: Monitore as [métricas de desempenho da recomendação](../manage-results/recommendation-performance.md) para identificar quais tipos de recomendação direcionam mais tráfego e conversões.

- **Realçar itens novos e promocionais**: use as regras de merchandising para impulsionar novos produtos ou itens promocionais nos resultados da pesquisa para atrair a atenção de novos visitantes.

- **Rastrear fontes de tráfego**: use os dados do evento para entender quais canais proporcionam o tráfego mais valioso e otimizam adequadamente seus esforços de marketing.

### Redução da taxa de rejeição

Para reduzir a taxa de rejeição, seu objetivo é manter os visitantes envolvidos e reduzir as visitas de página única.

![Taxa de rejeição das métricas de sucesso](../assets/bounce-rate.png)

#### Estratégias

- **Melhore a relevância da pesquisa**: use sinônimos e facetas inteligentes para garantir que os clientes encontrem produtos relevantes rapidamente. Resultados de pesquisa inadequados são a principal causa de altas taxas de rejeição.

- **Implementar unidades de recomendação**: implante unidades de recomendação nas páginas de categoria e resultados da pesquisa para fornecer opções de produto adicionais e manter os visitantes envolvidos.

- **Otimizar descoberta de produto**: use as regras de merchandising para garantir que os produtos mais relevantes e populares apareçam primeiro nos resultados da pesquisa.

- **Criar experiências envolventes na página inicial**: Use os tipos de recomendação &quot;Recomendado para você&quot; e &quot;Em tendência&quot; na página inicial para envolver imediatamente os visitantes com conteúdo relevante.

## Solução de problemas e otimização

### Quando as métricas estão em declínio

**Receita em declínio**:

- Verifique se as unidades de recomendação ainda estão ativas e apresentando bom desempenho
- Revisar as regras de merchandising para garantir que produtos com altas margens sejam promovidos
- Analise o desempenho da pesquisa para identificar se os produtos populares ainda estão bem classificados

**Descarte da taxa de conversão**:

- Verificar se a relevância da pesquisa é mantida (verificar sinônimos e aspectos)
- Verifique se as unidades de recomendação estão sendo exibidas corretamente
- Revisar as regras de merchandising para conflitos ou problemas

**Altas taxas de rejeição**:

- Verifique a relevância dos resultados da pesquisa e implemente sinônimos se necessário
- Verifique se as unidades de recomendação estão sendo carregadas corretamente
- Revisar a qualidade e a disponibilidade dos dados do produto

**Baixo envolvimento**:

- Diversificar tipos de recomendações para evitar a fadiga do cliente
- Implementar estratégias de recomendação mais personalizadas
- Otimizar a experiência de pesquisa com melhores aspectos e sinônimos

## Descrições dos campos

### Configuração do relatório

| Campo | Descrição |
|---|---|
| Intervalo de datas | As opções incluem **Últimos 3 meses**, **Últimos 7 dias**, **Últimos 30 dias**, **Últimos 6 meses**, **Últimos 12 meses** e **Ano até a data**. Use intervalos mais curtos para insights de otimização imediata e intervalos mais longos para análise de tendências. |
| País | Com base na origem de catálogo especificada para a sua [exibição de catálogo](../setup/catalog-view.md). Selecione o mercado apropriado para uma análise de desempenho precisa. |
| Moeda | A moeda especificada para a exibição do catálogo. Verifique se isso corresponde ao mercado alvo para obter relatórios precisos de receita. |
| Exportar | Salva o relatório como um PDF para compartilhamento com as partes interessadas ou análise offline. |

## Veja mais aqui

- [Desempenho da pesquisa](../manage-results/search-performance.md) - Analise os termos de pesquisa e otimize a relevância da pesquisa
- [Desempenho de recomendação](../manage-results/recommendation-performance.md) - Monitore e otimize a eficácia da recomendação
- [Visão geral das recomendações](../merchandising/recommendations/overview.md) - Saiba mais sobre as recomendações de produtos alimentados por IA
- [Regras de merchandising](../merchandising/rules/overview.md) - Aumente, interrompa, fixe ou oculte produtos nos resultados da pesquisa
- [Facetas](../merchandising/facets/overview.md) - Aprimorar a pesquisa com filtragem inteligente
- [Sinônimos](../merchandising/synonyms/overview.md) - Melhore a relevância da pesquisa e a experiência do cliente
- [Visão geral dos eventos](../setup/events/overview.md) - Entenda os dados que alimentam suas métricas
