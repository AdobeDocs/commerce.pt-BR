---
title: Notas de versão da Integração do AEM Assets
description: Revise as notas de versão para obter informações sobre todas as versões da Integração do AEM Assets.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 56f31a320411c28d267dfd677d36e5ec04f6f2d8
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# Notas de versão da Integração do AEM Assets

Essas notas de versão descrevem todas as versões da integração do AEM Assets e incluem:

![Novos](../assets/new.svg) Novos recursos
![Problema corrigido](../assets/fix.svg) Correções e melhorias
![Problema conhecido](../assets/bug.svg) Problemas conhecidos

Para alterações e correções de recursos lançadas fora da versão normal do recurso, revise as seções _Atualizações do serviço hospedado_.

Saiba mais sobre as próximas versões, o suporte ao produto e quais versões do Adobe Commerce oferecem suporte à extensão de Integração do AEM Assets, consulte os tópicos [Agendamento de versão](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) e [Disponibilidade do produto](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) do Adobe Commerce.

## Atualizações do serviço hospedado

Essas notas de versão descrevem alterações e correções de recursos que ocorreram e foram lançadas fora das versões de recursos regulares do serviço hospedado.

+++Atualizações do serviço hospedado

_11 de setembro de 2025_

![Novo problema](../assets/new.svg) Atualizou os pontos de extremidade de [correspondência automática personalizada](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} com um novo atributo `asset_matches`.

_11 de fevereiro de 2025_

![Novo problema](../assets/new.svg) Agora, os comerciantes podem sincronizar imagens para produtos e categorias.

+++

## v1.2.14

_13 de fevereiro de 2026_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACCS-171 --> Correção de um problema de [correspondência personalizada](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match) em que a lista suspensa de ações de tempo de execução mostrava dados de espaço de trabalho não salvos após o recarregamento da página.

## v1.2.13

_10 de fevereiro de 2026_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACCS-171 --> Adição de um campo **[!UICONTROL Adobe I/O Workspace Configuration]** que simplifica a configuração de [correspondência personalizada](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank}. Os comerciantes agora podem carregar o arquivo `workspace.json` do App Builder para preencher automaticamente as credenciais do OAuth e os pontos de extremidade da ação de tempo de execução.

## v1.2.12

_29 de janeiro de 2026_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1206 --> em que valores `no_selection` obsoletos em atributos personalizados para funções de ativos não eram removidos durante a sincronização de ativos, fazendo com que algumas imagens não fossem exibidas corretamente no Edge Delivery Services.

## v1.2.11

_15 de janeiro de 2026_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1180 --> Melhoria na página de edição do produto ao ocultar o tamanho do arquivo e as dimensões dos ativos do AEM, pois eles são otimizados dinamicamente pela CDN. Agora, as páginas são pré-renderizadas corretamente quando a integração do AEM Assets é ativada.

## v1.2.10

_12 de janeiro de 2026_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1178 --> em que os atributos personalizados do produto não podiam ser atualizados por meio da API REST quando o produto tinha uma imagem e a integração do AEM Assets estava habilitada. Agora, os atributos personalizados do produto são atualizados corretamente por meio da API REST.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1172 --> que fazia com que imagens ocultas do produto não fossem exibidas como ocultas na interface do usuário do Administrador na página de edição do produto. Agora, o status de visibilidade da imagem é exibido corretamente.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1170 --> que fazia com que imagens de produtos da AEM Assets não fossem sincronizadas com o Adobe Commerce devido a um erro de desserialização. Agora, todos os atributos de imagem (`image`, `small_image` e `swatch_image`) são sincronizados corretamente.

## v1.2.7

_6 de novembro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1169 --> em que as imagens em miniatura do produto eram exibidas de forma inconsistente após a habilitação da integração do AEM Assets nas páginas **Minicarrinho**, **Carrinho** e **Check-out**. Agora, as imagens do produto são renderizadas de forma consistente em todas as páginas, mesmo depois da atualização.

## v1.2.6

_24 de outubro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1163 --> que resolvia um problema em que solicitações consecutivas de atualização de produtos em massa podiam deixar o sinalizador de rastreamento de status travado, impedindo o processamento correto de atualizações subsequentes. Agora, o status é redefinido mesmo se ocorrer um erro.

## v1.2.5

_22 de outubro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1161 -->. Correção de um problema em que a atualização da posição de um mapeamento de imagem existente no Adobe Commerce Admin resultava em um erro de tipo PHP.

## v1.2.4

_17 de outubro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1155 --> Melhoria na estabilidade geral dos atributos personalizados. Agora os atributos personalizados são atualizados corretamente ao usar APIs assíncronas.

![Problema corrigido](../assets/fix.svg)<!-- Issue ACAP-1074 --> Agora, a [sincronização produto-ativo](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank} não falha quando uma URL de link base é definida.

## v1.2.3

_2 de outubro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1135 --> Corrigido um problema com a atualização dos atributos do produto. Agora os atributos do produto são atualizados conforme esperado, e um erro apropriado é retornado em vez de uma resposta 200 quando as atualizações falham.

## v1.2.2

_18 de setembro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-1110 --> Melhoria na estabilidade geral da imagem em páginas de minicarrinho, carrinho e check-out. As imagens nessas páginas agora são carregadas corretamente.

## v1.2.0

_7 de agosto de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-1018 --> Agora, os comerciantes podem escolher a origem dos ativos de imagem e mídia selecionando um [Proprietário da visualização](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} ao configurar a integração do Assets no Administrador.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-1078 --> Atualizou os pontos de extremidade de [correspondência automática personalizada](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} com um novo atributo `asset_matches`. Essa alteração permite implementar sua própria lógica de correspondência para retornar todos os ativos associados a um `productSku` específico.

## v1.1.2

_11 de junho de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-1041 --> Adição de suporte para Adobe Commerce 2.4.8 e PHP 8.4.

## v1.1.0

_23 de abril, 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-955 --> Agora, um [URL de Domínio Personalizado](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) pode ser usado em vez do URL de Entrega do AEM. Se um comerciante definir um **Nome de domínio personalizado** no painel do AEM, será necessário adicionar este **URL de domínio personalizado** no Commerce.

![Correção de um problema](../assets/fix.svg)<!-- Issue ACAP-987 --> Melhoria nos logs gerais dos processos de sincronização do AEM Assets.

## v1.0.22

_12 de março de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Novo problema](../assets/new.svg)<!-- Issue ACAP-xx --> Agora, a [ID do Cliente IMS do seletor do Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization) é exigida pelo Seletor do Assets para habilitar o mapeamento de imagens do AEM Assets com categorias de produto e conteúdo gerado pelo Page Builder.

## v1.0.20

_11 de fevereiro de 2025_

[!BADGE Com Suporte]{type=Informative tooltip="Compatível"} no Adobe Commerce versão 2.4.5 e posteriores.

![Nova](../assets/new.svg)<!-- Issue ACAP-xx --> Versão de disponibilidade geral.
