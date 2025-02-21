---
title: Visão Geral da Configuração para Atendimento da Loja
description: Saiba mais sobre os tipos de definições de configuração de Administrador disponíveis para personalizar os recursos de preenchimento estendido fornecidos pela solução Store Fulfillment e forneça um link para as instruções de conclusão da configuração.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Visão geral da configuração para Atendimento da loja

No Administrador do Adobe Commerce, as definições de configuração para Serviços de Atendimento da Loja pela Walmart Commerce Technologies são categorizadas por tipo.

**Armazenar definições de configuração de Abastecimento por tipo**

| **Tipo** | **Descrição** | **API Configurável** |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [Configuração Geral](enable-general.md) | Integração geral configurada para a solução Store Fulfillment, seus recursos ativos e credenciais para se conectar aos serviços de fulfillment. | Não |
| [Configuração de email de vendas](sales-emails.md) | Configurar modelos de email adicionais para notificações de clientes enviadas durante o processo de check-in. | Não |
| [Configuração da Loja do Comerciante](merchant-store-configuration.md) | Configure origens aprimoradas do Inventory management como lojas de comerciantes. | Sim |
| [Gerenciamento do Estoque de Produtos](product-stock.md) | Configurar as mensagens e os recursos do estoque de comerciantes disponíveis para os clientes. | Sim |
| [Transferência do Inventory management Source](inventory-stock-transfer.md) | Configure um novo estoque, transfira o estoque do estoque padrão. | Sim |
| [Várias Configurações de Site/Escopo](multi-site-and-scope-config.md) | Configurar estoques e métodos de entrega para vários sites/escopos de loja. | Não |
| [Configuração de Sistema de Processo em Segundo Plano](background-processes.md) | Configure os cronogramas dos processos em segundo plano usados na sincronização de dados com os serviços de preenchimento. | Não |
| [Local de Armazenamento e Configuração de Mapeamento](store-location-map-provider-setup.md) | Configurar a capacidade de usar um provedor de distância para procurar lojas de varejo e exibir essas informações no mapa de SLS | Sim |
| [Configuração da Experiência de Check-in](check-in-experience-setup.md) | Configurar a cor do carro e as opções de fabricação do carro que estarão disponíveis durante o processo de check-in | Sim |
| [Configuração de Usuário](user-setup.md) | Gerencie contas de usuário, funções e permissões para associados da loja que usam o aplicativo Store Assist. escopos. | Sim |
| [Instalação do aplicativo](app-setup.md) | Examine as configurações disponíveis para o Aplicativo de Assistência da Loja, necessárias para concluir o processo de integração. Essas configurações não podem ser definidas pelo administrador do Adobe Commerce. | Sim |

## Usar a referência de configuração

Exiba a referência de configuração para cada tipo de configuração selecionando o nome do tipo na tabela _Configurações de Atendimento da Loja por tipo_.

Na referência de configuração de cada tipo, os detalhes da configuração são exibidos em uma tabela com os seguintes cabeçalhos de coluna:

- **Campo** refere-se ao nome do campo a ser configurado

- **Descrição** fornece detalhes importantes sobre a finalidade e o comportamento do campo

- **Escopo** indica o escopo de configuração do Adobe Commerce para a configuração (global, site, armazenamento)

- O valor **Obrigatório** indica se um valor deve ser definido no campo

Para referência técnica, você também pode encontrar o caminho de configuração interno para cada campo.
