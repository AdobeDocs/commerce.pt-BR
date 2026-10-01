---
title: Visualizações do catálogo privado
description: Saiba como as exibições de catálogo privado restringem o acesso aos dados do catálogo, criadas automaticamente para catálogos compartilhados B2B ou configuradas manualmente com a Proteção de catálogo.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente ao Adobe Commerce as a Cloud Service e a projetos [!DNL Adobe Commerce Optimizer] (infraestrutura SaaS gerenciada pela Adobe)."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
    internal-label: Optimization
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%
---
# Exibições de catálogo privado

Por padrão, uma [exibição de catálogo](catalog-view.md) é pública. Restrinja o acesso a uma exibição de catálogo para que somente as solicitações com um token assinado válido possam recuperar seus dados.

Uma exibição de catálogo se torna privada de uma das duas formas a seguir:

- [!BADGE Private Beta]{type=Caution tooltip="Requer a extensão B2B do Adobe Commerce Optimizer Connector, que atualmente está em beta privado."} **Automaticamente, para catálogos compartilhados B2B** — Para implantações do Commerce que usam a integração [!DNL Adobe Commerce Optimizer Connector] com a extensão B2B, exibições de catálogos privados são criadas e configuradas automaticamente para você, com base na configuração de catálogo compartilhado em [!DNL Adobe Commerce]. Consulte [Exibições automáticas de catálogo privado para catálogos B2B compartilhados](#automatic-private-catalog-views-for-b2b-shared-catalogs).

- **Manualmente, para qualquer exibição de catálogo**—Para restringir o acesso a uma exibição de catálogo que seria pública, incluindo uma exibição de catálogo B2C, siga as etapas em [Proteger uma exibição de catálogo](#protect-a-catalog-view). Consulte [Casos de uso da chave de acesso restrito](restricted-access-keys.md#restricted-access-key-use-cases) para obter exemplos, como portais de parceiros e visualizações de pré-lançamento.

A proteção de catálogo se aplica somente à exibição de catálogo selecionada. Isso não altera as políticas ou camadas da exibição. Ela restringe a exibição a um único catálogo de preços — consulte [Restrição de catálogo de preços em exibições de catálogo privado](#price-book-restriction-on-private-catalog-views).

## Entender o limite de proteção

A proteção de catálogo se aplica somente à exibição de catálogo em que está habilitada. Ela protege solicitações de catálogo e pesquisa, mas não altera as políticas ou camadas da exibição, protege outras exibições de catálogo ou protege o carrinho, a finalização ou as operações de pedido.

O back-end de comércio conectado deve impor independentemente a qualificação de compra.

## Restrição de catálogo de preços em exibições de catálogo privado

Uma exibição de catálogo privado pode fazer referência a apenas um catálogo de preços. Isso é diferente de uma exibição de catálogo público, que pode usar vários catálogos de preços.

Quando [!UICONTROL Catalog Protection] está habilitado, o seletor de catálogo de preços no formulário de exibição de catálogo alterna de um controle de seleção múltipla para um controle de seleção única (botão de opção).

![Restrição de catálogo de preços de exibição de catálogo privado](../assets/catalog-view-private-pricebook-restrictions.png)

- Se você habilitar [!UICONTROL Catalog Protection] em uma exibição de catálogo com vários catálogos de preços atribuídos, não poderá salvar a exibição até remover todos, exceto um catálogo de preços.
- Se você tiver salvo anteriormente uma exibição de catálogo privado com várias atribuições de catálogo de preços antes dessa restrição existir, a configuração da exibição de catálogo não será alterada automaticamente. No entanto, na próxima vez que você editar a view, deverá remover todos, exceto um catálogo de preços, antes de salvar as atualizações.

Em cada um desses casos, [!DNL Adobe Commerce Optimizer] exibe a seguinte mensagem de validação: `A protected catalog view can use only one price book. Select 'Single price book only' to continue.`

As exibições de catálogo público não são afetadas por essa restrição e podem continuar fazendo referência a vários catálogos de preços.

## Exibições automáticas de catálogo privado para catálogos compartilhados B2B

[!BADGE Private Beta]{type=Caution tooltip="Requer a extensão B2B do Adobe Commerce Optimizer Connector, que atualmente está em beta privado."}

Para implantações integradas ao [!DNL Adobe Commerce Optimizer Connector for B2B] para oferecer suporte a catálogos compartilhados, a extensão cria e configura exibições de catálogo privado automaticamente, com base na configuração de catálogo compartilhado em [!DNL Adobe Commerce]. Essa configuração inclui a exibição do catálogo, a política, uma chave de acesso restrito inicial e uma referência de catálogo de preços. Com essa configuração, você gerencia chaves de acesso restrito da página **Chaves de Acesso Restrito** do Administrador do Commerce (**Sistema** > **Transferência de Dados**). Para obter detalhes, consulte [Alterações no catálogo compartilhado B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes) no *[!DNL Adobe Commerce Optimizer Connector]Guia de Integração*.

Se você não estiver usando catálogos compartilhados B2B, por exemplo, para proteger uma exibição de catálogo para um portal de parceiro ou pré-visualização de pré-lançamento, use as instruções em [Proteger uma exibição de catálogo](#protect-a-catalog-view) para configurar um manualmente.

## Proteger uma exibição de catálogo

>[!NOTE]
>
>Ignore este procedimento para exibições de catálogo associadas a catálogos compartilhados B2B gerenciados pelo [!DNL Adobe Commerce Optimizer Connector for B2B]. Consulte [Exibições automáticas de catálogo privado para catálogos B2B compartilhados](#automatic-private-catalog-views-for-b2b-shared-catalogs).

Antes de começar, [crie uma chave de acesso restrito](restricted-access-keys.md) a partir da chave pública gerada pelo aplicativo cliente.

1. Na exibição do catálogo, criar ou editar formulário, alterne **[!UICONTROL Catalog Protection]** para **[!UICONTROL Enabled]**.

1. Em **[!UICONTROL Restricted Access Keys]**, selecione até três [chaves de acesso restrito](restricted-access-keys.md) para atribuir a esta exibição de catálogo.

   ![Proteção de Catálogo habilitada no formulário de edição de exibição de catálogo, com uma chave de acesso restrita atribuída](../assets/catalog-view-protected.png){width="70%" zoomable="yes"}

1. Clique em **[!UICONTROL Save catalog view]**.

   A exibição do catálogo agora está protegida. Somente as solicitações que carregam um token assinado válido de uma chave atribuída podem recuperar seus dados.

   >[!NOTE]
   >
   >Aguarde até cinco minutos para que as alterações de configuração da Proteção de catálogo entrem em vigor.

## Verificar se o acesso é aplicado

Para confirmar se uma exibição de catálogo privado rejeita solicitações não autorizadas, chame seu [endpoint do GraphQL](../get-started.md#get-instance-details) com e sem um token assinado, usando estes cabeçalhos:

| Cabeçalho | Finalidade |
| --- | --- |
| `AC-View-ID` | A exibição do catálogo a ser consultada. |
| `AC-Price-Book-ID` | O catálogo de preços a ser aplicado. |
| `AC-Catalog-View-Access-Token` | O JWT assinado que prova a autorização para a exibição do catálogo. |

Uma solicitação sem um token válido retorna um erro de GraphQL em vez de dados de catálogo, por exemplo:

```json
{
  "errors": [
    {
      "message": "Access key validation failed: Missing token",
      "extensions": { "x-commerce-exception": "access-key-invalid" }
    }
  ]
}
```

Uma solicitação que transporta um token assinado por uma chave atribuída e não expirada retorna os dados do catálogo conforme esperado. Para obter detalhes sobre como assinar um JWT e chamar a API de merchandising, consulte a [documentação para desenvolvedores](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication).

## Gerenciar chaves de acesso restrito

Se [!UICONTROL Catalog Protection] estiver habilitado e todas as chaves atribuídas expirarem, a exibição do catálogo ficará inacessível. As vitrines que dependem dessa exibição de catálogo não podem fornecer dados a partir dela. Atribua uma chave nova e não expirada para restaurar o acesso. Para obter instruções, consulte [Girar chaves](restricted-access-keys.md#rotate-a-key).

>[!NOTE]
>
>Para implantações integradas à extensão [!DNL Adobe Commerce Optimizer Connector for B2B], você gerencia chaves de acesso da página **Chaves de Acesso Restrito** do Administrador do Commerce (**Sistema** > **Transferência de Dados**). Para obter detalhes, consulte [Gerenciamento de chave de acesso restrito](../../aco-connector/restricted-access-keys.md) no *[!DNL Adobe Commerce Optimizer Connector]Guia de Integração*.

## Veja mais aqui

- [Exibições de catálogo](catalog-view.md) — Saiba como as exibições de catálogo organizam o catálogo de produtos por estrutura de negócios, políticas e preços.
- [Chaves de acesso restrito](restricted-access-keys.md)—Crie, atribua e gire as chaves usadas para assinar tokens para a Proteção de Catálogo.
