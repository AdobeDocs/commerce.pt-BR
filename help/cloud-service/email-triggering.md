---
title: Acionamento de email por meio do REST
description: Saiba como acionar emails transacionais sob demanda usando a API REST especificando uma ID de modelo, email de destinatário e variáveis de modelo para  [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Experienced
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Acionamento de email por meio da API REST

Anteriormente, só era possível enviar emails quando os eventos eram acionados, como durante o registro do cliente ou a compra do pedido. No [!DNL Adobe Commerce as a Cloud Service], você pode enviar emails por meio da API REST sob demanda especificando uma ID de modelo, email de destinatário e variáveis de modelo.

>[!NOTE]
>
>Atualmente, somente templates recém-criados e personalizados podem ser enviados. Não há suporte para modelos predefinidos e do sistema.

O ponto de extremidade `V1/custom-email/send` permite que **sistemas de terceiros**, como integrações e serviços externos, enviem emails sob demanda especificando:

- **ID do Modelo** - ID do modelo de email.
- **Email do destinatário** - O endereço de email de destino desta solicitação.
- **Variáveis** - (Opcional) Pares de valores-chave definidos pelo cliente para inserir no modelo, como `customer_name` ou `order_id`.

>[!NOTE]
>
>O email é enviado de forma síncrona usando o escopo de armazenamento atual e o endereço de email padrão **De** ou o endereço de email definido para modelos.

## Contrato REST

A seção a seguir explica como enviar emails transacionais sob demanda usando a API REST.

### Endpoint

- **URL** - `POST /rest/V1/custom-email/send`
- **Autorização** - Apenas **autorização IMS de serviço para serviço** tem suporte. O chamador deve ter acesso ao recurso **Enviar Email Personalizado via API** (`Magento_CustomEmailSend::send_custom_email`). Consulte [Autenticação REST](https://developer.adobe.com/commerce/webapi/rest/authentication/) para obter mais informações.
- **Uso assíncrono** (recomendado) - Embora este ponto de extremidade seja implementado de forma síncrona, recomendamos chamá-lo usando a **API REST assíncrona** para que a solicitação seja enfileirada e processada por um consumidor, evitando conexões HTTP de longa duração. Em [!DNL Adobe Commerce as a Cloud Service], você pode usar a rota com `/async` depois de `V1`, por exemplo: `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`.

  Consulte [Pontos de extremidade da Web assíncronos (SaaS)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/) para obter mais informações.

### Corpo da solicitação

- **templateId** (inteiro, obrigatório) - ID de modelo de email conforme definido no Administrador em [!UICONTROL **Marketing**] > [!UICONTROL _Comunicações_] > [!UICONTROL **Modelos de email**].

- **recipientEmail** (cadeia de caracteres, obrigatório) - O endereço de email de destino. Deve ser um formato de email válido. Valores ausentes ou vazios acionam um erro de validação.
- **variáveis** (objeto, opcional) - mapa de valor-chave inserido no modelo como um `UnstructuredArray`.

  Se você não estiver usando variáveis, transmita ou omita um objeto vazio. No corpo e no assunto do modelo de email, use a sintaxe de variável para fazer referência a uma variável, por exemplo `var order_id`. O assunto também oferece suporte às mesmas variáveis personalizadas e sintaxe descritas em [Cenários de modelo com suporte](#supported-template-scenarios).

### Resposta de sucesso (HTTP 200)

A API retorna HTTP 200 no envio bem-sucedido.

### Respostas de erro

- **HTTP 400 - Erro de validação**

  A integração deve fornecer um `templateId` e `recipientEmail` válidos para cada solicitação.

   - `"message": "Invalid recipient email format"` - endereço de destinatário inválido ou malformado
   - `"message": "Recipient email is required."` - ausente ou vazio `recipientEmail`
   - `"message": "Template ID must be a positive integer."` - ausente, zero ou inválido `templateId`

- **HTTP 404 - Modelo não encontrado**

  Exemplo: `"message": "Email template with ID \"999\" does not exist."`

## Cenários de modelo compatíveis

Os seguintes recursos de modelo são suportados no **corpo do email** e no **assunto do modelo**:

>[!NOTE]
>
>O assunto do modelo também é compatível com variáveis personalizadas. Use `var variableName` e outra sintaxe conforme descrito na seção a seguir.

- **Incluir diretiva** - para incluir outros modelos de design, como um cabeçalho de email.

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **Variáveis simples** - use `var variableName`, por exemplo `var order_id` ou `var g`.

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **Notação aninhada/de pontos** - para chaves aninhadas transmitidas na solicitação `variables`, em traduções, use nomes com prefixos em dólar, como `$order_data.customer_name`, `$order.increment_id` ou `$order_data.frontend_status_label`.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Tradução (trans)** - texto com parâmetros, traduções de várias linhas com vários espaços reservados e marcas HTML.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Saída bruta** - use o filtro `|raw` quando o conteúdo traduzido ou variável contiver HTML (por exemplo, `<strong>` ou `<a>`).

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **URL helper** - para armazenar URLs dentro de traduções.

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
