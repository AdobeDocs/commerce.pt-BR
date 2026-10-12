---
title: Solução de problemas [!DNL App Management]
description: Resolva problemas comuns com a associação e configuração do aplicativo.
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%
---
# Solução de problemas [!DNL App Management]

Use as seguintes soluções para resolver problemas comuns com a associação e configuração do aplicativo.

## O aplicativo não é exibido

Se o aplicativo não for exibido na lista após a implantação, verifique as seguintes etapas:

1. Verifique se o aplicativo foi implantado e está disponível em sua organização.

1. Confirme se você está conectado à organização correta da Adobe no Developer Console.

1. Verifique se o aplicativo está pronto para se conectar (o desenvolvedor ou parceiro de aplicativo pode confirmar).

Se o aplicativo ainda não aparecer, contate o desenvolvedor do aplicativo ou verifique a documentação do [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} para obter informações técnicas.

## Falha na sincronização de escopo

Se a sincronização de escopo falhar ao associar um aplicativo, tente o seguinte:

1. Verifique se a sua instância do Commerce está acessível e online.

1. Verifique se as credenciais da API são válidas e têm as permissões corretas.

1. Tente sincronizar manualmente de **[!UICONTROL Manage Scopes]** na configuração do aplicativo.

## Configuração não salva

Se as alterações de configuração não forem salvas, tente o seguinte:

1. Verifique se todos os campos obrigatórios estão preenchidos e são válidos.

1. Verifique se você tem as permissões corretas para modificar a configuração do aplicativo.

1. Tente atualizar a página e salvar novamente.

Se o problema persistir, verifique se há erros no console do navegador ou entre em contato com o desenvolvedor do aplicativo.

Para obter solução de problemas técnicos, consulte [Extensibilidade do Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} para obter mais informações.
