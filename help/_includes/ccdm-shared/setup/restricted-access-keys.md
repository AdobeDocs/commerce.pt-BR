---
source-git-commit: b6b737220a6dadf55b03da54e8d74226ed578cd0
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%
---
# Teclas de acesso restrito

As chaves de acesso restrito permitem que aplicativos clientes autorizados acessem uma [exibição de catálogo privado](private-catalog-view.md). Somente as solicitações que carregam um token assinado válido de uma chave atribuída podem recuperar dados de catálogo. Todas as outras solicitações são negadas, incluindo as de compradores que não têm acesso explícito a essa exibição de catálogo e scripts que sondam a API de serviços de merchandising da Adobe Commerce.

As chaves de acesso restrito são provisionadas de uma das duas formas a seguir:

- **Automaticamente, para catálogos compartilhados B2B** — O sistema provisiona e atribui a chave inicial para exibições de catálogo associadas a um catálogo compartilhado B2B. Em seguida, gerencie as chaves e a atribuição de chaves do administrador do Commerce. Consulte [Autenticação de exibição de catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) no *Guia de Administração do Commerce*. O provisionamento automático está disponível nas seguintes implantações:

  - **Adobe Commerce as a Cloud Service com CCDM** para Adobe Commerce B2B.
  - **Adobe Commerce na nuvem ou no local** integrado ao Adobe Commerce Optimizer por meio de [!DNL Adobe Commerce Optimizer Connector for B2B]. A extensão B2B para o conector é necessária.

- **Manualmente, para qualquer exibição de catálogo**—Para proteger uma exibição de catálogo por conta própria—por exemplo, para um portal de parceiro ou pré-lançamento—siga as etapas deste tópico, começando com [Criar uma chave de acesso restrita](#create-a-restricted-access-key).

## Casos de uso da chave de acesso restrito

**[!UICONTROL Price Book ID]** determina quais preços uma solicitação vê; ela define o escopo dos preços, não quem pode fazer a solicitação. Qualquer cliente que conheça a ID de uma exibição de catálogo e a ID do catálogo de preços pode recuperar esses dados por meio da API de serviços de merchandising. As chaves de acesso restrito adicionam um controle complementar separado: elas definem quem pode acessar uma visualização de catálogo, independentemente do catálogo de preços aplicado.

As chaves de acesso restrito são normalmente usadas para:

- **Preços B2B com base em contrato**—Restrinja uma exibição de catálogo vinculada a um catálogo de preços negociado para que somente o comprador ao qual ele se aplica possa consultá-lo. Outras organizações compradoras e o público não podem. Para catálogos compartilhados B2B, isso é configurado automaticamente. Consulte [Rotação e gerenciamento de chaves](#key-management-and-rotation).
- **Portais para parceiros e revendedores** — limite um subconjunto do catálogo para parceiros aprovados que se integram diretamente com a API de serviços de merchandising.
- **Pré-visualizações de pré-lançamento** — Permita que um sistema interno ou de parceiros confiável visualize os produtos futuros antes que eles sejam visíveis publicamente.

## Como funcionam as teclas de acesso restrito

Uma chave de acesso restrito é o componente público de um par de chaves RSA. O aplicativo cliente gera e usa essa chave para comprovar que está autorizado a ler uma visualização de catálogo privado. Neste contexto, o _aplicativo cliente_ refere-se ao sistema de back-end que autentica compradores - por exemplo, lógica personalizada em [!DNL Adobe Commerce] ou um back-end de terceiros - nunca o próprio front-end da loja.

As etapas a seguir descrevem como um par de chaves e um token assinado mudam de criação para validação para exibições de catálogo que não fazem parte de um catálogo compartilhado B2B.

1. O aplicativo cliente gera um par de chaves RSA e mantém a chave privada.
1. Você registra a chave **pública** no sistema como uma chave de acesso restrito.
1. Seu aplicativo cliente assina um JSON Web Token (JWT) com a chave privada e o inclui com cada solicitação para uma exibição de catálogo privado.

   O sistema valida a assinatura do token em relação à chave pública registrada e, se for válida, retorna os dados de catálogo solicitados.

## Acessar o espaço de trabalho da chave de acesso restrito

A forma como você abre o espaço de trabalho de chaves de acesso restrito depende do produto que você usa:

- **Administrador Do Adobe Commerce** (Adobe Commerce as a Cloud Service)—Selecione *Sistema* > *Transferência De Dados* > **Chaves De Acesso Restrito**.
- **Adobe Commerce Optimizer Studio**—Selecione *Configuração de armazenamento* > **Chaves de acesso restrito**.

## Criar uma chave de acesso restrito

>[!NOTE]
>
>Esta seção e as duas seguintes descrevem o processo manual para gerenciar chaves de acesso restrito. Para catálogos compartilhados B2B com provisionamento automático de chaves, gerencie as chaves do administrador do Commerce. Consulte [Chaves de Acesso Restrito](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

### Adicionar uma chave de acesso restrito

Selecione a guia da ferramenta usada para gerenciar chaves: Commerce Admin ou Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Administrador do Adobe Commerce]

Os clientes que usam o Adobe Commerce as a Cloud Service com CCDM ou o Adobe Commerce Optimizer conectado ao Adobe Commerce por meio do conector podem gerar pares de chaves RSA do administrador do Commerce. Consulte [Gerenciar chaves de acesso restrito](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

>[!TAB Adobe Commerce Optimizer Studio - gerenciamento manual de chaves]

Os clientes que usam o Adobe Commerce Optimizer Studio devem gerar e gerenciar seus próprios pares de chaves RSA e, em seguida, adicionar a chave pública ao sistema. Esse é o fluxo de trabalho necessário para o Adobe Commerce Optimizer com um back-end de terceiros. Os clientes que usam o conector também podem usar esse fluxo de trabalho em vez do Administrador do Commerce.

**Gerar um par de chaves RSA**

Para testes iniciais de exibições de catálogos privados, gere um par de chaves usando uma ferramenta como o [!DNL OpenSSL]. Mantenha a chave privada em segredo. Somente a chave pública é carregada no sistema como uma chave de acesso restrito.

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

O tamanho da chave deve estar entre 2048 e 8192 bits. `public-key.pem` contém o valor que você cola no campo **[!UICONTROL Public key]** abaixo.

**Adicionar a chave pública ao sistema**

1. No espaço de trabalho da chave de Acesso Restrito, clique em **[!UICONTROL Add Restricted Access Key]**.

   ![Lista de Chaves de Acesso Restrito, com o botão Adicionar Chave de Acesso Restrito](/help/assets/ccdm-shared/setup/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Insira os detalhes principais:

   ![Adicionar formulário de chave de acesso restrito, com os campos Título, Data de expiração e Chave pública](/help/assets/ccdm-shared/setup/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** — Um rótulo para identificar a chave, mostrado na lista de chaves e no seletor de chaves de exibição de catálogo, por exemplo `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** — Data e hora (UTC) após as quais a chave deixa de ser aplicada, mesmo para um token que ainda não expirou.
   - **[!UICONTROL Public key]** — A chave pública RSA codificada em PEM no formato SPKI (Subject Public Key Info), incluindo os marcadores `-----BEGIN PUBLIC KEY-----` e `-----END PUBLIC KEY-----`. Deve ser única em todo o ambiente.

1. Clique em **[!UICONTROL Save]**.

>[!ENDTABS]

As chaves são imutáveis após a criação. Para alterar qualquer valor, exclua a chave e crie uma nova. Consulte [Girar uma chave](#rotate-a-key) para fazer isso sem uma interrupção de acesso.

## Atribuir uma chave a uma exibição de catálogo

Uma chave de acesso restrito só autentica o acesso depois de ter sido atribuída a uma exibição de catálogo com o **[!UICONTROL Catalog Protection]** habilitado. Consulte [Proteger uma exibição de catálogo](private-catalog-view.md#protect-a-catalog-view) para obter etapas de configuração.

## Excluir uma chave

1. No espaço de trabalho **[!UICONTROL Restricted access keys]**, encontre a chave que deseja remover e exclua-a.

   Se a chave for atribuída a uma ou mais exibições do catálogo, um aviso explicará que os aplicativos clientes que dependem dessa chave perderão o acesso. As próprias visualizações do catálogo permanecem protegidas, pois não se tornam acessíveis publicamente.

1. Confirme a exclusão.

## Gerenciamento e rotação de chaves

As chaves de acesso restrito são gerenciadas de uma das duas formas a seguir, dependendo de como você usa a proteção de catálogo:

- **Automaticamente, para catálogos compartilhados B2B**—Para implantações B2B do Adobe Commerce usando Serviços de Merchandising com CCDM e para implantações do Adobe Commerce Optimizer integradas por meio do [!DNL Adobe Commerce Optimizer Connector for B2B] (que requer a extensão B2B), o serviço gera e atribui automaticamente a primeira chave de acesso restrito quando uma exibição de catálogo é criada. Cada exibição de catálogo recebe sua própria chave. Depois disso, você poderá gerenciar cada chave das páginas Catálogo Compartilhado ou Conta da Empresa. Você também pode exibir e gerenciar chaves da página **Chaves de Acesso Restrito** do Administrador do Commerce (**Sistema** > **Transferência de Dados**). Consulte [Gerenciar configuração de exibição do catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Cada combinação de um catálogo compartilhado e uma exibição de loja é projetada como uma exibição de catálogo separada. Uma projeção são os dados de configuração da exibição de catálogo, política, referência de catálogo de preços e acesso restrito que são exportados para a camada de dados dos Serviços de merchandising para essa combinação. Assim, um catálogo compartilhado atribuído a várias exibições de loja produz várias exibições de catálogo, cada uma com sua própria chave. Editar ou girar uma chave para uma exibição de catálogo sem afetar as outras.

  As chaves assumem como padrão um longo período de expiração. Se precisar girar uma chave, adicione a substituição no Admin e mantenha ambas ativas até remover a antiga.

- **Manualmente, para qualquer exibição de catálogo**—A forma como você gera e gerencia chaves depende do contexto do seu produto. Em ambos os casos, o cliente de back-end que autentica os compradores assina os tokens.

  - **Administrador do Commerce (Adobe Commerce as a Cloud Service com CCDM ou Adobe Commerce Optimizer com o conector)**—Gere pares de chaves RSA no Administrador do Commerce e crie, atribua e exclua chaves na página **Chaves de acesso restrito**. O Adobe Commerce não gira chaves automaticamente. Para girar uma chave, consulte [Girar uma chave](#rotate-a-key).
  - **Adobe Commerce Optimizer Studio** — O Studio não gera chaves. Esse é o fluxo de trabalho necessário para o Adobe Commerce Optimizer com um back-end de terceiros, e os clientes do conector também podem usá-lo. Use o aplicativo cliente para gerar o par de chaves RSA, manter a chave privada e adicionar a chave pública como uma chave de acesso restrito. Use as etapas anteriores neste tópico para criar, adicionar e excluir chaves. Para girar uma chave, consulte [Girar uma chave](#rotate-a-key).

### Girar uma chave

Para girar uma chave sem uma interrupção de acesso, observe que uma exibição de catálogo pode ter até três chaves atribuídas de uma só vez:

Selecione a guia da ferramenta usada para gerenciar chaves: Commerce Admin ou Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Administrador do Adobe Commerce]

Consulte [Seleção e rotação de chaves](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys#key-selection-and-rotation). Isso se aplica ao Adobe Commerce as a Cloud Service com CCDM e a projetos do Adobe Commerce integrados ao Adobe Commerce Optimizer por meio do conector do Adobe Commerce Optimizer.

>[!TAB Adobe Commerce Optimizer Studio (gerenciamento manual de chaves)]

Esse procedimento é necessário para o Adobe Commerce Optimizer com back-end de terceiros. Os clientes que usam o conector também podem usá-lo no lugar do administrador do Commerce.

1. Gere um novo par de chaves e adicione a nova chave pública como uma nova chave de acesso restrito.
1. Atribua a nova chave à exibição de catálogo junto com a chave existente.
1. Comece a assinar novos tokens com a nova chave privada para concluir a substituição de chaves.
1. Depois que todos os aplicativos clientes forem confirmados na nova chave, remova e exclua a chave antiga.

>[!ENDTABS]

## Limites

Consulte [Limites de política e exibições de catálogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits).

## Veja mais aqui

- [Exibições de catálogo privado](private-catalog-view.md) — Saiba como proteger uma exibição de catálogo com chaves de acesso restritas.
