---
title: Visão geral de segurança
description: Saiba mais sobre os recursos de segurança do Adobe Commerce as a Cloud Service.
role: Admin, Architect, Leader
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 0343c4f3ecc182145a97e08eca2790bd1512aa27
workflow-type: tm+mt
source-wordcount: '581'
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

Para obter mais informações sobre os recursos de segurança do [!DNL API Mesh], consulte a [documentação da API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}.

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

Ao usar o [!DNL API Mesh], os segredos devem ser armazenados no arquivo `secrets.yaml` na sua configuração de malha. [!DNL API Mesh] criptografa esses segredos usando a criptografia AES-256 ([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/)).

Todos os dados armazenados em [!DNL Adobe Commerce as a Cloud Service] são criptografados em repouso usando a criptografia de 256 bits do AES e todos os dados são criptografados em HTTPS usando TLS 1.2 ou posterior em trânsito.
