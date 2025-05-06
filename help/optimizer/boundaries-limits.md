---
title: Limites e limites
description: Saiba mais sobre os limites do  [!DNL Adobe Commerce Optimizer]  para garantir que ele atenda às necessidades da sua empresa.
role: Admin, Developer
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Limites e limites

>[!NOTE]
>
>Esta documentação descreve os limites e limites para o desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

A seguir são fornecidos limites e limites para o Adobe Commerce Optimizer.

## Catálogo

- A taxa garantida de assimilação do catálogo é: 1000 produtos/minuto e 5000 preços/minuto
- O número base de atualizações de produtos por dia é 1.000.000.
- O número total de SKUs permitidas em uma única instância é 250.000. 
- O número máximo de escopos é 50.
- O número de variantes por produto é 10.000.
- O tamanho do produto não pode exceder 200 kb.

## Preços

- O número máximo de tabelas de preços é 1.000.

## Pesquisa e loja

- O número de produtos que uma única solicitação de pesquisa pode retornar é 100.
- O número máximo de atributos filtráveis é 200
- O número máximo de atributos pesquisáveis é 200
- O número máximo de atributos classificáveis é 50
- O número máximo de facetas é 100. Todas as facetas devem ser atributos filtráveis.
- O número máximo de opções que um único facet cat retorna é 100, que pode ser aumentado por solicitação de suporte.

## Canais e políticas

- O número máximo de canais por locatário é 1000.
- O número máximo de políticas atribuídas a um canal é 10.
- O número máximo de valores de atributo usados em uma política é 100. 

## Detecção e recomendações de produtos

- Para a descoberta de produtos, não há suporte para merchandising baseado em atributos e configurações de preço.
- Para obter recomendações:

   - [!DNL Adobe Commerce Optimizer] dá suporte ao tipo de recomendação _Recentemente Visualizados_ para acesso antecipado.
   - Não há suporte para inclusões ou exclusões de categoria ou atributo.
   - Você não pode visualizar recomendações em [!DNL Adobe Commerce Optimizer].
