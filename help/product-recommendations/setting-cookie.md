---
title: Lidar com restrições de cookies
description: Saiba como as Recomendações de produto lidam com restrições de cookies e conformidade com a privacidade.
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
TQID: https://experienceleague.adobe.com/qqgwO4KI4koSBcYu9mdrjb6AQFW4guxk6dfLDBEwVb8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 454
ht-degree: 0%

---

# Lidar com restrições de cookies

O Adobe Commerce e o Magento Open Source solicitam consentimento antes que os dados sejam armazenados em cookies do navegador. Para obter mais informações, consulte [Modo de restrição de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html).

## Como as recomendações de produto lidam com restrições de cookies

Quando você implanta o módulo `magento/product-recommendations` na produção, ele começa a coletar eventos de interação do comprador na loja. Esses dados podem ser armazenados em cookies do navegador ou em armazenamento local para alimentar algoritmos de recomendação.

>[!IMPORTANT]
>
>As Recomendações de produto agora respeitam o modo de restrição de cookies, pois não coletam nem armazenam dados em cookies ou no armazenamento local quando as restrições de cookies são ativadas. Isso inclui dados comportamentais usados para recomendações personalizadas.

### Dados afetados pelas restrições de cookies

Os dados das seguintes Recomendações de produto não são coletados quando o modo de restrição de cookie está ativado:

- **Dados comportamentais**: exibições de produtos, ações de adição ao carrinho, compras e outras interações do comprador.
- **Dados da sessão**: informações da sessão do comprador e interações da unidade de recomendação.
- **Dados do Personalization**: dados usados para tipos de recomendações como &quot;Visualizados recentemente&quot; e &quot;Mais comprados&quot;.

### Impacto nos tipos de recomendação

Quando o modo de restrição de cookies está ativado e os compradores não aceitam cookies, determinados tipos de recomendação podem não ser exibidos ou podem mostrar resultados limitados:

- **Produtos visualizados recentemente**: requer dados de sessão armazenados em cookies/armazenamento local.
- **Recomendado para você**: requer dados comportamentais para personalização.
- **Compramos isto, compramos aquilo**: Requer dados do histórico de compras.

>[!NOTE]
>
>Os tipos de recomendação que não dependem de dados comportamentais, como &quot;Mais visualizados&quot; e &quot;Semelhança visual&quot; continuarão a funcionar normalmente mesmo com as restrições de cookie ativadas.

## Soluções de consentimento de cookies de terceiros

As Recomendações de produto podem não se integrar automaticamente a soluções de consentimento de cookies de terceiros. É responsabilidade do comerciante garantir que a coleta de dados esteja em conformidade com as leis e regulamentos de privacidade aplicáveis.

Se você usar uma solução de consentimento de cookie personalizada, poderá implementar o mecanismo de cookie não rastreado para controlar a coleta de dados.

### Implementação de cookies do-not-track

Você pode usar o cookie `mg_dnt` para controlar programaticamente a coleta de dados:

#### Nome do cookie

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### Desabilitar coleta de dados

Defina o cookie não rastreado quando os usuários recusarem cookies:

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### Habilitar coleta de dados

Limpar o cookie não rastreado quando os usuários aceitarem cookies:

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Testando o modo de restrição de cookie

Para testar como as Recomendações de produto se comportam com restrições de cookie:

1. Ative o modo de restrição de cookies na configuração do Adobe Commerce.
1. Visite sua loja sem aceitar cookies.
1. Verifique se as unidades de recomendação exibem o conteúdo de fallback apropriado.
1. Aceite cookies e verifique se as recomendações começam a coletar dados.

## Conformidade com privacidade

A coleta de dados do Recommendations de produto não inclui informações pessoalmente identificáveis (PII). Todos os identificadores de usuário, como IDs de cookies e endereços IP, são anônimos. Para obter mais informações, consulte a [Política de Privacidade da Adobe](https://www.adobe.com/privacy/policy.html).

>[!TIP]
>
>Para clientes da área de saúde que usam a extensão HIPAA do Data Services, pode ser necessária uma configuração adicional. Consulte [Preparação para a HIPAA](../data-connection/hipaa-readiness.md) para obter mais informações.
