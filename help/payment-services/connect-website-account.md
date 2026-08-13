---
title: Conectar uma conta diferente do PayPal a um site
description: Integração completa do PayPal no âmbito do site no Admin para conectar uma conta de comerciante do PayPal diferente a um site individual.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Conectar uma conta diferente do PayPal a um site

Para instâncias do Commerce com **vários sites**, talvez você precise de **contas de comerciante do PayPal diferentes**. [!DNL Payment Services] habilita a integração do PayPal **com escopo de site** após a integração do **global**.

>[!NOTE]
>
> Este recurso só oferece suporte à conexão de novas contas.

## Pré-requisitos para integração com escopo de site

A integração no nível do site só estará disponível depois que a loja atender aos seguintes requisitos:

- A instalação do [Commerce Services Connector](https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/integration-services/saas) foi concluída.
- Uma conta do PayPal é conectada ao escopo global (Configuração padrão).

Você pode confirmar isso verificando se os seguintes campos estão preenchidos no escopo padrão:

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

Se esses campos estiverem vazios, você deverá [concluir a integração global](configure-admin.md) primeiro. O botão **[!UICONTROL Connect different account]** ficará desabilitado até que você conclua os pré-requisitos.

## Iniciar a conexão no nível do site

1. Na barra lateral _Admin_, vá para **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**&#x200B;e escolha **[!UICONTROL Payment Methods]**.
1. No seletor de escopo, no canto superior esquerdo, alterne de **[!UICONTROL Default Config]** para o **[!UICONTROL Website]** que deseja integrar.
1. Clique em **[!UICONTROL Connect different account]**.

   Se o botão estiver desabilitado, seu armazenamento não atendeu aos [pré-requisitos](#prerequisites-global-scope) acima.

## Concluir o modal de integração

Uma janela pop-up é aberta.

1. Selecione seu **[!UICONTROL Country]** na lista suspensa.
1. Escolha seu tipo de integração: **[!UICONTROL Basic]** ou **[!UICONTROL Advanced]**.
1. Clique em **[!UICONTROL Next]**.

>[!NOTE]
>
> Se você estiver fazendo a integração na Hungria, Espanha ou Áustria, abra e exiba o link de Termos e Condições para poder clicar no botão **[!UICONTROL I Accept]**. O botão estará desativado até que você abra os Termos e Condições.

## Fazer logon no PayPal

Depois de ser redirecionado para o logon do PayPal, faça logon e conclua as etapas de integração no PayPal.

>[!IMPORTANT]
>
> Depois de clicar em **[!UICONTROL Confirm and Continue]**, a sessão do escopo global será encerrada e a conexão no nível do site será iniciada. Se você clicou acidentalmente em **[!UICONTROL Connect different account]**, é possível cancelar selecionando **[!UICONTROL Cancel]** ou clicando no ícone **X** antes de confirmar.

## Concluir e retornar ao administrador

1. Após concluir as etapas do PayPal, feche a janela PayPal.
1. Clique em **[!UICONTROL Finish]** ou em **X** no canto superior direito para fechar o pop-up de integração.
1. A página de configuração do Commerce é atualizada automaticamente.

## Confirmar o resultado

Depois que a página for atualizada, verifique se a página de configuração do escopo do site contém:

- Um **[!UICONTROL PayPal Merchant ID]** atualizado para esse site.
- Um rótulo de status mostrando o resultado da integração:

| Status | Significado |
| --- | --- |
| `ACTIVE` | Integração concluída com sucesso |
| `PENDING` | A integração ainda está em processamento |
| `ERROR` | A integração não foi concluída com êxito |

Se você vir um status `ERROR`, uma mensagem de erro será exibida explicando o problema. Você pode repetir o processo de integração clicando em **[!UICONTROL Connect different account]** novamente.
