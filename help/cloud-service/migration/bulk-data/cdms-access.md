---
title: Verificar Acesso ao Serviço de Migração
description: Saiba como verificar o acesso completo à API do serviço de migração de dados da Commerce, confirmando a acessibilidade da rede, a autenticação IMS e a autorização do locatário.
feature: Cloud
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# Verificar acesso ao serviço de migração

{{bulk-data-early-access}}

Use este guia para verificar o acesso completo à API do Serviço de migração de dados (CDMS) da Commerce a partir de seu ambiente. Uma chamada bem-sucedida valida simultaneamente a capacidade de alcance da rede dos IPs de saída (incluir na lista de permissões de IPs), da autenticação IMS e da autorização do locatário.

Conclua este guia depois de concluir todos os itens da [Lista de verificação de preparação do cliente](readiness-checklist.md) e antes de executar a migração descrita no [guia de migração](migration-guide.md).

## Pré-requisitos

- Uma credencial OAuth 2.0 Server-to-Server (ID de cliente e segredo do cliente) criada no [Adobe Developer Console](https://developer.adobe.com/console/).
- Sua ID da organização IMS, no formato `<org>@AdobeOrg`. A organização deve ser proprietária do locatário de destino.
- O destino `tenantId`, uma ID de locatário IMS alfanumérica de 22 caracteres.
- Endereços IP de saída enviados para o gateway CDMS e pelo Adobe. Entre em contato com a equipe do Adobe se não tiver certeza sobre os endereços IP ou seus status.
- O host de serviço específico da região da tabela [Hosts de serviço por ambiente e região](#service-hosts-by-environment-and-region).

## Gerar um token de acesso IMS

Gere um token de acesso usando suas credenciais de Servidor para Servidor do OAuth 2.0 com a concessão `client_credentials`. O host IMS nessa etapa é o mesmo para todas as regiões de dados. Somente o host CDMS é alterado por região.

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## Chamar a API de migração de lista

A solicitação a seguir recupera a lista de migrações para o locatário e requer o token de acesso da etapa anterior. Selecione o host da sua região na tabela [Hosts de serviço por ambiente e região](#service-hosts-by-environment-and-region). O sinalizador `-i` imprime a linha de status HTTP e os cabeçalhos de resposta para que você possa confirmar o resultado.

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## Interpretar a resposta

| Código HTTP | Significado | Exemplo de corpo de resposta |
| --- | --- | --- |
| 200 | Sucesso. Conectividade, autenticação e autorização do locatário foram transmitidas. O corpo da resposta contém a lista de migrações para o locatário. | `{"migrations":[...]}` |
| 401 | Token de portador ausente ou inválido, rejeitado antes de alcançar o serviço. [Regenerar o token](#generate-an-ims-access-token). | Varia (gerado pelo gateway) |
| 403 | O usuário autenticado não tem permissões de migração para este locatário. | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | Erro interno do servidor. | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>Se a solicitação atingir o tempo limite ou a conexão for recusada e nenhum status HTTP for retornado, o IP de saída provavelmente não será atualizado ou você está usando um host incorreto. Confirme o host da região na tabela a seguir e os IPs personalizados.

## Hosts de serviço por ambiente e região

| Região ou ambiente | Host |
| --- | --- |
| Sandbox ou pré-produção | `https://na1-sandbox.api.commerce.adobe.com` |
| América do Norte | `https://na1.api.commerce.adobe.com` |
| Europa | `https://eu1.api.commerce.adobe.com` |
| Índia | `https://in1.api.commerce.adobe.com` |
| Reino Unido | `https://uk1.api.commerce.adobe.com` |
| Austrália e Nova Zelândia | `https://au1.api.commerce.adobe.com` |

## Próximas etapas

Após confirmar o acesso, prossiga para o [guia de migração](migration-guide.md) para iniciar a configuração do ambiente e a execução da migração.
