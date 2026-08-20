---
title: O que são recomendações de produtos?
description: Saiba mais sobre Recomendações de produto no Adobe Commerce. Descubra unidades de vitrine orientadas por IA, privacidade, caminhos de administração e vitrine e retenção de dados principais.
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
TQID: https://experienceleague.adobe.com/kRTCG6D5k17Ah-1Q-XNZq4o48xqIwlpI8vDQJDTEeoU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bbbea26f-9621-49eb-9ab8-e06fb3bbce8cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 84cd0deaecda0790f9f123fc663d4db7b048746b
workflow-type: tm+mt
source-wordcount: 744
ht-degree: 0%

---

# O que são [!DNL Product Recommendations]?

O [!DNL Product Recommendations] ajuda você a mostrar recomendações de produto personalizadas nas vitrines da Adobe Commerce usando o [Adobe AI](https://business.adobe.com/ai.html) e o aprendizado de máquina em comportamentos agregados de compradores e no seu catálogo. Essa visão geral abrange restrições de serviço (incluindo HIPAA), dados e privacidade, onde as unidades de recomendação são exibidas, caminhos de implementação da loja, como as recomendações complementam os relacionamentos com os produtos e a retenção de dados do catálogo.

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]não é um serviço pronto para HIPAA.** Não habilite ou use o [!DNL Product Recommendations] em nenhuma implementação do Adobe Commerce que use a oferta pronta para HIPAA ou que processe informações de integridade protegidas (PHI) de outra forma. [!DNL Product Recommendations] faz parte dos serviços SaaS da Commerce que estão classificados como prontos para não HIPAA.
>
>Para obter detalhes sobre quais recursos do Adobe Commerce estão prontos para HIPAA e quais serviços não devem ser usados com PHI, consulte [Preparação para HIPAA no Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) e [Operações](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

## Manuseio e privacidade de dados

A coleta de dados de [!DNL Product Recommendations] não inclui informações pessoalmente identificáveis (PII). Todos os identificadores de usuário, como IDs de cookies e endereços IP, são estritamente anônimos. Para saber mais, consulte a [Política de Privacidade da Adobe](https://www.adobe.com/privacy/policy.html).

Para obter mais informações sobre a sincronização de dados, consulte o [Painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard).

## Onde as recomendações são exibidas

As recomendações aparecem na loja como unidades com rótulos, como &quot;Clientes que visualizaram este produto também visualizaram&quot;. Você pode criar, gerenciar e implantar recomendações nas visualizações da loja com o Administrador do Adobe Commerce. Se o seu projeto do Commerce usa o [Adobe Commerce Optimizer Connector](https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/overview), você criará, gerenciará e implantará recomendações por meio do [Adobe Commerce Optimizer](../optimizer/overview.md).

## Implementações da loja

Escolha a documentação que corresponde à loja:

- **PWA Studio** — [Documentação do PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **Front-ends personalizados (por exemplo, React ou Vue.js)** — [Integrar [!DNL Product Recommendations]](headless.md) em uma loja headless
- **Commerce Edge Delivery Services (EDS)** — [Documentação da Adobe Commerce Storefront para EDS](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)

>[!NOTE]
>
>As configurações headless e personalizadas variam de acordo com a pilha. Essa área de produtos documenta um caminho PWA Studio e um padrão geral de integração headless; não abrange todos os cenários de terceiros ou personalizados.

## Recomendações de produto versus relacionamentos de produto

Dadas as complexidades em constante mudança das compras online, o que funciona melhor para sua loja geralmente é uma combinação de várias tecnologias principais. Usar as [!DNL Product Recommendations] e as [Relações de Produto](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships) oferece mais flexibilidade ao promover produtos. Você pode usar o [!DNL Product Recommendations] da tecnologia do Adobe AI para automatizar de forma inteligente suas recomendações em escala. Em seguida, você poderá aproveitar as [Regras de Produto Relacionadas](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules) quando precisar intervir manualmente e garantir que uma recomendação específica esteja sendo feita a um segmento de comprador de destino ou quando determinadas metas comerciais precisarem ser atendidas.

As recomendações de produto permitem:

- Escolha entre nove tipos de recomendações inteligentes distintos com base nas seguintes áreas: com base no comprador, com base em item, com base em popularidade, tendência e com base em similaridade
- Use dados comportamentais para personalizar recomendações na jornada da loja do comprador
- Avalie as métricas principais relevantes para cada recomendação para ajudar você a entender o impacto de suas recomendações

## Demonstração das recomendações de produto

Assista a este vídeo para saber mais sobre [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## Política de retenção de dados do catálogo

O serviço [!DNL Product Recommendations] depende de dados de catálogo que permanecem sincronizados com seu ambiente do Adobe Commerce. Catálogos ou ambientes inativos que param de consultar esses dados podem entrar em hibernação, o que afeta o que o serviço retorna até que você reative.

Se você não enviar uma consulta para os dados do catálogo no ambiente **teste** por 90 dias consecutivos, os dados do catálogo serão definidos para o modo de hibernação e nenhum dado será retornado para nenhuma consulta. Os dados do catálogo no ambiente de **produção** não são afetados pela regra de 90 dias.

Se o ambiente tiver um **catálogo vazio** 45 dias após a criação, os dados do catálogo serão definidos para o modo de hibernação e nenhum dado será retornado para qualquer consulta. Isso se aplica aos ambientes de produção e teste.

### Reativar dados do catálogo

Para restaurar os dados do catálogo após a hibernação, [envie uma solicitação de suporte](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#experience-league-start-page) com o título &quot;Reativar [!DNL Product Recommendations]&quot; e inclua as IDs de ambiente. Os dados do catálogo devem ser restaurados em algumas horas.
