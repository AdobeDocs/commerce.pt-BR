---
title: Teclas de acesso restrito
description: Saiba como as chaves de acesso restrito protegem exibições de catálogo no [!DNL Adobe Commerce Optimizer], criadas automaticamente para catálogos compartilhados B2B ou gerenciadas manualmente.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente ao Adobe Commerce as a Cloud Service e a projetos [!DNL Adobe Commerce Optimizer] (infraestrutura SaaS gerenciada pela Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
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
nudge: true
source-git-commit: f93bd673624c58050696da772ce733874ce594e5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%
---
# Chaves de acesso restrito

As chaves de acesso restrito permitem que aplicativos clientes autorizados acessem uma [exibição de catálogo privado](catalog-view.md). Somente as solicitações que carregam um token assinado válido de uma chave atribuída podem recuperar dados de catálogo. Todas as outras solicitações são negadas, incluindo as de compradores que não receberam acesso explicitamente a essa visualização de catálogo e scripts que sondam a API.

As chaves de acesso restrito são provisionadas de uma das duas formas a seguir:

- [!BADGE Private Beta]{type=Caution tooltip="Requer a extensão B2B do Adobe Commerce Optimizer Connector, que atualmente está em beta privado."} **Automaticamente, para catálogos compartilhados B2B**—Para implantações integradas ao [!DNL Adobe Commerce Optimizer Connector for B2B], o conector provisiona e atribui a chave inicial. Em seguida, gerencie as chaves e a atribuição de chaves do administrador do Commerce. Consulte [Autenticação de exibição de catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) no *Guia de Administração do Commerce**.

- **Manualmente, para qualquer exibição de catálogo**—Para proteger uma exibição de catálogo por conta própria—por exemplo, para um portal de parceiro ou pré-lançamento—siga as etapas deste tópico, começando com [Criar uma chave de acesso restrita](#create-a-restricted-access-key).

## Casos de uso da chave de acesso restrito

Em [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** determina quais preços uma solicitação vê; ela define o escopo dos preços, não quem pode fazer a solicitação. Qualquer cliente que conheça a ID de uma exibição de catálogo e a ID do catálogo de preços pode recuperar esses dados por meio da API de merchandising. As chaves de acesso restrito adicionam um controle complementar separado: elas definem quem pode acessar uma visualização de catálogo, independentemente do catálogo de preços aplicado.

As chaves de acesso restrito são normalmente usadas para:

- **Preços B2B com base em contrato**—Restrinja uma exibição de catálogo vinculada a um catálogo de preços negociado para que somente o comprador ao qual ele se aplica possa consultá-lo. Outras organizações compradoras e o público não podem. Para catálogos compartilhados B2B, isso é configurado automaticamente. Consulte [Rotação e gerenciamento de chaves](#key-management-and-rotation).
- **Portais para parceiros e revendedores** — limite um subconjunto do catálogo para parceiros aprovados que se integram diretamente com a API de merchandising.
- **Pré-visualizações de pré-lançamento** — Permita que um sistema interno ou de parceiros confiável visualize os produtos futuros antes que eles sejam visíveis publicamente.

## Como funcionam as teclas de acesso restrito

Uma chave de acesso restrito é o componente público de um par de chaves RSA. O aplicativo cliente gera e usa essa chave para comprovar que está autorizado a ler uma visualização de catálogo privado. Neste contexto, o _aplicativo cliente_ refere-se ao sistema de back-end que autentica compradores - por exemplo, lógica personalizada em [!DNL Adobe Commerce] ou um back-end de terceiros - nunca o próprio front-end da loja.

As etapas a seguir descrevem como um par de chaves e um token assinado mudam de criação para validação para exibições de catálogo que não fazem parte de um catálogo compartilhado B2B.

1. O aplicativo cliente gera um par de chaves RSA e mantém a chave privada.
1. Você registra a chave **pública** em [!DNL Commerce Optimizer] como uma chave de acesso restrito.
1. Seu aplicativo cliente assina um JSON Web Token (JWT) com a chave privada e o inclui com cada solicitação para uma exibição de catálogo privado.
1. [!DNL Commerce Optimizer] valida a assinatura do token com base na chave pública registrada e, se for válida, retorna os dados de catálogo solicitados.

## Criar uma chave de acesso restrito

>[!NOTE]
>
>Esta seção e as três seguintes descrevem o fluxo manual do [!DNL Adobe Commerce Optimizer] Studio. Se você usa catálogos compartilhados B2B com o [!DNL Adobe Commerce Optimizer Connector B2B extension], gerencie as chaves do Administrador do Commerce. Consulte [Chaves de Acesso Restrito](../../aco-connector/restricted-access-keys.md) na documentação do _Adobe Commerce Optimizer Connector_.

Para testes iniciais de exibições de catálogos privados, gere um par de chaves usando uma ferramenta como o [!DNL OpenSSL]. Mantenha a chave privada em segredo. Somente a chave pública é carregada para [!DNL Commerce Optimizer].

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

O tamanho da chave deve estar entre 2048 e 8192 bits. `public-key.pem` contém o valor que você cola no campo **[!UICONTROL Public key]** abaixo.

## Adicionar uma chave de acesso restrito a [!DNL Commerce Optimizer]

1. No menu esquerdo em [!DNL Adobe Commerce Optimizer Studio], vá para **[!UICONTROL Store setup]** e clique em **[!UICONTROL Restricted access keys]**.

   ![Lista de Chaves de Acesso Restrito, com o botão Adicionar Chave de Acesso Restrito](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Clique em **[!UICONTROL Add Restricted Access Key]**.

1. Insira os detalhes principais:

   ![Adicionar formulário de chave de acesso restrito, com os campos Título, Data de expiração e Chave pública](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** — Um rótulo para identificar a chave, mostrado na lista de chaves e no seletor de chaves de exibição de catálogo, por exemplo `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** — Data e hora (UTC) após as quais a chave deixa de ser aplicada, mesmo para um token que ainda não expirou.
   - **[!UICONTROL Public key]** — A chave pública RSA codificada em PEM no formato SPKI (Subject Public Key Info), incluindo os marcadores `-----BEGIN PUBLIC KEY-----` e `-----END PUBLIC KEY-----`. Deve ser única em todo o ambiente.

1. Clique em **[!UICONTROL Save]**.

As chaves são imutáveis após a criação. Para alterar qualquer valor, exclua a chave e crie uma nova. Consulte [Girar uma chave](#rotate-a-key) para fazer isso sem uma interrupção de acesso.

## Atribuir uma chave a uma exibição de catálogo

Uma chave de acesso restrito só autentica o acesso depois de ter sido atribuída a uma exibição de catálogo com o **[!UICONTROL Catalog Protection]** habilitado. Consulte [Proteger uma exibição de catálogo](private-catalog-view.md#protect-a-catalog-view) para obter etapas de configuração.

## Excluir uma chave

1. Na página **[!UICONTROL Restricted access keys]**, encontre a chave que deseja remover e clique em **[!UICONTROL Delete]**.

   Se a chave for atribuída a uma ou mais exibições do catálogo, um aviso explicará que os aplicativos clientes que dependem dessa chave perderão o acesso. As próprias visualizações do catálogo permanecem protegidas, pois não se tornam acessíveis publicamente.

1. Confirme a exclusão.

## Gerenciamento e rotação de chaves

As chaves de acesso restrito são gerenciadas de uma das duas formas a seguir, dependendo de como você usa a proteção de catálogo:

- **Automaticamente, para catálogos compartilhados B2B**—[!BADGE Private Beta]{type=Caution tooltip="Requer a extensão B2B do Adobe Commerce Optimizer Connector, que atualmente está em beta privado."} Para implantações integradas ao [!DNL Adobe Commerce Optimizer Connector for B2B], o serviço gera e atribui automaticamente a primeira chave de acesso restrito quando uma exibição de catálogo é criada. Cada exibição de catálogo recebe sua própria chave. Depois disso, você poderá gerenciar cada chave das páginas Catálogo Compartilhado ou Conta da Empresa. Você também pode exibir e gerenciar chaves da página **Chaves de Acesso Restrito** do Administrador do Commerce (**Sistema** > **Transferência de Dados**). Consulte [Gerenciar configuração de exibição do catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Cada combinação de um catálogo compartilhado e uma exibição de loja à qual está atribuído é projetada como uma exibição de catálogo separada. Uma projeção são os dados de configuração de exibição de catálogo, política, referência de catálogo de preços e chave de acesso restrito que o conector exporta para [!DNL Adobe Commerce Optimizer] para essa combinação. Assim, um catálogo compartilhado atribuído a várias exibições de loja produz várias exibições de catálogo, cada uma com sua própria chave. Editar ou girar uma chave para uma exibição de catálogo sem afetar as outras.

  As chaves assumem como padrão um longo período de expiração. Se precisar girar uma chave, adicione a substituição no Admin e mantenha ambas ativas até remover a antiga. Consulte [Alterações no catálogo compartilhado B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes).

- **Manualmente, para qualquer exibição de catálogo** — Para exibições de catálogo não associadas a um catálogo compartilhado B2B no back-end do Adobe Commerce, a geração de chaves, a assinatura de token e a rotação são gerenciadas inteiramente pelo aplicativo cliente back-end que autentica compradores. [!DNL Adobe Commerce Optimizer] não gera nem gira essas chaves em seu nome. Use as etapas anteriores neste tópico para criar, adicionar e excluir chaves. Para girar uma chave, consulte [Girar uma chave](#rotate-a-key).

### Girar uma chave

Para girar uma chave sem uma interrupção de acesso, observe que uma exibição de catálogo pode ter até três chaves atribuídas de uma só vez:

1. Gere um novo par de chaves e adicione a nova chave pública como uma nova chave de acesso restrito.
1. Atribua a nova chave à exibição de catálogo junto com a chave existente.
1. Comece a assinar novos tokens com a nova chave privada para concluir a substituição de chaves.
1. Depois que todos os aplicativos clientes forem confirmados na nova chave, remova e exclua a chave antiga.

## Limites

Consulte [Limites de política e exibições de catálogo](../boundaries-limits.md#catalog-views-and-policies).

## Veja mais aqui

- [Exibições de catálogo privado](private-catalog-view.md) — Saiba como proteger uma exibição de catálogo com chaves de acesso restritas.
- [Alterações no catálogo compartilhado B2B](/help/aco-connector/get-started.md#monitor-b2b-shared-catalog-changes)—Saiba como o [!DNL Adobe Commerce Optimizer Connector] automatiza o gerenciamento de chaves para catálogos compartilhados B2B.

