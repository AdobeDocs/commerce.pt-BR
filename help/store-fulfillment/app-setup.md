---
title: Configuração do aplicativo
description: Configure o aplicativo  [!DNL Store Assist]  para gerenciar fluxos de trabalho e processos completos de atendimento de lojas para compras online, retirada em pedidos de lojas.
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Configuração do aplicativo

O Store Assist é um aplicativo de plataforma de preenchimento como serviço (FaaS) desenvolvido pela Walmart Commerce Technologies. O aplicativo fornece recursos de preenchimento na loja para lidar com pedidos de [!DNL buy online, pick up in store] (BOPIS). Com o Store Assist, os associados da loja podem ver quais itens os clientes solicitaram, escolher os itens corretos mais rapidamente e configurar ordens preenchidas para entrega de coleta na loja ou na beira da calçada aos clientes.

O aplicativo Store Assist recebe todas as informações de pedidos e clientes, desde detalhes do pedido até os horários de coleta, e disponibiliza os dados para armazenar associados online, por meio de dispositivos móveis. O aplicativo inclui os módulos [!UICONTROL Pick], [!UICONTROL Stage], [!UICONTROL Handoff] e [!UICONTROL Orders] para ajudar a Store Associates a realizar atividades como as seguintes:

- Atribuir datas e horas de entrega da ordem.
- Receba notificações dos clientes quando eles chegarem para retirada de pedido.
- Faça pedidos de transferência para os clientes.
- Rastrear status de ordem para todas as ordens em seus locais de armazenamento atribuídos.

>[!NOTE]
>
>Saiba mais sobre o aplicativo Store Assist revisando o tópico [Fluxos de trabalho de atendimento do Store Assist](store-assist-modules.md).

## Configurar o aplicativo de assistência da loja

O aplicativo Store Assist requer dois tipos de configuração:

- As configurações do sistema do Administrador do Adobe Commerce para [gerenciar contas de usuário, funções de usuário, permissões de recursos](user-setup.md) e [disponibilizar as seleções de modelo e marca-veículo para os clientes durante o processo de check-in](check-in-experience-setup.md).

- Configurações de front-end para personalizar a interface do aplicativo Store Assist e outras configurações, incluindo:

   - **Marque o aplicativo Store Assist**. Personalize a interface do usuário do aplicativo com o logotipo e as cores da sua empresa.

   - **Atualizar as instruções padrão**—Personalize as instruções nos módulos Selecionar, Preparo, Transmissão e Pedido da Assistência da Loja para orientar os Associados da Loja em cada etapa do fluxo de trabalho de preenchimento da sua empresa.

   - **Localização** — Selecione o idioma disponível para o aplicativo. Escolha o formato de data e hora e selecione as unidades de medida padrão e a moeda padrão.

   - **Tempo de inatividade** — Especifique por quanto tempo o aplicativo deve ficar inativo antes de ser desconectado.

   - **Cancelamento do armazenamento** — Especifique se os pedidos podem ser cancelados no armazenamento e quais funções têm permissões de cancelamento

   - **Janela de limpeza da ordem**—Especifique quanto tempo passou o [Prazo de Entrega Estimado](enable-general.md#delivery-method-title-configuration) em que uma ordem separada permanece na preparação antes de ser reabastecida—por exemplo, três dias. O valor padrão é sete dias. Se essa configuração estiver ativada, a ordem será automaticamente cancelada quando esse tempo expirar. Os itens são reabastecidos e o comerciante recebe um email de cancelamento.

   - Personalize tudo nas instruções do aplicativo (seleção, preparo, entrega).

   - **Notificações de separação** — Especifique se deseja enviar uma notificação por push para iniciar o processo de separação depois que um cliente fizer um pedido.

   - **Notificações de check-in**—Especifique se deseja enviar uma notificação por push durante o processo de check-in para retiradas de pedidos- depois do check-in, depois que o tempo de espera do cliente exceder um período especificado. Ou desative a notificação.

   - **Processo de entrega**—Habilite processos opcionais quando o Associado da Loja entregar o pedido ao cliente, por exemplo, exigir uma assinatura do cliente ou solicitar que o associado verifique a ID do cliente.

   - **Habilitar rejeição de item na entrega**—Permite que os clientes devolvam ou cancelem itens de pedido durante a entrega do pedido.

  Trabalhe com a equipe de Serviços ao Cliente da Walmart Commerce Technologies para concluir a configuração de front-end para o aplicativo Store Assist.

## Download e instalação do aplicativo

Após a instalação e configuração do aplicativo Store Assist, os associados da loja poderão baixar, instalar e fazer logon no aplicativo Store Assist a partir de seus dispositivos móveis.

- Verifique se o dispositivo móvel atende aos [requisitos de hardware e software](solution-requirements.md#store-assist-app-requirements) da solução de Atendimento da Loja.

- Baixe o aplicativo Store Assist da [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} ou da [Google Play store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.

- Os associados da loja exigem as seguintes informações para fazer logon:

   - **[!UICONTROL Company name]** associado à conta de Assistência de Repositório

   - **Credenciais da conta de Assistência de Repositório** — credenciais de nome de usuário e senha para a conta.

  Um Administrador do Adobe Commerce pode criar e gerenciar contas de usuário do [!DNL Store Assist app] para todos os locais de armazenamento que têm a [Seleção na Loja](merchant-store-configuration.md#pickup-location-configuration) habilitada nas configurações de Admin Stores.
