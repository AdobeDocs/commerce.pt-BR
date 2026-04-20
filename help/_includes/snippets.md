---
source-git-commit: 966daee60fa8945a68424fca8bda4fe4b9599872
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---
# Commerce snippets


## Verificação da Sincronização de Dados para o Otimizador {#aco-data-sync-verification}

>[!NOTE]
>
>Se você instalou o [Conector do Adobe Commerce Optimizer](../aco-connector/overview.md) para exportar dados de catálogo para o Adobe Commerce Optimizer, use a [página Status de sincronização do feed de dados](../optimizer/setup/data-sync.md) na interface do usuário do Commerce Optimizer para verificar os dados sincronizados com êxito com o Adobe Commerce Optimizer em vez do Painel de Gerenciamento de Dados.

## Acesso antecipado ao ACCS {#accs-early-access}

>[!NOTE]
>
>Esta documentação descreve um produto em desenvolvimento de acesso antecipado e não reflete toda a funcionalidade destinada à disponibilidade geral.

<!--
## Nav hack ACCS {#nav-hack-accs}

>[!BEGINSHADEBOX]

<table style="table-layout:fixed">
  <tr>
    <td style="vertical-align: middle;"><a href="https://developer.adobe.com/commerce/webapi/"><img alt="Developers" src="../assets/icons/developers.svg" /> <strong>Developers</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/"><img alt="Storefront" src="../assets/icons/storefront.svg" /> <strong>Storefront</strong></a></td>
    <td style="vertical-align: middle;"><a href="../cloud-service/overview.md"><img alt="Merchants" src="../assets/icons/merchants.svg" /> <strong>Merchants</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/commerce-as-a-cloud-service/overview"><img alt="Videos" src="../assets/icons/videos.svg" /> <strong>Videos</strong></a></td>
    <td style="vertical-align: middle;"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/playgrounds/commerce-services/"><img alt="Playgrounds" src="../assets/icons/playgrounds.svg" /> <strong>Playgrounds</strong></a></td>
  </tr>
</table>

>[!ENDSHADEBOX]
-->

## Recurso experimental somente de sandbox ACCS {#accs-sandbox-experimental}

>[!IMPORTANT]
>
>Este recurso é experimental e só está disponível em ambientes de sandbox do [!DNL Adobe Commerce as a Cloud Service].
>
>Este recurso está sujeito a alterações sem aviso prévio.

[!BADGE Sandbox]{type=Caution tooltip="Os itens listados estão disponíveis atualmente apenas em ambientes de sandbox. A Adobe disponibiliza novas versões em ambientes de sandbox primeiro para fornecer tempo para testar alterações futuras antes que a versão esteja disponível em ambientes de produção."}

## Mapeamento de instâncias do AEM Assets {#aem-assets-instance-mapping}

>[!NOTE]
>
>Ao conectar [!DNL Adobe Commerce as a Cloud Service] a [!DNL AEM Assets], sua instância de Preparo [!DNL AEM Assets] mapeia para sua instância de Sandbox [!DNL Adobe Commerce as a Cloud Service] e quaisquer outros ambientes de não produção. Sua instância de Produção [!DNL AEM Assets] mapeia para sua instância de Produção [!DNL Adobe Commerce as a Cloud Service].

## Identidade do IMS e informações de logon único {#ims-identity-and-sso-config}

O gerenciamento e a autenticação de identidade da Adobe Commerce são gerenciados pelo Adobe Identity Management System (IMS) por meio da Adobe Admin Console.

Para obter informações sobre opções de configuração de identidade, incluindo Adobe ID, Enterprise ID e Federated ID, e instruções para configurar o Logon Único (SSO) para acesso seguro a aplicativos Adobe, consulte [Configurar identidade e logon único](https://helpx.adobe.com/enterprise/using/set-up-identity.html) na documentação do *Enterprise Admin Console*.

## Notas de versão de serviços e extensibilidade do ACCS {#accs-release}

### Notas de versão adicionais

[!DNL Adobe Commerce as a Cloud Service] contém as versões mais recentes dos serviços de merchandising, serviços de pagamento e versões de extensibilidade. Use os links a seguir para exibir as notas de versão de cada um:

| Serviços | Extensibilidade | Loja |
| --- | --- | --- |
| <ul><li>[Serviço de catálogo](../catalog-service/release-notes.md)</li><li>[Live Search](../live-search/release-notes.md)</li><li>[Serviços de pagamento](../payment-services/release-notes.md)</li><li>[Recomendações de produto](../product-recommendations/release-notes.md)</li><li>[Exportação De Dados SaaS](../data-export/release-notes.md)</li></ul> | <ul><li>[SDK da interface do administrador](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)</li><li>[API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)</li><li>[Eventos](https://developer.adobe.com/commerce/extensibility/events/release-notes/)</li><li>[Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)</li></ul> | <ul><li>[Informações sobre a versão](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)</li><li>[Log de alterações](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/)</li></ul> |

## Notas de versão dos serviços da Adobe Commerce Optimizer {#aco-release}

### Notas de versão adicionais

O [!DNL Adobe Commerce Optimizer] funciona com as versões mais recentes da integração do AEM Assets, o conector do Commerce Optimizer e o [!DNL Adobe Commerce Storefront]. Use os links a seguir para exibir as notas de versão de cada área:

| Serviços | Loja |
| --- | --- |
| [integração do AEM Assets](../aem-assets-integration/release-notes.md)<br>[conector do Commerce Optimizer](../aco-connector/release-notes.md) | [Informações sobre a versão da loja](https://experienceleague.adobe.com/developer/commerce/storefront/releases/)<br>[changelog da loja](https://experienceleague.adobe.com/developer/commerce/storefront/releases/changelog/) |
