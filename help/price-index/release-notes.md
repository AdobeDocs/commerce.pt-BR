---
title: Notas de versão do [!DNL Catalog Adapter]
description: As informações da versão mais recente do  [!DNL Catalog Adapter] para Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Notas de versão da extensão [!DNL Catalog Adapter]

Essas notas de versão descrevem as versões mais recentes da extensão [!DNL Catalog Adapter]. O suporte é fornecido para a versão principal atual lançada. As notas de versão para versões mais antigas são fornecidas para referência.

As atualizações incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos


>[!NOTE]
>
>A [Extensão do Adaptador de Catálogo](catalog-adapter.md) desabilita a indexação de preços do Adobe Commerce. Se você o instalou, pode verificar a versão instalada em seu sistema usando o Composer. Em alguns casos, convém atualizar a extensão do adaptador de catálogo no sistema para obter correções ou novos recursos sem atualizar a versão do Commerce Service.

## Versão principal atual

## Versão 1.0.10

![Correção](../assets/fix.svg) Correção de um problema em que as consultas de preço para produtos de pacote importados ou recém-criados podiam resultar em erros internos de servidor porque o sistema tentou usar uma SKU concatenada para pesquisa em vez da SKU válida e correta. Consultas de preço para produtos do pacote agora usam o SKU apropriado e são resolvidas corretamente.<!--MDEE-1040-->

## Versão 1.0.9

![Correção](../assets/fix.svg) Compatibilidade adicionada para PHP 8.4. <!--MDEE-941-->

## Versão 1.0.8

![Correção](../assets/fix.svg) Corrigido um problema que causava um erro no log de exceções ao adicionar variantes de produtos configuráveis com SKUs numéricas à lista de desejos. <!--MDEE-876-->
