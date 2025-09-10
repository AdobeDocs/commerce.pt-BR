---
title: Introdução a  [!DNL Product Recommendations]
description: O [!DNL Product Recommendations] é uma poderosa ferramenta de marketing que pode ser usada para aumentar as conversões, aumentar a receita e estimular o envolvimento do comprador.
recommendations: noCatalog
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Introdução ao [!DNL Product Recommendations]

As recomendações de produto são uma poderosa ferramenta de marketing que pode ser usada para aumentar as conversões, aumentar a receita e estimular o engajamento do comprador. As recomendações de produtos do Adobe Commerce são viabilizadas pelo [Adobe Sensei](https://www.adobe.com/sensei.html), que usa inteligência artificial e algoritmos de aprendizado de máquina para executar uma análise detalhada dos dados agregados do visitante. Esses dados, quando combinados com seu catálogo do Adobe Commerce, resultam em uma experiência altamente envolvente, relevante e personalizada.

As recomendações de produto são exibidas na loja como unidades com rótulos, como &quot;Clientes que viram este produto também viram&quot;. Você pode criar, gerenciar e implantar recomendações nas visualizações da loja diretamente do administrador do Adobe Commerce.

Se sua loja for implementada com o PWA Studio, consulte a [documentação do PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se você usa uma tecnologia de front-end personalizada, como o React ou o Vue JS, saiba como [integrar](headless.md) [!DNL Product Recommendations] à sua loja headless.

>[!NOTE]
>
>Há muitas maneiras de desenvolver uma implementação headless ou personalizada. Este guia descreve uma maneira de fazer isso, usando o PWA Studio. Não abrange todos os cenários ou eventualidades.

## Privacidade

A coleta de dados para os fins de [!DNL Product Recommendations] não inclui informações pessoalmente identificáveis (PII). Além disso, todos os identificadores de usuários, como IDs de cookies e endereços IP, são estritamente anônimos. Para saber mais, consulte a [Política de Privacidade da Adobe](https://www.adobe.com/privacy/policy.html).

[!DNL Product Recommendations] usuários podem consultar o [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=pt-BR) para obter mais dados sobre a sincronização de dados.

## Recomendações de produto versus relacionamentos de produto

Dadas as complexidades em constante mudança das compras online, o que funciona melhor para sua loja geralmente é uma combinação de várias tecnologias principais. Usar as [!DNL Product Recommendations] e as [Relações de Produto](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=pt-BR) oferece mais flexibilidade ao promover produtos. Você pode usar o [!DNL Product Recommendations] da tecnologia do Adobe Sensei para automatizar de forma inteligente suas recomendações em escala. Em seguida, você poderá aproveitar as [Regras de Produto Relacionadas](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=pt-BR) quando precisar intervir manualmente e garantir que uma recomendação específica esteja sendo feita a um segmento de comprador de destino ou quando determinadas metas comerciais precisarem ser atendidas.

As recomendações de produto permitem:

- Escolha entre nove tipos de recomendações inteligentes distintos com base nas seguintes áreas: com base no comprador, com base em item, com base em popularidade, tendência e com base em similaridade
- Use dados comportamentais para personalizar recomendações na jornada da loja do comprador
- Avalie as métricas principais relevantes para cada recomendação para ajudar você a entender o impacto de suas recomendações

## Demonstração do [!DNL Product Recommendations]

Assista a este vídeo para saber mais sobre [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/3449963?quality=12&captions=por_br)

## Política de retenção de dados do catálogo

Se você não enviar uma consulta para os dados do catálogo no ambiente de teste por 90 dias consecutivos, os dados do catálogo serão definidos para o modo de hibernação e nenhum dado será retornado para nenhuma consulta. Os dados do catálogo em seu ambiente de produção não são afetados por essa política.

Para reativar os dados do catálogo no ambiente de teste, [envie uma solicitação de suporte](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) com o título: &quot;Reativar [!DNL Product Recommendations]&quot; e incluir as IDs de ambiente. Os dados do catálogo no ambiente de teste devem ser restaurados em algumas horas.
