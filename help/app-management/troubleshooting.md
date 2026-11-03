---
title: Solução de problemas [!DNL App Management]
description: Resolva problemas comuns com a associação, instalação, configuração e atualizações do aplicativo.
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
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# Solução de problemas [!DNL App Management]

Use as seguintes soluções para resolver problemas comuns com a associação, instalação, configuração e atualizações do aplicativo.

## Antes de entrar em contato com o provedor do aplicativo

Siga as etapas para o problema abaixo. Se precisar de ajuda do desenvolvedor ou provedor do aplicativo, colete as seguintes informações:

* Nome do aplicativo e versão instalada, se disponíveis em **[!UICONTROL Manage]** > **[!UICONTROL Details]** no cartão do aplicativo.
* Instância da Commerce e organização da Adobe afetadas.
* Operação que falhou, como instalação ou atualização, e a etapa que falhou.
* Exibida uma mensagem de erro e uma captura de tela da falha, se disponível.
* Hora aproximada da falha, incluindo o fuso horário.
* Qualquer tentativa de repetição e seus resultados.

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

## Falha na instalação

Mantenha a página de instalação aberta sem atualizar até que a instalação seja concluída. Fechá-lo ou atualizá-lo pode impedir a conclusão correta da instalação.

Se a instalação reportar uma falha:

1. Anote o item com falha e as mensagens de erro exibidas.

1. Verifique se você concluiu as instruções de pré-instalação do aplicativo.

1. Peça ao desenvolvedor do aplicativo para inspecionar a etapa que falhou e corrigir a causa antes de tentar a instalação novamente.

Uma instalação com falha pode deixar algumas alterações aplicadas. Quando a instalação é repetida, as etapas personalizadas registradas como bem-sucedidas são ignoradas; etapas com falha ou interrompidas podem ser executadas novamente. Peça ao desenvolvedor para verificar os recursos criados pela execução parcial.

## Falha na atualização

Uma atualização com falha pode deixar algumas operações aplicadas. Não desassocie e reinstale o aplicativo como uma etapa de recuperação de rotina, pois a desassociação remove a configuração e pode executar scripts de limpeza destrutivos.

1. Identifique a etapa que falhou e registre as mensagens de erro exibidas.

1. Peça ao desenvolvedor do aplicativo para inspecionar os logs, verificar se há alterações já feitas no Commerce ou em recursos externos e corrigir a causa.

1. Em [!DNL App Management], selecione **[!UICONTROL Retry Upgrade]**. Esta ação está disponível para os modos de atualização manual e automático.

Cada tentativa cria um novo plano a partir do estado atual. Etapas de instalação personalizadas registradas como bem-sucedidas são ignoradas; etapas com falha ou interrompidas podem ser executadas novamente. No modo automático, a implantação do aplicativo novamente também aciona outra tentativa de atualização.

Se tentativas repetidas falharem, peça ao desenvolvedor do aplicativo para manter as IDs de execução ou tentativa e qualquer ID de ativação de execução para solução de problemas. Para comandos de status, histórico de tentativas e logs de Tempo de Execução, consulte [Repetir uma atualização com falha](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"} na documentação do desenvolvedor.

## Os recursos permanecem após uma atualização

A remoção de uma etapa de instalação personalizada da configuração de um aplicativo não executa seu script de desinstalação nem remove os recursos que ele criou. O plano de atualização avisa que nenhum script é executado para a etapa removida e a etapa não é exibida na tela de progresso ou nos detalhes do aplicativo após a atualização.

Peça ao desenvolvedor do aplicativo para confirmar se os recursos ainda são necessários e fornecer uma migração de limpeza quando necessário. Consulte [Atualizar um aplicativo](manage-app.md#upgrade-an-app) para obter o fluxo de trabalho do administrador.

Para obter solução de problemas técnicos, consulte [Extensibilidade do Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} para obter mais informações.
