---
title: Tipos de facetas
description: Saiba mais sobre os diferentes tipos de facetas no [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Tipos de facetas

[!DNL Adobe Commerce Optimizer] usa uma variedade de tipos de facetas e elas aparecem na lista *Filtros* somente quando relevantes. A lista de aspectos disponíveis muda de acordo com os produtos retornados. As seguintes características afetam sua apresentação e comportamento:

- Facetas fixadas - As facetas mais usadas podem ser fixadas no topo da lista. As facetas restantes estão listadas na ordem *Tipo de classificação* depois das facetas fixadas.
- Aspectos dinâmicos - Atributos de produto que o [Adobe Sensei](https://www.adobe.com/sensei.html) considera mais relevantes para um conjunto de produtos e uma consulta. O cálculo leva em conta os metadados do atributo de todo o catálogo e determina, no momento da consulta, os aspectos mais relevantes da consulta.
- Facetas de preço - Devolver produtos por faixa de preço. Você pode especificar o número de seleções e o intervalo de preços no espaço de trabalho [*Configurações*](../../settings.md).

## Rótulos de facetas

Você pode editar rótulos de facetas no [espaço de trabalho de facetas](workspace.md).

## Tipo de classificação

Todas as facetas renderizadas para a loja são classificadas alfabeticamente ou por contagem.

| Tipo de classificação | Descrição |
|--- |--- |
| Em ordem alfabética | Na lista *Filtros* da loja, os aspectos são classificados em ordem alfabética. |
| Contagem | Facetas também podem ser classificadas pelo número de valores encontrados por faceta no conjunto atual de produtos devolvidos. |
