---
title: Fazer logon como cliente com códigos únicos
description: Saiba como usar o recurso Login como Cliente OTC para gerar códigos únicos para autenticação do cliente no [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Intermediate
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Fazer logon como cliente

{{accs-sandbox-experimental}}

O recurso Logon como cliente OTC (Código único) permite que os usuários administradores gerem um código de curta duração e de uso único para um cliente. Este código pode ser trocado por um token de acesso do cliente por meio do GraphQL, habilitando fluxos de trabalho de **Logon como Cliente** sem senha para cenários de compras com auxílio do vendedor.

O logon como cliente é composto pelos seguintes componentes:

* **Interface do administrador** - Na página de edição do cliente, os administradores podem solicitar um código único (OTC) em vez de fazer logon diretamente como cliente.
* **API REST** - Um ponto de extremidade programático para geração OTC, útil para scripts de administrador e integrações de terceiros.
* **API do GraphQL** - Mutações que trocam um OTC por um token de acesso do cliente para fluxos comerciais headless ou de vitrine.

## Gerar um código único do Administrador

O botão Fazer logon como OTC do cliente substitui o logon padrão como cliente na página de edição do cliente por um botão [!UICONTROL **Obter logon do cliente OTC**]. O código único gerado pode ser usado com a loja ou o GraphQL para compras assistidas pelo vendedor.

>[!NOTE]
>
>O botão **Fazer Logon como Cliente** não está disponível nas páginas Ordem, Fatura, Remessa e Aviso de Crédito.

### Pré-requisitos

Você deve atender aos seguintes requisitos antes de usar o recurso de logon como cliente:

* **Permissão de administrador** - O usuário administrador deve ter a permissão de ACL (Lista de Controle de Acesso) de `Magento_LoginAsCustomer::login` ativada em sua função de administrador para fazer logon como cliente.

* **Consentimento do cliente** - O cliente deve ter o atributo de extensão `login_as_customer_assistance_allowed` definido como **2**. Isso pode ser configurado na página **Editar Cliente** do Administrador ou por meio da GraphQL ao criar ou editar um cliente.

  ![Configuração de atributo de extensão de consentimento do cliente na página Editar Cliente](./assets/customer-consent-attribute.png){width="600" zoomable="yes"}

* **Logon como extensão do cliente habilitada** - A funcionalidade de fazer logon como cliente não está disponível quando a extensão de logon como cliente está desabilitada. Para verificar se a extensão está habilitada, navegue até [!UICONTROL **Lojas**] > [!UICONTROL **Configuração**] > [!UICONTROL **Clientes**] > [!UICONTROL **Fazer logon como Cliente**] > [!UICONTROL **Habilitar Extensão**].

### Solicitar um código de uso único (OTC)

1. Navegue até [!UICONTROL **Clientes**] e selecione um cliente para abrir a página de edição.

1. Na página Editar Cliente, clique em [!UICONTROL **Obter Logon de Cliente OTC**].

   ![Botão Obter Logon OTC do Cliente na página Editar Cliente](./assets/get-customer-login-otc-button.png){width="600" zoomable="yes"}

1. Insira um [!UICONTROL **Motivo**] (obrigatório) e clique em [!UICONTROL **Solicitação**].

   ![Solicitação OTC modal com campo Motivo](./assets/otc-reason-modal.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >O campo **Motivo** é obrigatório. Ele é passado para o fluxo de geração de OTP e é reservado para uso em recursos futuros de auditoria e registro de eventos.

1. O OTC gerado é exibido na modal. Use este código com a mutação do GraphQL `generateCustomerToken` ou `exchangeOtpForCustomerToken` para autorização do cliente.

   ![OTC gerado exibido no modal](./assets/otc-generated-code.png){width="300" zoomable="yes"}

>[!IMPORTANT]
>
>O OTC de código único gerado é válido por 30 segundos por padrão e é invalidado após um único uso. O TTL pode ser configurado através do CPS usando a configuração `customer/otp/ttl_seconds`.

Depois que o código único é gerado, é possível usá-lo navegando até a loja e fazendo logon com as seguintes credenciais:

* **Email**: o endereço de email do cliente
* **Senha**: o OTC (One-Time Code) gerado

## Gerar um código único usando a REST API

O ponto de extremidade `V1/customer/:customerId/otp` do POST fornece uma maneira programática de gerar um OTC para um cliente. Isso é útil para interfaces do administrador, scripts ou integrações de terceiros que precisam acionar a emissão OTC de forma consistente.

### Contrato REST

| Item | Valor |
|---|---|
| **Método** | POST |
| **URL** | `/rest/V1/customer/:customerId/otp` |
| **Autenticação** | Token de administrador (Portador). ACL necessária: `Magento_LoginAsCustomer::login`. |
| **Solicitar corpo** | JSON com campo `reason` opcional. Usado para auditoria e registro. |
| **Resposta bem-sucedida** | HTTP 200, JSON com `otp` (sequência hexadecimal de 32 caracteres). |
| **Respostas de erro** | Erros de API da Web padrão (por exemplo, 401, 403). Se a opção Fazer logon como Assistência ao cliente estiver desativada para o cliente, poderá aparecer como 500 ou uma exceção mapeada. |

### Exemplo de solicitação

```text
POST /rest/V1/customer/:customerId/otp
Content-Type: application/json
```

```json
{"reason": "Support session"}
```

### Exemplo de resposta

```json
{"otp": "a1b2c3d4e5f6789012345678abcdef01"}
```

## Trocar um código único por um token de cliente usando o GraphQL

Depois de gerar um OTC (da interface do usuário do administrador ou da API REST), use uma das seguintes mutações do GraphQL para trocá-lo por um token de acesso do cliente.

### `generateCustomerToken` mutação

A mutação `generateCustomerToken(email, password)` retorna um token de cliente. O argumento `password` é avaliado na seguinte ordem:

1. **Senha do cliente (padrão)** - A senha da conta do cliente.
1. **Token de Senha Redefinida pelo Cliente (uso único)** - Um token válido de **Esqueceu a senha** (por exemplo, a mutação `requestPasswordResetEmail`). Consumido na primeira utilização.
1. **OTC gerado pelo administrador (código único)** - Um código gerado por um administrador para o cliente por meio da API REST ou da interface do administrador. Uso único, vida curta (30 segundos por padrão).

**Esquema:**

```graphql
type Mutation {
  generateCustomerToken(email: String!, password: String!): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**Exemplo: logon com OTC de administrador**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variáveis (use o OTC como `password`):

```json
{
  "email": "customer@example.com",
  "password": "<admin-generated-OTC>"
}
```

**Exemplo: logon com senha**

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variáveis:

```json
{
  "email": "customer@example.com",
  "password": "CustomerPassword123"
}
```

**Exemplo: logon com token para redefinição de senha**

Depois que o cliente solicitar uma redefinição de senha (por exemplo, `requestPasswordResetEmail`), o token de redefinição recebido por meio do link de email poderá ser usado como `password` em `generateCustomerToken` (uso único).

```graphql
mutation GenerateCustomerToken($email: String!, $password: String!) {
  generateCustomerToken(email: $email, password: $password) {
    token
  }
}
```

Variáveis (use o token de redefinição como `password`):

```json
{
  "email": "customer@example.com",
  "password": "<reset-password-token-from-email-link>"
}
```

**Exemplo de resposta:**

```json
{
  "data": {
    "generateCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### `exchangeOtpForCustomerToken` mutação

A mutação `exchangeOtpForCustomerToken` troca um token de redefinição de senha ou OTP gerado por um administrador por um token de acesso do cliente. O OTP é invalidado após a troca bem-sucedida (uso único). Esse endpoint respeita a configuração do reCAPTCHA.

**Esquema:**

```graphql
type Mutation {
  exchangeOtpForCustomerToken(
    email: String!
    otp: String!
  ): CustomerToken
}

type CustomerToken {
  token: String!
}
```

**Exemplo de solicitação:**

```graphql
mutation ExchangeOtpForCustomerToken($email: String!, $otp: String!) {
  exchangeOtpForCustomerToken(email: $email, otp: $otp) {
    token
  }
}
```

Variáveis:

```json
{
  "email": "customer@example.com",
  "otp": "<one-time-password>"
}
```

**Exemplo de resposta:**

```json
{
  "data": {
    "exchangeOtpForCustomerToken": {
      "token": "<customer-access-token>"
    }
  }
}
```

### Resumo da mutação

| Mutação | Caso de uso |
|---|---|
| `generateCustomerToken(email, password)` | Ponto de entrada único: senha do cliente, token de redefinição de senha, OTC de administrador ou OTP (tentativa após a senha/redefinição). |
| `exchangeOtpForCustomerToken(email, otp)` | Troca de token de senha OTP ou Redefinir. OTP (ou Redefinir token de senha) é consumido após o uso. |

O token de redefinição de senha e o OTC de administrador são ambos passados como o argumento `password` para `generateCustomerToken`. O resolvedor detecta o tipo de token e faz a validação de acordo.
