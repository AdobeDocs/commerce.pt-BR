---
title: Fluxo de trabalho de implementação
description: Saiba mais sobre as etapas para implementar o [!DNL Product Recommendations] com êxito em sua loja.
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Fluxo de trabalho de implementação

[!DNL Product Recommendations] usa dados comportamentais e de catálogo:

- Comportamental - Dados do envolvimento de um comprador no site, como exibições de produtos, itens adicionados a um carrinho e compras. A Adobe Commerce e a IA do Adobe não coletam informações de identificação pessoal.

- Catálogo - Metadados do produto, como nome, preço e disponibilidade.

Quando você instala o `magento/product-recommendations module`, a IA do Adobe agrega os dados comportamentais e de catálogo e cria [!DNL Product Recommendations] para cada tipo de recomendação. O serviço [!DNL Product Recommendations] implanta essas recomendações na vitrine. Para ajudar você a implementar as recomendações de produtos em sua loja, use o seguinte fluxo de trabalho:

>[!NOTE]
>
> Se sua loja for implementada com o PWA Studio, consulte a [documentação do PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se você usa uma tecnologia de front-end personalizada, como o React ou o Vue JS, saiba como [integrar](headless.md) [!DNL Product Recommendations] à sua loja headless.

## Fluxo de trabalho (WRK)

1. **Implantar coleção de dados para produção**

   A implantação de [!DNL Product Recommendations] requer duas [fontes de dados](type.md) principais: catálogo e comportamental. Como a produção é o único ambiente em que as ações dos compradores são capturadas e analisadas, inicie a coleta de dados sobre a produção o mais rápido possível. [Saiba](events.md) como a IA do Adobe treina modelos de aprendizado de máquina que resultam em recomendações de melhor qualidade. Como benefício adicional, ao começar a coletar dados comportamentais na produção, você pode [buscar recomendações](staging-environment.md#fetch-recommendations-from-production-environment-recommended) com base nesses dados de produção enquanto opera em ambientes de não produção. Em seguida, você pode testar e experimentar com diferentes recomendações que são computadas com base nos dados reais do comprador coletados na produção.

   Para implantar a coleção de dados na produção, você deve [instalar e configurar](install-configure.md) o módulo [!DNL Product Recommendations] fornecendo uma [chave de API](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=pt-BR).

   >[!TIP]
   >
   > A implantação da coleção de dados não altera a aparência da loja nem a experiência dos compradores. Somente criar e implantar unidades de recomendação altera a experiência do cliente em sua loja. Certifique-se de testar seu ambiente de não produção antes de implantar na produção. Além disso, não crie unidades de recomendação até personalizar o modelo. Consulte a próxima etapa.

1. **Personalizar o modelo para corresponder ao seu estilo**

   Sua loja representa sua marca, portanto, modifique o modelo de recomendações de produto para corresponder ao tema do site.

   >[!TIP]
   >
   > Personalizando o modelo, você pode especificar sua folha de estilos, substituir onde uma unidade de recomendação aparece em uma página e assim por diante.

   Consulte [Personalizar](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html?lang=pt-BR) na documentação do desenvolvedor para saber como concluir esta etapa.

1. **Testar recomendações em seu ambiente de não produção**

   É sempre uma prática recomendada testar uma nova tecnologia em seu ambiente de não produção antes de implantar na produção. O teste de recomendações em seu ambiente de não produção permite que você jogue com diferentes tipos de unidade de recomendação, posicionamento e páginas. Você pode extrair recomendações com base em dados comportamentais já coletados na produção enquanto testa em seu ambiente de não produção, de modo que os resultados da recomendação se baseiem no comportamento de compra dos clientes reais.

   >[!TIP]
   >
   > Certifique-se de que o catálogo de ambientes de não produção seja basicamente o mesmo que o que você tem em produção. Usar catálogos semelhantes garante que os produtos retornados nas unidades de recomendação mimetizem os produtos na produção.

   Consulte [Buscar](staging-environment.md) dados comportamentais do seu ambiente de produção para saber como concluir esta etapa.

1. **Criar e implantar recomendações em sua vitrine de produção**

   Agora que você implantou a coleção de dados comportamentais na produção, modificou o modelo de recomendações de produto e testou as recomendações usando o comportamento real do comprador, você está pronto para promover todo o código à produção e [criar](create.md) recomendações de produto em tempo real.
