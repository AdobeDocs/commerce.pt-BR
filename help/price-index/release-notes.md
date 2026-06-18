---
title: Notas de versão do [!DNL Catalog Adapter]
description: As informações da versão mais recente do  [!DNL Catalog Adapter] para Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
TQID: https://experienceleague.adobe.com/btPlBYpdRdf-gMfqSv2px6iMfiI3FfXJSN40j61HXOU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: d5e10c1b3014d2b74c323d6a34e5f73a97d494ce
workflow-type: tm+mt
source-wordcount: 218
ht-degree: 0%

---

# Notas de versão da extensão [!DNL Catalog Adapter]

Essas notas de versão descrevem as versões mais recentes da extensão [!DNL Catalog Adapter]. O suporte é fornecido para a versão principal atual lançada. As notas de versão para versões mais antigas são fornecidas para referência.

As atualizações incluem:

![Novos](../assets/new.svg) Novos recursos
![Correção](../assets/fix.svg) Correções e melhorias
![Bug](../assets/bug.svg) Problemas conhecidos


>[!NOTE]
>
>A [Extensão do Adaptador de Catálogo](catalog-adapter.md) desabilita a indexação de preços do Adobe Commerce. Se você o instalou, pode verificar a versão instalada em seu sistema usando o Composer. Em alguns casos, convém atualizar a extensão do adaptador de catálogo no sistema para obter correções ou novos recursos sem atualizar a versão do Commerce Service.

## Versão principal atual

## Versão 1.0.11

_18 de junho de 2026_

![Correção](../assets/fix.svg) **Compatibilidade com o PHP 8.5** - O Adobe Commerce Catalog Adapter agora oferece suporte ao PHP 8.5 para compatibilidade com o Adobe Commerce versão 2.4.9+. <!--MDEE-1368-->

## Versão 1.0.10

![Correção](../assets/fix.svg) Correção de um problema em que as consultas de preço para produtos de pacote importados ou recém-criados podiam resultar em erros internos de servidor porque o sistema tentou usar uma SKU concatenada para pesquisa em vez da SKU válida e correta. Consultas de preço para produtos do pacote agora usam o SKU apropriado e são resolvidas corretamente.<!--MDEE-1040-->

## Versão 1.0.9

![Correção](../assets/fix.svg) Compatibilidade adicionada para PHP 8.4. <!--MDEE-941-->

## Versão 1.0.8

![Correção](../assets/fix.svg) Corrigido um problema que causava um erro no log de exceções ao adicionar variantes de produtos configuráveis com SKUs numéricas à lista de desejos. <!--MDEE-876-->
