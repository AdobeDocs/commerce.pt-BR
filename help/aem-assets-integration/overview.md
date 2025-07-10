---
title: Integração do AEM Assets para o Commerce
description: Saiba como integrar o Adobe Experience Manager Assets com sua instância  [!DNL Commerce]  para criar e gerenciar os arquivos de mídia para sua loja da Commerce.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
source-git-commit: 9e6f8ae86b28577e2b2c675dbf274c762abe9f3f
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Integração do AEM Assets para o Commerce

A demanda por conteúdo personalizado está aumentando rapidamente, enquanto os orçamentos de marketing estão sob pressão. Os varejistas e as marcas estão se esforçando para acompanhar a crescente necessidade de variações nas imagens do produto, impulsionadas por requisitos regionais, sazonais e específicos do segmento.

Considere uma retailer com 1.000 produtos. Mesmo antes de considerar as variações de atributo, o número de ativos digitais necessários se expande significativamente ao considerar diferentes regiões, segmentos de clientes e esforços de personalização. Isso pode levar a um grande número de variações de ativos, chegando a milhões.

![visão geral](assets/product-visuals-example.png){width="700" zoomable="yes"}

A integração do AEM Assets soluciona esse desafio automatizando os fluxos de trabalho de gerenciamento de ativos. A integração garante que ativos digitais, como imagens de produtos e conteúdo de marketing, sejam vinculados dinamicamente às entidades de merchandising apropriadas, incluindo produtos e categorias no Adobe Commerce, com base na SKU ou outros atributos principais. Esse processo simplifica as operações e aumenta a eficiência ao permitir:

* **Instalação e configuração perfeitas**- As equipes e desenvolvedores de merchandising podem configurar rapidamente a integração usando ferramentas e fluxos de trabalho familiares da Adobe.

* **Atualizações dinâmicas de ativos** - As imagens de produtos e os ativos de marketing refletem automaticamente as alterações mais recentes no AEM Assets, mantendo as vitrines precisas e relevantes.

* **Gerenciamento simplificado de catálogos** - Automatiza a atualização e a limpeza de ativos, minimizando o esforço manual e garantindo um catálogo de produtos consistente e com boa manutenção.

## Requisitos para usar a integração

Para aproveitar essa integração com Visuais de produto ou AEM Assets, as empresas devem atender aos seguintes requisitos:

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

![verificação](assets/icon-check.png) **Sem custo adicional**-Essa integração é fornecida gratuitamente para comerciantes que atendem aos requisitos de licenciamento.

![verificar](assets/icon-check.png) **Solução oficial da Adobe**- Desenvolvida, mantida e totalmente suportada pela Adobe, garantindo estabilidade e alinhamento com futuros aprimoramentos da plataforma.

![verificar](assets/icon-check.png) **Modelo de suporte gerenciado da Adobe** - A assistência e a solução de problemas são tratadas diretamente pela Adobe, fornecendo tranquilidade e solução de problemas simplificada.

![verifique](assets/icon-check.png) **os recursos do Adobe Storefront Builder**-A solução de gerenciamento de ativos digitais (DAM) permite o uso de ativos como imagens, vídeos e outras mídias no [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=pt-BR#userlabs-commerce-genai-product-visuals).

>[!ENDSHADEBOX]

Assista a este vídeo para saber como o Adobe Commerce e o AEM Assets trabalham juntos para simplificar os fluxos de trabalho de conteúdo:

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

## Próximas etapas

A habilitação da integração do Commerce com o Experience Manager Assets é um processo de três etapas:

1. [Configure seu projeto do AEM Assets para oferecer suporte aos metadados do Commerce](get-started/configure-aem.md).

1. [!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."} [Instalar pacotes do Adobe Commerce](get-started/configure-commerce.md).

1. [Configurar a integração](get-started/setup-synchronization.md).

## Suporte

Se precisar de informações ou se tiver dúvidas não abordadas neste guia, entre em contato com o representante de vendas da Integração da AEM Assets ou crie um [tíquete de suporte](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html?lang=pt-BR#submit-ticket) para receber ajuda adicional.
