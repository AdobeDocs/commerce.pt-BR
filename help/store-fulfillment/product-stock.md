---
title: Gerenciamento de Estoque de Produtos
description: Configurar as mensagens e os recursos do estoque de comerciantes disponíveis para os clientes.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Gerenciamento de Estoque de Produtos

Como comerciante, você pode usar as opções de ações e de origem do Adobe Commerce [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction). Além disso, você pode usar a solução Store Fulfillment para controlar outras opções de disponibilidade de estoque relacionadas às operações de sua loja de comerciantes.

- Opção de entrega doméstica de lojas comerciantes

- Permitir/Disponível para retirada de loja

- UPC / SKU / Outros identificadores exclusivos do produto

- Limite de Fora do Estoque

- Diminuindo o Inventário a partir de locais específicos na ordem

Configurar opções de estoque do produto do Administrador: **[!UICONTROL Catalog > Products > Select Product]**

## **Opções de Estoque de Produtos**

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|
| **Disponível para Entrega Doméstica** | <p>Define a disponibilidade da Distribuição inicial (Entrega da loja) do produto. Quando ativado, qualquer local de loja do comerciante atribuído com estoque disponível para o produto é considerado qualificado para a opção Entrega doméstica. Quando essa opção está desativada, o produto nunca é qualificado para a Entrega inicial.</p>Normalmente, definir essa opção no nível da loja de comerciante é suficiente. No entanto, pode haver casos únicos de produtos específicos, como aqueles sob restrições federais de envio, que não devem ser qualificados para Entrega doméstica.</p> | Site | Não |
| **[!UICONTROL Available for Store Pickup]** | <p>Defina a disponibilidade da Seleção da loja para o produto. Quando habilitado, qualquer local de loja de comerciante atribuído com estoque disponível para o produto é considerado qualificado para a opção Retirada da loja. Quando desativado, o produto nunca está qualificado para Coleta na loja.</p><p>Essa opção pode ser útil para rastrear o inventário do comerciante no sistema que você não deseja vender do seu canal de comércio eletrônico.</p> | Site | Não |
| **[!UICONTROL UPC / SKU / Custom Scannable Identifier]** | Este atributo deve existir como um atributo de produto e está relacionado à configuração **[!UICONTROL Barcode Source / Barcode Type]**. Esse atributo é usado para rastrear um código de barras digitalizável para seus produtos. Esse valor pode ser enviado quando um pedido é enviado às lojas de comerciantes para separação. Os associados da loja podem usar o valor com a lista de separação para corresponder produtos na prateleira usando um scanner de código de barras. | Exibição da loja | Não |

{style="table-layout:auto"}

## Origens para estoque no nível de produto

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Out of Stock Threshold]** | <p>Defina o limite de estoque para o item em cada origem. Quando o estoque cai abaixo do limite, ele é considerado esgotado na origem.</p><p>Para usar a configuração de armazenamento global, marque a opção **[!UICONTROL Use Default]**.</p> | Global | Não |
| **[!UICONTROL Allow Store Pickup]** | <p>Defina explicitamente se o item está disponível para retirada de armazenamento, independentemente da configuração disponível de estoque ou localização de armazenamento do comerciante.</p><p>Para usar a configuração de nível de produto, desmarque a opção [!UICONTROL Use Default] e faça a seleção. Caso contrário, essa configuração será escolhida com base na configuração de **[!UICONTROL Allow In-Store Pickup]** definida na origem do estoque.</p> | Global | Não |

{style="table-layout:auto"}

