---
title: Estimar o volume de dados e o tempo de sincronização
description: Saiba como estimar o volume de dados e o tempo de sincronização dos feeds do [!DNL Adobe Commerce Optimizer Connector] para planejar sincronizações de catálogo e evitar interrupções.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
source-git-commit: 2dbf2b973af0cb7b831a17ca1a868a81b11bc9ee
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%
---

# Estimar o volume de dados e o tempo de sincronização

A Adobe recomenda estimar o volume de dados e o tempo de sincronização antes de iniciar qualquer sincronização de feed para garantir uma programação tranquila e evitar interrupções nas operações do site. Isso é especialmente importante ao planejar sincronizações iniciais ou atualizações de catálogo em larga escala, como alterações de preço em massa.

Por padrão, o conector processa feeds no modo de thread único. Não há paralelização no processo de envio do feed. A API de assimilação aceita até 2 solicitações por segundo. No entanto, a alocação básica para a taxa de assimilação [!DNL Adobe Commerce Optimizer] limita a taxa de transferência ao seguinte:

- Até 1.000 produtos por minuto (um produto é uma SKU com atributos em uma exibição de loja específica). Consulte [Limites e limites](../../optimizer/boundaries-limits.md) para obter detalhes de alocação base.
- Até 50 mil preços por minuto

## Fatores que afetam o tempo de sincronização

As estimativas abaixo assumem as seguintes condições:

- Contagem de threads: 1 (padrão)
- Taxa de aceitação do feed: 2 solicitações por segundo (0,5 segundo por solicitação)
- Todos os produtos são atribuídos a todos os sites existentes

A velocidade de transmissão real varia dependendo do tamanho da carga da solicitação e da carga atual no servidor de aplicativos do Commerce.

## Calcular tempo de sincronização por feed

Use a tabela a seguir para estimar o número de registros, solicitações e tempo de sincronização para cada feed do conector. Os valores de tamanho do lote refletem os limites definidos na referência de [feeds com suporte](connector-reference.md#supported-feeds).

>[!NOTE]
>
>O tempo de sincronização do produto se baseia no limite básico de alocação de 1.000 produtos por minuto. Para outros feeds, os cálculos são baseados em uma taxa de transmissão de 2 solicitações por segundo. A velocidade real depende do tamanho da carga e da carga do servidor.
>
>A estimativa de preços presume que todos os grupos de clientes tenham preços exclusivos.

| Feed | Exemplo de dados | Fórmula | Solicitações previstas | Tempo de sincronização previsto |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| Produtos | Produtos (P): 10.000, Visualizações da loja (SV): 4 | P × SV = 40.000 registros | 40.000 ÷ tamanho do lote (100) = 400 | 40.000 ÷ 1.000 registros/min = **40 min** |
| Categorias | Categorias (C): 500, Visualizações da loja (SV): 4 | C × SV = 2.000 registros | 2.000 ÷ tamanho do lote (100) = 20 | (20 × 0,5 s) ÷ 60 = **~10 s** |
| Atributos do produto | Atributos (A): 200, Visualizações da loja (SV): 4 | A × SV = 800 registros | 800 ÷ tamanho do lote (100) = 8 | (8 × 0,5 s) ÷ 60 = **~4 s** |
| Preços | Produtos (P): 10.000, Sites (WS): 2, Grupos de clientes (CG): 6 | P × WS × CG = 120.000 registros | 120.000 ÷ tamanho do lote (500) = 240 | (240 × 0,5 s) ÷ 60 = **2 min** |
| Catálogos de preços | Sites (WS): 2, Grupos de clientes (CG): 6 | WS × CG = 12 registros | 12 ÷ tamanho do lote (500) = 1 | (1 × 0,5 s) ÷ 60 = **&lt; 1 s** |

>[!MORELIKETHIS]
>
> - [Módulos de conector e pontos de extremidade de feed](connector-reference.md) - Revise limites de lote e feeds com suporte
> - [Gerenciar sincronização](../data-sync-status.md) - Monitorar status de sincronização e acionar ressincronizações manuais
> - [Pipeline de sincronização do conector](../connector-sync-pipeline.md) - Entenda como as agendas de cron e a sincronização automatizada funcionam
