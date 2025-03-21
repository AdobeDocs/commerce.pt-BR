---
title: Notas de versão
description: As informações da versão mais recente da extensão  [!DNL Data Connection]  do Adobe Commerce.
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: e92f6c2b748683fbe1a358680b03eefb27fe0093
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 1%

---

# Notas de versão

>[!IMPORTANT]
>
>O conector do Experience Platform foi renomeado para [!DNL Data Connection].

Estas notas de versão contêm atualizações para a extensão [!DNL Data Connection] e incluem:

![Novos](../assets/new.svg) - Novos recursos
![Correção](../assets/fix.svg) - Correções e melhorias
![Bug](../assets/bug.svg) - Problemas conhecidos

Para obter alterações e correções de recursos relacionadas a extensões usadas pela extensão [!DNL Data Connection], consulte **Atualizações de serviço com suporte**.

Consulte [Versões futuras](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) para saber mais sobre os cronogramas de lançamento e o suporte.

Consulte a documentação do desenvolvedor para [saber quais versões do Commerce são compatíveis com este módulo](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Atualizações de serviço compatíveis

Essas notas de versão descrevem alterações de recursos e correções relacionadas a extensões usadas pela extensão [!DNL Data Connection].

+++Atualizações de serviço com suporte

_2 de agosto de 2024_

![Correção](../assets/fix.svg) - Corrigido o valor total de pagamentos quando o total de pedidos está configurado para incluir impostos.
![Novo](../assets/new.svg) - Adição de um campo `taxAmount` para solicitar eventos de compra.
![Novo](../assets/new.svg) - Adição da capacidade de adicionar dados personalizados a eventos. Consulte o seguinte para obter um [exemplo](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md).

_24 de janeiro de 2024_

![Novo](../assets/new.svg) - A extensão `data-services-b2b` foi atualizada para incluir um novo evento de requisição chamado [deleteRequisitionList](events.md#deleterequisitionlist) para comerciantes B2B.

_16 de novembro de 2023_

![Correção](../assets/fix.svg) - Corrigido um problema no qual uma mensagem de erro aparecia incorretamente quando você fazia um pedido com vários endereços de envio.
![Correção](../assets/fix.svg) - Corrigido um problema no evento [productPageView](events.md#productpageview) em que o campo de evento `productListItems.priceTotal` não convertia o preço após alternar a moeda no modo de exibição de armazenamento.
![Correção](../assets/fix.svg) - Corrigido um problema no campo de evento `productListItems`, em que o código de moeda não era atualizado quando o comerciante trocou a exibição de armazenamento.

_10 de outubro de 2023_

![Novo](../assets/new.svg) - Adição de novos eventos de status de pedido: [Pedido faturado](events-backoffice.md#orderinvoiced), [Devolução de item de pedido iniciada](events-backoffice.md#orderitemsreturninitiated) e [Devolução de item de pedido concluída](events-backoffice.md#orderitemreturncompleted).
![Correção](../assets/fix.svg) - Corrigido um problema no qual as alterações na configuração de moeda não eram refletidas nos eventos após a atualização do cache.
![Correção](../assets/fix.svg) - Corrigido um erro quando a mensagem de confirmação de pedido não era exibida se o posicionamento assíncrono de pedido estivesse habilitado.
![Novo](../assets/new.svg) - Dados adicionados ao evento [addToRequisitionList](events.md#addtorequisitionlist) para produtos simples na página de exibição Categoria.
![Correção](../assets/fix.svg) - Corrigido um problema nos dados `selectedOptions` do evento [addToRequisitionList](events.md#addtorequisitionlist) quando produtos eram adicionados da página Confirmação de pedido.
![Novo](../assets/new.svg) - Adição de dados do produto ao evento [addToRequisitionList](events.md#addtorequisitionlist) quando produtos são adicionados à lista de requisições da página de exibição de Categoria.
![Novo](../assets/new.svg) - Adição do evento [addToRequisitionList](events.md#addtorequisitionlist) quando produtos configuráveis são adicionados à lista de requisições da página Exibição de produto.
![Novo](../assets/new.svg) - Adição dos eventos [addToRequisitionList](events.md#addtorequisitionlist) e [removeFromRequisitionList](events.md#removefromrequisitionlist) quando a quantidade de produtos aumenta e/ou diminui de uma lista de requisições.

_10 de junho de 2023_

![Correção](../assets/fix.svg) - Corrigido um problema quando `orderId` não era transmitido no contexto devido a prefixos no identificador de pedido Commerce.
![Correção](../assets/fix.svg) - Configurações de Política de Segurança de Conteúdo atualizadas.

_30 de março de 2023_

![Novo](../assets/new.svg) - Adição de uma extensão chamada `data-services-b2b` que inclui [eventos da lista de requisições](events.md#b2b-events) para comerciantes B2B.
![Novo](../assets/new.svg) - Adição do campo `uniqueIdentifier` aos eventos [pesquisa](events.md#search-events). Esse novo campo permite que os comerciantes façam referência cruzada de solicitações de pesquisa e respostas de pesquisa.

_12 de outubro de 2022_

![Novo](../assets/new.svg) - Adição de dois [eventos de vitrine](events.md), `openCart` e `removeFromCart` ao SDK e ao Coletor de Eventos da Adobe Commerce Storefront.
![Novo](../assets/new.svg) - Suporte adicionado para uma [vitrine do AEM](overview.md#aem-support).

+++

## 3.3.0

_21 de março de 2025_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) adicionou suporte ao PHP 8.4.

## 3.2.1

_17 de janeiro de 2025_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) - Adicionada a [extensão pronta para HIPAA](hipaa-readiness.md) a [!DNL Data Connection] para que os comerciantes possam compartilhar [!DNL Commerce] dados de eventos de back office com a Experience Platform e manter a conformidade com a HIPAA.
![Correção](../assets/fix.svg) - Corrigido um problema no qual a extensão [!DNL Data Connection] substituía os dados `eventForwarding` e definia o sinalizador `HIPAA` para todos os clientes. Agora, a extensão só define o sinalizador para clientes da HIPAA.

## 3.2.0

_7 de outubro de 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) - Adição da capacidade de criar [atributos de pedido personalizados](custom-attributes.md) para dados de back office.
![Novo](../assets/new.svg) - Adição de uma nova tabela de [Atributos de Pedido Personalizado](connect-data.md#data-customization) para ajudá-lo a exibir atributos personalizados configurados no [!DNL Commerce] e enviados para a Experience Platform.
![Novo](../assets/new.svg) - Adição da capacidade de [coletar e enviar registros de perfil](connect-data.md#send-customer-profile-data) e dados para a Experience Platform.

## 3.2.0-beta3

_27 de agosto de 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) - Se você estiver participando do beta, verifique se o arquivo `composer.json` tem o seguinte no nível raiz: ` "minimum-stability": "beta"`. Além disso, adicione `composer require "magento/customers-connector: ^1.2.0"` para enviar perfis de clientes da sua instância do Commerce para o SaaS.
![Novo](../assets/new.svg) - Esta versão contém os patches lançados nas versões 3.1.1, 3.1.2, 3.1.3 e 3.1.4.

## 3.1.4

_9 de agosto de 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Correção](../assets/fix.svg) - Atualizado o metapackage `experience-platform-connector` para remover exportadores e indexadores de dados não utilizados.

## 3.1.3

_22 de julho de 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Correção](../assets/fix.svg) - Atualizado o metapackage `experience-platform-connector` para remover exportadores e indexadores de dados não utilizados.

## 3.1.2

_5 de junho de 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Correção](../assets/fix.svg) - Corrigido um problema no qual o formato de data incorreto estava sendo usado ao iniciar uma [sincronização histórica](connect-data.md#specify-order-history-date-range).
![Correção](../assets/fix.svg) - Corrigido um problema no qual o evento [startCheckout](events.md#startcheckout) não estava sendo enviado no Adobe Commerce 2.4.7.

## 3.1.1

_4 de abril, 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) - Suporte adicionado para PHP 8.3 para todas as extensões [!DNL Data Connection].
![Novo](../assets/new.svg) - Adição de um artigo sobre como [integrar](mobile-sdk-epc.md) o Adobe Experience Platform Mobile SDK com o Commerce.

## 3.2.0-beta2

_4 de março de 2024_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) - Se você estiver participando do beta, verifique se o arquivo `composer.json` tem o seguinte no nível raiz: ` "minimum-stability": "beta"`. Além disso, adicione `composer require "magento/customers-connector: ^1.2.0"` para enviar perfis de clientes da sua instância do Commerce para o SaaS.
![Novo](../assets/new.svg) - Adição da capacidade de [adicionar atributos personalizados](custom-attributes.md).
![Novo](../assets/new.svg) - Adição da capacidade de [coletar e enviar registros de perfil](connect-data.md#send-customer-profile-data) e dados para a Experience Platform.

## 3.1.0

_16 de novembro de 2023_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

![Novo](../assets/new.svg) - O conector do Experience Platform foi renomeado para [!DNL Data Connection].
![Correção](../assets/fix.svg) - Adição da capacidade de registrar resposta de erro se o Adobe IMS não puder gerar o token de acesso.
![Correção](../assets/fix.svg) - Adicionou uma mensagem de notificação se você tentar sincronizar Pedidos Históricos, mas não especificou credenciais de conta.

## 3.0.0

_10 de outubro de 2023_

[!BADGE Compatibilidade]{type=Informative tooltip="Compatibilidade"}

Esta é uma versão principal. [Edite](install.md#update-the-data-connection) o arquivo composer.json raiz do seu projeto.

![Novo](../assets/new.svg) - Disponibilidade geral para [enviar dados e status de ordem histórica](connect-data.md#send-historical-order-data) para a Experience Platform.
![Novo](../assets/new.svg) - Adição de suporte para OAuth 2.0 ao [configurar](connect-data.md#connect-commerce-data-to-adobe-experience-platform) a extensão [!DNL Data Connection].
![Novo](../assets/new.svg) - Encerrou o suporte ao Adobe Commerce 2.4.3.

## 2.3.0

_27 de junho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - Adição da capacidade de [desativar o envio de eventos de vitrine](connect-data.md#data-collection) para a Experience Platform.
![Correção](../assets/fix.svg) - Configurações de Política de Segurança de Conteúdo atualizadas.
![Correção](../assets/fix.svg) - Corrigido o suporte a eventos de back office na versão 2.4.7 do Commerce.
![Novo](../assets/new.svg) - Adição de uma mensagem de notificação sobre a invalidação do cache ao salvar alterações no formulário de extensão [!DNL Data Connection].

## 3.0.0-beta1 (somente interno)

_13 de junho de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - (Beta) Adição da capacidade de [enviar dados e status de ordem histórica](connect-data.md#beta-send-historical-order-data) para a Experience Platform.

## 2.2.0

_30 de março de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - Agrupou as dependências `commerce-data-export` e `saas-export` com a extensão `experience-platform-connector`. Anteriormente, você tinha que instalar essas dependências separadamente. Essas dependências, juntamente com a configuração de comerciante, permitem o processamento do lado do servidor de [eventos de back office](events-backoffice.md).
![Novo](../assets/new.svg) - Adição de um novo evento de back office chamado [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted).

## 2.1.1

_28 de fevereiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - Suporte adicionado para PHP 8.2 para todas as extensões [!DNL Data Connection].

## 2.1.0

_17 de janeiro de 2023_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - O [[!DNL Data Connection] administrador de extensão](connect-data.md) foi atualizado para que você possa especificar seu próprio AEP Web SDK (alloy).
![Correção](../assets/fix.svg) alterada para usar `identityMap` em vez de `personID` ao definir a identidade principal para quaisquer dados enviados para a borda.

## 2.0.1

_10 de novembro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Correção](../assets/fix.svg) - Agora o contexto do Adobe Experience Platform é definido somente após o Coletor de Eventos da Storefront e o SDK de Eventos da Storefront serem carregados com êxito.

## 2.0.0

_12 de outubro de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - Adição da capacidade de especificar seu próprio AEP Web SDK ao [conectar](connect-data.md) sua instância do Adobe Commerce à Experience Platform.
![Correção](../assets/fix.svg) - Atualização do requisito de escopo da sequência de dados para que as IDs da sequência de dados devam ser enviadas ao site em vez de armazenadas.

## 1.0.0

_9 de agosto de 2022_

[!BADGE Com suporte]{type=Informative tooltip="Compatível"}

![Novo](../assets/new.svg) - Versão de disponibilidade geral.
