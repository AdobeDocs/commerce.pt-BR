---
title: Notas de versão do [!DNL Store Fulfillment by Walmart Commerce Technologies]
description: Revise as notas de versão para obter informações sobre todas as  [!DNL Store Fulfillment by Walmart Commerce Technologies]  versões.
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Notas de versão

Estas notas de versão descrevem a versão inicial do [!DNL Store Fulfillment Services by Walmart Commerce Technologies] e incluem:

![Novos](../assets/new.svg) Novos recursos
![Problema corrigido](../assets/fix.svg) Correções e melhorias
![Problema conhecido](../assets/bug.svg) Problemas conhecidos

Consulte [Versões futuras](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html?lang=pt-BR) para saber mais sobre os cronogramas de lançamento e o suporte.

Consulte [Disponibilidade do Produto](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=pt-BR) para saber quais versões do Adobe Commerce oferecem suporte a esta extensão.

## v1.5.0

*3 de agosto de 2023*

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}[Adobe Commerce 2.4.4 a 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=pt-BR), incluindo as versões de patch de segurança 2.4.6-p1, 2.4.5-p3 e 2.4.4-p4

Esta versão inclui as seguintes atualizações:

![Novo](../assets/fix.svg) Atualização da extensão para oferecer suporte às [versões de patch de segurança do Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html?lang=pt-BR) 2.4.6-p1, 2.4.5-p3 e 2.4.4-p4.

![Novo](../assets/new.svg)<!-- WMTP-918 --> Suporte adicionado para a opção de configuração [Envio assíncrono](sales-emails.md) para emails de vendas. Os comerciantes que atualizam para a versão 1.5.0 têm a opção de enviar emails imediatamente (padrão) ou de forma assíncrona.

![Novo](../assets/new.svg)<!-- WMTP-916--> Atualizou a [Configuração de fontes](merchant-store-configuration.md) para dar suporte a formatos de números de telefone internacionais.

![Novo](../assets/new.svg) Lógica adicionada para impedir que os valores de reembolso excedam o valor restante ou faturado.

![Novo](../assets/new.svg)<!-- WMTP-882 --> substituiu o objeto `google.map.LatLng` por literais JSON para oferecer suporte à compatibilidade com versões anteriores do [!DNL Google Maps].

![Problema corrigido](../assets/fix.svg)<!-- WMTP- --> Atualizado o script que cria os atributos de produto `[!DNL Available for Store Pickup]` e `[!DNL Available for Home Delivery]` para evitar conflito de categoria de atributo.

![Correção de um problema](../assets/fix.svg)<!-- WMTP-915 --> que corrigia um problema de compatibilidade que causava um loop infinito ao carregar e salvar algumas entidades.

![Correção de um problema](../assets/fix.svg)<!-- WMTP-921 --> que impedia o acionamento da validação de cotação [!DNL Ship to Store] quando um item era adicionado ao carrinho a partir de uma PDP (página de detalhes do produto).

![Problema corrigido](../assets/fix.svg)<!-- WMTP- 932 --> Corrigido um problema de check-out que permitia aos clientes selecionar o método de entrega doméstico para itens não qualificados para entrega doméstica.

![Correção de um problema](../assets/fix.svg) Atualizações de instalação:

- &#x200B;<!-- WMTP-880--> Correção de um problema que fazia com que um código de site incorreto fosse retornado ao instalar a extensão [!DNL Store Fulfillment].

- &#x200B;<!-- WMTP-878--> Correção de um problema para inteiros SKU que exigia que o tipo de dados fosse convertido em tipo de string durante a instalação.

![Correção de um problema](../assets/fix.svg)<!-- WMTP-915--> Correção de uma falha causada por um código de erro de check-in ausente.

![Correção de um problema](../assets/fix.svg)<!-- WMTP-932 --> Corrigido um erro relacionado à rejeição parcial durante operações de dispensa.

![Novo](../assets/new.svg)<!-- WMTP-953 --> Atualizou o ponto de extremidade da API de Cancelamento para consumir o parâmetro de status como um objeto opcional.

![Novo](../assets/new.svg)<!-- WMTP-960 --> detalhes de log aprimorados para o ponto de extremidade da API de dispensação.

## v1.4.0

*13 de abril de 2023*

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/fix.svg) [!DNL Store Fulfillment] agora é [compatível com [!DNL Adobe Commerce] 2.4.4 a 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=pt-BR).


## v1.3.0

*27 de fevereiro de 2023*

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

Esta versão inclui a seguinte atualização:

![Novo](../assets/fix.svg)<!-- WMTP-795 --> Adicionou a capacidade de desabilitar a solução de Atendimento de Repositório para um site específico alterando o escopo padrão da configuração Configuração do Sistema de site para global.

## v1.2.0

*27 de setembro de 2022*

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

Esta versão inclui a seguinte atualização:

![Novo](../assets/fix.svg) [!DNL Store Fulfillment] agora é [compatível com [!DNL Adobe Commerce] 2.4.4 a 2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=pt-BR).


## v1.1.0

*15 de julho de 2022*

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

Estabilidade: disponibilidade geral

![Novo](../assets/fix.svg)<!-- WMTP-731 --> Simplificou a [configuração da experiência de check-in](check-in-experience-setup.md) para o aplicativo Store Assist adicionando a marca de carro padrão e as seleções de modelo. Na versão anterior, os comerciantes tinham que configurar manualmente a marca do carro e as seleções do modelo.

## v1.0.0

*4 de março de 2022*

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

Estabilidade: disponibilidade geral

## Aplicativo de assistência da loja

Para obter informações sobre novas versões do aplicativo Store Assist, consulte as informações do aplicativo na [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} ou [Google Play store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.
