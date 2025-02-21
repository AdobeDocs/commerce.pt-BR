---
title: Proteção contra fraude Signifyd
description: Habilite a proteção automatizada contra fraude para  [!DNL Payment Services]  com Signifyd.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Proteção contra fraude Signifyd

Você pode habilitar a proteção automatizada contra fraude para [!DNL Payment Services] com a [extensão Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html).

O Adobe Commerce é compatível com o Signifyd versões 5.4.0 e mais recentes. [!DNL Payment Services] dá suporte a fluxos Signifyd de pré-autenticação e pós-autenticação.

A integração Signifyd/[!DNL Payment Services] fornece cobertura para cartões de crédito, cartões de débito, cartões com cofre, check-out por meio do Admin e métodos de pagamento PayPal e Apple. Embora alguns detalhes das transações não sejam compartilhados entre os Serviços de Pagamento e a Signifyd, a Signifyd fornece uma cobertura de risco abrangente para todos os métodos de pagamento, garantindo o máximo de proteção.

Consulte a [documentação do Signifyd](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension) para saber mais sobre como instalar e configurar a extensão.

## Integração

Você deve se comunicar diretamente com o Signifyd para integrar a extensão para uso com o [!DNL Payment Services]—não há necessidade de configuração do [!DNL Payment Services]. Depois de instalada, é possível configurar a extensão Signifyd no Admin. Qualquer suporte relacionado a esta extensão será gerenciado pela Signifyd.

Ao integrar com o Signifyd, você deve:

1. Contate Signifyd para configurar uma nova conta.
1. Incluir na lista de permissões Por padrão, Signifyd é [](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md) para garantir que Signifyd não acione outras opções de pagamento não compatíveis no momento. Se quiser proibir um método de pagamento específico, faça alterações.
1. Confirme com a Signifyd que o PayPal não rejeitará pedidos, por meio da configuração de proteção contra fraude do comerciante no Paypal, que podem ser aprovados pela Signifyd.
1. Habilite a extensão Signifyd para ser compatível com [!DNL Payment Services]:
   * Ao usar [!DNL Payment Services] no modo _Live_, Signifyd deve estar no modo de Produção.
   * Ao usar [!DNL Payment Services] no modo _Sandbox_, Signifyd deve estar no modo de Teste.

## Configuração

Como Signifyd executa alguma ação em seus pedidos, é necessário configurar a extensão para que se comporte adequadamente com base na ação de pagamento definida para [!DNL Payment Services].

Estas opções de configuração não são compatíveis com os Serviços de pagamento e a integração com o Signifyd:

* Quando [!DNL Payment Services] é configurado com a ação de pagamento _and_ de `Authorize`, Signifyd está no modo `PostAuth` com a opção _[!UICONTROL Decline Guarantees]_definida como **Criar memorando de crédito**.

  Motivo: [!DNL Payment Services] cria uma transação de autorização que Signify e tenta reembolsar.


* [!DNL Payment Services] está configurado com a ação de pagamento _de `Authorize and Capture` e_ Signifyd está no modo `PostAuth` com a opção _[!UICONTROL Decline Guarantees]_definida como **Cancelar ordem**.

  Motivo: [!DNL Payment Services] cria uma transação de captura que Signifyd então tenta anular.


Consulte a documentação do Signifyd para obter informações sobre [como configurar a extensão](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension).

Consulte a documentação do Signifyd para [saber mais sobre os fluxos de trabalho de pedido](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works).
