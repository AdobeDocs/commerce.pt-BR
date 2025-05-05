---
title: Localização de armazenamento e configuração do sistema de mapeamento
description: Configure um provedor de distância para oferecer suporte ao mapeamento de localização de loja na interface de loja. As soluções de Atendimento da Loja exigem um provedor à distância para habilitar a pesquisa na loja de varejo e outros recursos de mapeamento e agendamento para o fluxo de trabalho de atendimento completo.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Localização de armazenamento e configuração de mapeamento

Habilite o local de armazenamento e os recursos de mapeamento para Atendimento de Loja configurando um [provedor de distância](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/configuration/distance-priority-algorithm) para procurar locais de loja de varejo.

**Requisitos**

Durante o processo de configuração, você fornece uma chave de API do Google para a plataforma Google Maps. Se você não tiver um, [gere um da plataforma Google Maps](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps).

Para configurar o provedor de distância:

1. Na configuração **[!UICONTROL Stores > General]** em Admin, adicione a integração do Google Maps para o tipo de conteúdo Map.

   - Ir para **[!UICONTROL Stores > Configuration  > General > Content Management]**.

   - Adicione sua Chave da API do Google ao campo **[!UICONTROL Google Maps API Key]**.

1. Na configuração **[!UICONTROL Stores > Inventory]** em Admin, selecione o provedor de distância para Atendimento da Loja.

   - Ir para **[!UICONTROL Stores > Configuration > Catalog > Inventory]**.

   - Expanda a seção **[!UICONTROL Distance Provider for Distance Based SSA]**.

   - Defina o **Provedor** como **Mapa do Google**.

1. Definir configurações para o **[!UICONTROL Google Distance Provider]**.

   - Adicione sua **chave de API do Google**.

   - Definir **[!UICONTROL Computation Mode]** como `Driving` e **[!UICONTROL Value]** como `Distance`
