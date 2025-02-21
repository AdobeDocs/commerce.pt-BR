---
title: Visão geral de integração para serviços de fornecimento da loja
description: Fluxo de integração, requisitos do sistema, limites e limitações do [!DNL Live Search].
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Visão geral de integração do fornecimento da loja

Comece a usar o [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] instalando, configurando e habilitando os seguintes componentes:

- **Armazenar extensão de Abastecimento** - Instale e configure essa extensão de terceiros na sua instância do Adobe Commerce. Após a instalação, você pode configurar e gerenciar a solução Store Fulfillment do Administrador para dar suporte a cenários do [!DNL buys online, pickup in store] (BOPIS) na loja da Commerce.

  Configuração de ![[!DNL Store Fulfillment Service] no modo de exibição de Administração](assets/store-fulfillment-admin-home.png)

- **Conta de Atendimento da Loja** - Durante o processo de habilitação, um Gerente de Conta cria sua conta de Atendimento da Loja e fornece as informações e credenciais da conta. Essas credenciais são necessárias para habilitar a conexão entre o Adobe Commerce e a solução Store Fulfillment.

- **Aplicativo de Assistência da Loja** — Fornece associações da loja com um fluxo de trabalho completo de preenchimento da loja para gerenciar pedidos de BOPIS de dispositivos móveis. A Store Associates pode baixar e instalar o [!DNL Store Assist] do Walmart para dispositivos iOS e Android™. O processo de integração de aplicativos é gerenciado pelo Centro de Clientes de Tecnologias Walmart Commerce como um processo separado. No entanto, [algumas configurações do aplicativo](user-setup.md) foram concluídas com o Administrador do Adobe Commerce.

  | Aplicativo de Assistência da Loja - Exibição de introdução | Aplicativo Store Assist — visualização Módulos |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | ![[!DNL Store Assist App Getting Started] exibir no dispositivo móvel](assets/store-assist-get-started-small.png) | ![[!DNL Store Assist App Orders view] no dispositivo móvel](assets/store-assist-orders-small.png) |

## Etapas de provisionamento

- **Inscreva-se em[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]** - Preencha o formulário de inscrição em [business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html) ou entre em contato com seu Gerente de Contas da Adobe Commerce para obter assistência.

- **Iniciar a solicitação de provisionamento para Atendimento da Loja**-Preencha o formulário de entrada fornecido pelo seu Gerente de Conta para fornecer as informações necessárias para iniciar o processo de provisionamento.

- **Obter credenciais da conta de Atendimento da Loja** - Depois que a conta de Atendimento da Loja for criada para você, você receberá as credenciais necessárias para integrar a solução de Atendimento da Loja com a Adobe Commerce.

- **[Baixe o código fonte para instalar a [!DNL Store Fulfillment] extensão](install.md)**

## Etapas de integração

1. [Instalar a extensão Store Fulfillment para Adobe Commerce](install.md).

1. Do Administrador, [habilite a solução](enable-general.md).

1. [Configurar a extensão de Atendimento de Repositório do Administrador do Adobe Commerce](service-config-settings-overview.md).

1. [Conecte o serviço [!DNL Store Fulfillment] usando as credenciais de Atendimento de Armazenamento fornecidas](connect-set-up-service.md).

1. [Crie usuários e funções para o aplicativo Store Assist](user-setup.md).

1. [Baixe o aplicativo  [!DNL Store Assist] do Walmart no dispositivo desejado. O aplicativo está disponível nas lojas de aplicativos Apple (iOS) e Google Play (Android™)](app-setup.md).

Após instalar, configurar, concluir a integração com êxito e ter acesso ao aplicativo [!DNL Store Assist], você pode [começar a criar pedidos e testes](test-and-deploy.md).
