---
title: Notas de versão da Integração do AEM Assets
description: Revise as notas de versão para obter informações sobre todas as versões da Integração do AEM Assets.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Notas de versão da Integração do AEM Assets

Essas notas de versão descrevem a versão inicial da integração do AEM Assets e incluem:

![Novos](../assets/new.svg) Novos recursos
![Problema corrigido](../assets/fix.svg) Correções e melhorias
![Problema conhecido](../assets/bug.svg) Problemas conhecidos

Para alterações e correções de recursos lançadas fora da versão normal do recurso, revise as seções _Atualizações do serviço hospedado_.

Saiba mais sobre as próximas versões, o suporte ao produto e quais versões do Adobe Commerce oferecem suporte à extensão de Integração do AEM Assets, consulte os tópicos [Agendamento de versão](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/planning/schedule) e [Disponibilidade do produto](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/release/product-availability) do Adobe Commerce.

## Atualizações do serviço hospedado

Essas notas de versão descrevem alterações e correções de recursos que ocorreram e foram lançadas fora das versões de recursos regulares do serviço hospedado.

+++Atualizações do serviço hospedado

_11 de fevereiro de 2025_

![Novo problema](../assets/new.svg) Agora, os comerciantes podem sincronizar imagens para produtos e categorias.

+++

## v1.2.0

_7 de agosto de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-1018 --> Agora, os comerciantes podem escolher a origem dos ativos de imagem e mídia selecionando um [Proprietário da visualização](https://experienceleague.adobe.com/pt-br/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} ao configurar a integração do Assets no Administrador.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-1078 --> Atualizou os pontos de extremidade de [correspondência automática personalizada](https://experienceleague.adobe.com/pt-br/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} com um novo atributo `asset_matches`. Essa alteração permite implementar sua própria lógica de correspondência para retornar todos os ativos associados a um `productSku` específico.

## v1.1.2

_11 de junho de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-1041 --> Adição de suporte para Adobe Commerce 2.4.8 e PHP 8.4.

## v1.1.0

_23 de abril, 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-955 --> Agora, um [URL de Domínio Personalizado](https://experienceleague.adobe.com/pt-br/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) pode ser usado em vez do URL de Entrega do AEM. Se um comerciante definir um **Nome de domínio personalizado** no painel do AEM, será necessário adicionar este **URL de domínio personalizado** no Commerce.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-987 --> Melhoria nos logs gerais dos processos de sincronização do AEM Assets.

## v1.0.22

_12 de março de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-xx --> Agora, a [ID do Cliente IMS do seletor do Assets](https://experienceleague.adobe.com/pt-br/docs/commerce/aem-assets-integration/get-started/setup-synchronization) é exigida pelo Seletor do Assets para habilitar o mapeamento de imagens do AEM Assets com categorias de produto e conteúdo gerado pelo Page Builder.

## v1.0.20

_11 de fevereiro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Nova](../assets/new.svg)<!-- Issue ACAP-xx --> Versão de disponibilidade geral.
