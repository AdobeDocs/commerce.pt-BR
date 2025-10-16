---
title: Segurança e conformidade
description: Revisar os requisitos de segurança e conformidade do site.
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html?lang=pt-BR
source-git-commit: 999407f00b118441abe39209a15f587ec73fa75d
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Segurança e conformidade

A segurança é a maior preocupação no [!DNL Payment Services] e nenhuma informação privada ou regulamentada do PCI (Payment Card Industry, setor de cartões de pagamento) é passada para o seu [!DNL Payment Services].

## Segurança do Commerce

[!DNL Adobe Commerce] e [!DNL Magento Open Source] incluem suporte para vários recursos de segurança.

Consulte [Segurança](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/security/security){target="_blank"} no guia do usuário principal para analisar as práticas recomendadas de segurança e saber como gerenciar sessões e credenciais de administrador, implementar o CAPTCHA e gerenciar restrições de site.

## Conformidade com o PCI

O PCI (Payment Card Industry, setor de cartões de crédito e débito) estabeleceu um conjunto de requisitos para as empresas que aceitam pagamentos com cartão de crédito pela Internet. Além de manter um ambiente seguro, os comerciantes que lidam com as informações de cartão de crédito do cliente são responsáveis por atender a algumas diretrizes padrão.

Consulte as [Diretrizes de conformidade PCI](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"} para obter mais informações.

Os comerciantes podem preencher um [questionário de autoavaliação (SAQ)](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}, que é uma ferramenta de autovalidação para avaliar a segurança dos dados de titulares de cartão.

### Campos de cartão de crédito

Com os campos de cartão de crédito, nenhum dado regulado por PCI é transmitido em seus serviços. Você não precisa armazenar nem manter esses dados, o que reduz amplamente as preocupações com a conformidade com o PCI.

### 3DS

O PCI 3-D Secure (3DS) permite a autenticação do comprador com seu emissor de cartão de crédito ao fazer compras online de cartão de crédito. Essa camada adicional de segurança ajuda a impedir a fraude on-line e é necessária como parte das regulamentações de conformidade da União Europeia (UE).

O [!UICONTROL Payment Services] fornece a funcionalidade 3DS para permitir que os comerciantes cumpram os regulamentos da UE e protejam os clientes e comerciantes contra atividades fraudulentas em suas lojas.

Se você for um comerciante na UE ou na Grã-Bretanha onde a conformidade com 3DS é necessária, ative o 3DS manualmente (é `Off` por padrão) no [Administrador de Configuração](configure-admin.md#credit-card-fields).

>[!IMPORTANT]
>
>O requisito da 3DS aplica-se às transações em que o banco do titular do cartão e da empresa estão localizados no [Espaço Econômico Europeu](https://www.efta.int/eea) (EEE) e na Grã-Bretanha. Os comerciantes dos Estados Unidos não exigem o 3DS, mas podem habilitá-lo para suas transações, se desejado.

Os pedidos feitos ao comprador pelo comerciante ou pela equipe da loja não estão configurados com as medidas de conformidade 3DS. No entanto, se o emissor do cartão exigir 3DS, essa etapa não poderá ser ignorada, independentemente da configuração [!UICONTROL Payment Services].

>[!MORELIKETHIS]
>
> * Consulte [3DS nas configurações](configure-admin.md#3ds) para obter mais informações.
> * Consulte [cartões de teste](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/) na documentação do desenvolvedor do PayPal para obter mais informações sobre cartões de crédito específicos para testes 3DS.

### Compartimentalização da placa

Quando um comprador [salva—ou &quot;salva&quot;—suas informações de cartão de crédito](vaulting.md) para compras futuras em suas lojas, as informações mínimas de cartão de crédito são compartilhadas com o comprador (últimos quatro dígitos, data de expiração do cartão e marca do cartão). As informações de cartão de crédito são armazenadas com o provedor de serviço de pagamento. Quando um cartão expira ou quando as informações não precisam mais ser salvas, eles podem excluir esse token para que as informações não sejam mais armazenadas pelo provedor de serviço de pagamento.

Consulte [Compartimentalização de cartão de crédito](vaulting.md) para obter mais informações.

### Botões de pagamento do PayPal

Com os botões de pagamento PayPal, nenhum dado regulado por PCI é transmitido em seus serviços. Você não precisa armazenar nem manter esses dados, o que reduz amplamente as preocupações com a conformidade com o PCI.

Por motivos de segurança, o PayPal não passa o endereço de faturamento durante o check-out: país, email e nome são as únicas informações de faturamento usadas. Como opção, você pode ativar o check-out do PayPal do seu site para retornar o endereço de cobrança completo entrando em contato com o PayPal e concluindo um processo de verificação.

O PayPal também tem proteção integrada contra fraude que usa aprendizagem de máquina para ajudá-lo a combater fraude. Consulte a [Documentação de proteção ao vendedor](https://www.paypal.com/us/webapps/mpp/security/seller-protection) do PayPal para obter mais informações.

## Proteção contra fraude

Você pode habilitar a proteção automatizada contra fraude para Serviços de Pagamento com a [extensão Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html). Consulte [Proteção contra fraude Signifyd](fraud-protection.md) para obter mais informações.

O PayPal fornece outras opções para [proteção contra fraude](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank} na documentação do desenvolvedor:

* Consulte [Proteção contra fraude avançada](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank} para obter mais informações.
* Consulte [Proteção de chargeback](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank} para obter mais informações.
