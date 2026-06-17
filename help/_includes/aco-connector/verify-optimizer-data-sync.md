---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# Verificar sincronização de dados do Otimizador

Confirme se os dados foram exportados com êxito do Administrador do Commerce e se foram entregues com êxito a [!DNL Commerce Optimizer]. Comece com a exportação no Administrador do Commerce e confirme a entrega em [!DNL Commerce Optimizer].

1. **Verifique o status de sincronização no Administrador do Commerce:**

   Vá para **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Página Status da sincronização do feed de dados com relatórios de status do item de feed](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   Quando a sincronização está em execução, os dados do feed mostram registros enviados com êxito. Selecione um feed para ver detalhes ou solucionar problemas de sincronização.

1. **Confirmar dados entregues para [!DNL Commerce Optimizer]:**

   No menu [!DNL Commerce Optimizer], selecione **[!UICONTROL Data Sync]**.

   ![Página de Sincronização de Dados no Adobe Commerce Optimizer mostrando os dados de catálogo sincronizados](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   Verifique se os produtos, preços e atributos esperados aparecem.

Quando a sincronização estiver funcionando como esperado:

- **[!UICONTROL Data Feed Sync Status]** mostra registros enviados com êxito para feeds de conector, sem erros de nível de item não resolvidos.
- **[!UICONTROL Data Sync]** em [!DNL Commerce Optimizer] lista as fontes de catálogo, os produtos, os preços e os atributos esperados.

>[!TIP]
>
>Se você tiver algum problema com a sincronização de dados, consulte o guia de [Solução de problemas](/help/aco-connector/troubleshooting.md).
