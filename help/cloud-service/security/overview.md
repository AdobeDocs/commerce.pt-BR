---
title: Visão geral de segurança
description: Saiba mais sobre os recursos de segurança do Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
autotag-review: '2026-06-18T16:18:52.695Z'
TQID: 'https://experienceleague.adobe.com/AmkzZgLeOa9zJkPE8kWM6lFcFNtBAAOmJeULI-y4gOw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: adedf3b3-e153-47a3-ae73-b5d65067b544
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 18f6be542e84f1769a91867c4d54ca3cde3c0ac1
workflow-type: tm+mt
source-wordcount: 577
ht-degree: 0%

---


# Visão geral de segurança

O [!DNL Adobe Commerce as a Cloud Service] foi projetado com segurança em sua essência — oferecendo uma plataforma comercial moderna, nativa de SaaS, que oferece proteção de nível empresarial, resiliência operacional e tranquilidade para empresas de todos os tamanhos.

Ao contrário dos modelos PaaS tradicionais, o modelo SaaS elimina a carga dos ciclos manuais de patch, manutenção da infraestrutura e upgrade. A segurança está incorporada em todas as camadas da plataforma — desde a infraestrutura gerenciada pela Adobe e pipelines de implantação automatizada até o gerenciamento de identidade e acesso por meio do [!DNL Adobe IMS].

O [!DNL Adobe Commerce as a Cloud Service] aproveita a estrutura global de segurança e conformidade da Adobe, garantindo o alinhamento com padrões do setor, como ISO 27001, SOC 2 e GDPR. Os clientes se beneficiam de um [modelo de responsabilidade compartilhada](./shared-responsibility.md) que define claramente a função da Adobe na proteção da plataforma e a função do cliente no gerenciamento de dados e acesso.

Com proteções integradas, como o WAF (Web Application Firewall), mitigação de DDoS, provisionamento seguro e verificação contínua de vulnerabilidades, o [!DNL Adobe Commerce as a Cloud Service] permite que as empresas inovem mais rapidamente sem comprometer a segurança.

Este documento descreve a arquitetura de segurança, as proteções operacionais e a postura de conformidade do [!DNL Adobe Commerce as a Cloud Service], permitindo que os clientes tomem decisões informadas e dimensionem com confiança suas operações de comércio digital.

## Rede de entrega de conteúdo (CDN) e firewall de aplicativo web (WAF)

### CDN da loja

Os comerciantes podem optar por implantar uma CDN gerenciada pela Adobe ou comprar sua própria solução de CDN para proteger a loja habilitada pela Commerce.

>[!IMPORTANT]
>
>Se os clientes optarem por implantar a CDN gerenciada pela Adobe, não poderão configurar regras de CDN. Regras personalizadas de armazenamento em cache ou regras do WAF podem ser configuradas pelos clientes quando eles trazem seu próprio CDN para proteger suas vitrines.

### [!DNL API Mesh for Adobe Developer App Builder] CDN

A camada CDN de [!DNL API Mesh] encerra o TLS, executa o gateway do GraphQL como Workers, fornece cache de borda global e DDoS/WAF automático e expõe `edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io` como pontos de extremidade de malha pública; os clientes podem adicionar seu próprio CDN na frente, mas o CDN de [!DNL API Mesh] é fixo e gerenciado pelo Adobe e os clientes não podem configurar suas próprias regras do WAF.

Para obter mais informações sobre os recursos de segurança do [!DNL API Mesh], consulte a [documentação da API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/security){target="_blank"}.

### CDN de back-end

Uma CDN interna protege [!DNL Adobe Commerce as a Cloud Service].

Devido à arquitetura [!DNL Adobe Commerce as a Cloud Service], quando um comerciante provisiona uma instância em uma célula composta, como `na1`, `eu1`, `au1` ou outras regiões geográficas, três superfícies públicas são expostas:

| Superficial | Exemplo de padrão de URL |
| --- | --- |
| Interface do administrador | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| REST API | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| API do GraphQL | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service] usa uma WAF e uma CDN combinadas:

- **WAF** - Proteção do Firewall do Aplicativo Web para todas as [!DNL Adobe Commerce as a Cloud Service] superfícies públicas.
- **CDN** - cache do Edge para ativos estáticos e respostas do GraphQL que podem ser armazenadas em cache.

O WAF e o CDN são gerenciados pela plataforma [!DNL Adobe Commerce as a Cloud Service] e não podem ser configurados pelos clientes.

### Proteção de DDoS

O CDN e o WAF integrados fornecem proteção de DDoS de camada de rede e de camada HTTP. [!DNL Adobe Commerce as a Cloud Service] não expõe esses logs de WAF ou DDoS diretamente para os comerciantes.

## Armazenamento e criptografia de dados

Se os dados estiverem sendo armazenados em [!DNL App Builder], um comerciante poderá consultar as [!DNL App Builder] [opções de armazenamento](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/). [!DNL App Builder] força o isolamento do locatário e o acesso aos dados armazenados nesses serviços é restrito ao namespace de tempo de execução no qual a ação é executada. Não há criptografia de dados no armazenamento.

Ao usar o [!DNL API Mesh], os segredos devem ser armazenados no arquivo `secrets.yaml` na sua configuração de malha. O [!DNL API Mesh] criptografa esses segredos usando a criptografia AES-256 (consulte a [documentação da API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/security){target="_blank"}).

Todos os dados armazenados em [!DNL Adobe Commerce as a Cloud Service] são criptografados em repouso usando a criptografia de 256 bits do AES e todos os dados são criptografados em HTTPS usando TLS 1.2 ou posterior em trânsito.
