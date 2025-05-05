---
title: Lidar com restrições de cookies
description: Saiba como as recomendações de produto lidam com restrições de cookies.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Lidar com restrições de cookies

O Adobe Commerce e o Magento Open Source solicitam consentimento antes que os dados sejam armazenados em cookies do navegador. Para obter mais informações, consulte [Modo de restrição de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=pt-BR).

Quando você implanta o módulo `magento/product-recommendations` na produção, ele começa a coletar eventos de interação do comprador na loja. Como os dados desses eventos podem ser armazenados em cookies do navegador ou no armazenamento local, o recurso suporta o modo de restrição de cookie, pois não coleta eventos até que o comprador tenha dado o consentimento para o cookie.

Isso pode não funcionar com soluções de consentimento de cookies de terceiros. É responsabilidade de cada comerciante garantir que a coleta de dados não ocorra antes que o cookie tenha sido consentido, como é frequentemente exigido por lei. Se você gerenciar o consentimento de cookies com um código personalizado, poderá usar um cookie não rastreável chamado `mg_dnt` para restringir a coleta de dados.

- Nome do cookie:

  ```text
  `const DNT_COOKIE = "mg_dnt";`
  ```

- Defina o cookie do-not-track para desativar a coleta de dados:

  ```text
  `$.mage.cookies.set(DNT_COOKIE, true);`
  ```

- Para limpar o cookie quando o usuário aceitar os cookies:

  ```text
  `$.mage.cookies.clear(DNT_COOKIE);`
  ```
