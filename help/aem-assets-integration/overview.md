---
title: Integração do AEM Assets para o Commerce
description: Saiba como integrar o Adobe Experience Manager Assets com sua instância  [!DNL Commerce]  para criar e gerenciar os arquivos de mídia para sua loja da Commerce.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 1%

---

# Integração do AEM Assets para o Commerce

A demanda por conteúdo personalizado está aumentando rapidamente, enquanto os orçamentos de marketing estão sob pressão. Os varejistas e as marcas estão se esforçando para acompanhar a crescente necessidade de variações nas imagens do produto, impulsionadas por requisitos regionais, sazonais e específicos do segmento.

Considere uma retailer com 1.000 produtos. O número de ativos digitais necessários aumenta significativamente ao considerar diferentes regiões, segmentos de clientes e esforços de personalização. Essa situação pode levar a um grande número de variações de ativos, chegando a milhões.

![visão geral](assets/product-visuals-example.png){width="700" zoomable="yes"}

A integração do AEM Assets soluciona esse desafio automatizando os fluxos de trabalho de gerenciamento de ativos. A integração vincula dinamicamente ativos digitais aos produtos e categorias apropriados da Adobe Commerce com base no SKU ou em outros atributos principais. Esse processo simplifica as operações e aumenta a eficiência ao permitir:

* **Instalação e configuração perfeitas**- As equipes e desenvolvedores de merchandising podem configurar rapidamente a integração usando ferramentas e fluxos de trabalho familiares da Adobe.

* **Atualizações Dinâmicas de Ativos** - As imagens de produtos e os ativos de marketing refletem automaticamente as alterações mais recentes no AEM Assets, mantendo as vitrines precisas e relevantes.

* **Gerenciamento simplificado de catálogo** - Automatiza a atualização e a limpeza de ativos, minimizando o esforço manual e garantindo um catálogo de produtos consistente e com boa manutenção.

## Requisitos para usar a integração

Para aproveitar essa integração com o [Product Visuals ou o AEM Assets](https://experienceleague.adobe.com/pt-br/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets), as empresas devem atender aos seguintes requisitos:

>[!BEGINTABS]

>[!TAB Visuais do produto]

[!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} Licenças ativas para Adobe Commerce, Visualizações de Produtos viabilizadas pelo AEM Assets e [AEM Dynamic Media](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) (Essas licenças estão disponíveis prontas para uso com o [!DNL Adobe Commerce as a Cloud Service] e o [!DNL Adobe Commerce Optimizer]).

>[!TAB AEM Assets]

[!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} licenças ativas para Adobe Commerce, Adobe Experience Manager Assets e [AEM Dynamic Media](https://experienceleague.adobe.com/pt-br/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media).

[!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3 e 8.4

* Composer 2.x

[!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} O Adobe Experience Manager é provisionado com o [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

O usuário do Adobe Commerce que está configurando a integração deve ter acesso à [Organização IMS](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) onde o projeto do AEM Assets é provisionado.

>[!BEGINSHADEBOX]

## Principais benefícios para os negócios

![verificação](assets/icon-check.png) **Sem custo adicional** - Essa integração é fornecida gratuitamente para comerciantes que atendem aos requisitos de licenciamento.

![verificação](assets/icon-check.png) **Solução oficial da Adobe** - Desenvolvida, mantida e totalmente suportada pela Adobe, garantindo estabilidade e alinhamento com futuros aprimoramentos da plataforma.

![verificar](assets/icon-check.png) **Modelo de suporte gerenciado da Adobe** - a Adobe lida diretamente com a assistência e a solução de problemas, fornecendo suporte confiável e resolução simplificada de problemas.

![verificar](assets/icon-check.png) **recursos do Adobe Storefront Builder** - A solução de gerenciamento de ativos digitais (DAM) permite o uso de ativos como imagens, vídeos e outras mídias no [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=pt-BR#userlabs-commerce-genai-product-visuals).

>[!ENDSHADEBOX]

## Tutorial

Para saber como configurar e usar a integração do AEM Assets com o Adobe Commerce, assista a estes vídeos.

>[!BEGINTABS]

>[!TAB Tutorial do Adobe Commerce na nuvem ou no local]

Para saber como o Adobe Commerce e o AEM Assets trabalham juntos para simplificar os fluxos de trabalho de conteúdo, assista a este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3447888?captions=por_br)

>[!TAB Tutorial do Adobe Commerce as a Cloud Service]

Saiba como usar o Adobe Commerce as a Cloud Service com a integração do AEM Assets.

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## Próximas etapas

O processo para instalar e configurar a integração do AEM Assets depende da implantação do Adobe Commerce. Em todos os casos, primeiro você configura o AEM Assets e depois conecta o Commerce a ele.

Para entender o namespace, o esquema de metadados e a guia **[!UICONTROL Commerce]** adicionados pela integração ao seu ambiente do AEM Assets, revise os [metadados do Commerce no AEM Assets](metadata.md) antes de começar.

Selecione sua implantação para seguir as etapas necessárias em ordem:

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE Somente SaaS]{type=Positive tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service (infraestrutura SaaS gerenciada pela Adobe)."}

1. Para oferecer suporte aos metadados do Commerce, [configure o projeto do AEM Assets](get-started/configure-aem.md). Na versão `2026.5.26309` e posterior do AEM, use o [autoatendimento de integração](get-started/configure-aem.md#enable-aem-commerce-self-service); em versões anteriores, instale o pacote `assets-commerce` manualmente.

1. [Configure as permissões de usuário do IMS](get-started/permissions.md) para que o Seletor de ativos e os campos **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]** preenchidos automaticamente estejam disponíveis.

1. [Configurar a integração no Administrador do Commerce](get-started/setup-synchronization.md).

1. Opcional. [Habilite a exibição da imagem do produto](get-started/configure-storefront.md#enable-product-images) para que uma vitrine gerenciada pela Edge Delivery Services renderize imagens do produto gerenciadas pela AEM.

>[!TAB Adobe Commerce na nuvem (PaaS)]

[!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."}

1. Para oferecer suporte aos metadados do Commerce, [configure o projeto do AEM Assets](get-started/configure-aem.md). Na versão `2026.5.26309` e posterior do AEM, use o [autoatendimento de integração](get-started/configure-aem.md#enable-aem-commerce-self-service); em versões anteriores, instale o pacote `assets-commerce` manualmente.

1. [Instale pacotes do Adobe Commerce](get-started/configure-commerce.md) para adicionar a extensão e gerar as credenciais e conexões necessárias.

1. [Configure as permissões de usuário do IMS](get-started/permissions.md) para que o Seletor de ativos e os campos **[!UICONTROL Program ID]** e **[!UICONTROL Environment ID]** preenchidos automaticamente estejam disponíveis.

1. [Configurar a integração no Administrador do Commerce](get-started/setup-synchronization.md).

1. Opcional. [Habilite a exibição da imagem do produto](get-started/configure-storefront.md#enable-product-images) para que uma vitrine gerenciada pela Edge Delivery Services renderize imagens do produto gerenciadas pela AEM.

>[!TAB Adobe Commerce Optimizer]

[!BADGE Somente SaaS]{type=Positive tooltip="Aplicável somente a projetos do Adobe Commerce Optimizer."}

[!DNL Adobe Commerce Optimizer] Não possui interface de configuração de administrador. O Suporte da Adobe configura a integração do seu tíquete de integração, portanto, prepare o AEM Assets primeiro.

1. Para oferecer suporte aos metadados do Commerce, [configure o projeto do AEM Assets](get-started/configure-aem.md). Na versão `2026.5.26309` e posterior do AEM, use o [autoatendimento de integração](get-started/configure-aem.md#enable-aem-commerce-self-service); em versões anteriores, instale o pacote `assets-commerce` manualmente.

1. [Envie o tíquete de suporte de integração](get-started/configure-aco.md#onboarding) com sua ID de locatário, ID de programa do AEM, ID de ambiente do AEM, regra correspondente, camada e localidade.

1. [Configure sua exibição de catálogo](get-started/configure-aco.md#onboarding) com a mesma localidade e camada que você registrou no tíquete.

1. Opcional. [Habilite a exibição da imagem do produto](get-started/configure-storefront.md#enable-product-images) para que uma vitrine gerenciada pela Edge Delivery Services renderize imagens do produto gerenciadas pela AEM.

   Para obter o procedimento completo, as limitações e a orientação da camada, consulte [Configurar o AEM Assets para Commerce Optimizer](get-started/configure-aco.md).

>[!ENDTABS]

## Suporte

Se precisar de informações ou se tiver dúvidas não abordadas neste guia, entre em contato com o representante de vendas da Integração da AEM Assets ou crie um [tíquete de suporte](https://experienceleague.adobe.com/pt-br/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case) para receber ajuda adicional.
