---
title: Pontos de Extremidade REST da Conta de Cartão-presente
description: Saiba como usar APIs REST de conta de cartão-presente para criar, atualizar, excluir e consultar contas de cartão-presente de forma programática no  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer
level: Experienced
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# API da conta de cartão-presente

{{accs-sandbox-experimental}}

Os endpoints REST da conta de cartão-presente oferecem gerenciamento programático de contas de cartão-presente no nível da conta, não no nível do carrinho ou da cotação. Use essa API para criar, recuperar, atualizar e excluir contas de cartão-presente ou provisionar contas de cartão-presente em massa por meio do endpoint de importação JSON.

Esses endpoints foram projetados para:

* Administradores que gerenciam programas de cartão-presente
* Integrações de terceiros que provisionam cartões-presente de sistemas externos, como ERP, CRM e plataformas de marketing
* Fluxos de trabalho automatizados para a criação de vale-presente em massa

## Autenticação

Todos os endpoints exigem um token de portador de administrador ou integração. O token deve ser associado a uma função que inclua o recurso ACL (Lista de Controle de Acesso) `Magento_GiftCardAccount::giftcardaccount`.

Para operações de importação em massa, a função também deve incluir o recurso de ACL `Magento_ImportExport::import_api`.

## Contexto do site e da loja

Os valores de exibição do site e da loja são resolvidos dos cabeçalhos de solicitação HTTP, não do corpo da solicitação. Transmita um dos seguintes cabeçalhos com cada solicitação:

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

A API resolve o site automaticamente a partir desses cabeçalhos. Não inclua `website_id` na carga da solicitação REST.

>[!NOTE]
>
>O ponto de extremidade de importação em massa é uma exceção. Como a importação opera em massa e pode direcionar sites específicos, cada linha na carga de importação requer um valor `website_id` explícito.

## Referência da API REST

A API expõe as seguintes operações em `/V1/giftcardaccounts`, todas protegidas pelo recurso de ACL `Magento_GiftCardAccount::giftcardaccount`:

| Método | URL | Descrição |
|--------|-----|-------------|
| POST | `/rest/V1/giftcardaccounts` | Criar uma conta de cartão-presente |
| GET | `/rest/V1/giftcardaccounts` | Listar contas (suporta searchCriteria) |
| GET | `/rest/V1/giftcardaccounts/:id` | Obter conta por ID |
| GET | `/rest/V1/giftcardaccounts/code/:code` | Obter conta por código |
| PUT | `/rest/V1/giftcardaccounts/:id` | Atualizar conta (semântica de mesclagem) |
| DELETE | `/rest/V1/giftcardaccounts/:id` | Excluir conta |

### Referência do campo

| Campo | Tipo | Valores válidos | Criar REST | Importar |
|---|---|---|---|---|
| `code` | string | Máximo de 255 caracteres | Obrigatório | Obrigatório |
| `balance` | flutuante | >= 0 | Obrigatório | Obrigatório |
| `status` | int | `0` (desabilitado), `1` (habilitado) | Opcional, o padrão é `1` | Opcional, o padrão é `1` |
| `state` | int | `0` (disponível), `1` (usado), `2` (resgatado), `3` (expirado) | Opcional, o padrão é `0` | Opcional, o padrão é `0` |
| `is_redeemable` | int | `0` ou `1` | Opcional, o padrão é `1` | Opcional, o padrão é `1` |
| `date_expires` | string | `YYYY-MM-DD` ou nulo | Opcional | Opcional |
| `date_created` | string | `YYYY-MM-DD` | Configuração automática | Opcional, definir automaticamente se omitido |
| `website_id` | int | ID de site válida | Não aceito (resolvido automaticamente a partir de cabeçalhos) | Obrigatório |

### Criar uma conta de cartão-presente

Cria uma nova conta de cartão-presente com detecção de código duplicado.

| Item | Valor |
|---|---|
| **Método** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**Corpo da solicitação:**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**Resposta (200):**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### Recuperar uma conta de cartão-presente por ID

| Item | Valor |
|---|---|
| **Método** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Resposta (200):**

Retorna um único objeto de conta de cartão-presente.

### Recuperar uma conta de cartão-presente por código

| Item | Valor |
|---|---|
| **Método** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>Se um código de cartão-presente for meramente numérico (por exemplo, `12345`), uma solicitação para `/V1/giftcardaccounts/12345` corresponderá à rota da ID, não à rota do código. Sempre use `/V1/giftcardaccounts/code/12345` para pesquisas baseadas em código quando o código puder ser numérico.

**Resposta (200):**

Retorna um único objeto de conta de cartão-presente.

### Listar contas de cartão-presente com critérios de pesquisa

| Item | Valor |
|---|---|
| **Método** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

Transmita os critérios de pesquisa como parâmetros de consulta. O exemplo a seguir retorna contas de cartão-presente nas quais `status` é igual a `1` (habilitado):

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**Resposta (200):**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### Atualizar uma conta de cartão-presente

Atualiza uma conta de cartão-presente existente usando a semântica de mesclagem. Somente campos não nulos são aplicados na solicitação. O campo `code` é imutável. Transmitir um código diferente retorna um erro de validação.

| Item | Valor |
|---|---|
| **Método** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Corpo da solicitação:**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**Resposta (200):**

Retorna o objeto de conta de cartão-presente atualizado.

### Excluir uma conta de cartão-presente

| Item | Valor |
|---|---|
| **Método** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Resposta (200):**

```json
true
```

## Importação em massa via JSON

As contas de cartão-presente podem ser provisionadas em massa usando `POST /V1/import/json` com o tipo de entidade `giftcardaccount`. Este ponto de extremidade requer o recurso ACL (Lista de Controle de Acesso) do `Magento_ImportJsonApi::import_api`, além da ACL da conta de cartão-presente.

### Comportamentos compatíveis

| Comportamento | Descrição |
|---|---|
| `append` | Cria novas contas de cartão-presente. Se um código já existir, essa linha falhará e a importação continuará com as linhas restantes. |
| `replace` | Atualiza e insere as contas de cartão-presente por código. Cria a conta se o código não existir e o substitui se existir. |
| `delete` | Remove contas de cartão-presente por código. |

### Exemplo de solicitação

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### Importar detalhes de comportamento

* Cada linha na carga de importação requer um `website_id` explícito, ao contrário dos pontos de extremidade REST que inferem o site dos cabeçalhos de solicitação.
* Cada linha é validada independentemente. Linhas inválidas produzem erros por linha sem afetar linhas válidas no mesmo lote.
* Códigos duplicados no mesmo lote são detectados e relatados como erros por linha em vez de causar uma reversão de transação.
* A importação grava diretamente no banco de dados para fins de desempenho e ignora o ciclo de vida de salvamento do modelo do fornecedor. As entradas do histórico de alteração de saldo não são criadas durante a importação.
* As operações de criação REST rejeitam datas de expiração passadas. A importação aceita datas de expiração anteriores por design, para oferecer suporte à migração de dados históricos.

## Tratamento de erros

A API retorna códigos de status HTTP padrão:

| Código de status | Condição |
|---|---|
| `400` | Erro de validação. Campos obrigatórios ausentes, valores inválidos ou data de expiração passada na criação de REST. |
| `401` | Token de portador ausente ou inválido. |
| `403` | O token não tem o recurso de ACL necessário. |
| `404` | Conta de cartão-presente não encontrada. |
| `409` | Código de cartão-presente duplicado. |

A validação de entrada abrange campos obrigatórios, intervalos de valores (o status deve ser `0` ou `1`, o estado deve ser `0`-`3`, o saldo deve ser não negativo), o formato de data e a segurança de tipo. Valores não numéricos para campos numéricos são rejeitados.
