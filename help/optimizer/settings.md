---
title: Configurações
description: Definir configurações para  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Configurações

Use o espaço de trabalho *Configurações* para configurar os intervalos e os intervalos de facetas de preços e o idioma padrão para a descoberta de produtos.

A facetagem de preços especifica o número de grupos de faixas de preços e como os valores de preços são distribuídos entre eles.

A configuração **Language** informa a [!DNL Adobe Commerce Optimizer] qual idioma esperar ao gravar o índice.

## Faceting de preço

Você pode especificar o número de grupos de faixas de preços e como os valores de preços são distribuídos entre eles. Cada faixa de preços sobrepõe o grupo anterior em um. Por exemplo, cinco grupos com um intervalo de 20 criam as seguintes faixas de preço: 0-20, 20-40, 40-60, 60-80 e >80. Se não houver produtos suficientes no catálogo para preencher todos os intervalos definidos, a exibição dos grupos disponíveis será ajustada de acordo. Por exemplo: 0-20, 60-80, >80.

1. No espaço de trabalho **Configurações**, selecione **[!UICONTROL Search]** e, em **Preço facetado**, faça o seguinte:
   - Insira o **Número de seleções** ou agrupamentos de preços que estarão disponíveis. Até 50 agrupamentos de preços podem ser definidos.
   - Insira o **Valor do intervalo** ou o intervalo de preços para cada grupo. O valor máximo é 40.000.000.
1. Clique em **Salvar**.

   Leva aproximadamente 15 minutos para as configurações atualizadas estarem disponíveis na loja.

### Descrições dos campos

| Campo | Descrição |
|--- |--- |
| Número de seleções | Especifica o número de agrupamentos de intervalo de preços que podem ser usados como filtros de pesquisa na loja. Valor padrão: 8, Valor máximo: 50 |
| Valor do intervalo | Especifica o intervalo de preço para cada grupo. Por exemplo, cinco seleções com um valor de intervalo de 20 cria cinco agrupamentos de 0-20, 20-40, 40-60, 60-80 e >80. Valor padrão: 5, Valor máximo: 40.000.000 |

## Idioma

A configuração Idioma informa a [!DNL Adobe Commerce Optimizer] qual idioma esperar ao ler o catálogo e gravar o índice.

As línguas têm diferentes conjuntos de regras para a gramática: como as palavras são separadas, tempos verbais e formas de palavras, por exemplo.
A configuração Idioma garante que o conjunto correto de regras seja aplicado ao mecanismo de indexação.

Defina a configuração Idioma para o idioma principal do catálogo. Ao alterar o idioma do índice, pode levar de 5 a 60 minutos para refletir a alteração na loja, dependendo do tamanho e da complexidade do catálogo.

| Idioma | Código |
|----|----|
| Árabe | ar |
| Armênio | hy |
| Basco | eu |
| Bengali | bn |
| Brasileiro | pt-br |
| Búlgaro | bg |
| Catalão | ca |
| Chinês (simplificado) | zh-cn |
| Chinês (tradicional) | zh-tw |
| Tcheco | cs |
| Dinamarquês | da |
| Holandês | nl |
| Inglês | en |
| Estoniano | et |
| Finlandês | fi |
| Francês | fr |
| Galego | gl |
| Alemão | de |
| Grego | el |
| Hindi | oi |
| Húngaro | hu |
| Indonésio | id |
| Irlandês | ga |
| Italiano | it |
| Japonês (Katakana) | ja |
| Coreano | ko |
| Letão | lv |
| Lituano | lt |
| Norueguês | não |
| Persa | fa |
| Português | pt |
| Romeno | ro |
| Russo | ru |
| Sorani | ku |
| Espanhol | es |
| Sueco | sv |
| Turco | tr |
| Tailandês | th |
