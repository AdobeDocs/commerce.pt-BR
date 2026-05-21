---
title: Teste no ambiente de preparo
description: Saiba como usar o [!DNL Product Recommendations] do seu ambiente de produção no seu ambiente de preparo para fins de teste.
feature: Services, Recommendations, Staging
exl-id: 5b6d7615-6021-4419-98ea-006c8a299fe4
TQID: https://experienceleague.adobe.com/7e7e3T-vgkN-Pbqx6TwrBAWTEozhzS0h--tguOGe0yI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: null
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# Teste no ambiente de preparo

Antes de implantar recomendações em seu ambiente de produção, teste o serviço em um ambiente que não seja de produção para garantir que tudo esteja funcionando como o esperado.

[!DNL Product Recommendations] retorna produtos com base em [dados comportamentais do comprador](events.md) coletados de sua loja. No entanto, em um ambiente de não produção, é provável que você não tenha dados comportamentais de compradores. O único tipo de recomendação que você pode testar sem dados comportamentais é `More like this`. Esse tipo de recomendação não requer dados de entrada, pois usa uma correspondência direta de similaridade de conteúdo.

Os seguintes tipos de recomendações exigem dados comportamentais:

- Mais visualizados
- Visualizou isto, visualizou aquilo
- Comprei isto, comprei aquilo

Como você pode testar suas recomendações em um ambiente de não produção usando dados comportamentais? Há algumas opções.

## Buscar recomendações do ambiente de produção (recomendado)

O Adobe Commerce permite que você busque recomendações de seu ambiente de produção e as visualize em seu ambiente de não produção ao [alternar](settings.md) o espaço de dados SaaS.

Para buscar recomendações do seu ambiente de produção, você deve se certificar de que:

- A coleção de dados da vitrine está [configurada e habilitada](install-configure.md) no ambiente de produção.
- O catálogo em seu ambiente de não produção é basicamente o mesmo do ambiente de produção. Usar catálogos semelhantes garante que os produtos retornados nas unidades de recomendação mimetizem de perto aqueles no ambiente de produção.

## Gerar dados comportamentais em ambiente de não produção

1. Implante o módulo `magento/product-recommendations` em um ambiente de não produção no qual os dados do catálogo sejam semelhantes ao seu catálogo de produção.

1. Use uma das IDs de Espaço de Dados de não produção para [configuração](../landing/saas.md#saas-configuration) no Administrador.

1. Gere os dados sozinho clicando em torno da loja para imitar o comportamento de compradores reais (ou criar um script de automação). Por meio de testes, você gera eventos comportamentais no ambiente de não produção. Esses eventos são usados para produzir as afinidades de produto que potencializam as recomendações. Para testes, [!DNL Commerce] sugere que você interaja com os seguintes tipos de recomendações:

   - Mais visualizados - Requer o mínimo de dados de entrada. Os usuários devem visualizar os produtos.
   - Exibido isto, exibido aquilo - Requer que vários usuários visualizem vários produtos.
   - Comprei isto, comprei aquilo - Requer que vários usuários comprem vários produtos.

### Avisos

- Os dados comportamentais e de catálogo do [Espaço de dados SaaS](../landing/saas.md#saas-configuration) de não produção identificam um ambiente isolado em que as recomendações do produto resultante se baseiam inteiramente nos dados comportamentais gerados na loja associada.

- Como você não tem grandes quantidades de dados comportamentais, os dados de entrada para associações de produto de computação são escassos. No entanto, esses dados ainda são enviados para o Sensei para computar os modelos de aprendizado de máquina e fornecer recomendações com base nos dados gerados nesse ambiente.
