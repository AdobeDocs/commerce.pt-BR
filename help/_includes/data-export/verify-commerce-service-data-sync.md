---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# Verificar sincronização de dados do serviço Commerce

Para verificar se a sincronização de dados está funcionando, confirme se os dados foram exportados com êxito do [!DNL Adobe Commerce] e se foram entregues com êxito ao serviço Commerce conectado. Use os painéis da sua implantação para verificar ambas as etapas.

Comece com export e depois confirme o delivery.

1. Verifique o status de sincronização no Commerce Admin.

   Vá para **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Página Status da sincronização do feed de dados com relatórios de status do item de feed](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   Quando a sincronização está em execução, os dados do feed mostram registros enviados com êxito. Selecione um feed para ver detalhes ou solucionar problemas de sincronização.

1. Confirme se os dados foram entregues aos Serviços Commerce conectados.

   No Administrador do Commerce, vá para **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Painel de Gerenciamento de Dados mostrando dados de catálogo sincronizados nos Serviços Commerce conectados](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Verifique se os produtos, preços e atributos esperados aparecem.

>[!TIP]
>
>Se você tiver problemas adicionais com a sincronização de dados, consulte [Revisar logs e solucionar problemas](/help/data-export/troubleshooting/logging.md).

