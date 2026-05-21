---
title: Como O  [!DNL Commerce] Services Lida Com Solicitações De Privacidade
description: Saiba como o  [!DNL Commerce] services lida com solicitações para acessar e excluir dados.
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
TQID: https://experienceleague.adobe.com/KhsveSMPR0tKmNzViEaWWHDu8fWve0GZjwsl2oyvx1k
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: d00e9f03-e50b-4162-b143-0c0817c937c2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 595
ht-degree: 1%

---

# Solicitações de privacidade

O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface para ajudar você a gerenciar solicitações de dados do cliente. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

Para obter mais informações sobre o Privacy Service e como criar e gerenciar solicitações de privacidade, consulte a documentação do Adobe Experience Platform:

* [Visão geral do Privacy Service](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/home)
* [Gerenciamento de processos de privacidade na interface do usuário do Privacy Service](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide)

## Gerenciar solicitações individuais de privacidade de dados

Você pode enviar solicitações individuais para acessar e excluir dados do consumidor de [!DNL Commerce] de duas maneiras:

* Por meio da **interface do usuário do Privacy Service**. Consulte a documentação [aqui](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide#_blank).
* Por meio da **API do Privacy Service**. Consulte a documentação [aqui](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) e as informações sobre a API [aqui](https://developer.adobe.com/experience-platform-apis/#_blank).

O Privacy Service oferece suporte a dois tipos de solicitações: **acesso aos dados** e **exclusão de dados**.

>[!NOTE]
>
>Este artigo se concentra em fazer solicitações de privacidade para [!DNL Commerce]. Se você planeja fazer solicitações de privacidade para o [data lake da Platform](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/privacy), o [Perfil de cliente em tempo real](https://experienceleague.adobe.com/en/docs/experience-platform/profile/privacy) ou o [Serviço de identidade](https://experienceleague.adobe.com/en/docs/experience-platform/identity/privacy), consulte os respectivos guias de usuário. Observe que as solicitações de exclusão e acesso devem ser feitas a cada sistema individualmente, pois uma solicitação de privacidade para o Commerce não remove dados de todos esses sistemas.

## Acesso aos dados

Para **solicitações de acesso**, especifique &quot;Commerce (Personalization)&quot; na interface do usuário (ou `commerceMarketingData` como um código de produto na API).

## Exclusão de dados

Para solicitações de exclusão, o Privacy Service exclui [!DNL Commerce] dados armazenados nos serviços SaaS da Commerce para fins de marketing, o que significa que perfis e pedidos de titulares de dados não são mais enviados para aplicativos de marketing da Adobe para uso em campanhas e jornadas de clientes. No entanto, a Privacy Service não exclui dados no aplicativo [!DNL Commerce], pois eles podem ser necessários para necessidades transacionais de comerciante. Os comerciantes são responsáveis por qualquer solicitação de exclusão/acesso de dados no aplicativo [!DNL Commerce]. Consulte [Modelo operacional e de segurança de responsabilidade compartilhada](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility) para saber mais.

[!DNL Commerce] notificará os comerciantes sobre solicitações de exclusão enviando informações para titulares de dados que solicitam a exclusão de determinados dados.

## Como criar solicitações de acesso e exclusão

### Pré-requisitos

Para fazer solicitações de acesso e exclusão de dados para o Adobe [!DNL Commerce], você deve ter:

* uma ID organizacional IMS
* um Identificador de identidade da pessoa que você deseja agir e os namespaces correspondentes. Para obter mais informações sobre namespaces de identidade no Adobe [!DNL Commerce] e no Experience Platform, consulte a [visão geral sobre namespaces de identidade](https://experienceleague.adobe.com/pt-br/docs/experience-platform/identity/features/namespaces).

### Exemplo de acesso de solicitação/exclusão de GDPR:

Para **solicitações de acesso**, especifique &quot;Commerce (Personalization)&quot; da interface do usuário (ou &quot;commerceMarketingData&quot; como código de produto na API).

Para **excluir solicitações**, verifique se a caixa de seleção &quot;Commerce (Personalization)&quot; está habilitada. Além disso, se o perfil do cliente e os dados do pedido já tiverem sido enviados de [!DNL Commerce] para a Adobe Experience Platform, você deverá enviar solicitações de exclusão para os seguintes serviços downstream.

* Perfil (código do produto: &quot;profileService&quot;)
* AEP Data Lake (código do produto: &quot;AdobeCloudPlatform&quot;)
* Identidade (código do produto: &quot;identidade&quot;)

Para enviar solicitações de acesso e exclusão por meio da API de privacidade, é necessário autenticar e gerenciar permissões para o Privacy Service:

* [Autenticar e acessar a API do Privacy Service](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/api/getting-started)
* [Gerenciar permissões do Privacy Service](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/permissions)

**Cabeçalhos obrigatórios**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**Solicitação**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**Resposta**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
