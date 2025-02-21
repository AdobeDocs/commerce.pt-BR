---
title: Configuração de lojas de comerciantes
description: Configure origens aprimoradas do Inventory management como lojas de comerciantes.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Configuração de lojas de comerciantes (Source)

Essa solução aprimora os recursos nativos do Inventory management, estendendo as fontes de estoque com recursos orientados para operações para os comerciantes.

- Adicionar coordenadas geográficas para o local da loja
- Designar a origem como [!DNL Store Pickup Location] e especificar os recursos de remessa disponíveis (Entregar para Loja, Remeter de Loja)
- Especifique as opções de retirada disponíveis (na loja ou na berma), as instruções de retirada personalizadas e outras informações para comunicar os detalhes e as instruções da retirada aos clientes

Os termos _origem_ e _local de armazenamento de comerciante_ são usados alternadamente. Todos os registros são origens de inventário, mas as origens também podem ser locais de armazenamento do comerciante, dependendo das definições de configuração.

Gerenciar a configuração de Lojas do Comerciante no Administrador: **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**.

>[!NOTE]
>
>Durante o processo de configuração, pode ser necessário liberar o cache após criar origens ou atualizar origens existentes.

## **Geral**

<table>
<tbody>
<tr>
<th>Campo</th>
<th>Descrição</th>
<th>Escopo</th>
<th>Obrigatório</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordenada latitudinal do local de armazenamento do comerciante. Essas informações necessárias são usadas na pesquisa de localização e no posicionamento do mapa na experiência da loja. O valor deve corresponder ao endereço exato do armazenamento para passar na validação.</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordenada longitudinal do local de armazenamento do comerciante. Essas informações necessárias são usadas na pesquisa de localização e no posicionamento do mapa na experiência da loja. O valor deve corresponder ao endereço exato do armazenamento para passar na validação.</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Designar a origem como um local de Retirada de Armazenamento disponível. Essa configuração determina se a origem é sincronizada e exibida aos visitantes.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>Configurar recursos de entrega para armazenamento no nível da origem. Para obter mais informações, consulte a opção [Configuração Geral](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordenada latitudinal do local de armazenamento do comerciante. Essas informações necessárias são usadas na pesquisa de localização e no posicionamento do mapa na experiência da loja. O valor deve corresponder ao endereço exato do armazenamento para passar na validação.</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordenada longitudinal do local de armazenamento do comerciante. Essas informações necessárias são usadas na pesquisa de localização e no posicionamento do mapa na experiência da loja. O valor deve corresponder ao endereço exato do armazenamento para passar na validação.</td>
<td>Global</td>
<td>Sim</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Designar a origem como um local de Retirada de Armazenamento disponível. Essa configuração determina se a origem é sincronizada e exibida aos visitantes.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>Configurar recursos de entrega para armazenamento no nível da origem. Para obter mais informações, consulte a opção [Configuração Geral](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]</strong>.</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>Configurar recursos de entrega de armazenamento no nível da origem. Para obter mais informações, consulte a opção [Configuração Geral](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td>Global</td>
<td>Não</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>Configurar recursos de entrega de armazenamento no nível da origem. Para obter mais informações, consulte a opção [Configuração Geral](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Global</td>
<td>Não</td>
</tr>
</tbody>
</table>



| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | Coordenada latitudinal do local de armazenamento do comerciante. Essas informações necessárias são usadas na pesquisa de localização e no posicionamento do mapa na experiência da loja. O valor deve corresponder ao endereço exato do armazenamento para passar na validação. | Global | Sim |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | Coordenada longitudinal do local de armazenamento do comerciante. Essas informações necessárias são usadas na pesquisa de localização e no posicionamento do mapa na experiência da loja. O valor deve corresponder ao endereço exato do armazenamento para passar na validação. | Global | Sim |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | Designar a origem como um local de Retirada de Armazenamento disponível. Essa configuração determina se a origem é sincronizada e exibida aos visitantes. | Global | Não |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | Configurar recursos de entrega para armazenamento no nível da origem. Para obter mais informações, consulte a opção [Configuração Geral](enable-general.md), **[!UICONTROL Enable Ship To Store]**. | Global | Não |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | Configurar recursos de entrega de armazenamento no nível da origem. Para obter mais informações, consulte a opção [Configuração Geral](enable-general.md), [!UICONTROL Enable Ship From Store] | Global | Não |

{style="table-layout:auto"}

## Configuração do local de retirada

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | Uma das duas opções de retirada. [!DNL In-Store Pickup] refere-se à capacidade de permitir que um cliente entre no local da loja de comerciante para recuperar seu pedido. </br></br>Quando habilitada, esta opção pode ser apresentada ao cliente durante o check-out. </br></br>Esta opção também substitui a configuração global para [!UICONTROL Enable In-store Pickup] que foi configurada em [!UICONTROL Delivery Method] para [!UICONTROL In-store Pickup] | Global | Não |
| **Instruções para retirada na loja**</br>`Extension Attribute: store_pickup_instructions` | Uma mensagem personalizável foi entregue ao cliente na notificação por email **Pedido pronto para retirada na loja**. | Global | Não |
| **Permitir Curbside**</br>`Extension Attribute: curbside_enabled` | Uma das duas opções de retirada. A entrega na calçada permite que um cliente estacione seu veículo em um ponto designado no local da loja. Nesse cenário, a ordem é entregue ao cliente por um associado da loja. </br></br>Quando habilitada, esta opção pode ser apresentada ao cliente durante o check-out. Além disso, o cliente pode ser solicitado a descrever o veículo e o local de estacionamento durante o processo de check-in. </br></br>Esta opção também substitui a configuração global para **Habilitar Seleção pela Curva** que foi configurada no **Método de Entrega** para **Seleção na loja** | Global | Não |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | Uma mensagem personalizável entregue ao cliente na notificação por email do [!UICONTROL Order Ready For Pickup in Store]. | Global | Não |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | O número de minutos necessários antes de uma ordem ser recebida, separada e pronta para ser retirada. </br></br>Essas informações são usadas para exibir tempos estimados para retirada de pedido para clientes no site.</br></br> A configuração dessa opção substitui a configuração global para **Lead Time de Retirada Estimado** configurado para o **Método de Entrega** na configuração **Retirada na Loja**. | Global | Não |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | Rótulo que exibe o número de minutos até que um pedido esteja pronto para ser retirado.</br></br> Ao personalizar este rótulo, você pode usar o código %1 para inserir seu **Prazo de Entrega Estimado**.</br></br> Essa opção substitui a configuração global de [!UICONTROL Estimated Pickup Time Label], definida para [!UICONTROL Delivery Method] em [!UICONTROL In-store Pickup]. | Global | Não |

### **Horário de funcionamento**

| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | O fuso horário do local de armazenamento do comerciante. Para cada dia, defina os horários de abertura e fechamento.</br></br>Essas configurações são usadas para otimizar os tempos estimados de retirada e nos relatórios do serviço de atendimento. | Global | Sim |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | O horário de funcionamento do local de armazenamento do comerciante. </br></br>Essas informações podem ser usadas para otimizar os tempos estimados de retirada e nos relatórios do serviço de atendimento. | Global | Sim |

### Configurar as opções da interface da experiência de check-in



| **Campo** | **Descrição** | **Escopo** | **Obrigatório** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | Especifique se o local da loja do comerciante tem vagas de estacionamento com designação para retirada na beira da calçada. </br></br>Quando habilitado, você pode configurar as vagas disponíveis. | Global | Não |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | Especifique se a identificação do local de estacionamento é necessária para os clientes durante a experiência de compras.</br></br>Se ativado, o cliente será solicitado a especificar seu local de estacionamento na chegada. Se estiver desativado, o cliente poderá ignorar essa entrada. | Global | Não |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | Os lugares de estacionamento disponíveis nesta loja de comércio local para retirada na calçada. Use a interface fornecida para nomear cada ponto.</br></br> Você não precisa nomear cada vaga de estacionamento, somente as vagas designadas como berço. Por exemplo, você pode ter linhas A-G de estacionamento disponíveis, mas apenas os primeiros 8 pontos da linha A são designados para coleta à beira-mar. Neste cenário, você pode definir 8 pontos; por exemplo: A1, A2, A3 e assim por diante. | Global | Não |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | Quando ativada, essa configuração permite que o cliente descreva seu local de estacionamento durante o check-in. | Global | Não |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | Especifique se a coleção de cores do veículo do cliente deve ser suportada durante o Check-in. </br></br> As seleções disponíveis para [!UICONTROL Car Color] estão definidas nas [configurações do sistema do Administrador para a Experiência de Check-in](check-in-experience-setup.md). | Global | Não |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | Especifique se a identificação de cor do veículo é necessária para clientes durante o Check-in.</br></br>Se habilitado, o cliente será solicitado a especificar a cor de seu veículo na chegada. Se estiver desativado, o cliente poderá ignorar essa entrada. | Global | Não |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | Especifique se a coleta de veículo deve ser suportada pelo cliente durante o Check-in.</br></br> As seleções disponíveis para [!UICONTROL Car Make] estão definidas nas [configurações do sistema do Administrador para a Experiência de Check-in](check-in-experience-setup.md). | Global | Não |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | Especifique se a identificação da marca do veículo é necessária para clientes durante o Check-in.</br></br>Se habilitado, o cliente será solicitado a especificar a marca de seu veículo na chegada. Se estiver desativado, o cliente poderá ignorar essa entrada. | Global | Não |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | Especifique se deseja oferecer suporte à coleta de informações adicionais do cliente durante o Check-in. | Global | Não |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | Especifique se informações adicionais são necessárias para clientes durante o Check-in. </br></br>Se habilitado, o cliente será solicitado a inserir informações adicionais na chegada. Se estiver desativado, o cliente poderá ignorar essa entrada. | Global | Não |
