---
title: Teclas de acesso restrito
description: Saiba como criar, atribuir e girar chaves de acesso restrito para proteger exibições de catálogo no  [!DNL Adobe Commerce Optimizer]  com autenticação de token assinado.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente ao Adobe Commerce as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  projetos (infraestrutura SaaS gerenciada pela Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# Chaves de acesso restrito

As chaves de acesso restrito permitem que aplicativos clientes autorizados acessem uma [exibição de catálogo privado](catalog-view.md). Somente as solicitações que carregam um token assinado válido de uma chave atribuída podem recuperar dados de catálogo. Todas as outras solicitações são negadas, incluindo as de compradores anônimos, compradores que não receberam acesso explícito a essa visualização de catálogo e scripts que sondam a API.

## Casos de uso da chave de acesso restrito

Em [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** determina quais preços uma solicitação vê; ela define o escopo dos preços, não quem pode fazer a solicitação. Qualquer cliente que conheça a ID de uma exibição de catálogo e a ID do catálogo de preços pode recuperar esses dados por meio da API de merchandising. As chaves de acesso restrito adicionam um controle complementar separado: elas definem quem pode acessar uma visualização de catálogo, independentemente do catálogo de preços aplicado.

As chaves de acesso restrito são normalmente usadas para:

- **Preços B2B com base em contrato**—Restrinja uma exibição de catálogo vinculada a um catálogo de preços negociado para que somente o comprador ao qual ele se aplica possa consultá-lo. Outras organizações compradoras e o público não podem.
- **Portais para parceiros e revendedores** — limite um subconjunto do catálogo para parceiros aprovados que se integram diretamente com a API de merchandising.
- **Pré-visualizações de pré-lançamento** — Permita que um sistema interno ou de parceiros confiável visualize os produtos futuros antes que eles sejam visíveis publicamente.

>[!IMPORTANT]
>
>Atualmente, a geração de chaves, a assinatura de tokens e a rotação são totalmente gerenciadas pelo aplicativo cliente de back-end que autentica os compradores. [!DNL Adobe Commerce Optimizer] não gera nem gira essas chaves em seu nome.

## Como funcionam as teclas de acesso restrito

Uma chave de acesso restrito é o componente público de um par de chaves RSA. O aplicativo cliente gera e usa essa chave para comprovar que está autorizado a ler uma visualização de catálogo privado. Neste contexto, &quot;aplicativo cliente&quot; significa o sistema de back-end que autentica compradores - por exemplo, lógica personalizada em [!DNL Adobe Commerce] ou um back-end de terceiros - nunca o front-end da loja em si.

As etapas a seguir descrevem como um par de chaves e um token assinado mudam da criação para a validação:

1. O aplicativo cliente gera um par de chaves RSA e mantém a chave privada.
1. Você registra a chave **pública** em [!DNL Commerce Optimizer] como uma chave de acesso restrito.
1. Seu aplicativo cliente assina um JSON Web Token (JWT) com a chave privada e o inclui com cada solicitação para uma exibição de catálogo privado.
1. [!DNL Commerce Optimizer] valida a assinatura do token com base na chave pública registrada e, se for válida, retorna os dados de catálogo solicitados.

## Criar uma chave de acesso restrito

Para testes iniciais de exibições de catálogos privados, gere um par de chaves usando uma ferramenta como o [!DNL OpenSSL]. Manter a chave privada em segredo — somente a chave pública é carregada para [!DNL Commerce Optimizer].

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

Uma chave de acesso restrito só restringe o acesso depois de ser atribuída a uma exibição de catálogo com o **[!UICONTROL Catalog Protection]** habilitado. Consulte [Proteger uma exibição de catálogo](private-catalog-view.md#protect-a-catalog-view) para obter etapas de configuração.

## Excluir uma chave

1. Na página **[!UICONTROL Restricted access keys]**, encontre a chave que deseja remover e clique em **[!UICONTROL Delete]**.

   Se a chave for atribuída a uma ou mais exibições do catálogo, um aviso explicará que os aplicativos clientes que dependem dessa chave perderão o acesso. As próprias visualizações do catálogo permanecem protegidas, pois não se tornam acessíveis publicamente.

1. Confirme a exclusão.

## Girar uma chave

Para girar uma chave sem uma interrupção de acesso, observe que uma exibição de catálogo pode ter até três chaves atribuídas de uma só vez:

1. Gere um novo par de chaves e adicione a nova chave pública como uma nova chave de acesso restrito.
1. Atribua a nova chave à exibição de catálogo junto com a chave existente.
1. Comece a assinar novos tokens com a nova chave privada para concluir a substituição de chaves.
1. Depois que todos os aplicativos clientes forem confirmados na nova chave, remova e exclua a chave antiga.

## Limites

Consulte [Limites de política e exibições de catálogo](../boundaries-limits.md#catalog-views-and-policies).

## Veja mais aqui

- [Exibições de catálogo privado](private-catalog-view.md) — Saiba como proteger uma exibição de catálogo com chaves de acesso restritas.

