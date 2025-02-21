---
title: Estimar o volume de dados e o tempo de transmissão
description: Saiba como estimar o volume de dados e o tempo de transmissão necessários para que a ferramenta [!DNL data export] sincronize dados de feed entre o Adobe Commerce e os serviços conectados.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Estimar o volume de dados e o tempo de transmissão para a sincronização de dados

A Adobe recomenda estimar o volume de dados e o tempo de sincronização antes de iniciar qualquer sincronização do feed de dados para garantir uma programação tranquila e evitar interrupções nas operações do site. Essa estimativa é importante ao planejar sincronizações iniciais ou atualizações de catálogos em larga escala, como alterações de preço em massa.

Por padrão, a ferramenta de exportação de dados processa dados no modo de thread único com um tamanho de lote padrão. Com a configuração padrão, não há paralelização do processo de envio do feed. Além disso, esse componente aceita solicitações por segundo (RPS), o que se traduz no seguinte:

- Até 10.000 produtos por minuto quando um produto for um SKU com atributos em uma loja específica
- Até 50 mil preços por minuto

Os seguintes fatores afetam o tempo de transmissão de dados durante a sincronização.

- A contagem de threads está definida como 1 (por padrão)
- O tamanho do lote está definido como _100_ para todos os feeds, exceto para o feed `prices`, no qual está definido como _500_.
- A taxa de aceitação do feed é de 2 solicitações por segundos.
- Todos os produtos são atribuídos a todos os sites existentes
- Para os cenários de cálculo de preço, todos os produtos têm preços especiais e agrupados atribuídos a eles


## Calcular a transmissão de dados por feed

Use os valores e as fórmulas na tabela a seguir para calcular o volume de dados e o tempo de sincronização para cada feed de dados.

>[!NOTE]
>
>Esses cálculos são baseados em uma taxa de transmissão de 2 solicitações por segundo. A velocidade se baseia no tempo necessário para a coleta e o envio de dados. A velocidade de transmissão real varia dependendo do tamanho do payload da solicitação e da carga atual no servidor de aplicativos do Commerce.

| Feed | Exemplo de dados | Fórmula para Calcular Registros | Contagem de Solicitações Previstas | Tempo de ressincronização previsto |
| --- | --- | --- | --- | --- |
| Produtos | Produtos (P): 10000, Visualizações da loja (SV): 4 | P * SV = 40000 | 40000 / Tamanho de Lote (100) = 400 solicitações | (400 solicitações * 0,5 segundo por solicitação) / 60 = 3,3 minutos |
| Categorias | Categorias (C): 500, Visualizações da loja (SV): 4 | C * SV = 2000 | 2000 / Tamanho de Lote (100) = 20 solicitações | (20 solicitações * 0,5 segundo por solicitação) / 60 = 0,1 minuto (4 segundos) |
| Preços | Produtos (P): 10000, Grupos de clientes (CG): 6 (por exemplo, preço único no catálogo compartilhado), Sites (WS): 2 | P \* WS * CG = 120000 | 120000 / Tamanho de Lote (500) = 240 solicitações | (240 solicitações * 0,5 segundo por solicitação) / 60 = 2 minutos |
| Substituições de produto | Produtos com permissões ou no catálogo compartilhado (P): 10000, Grupos de clientes afetados (CG): 5, Sites atribuídos WS: 2 | P \* WS * CG = 100000 | 100000 / Tamanho de Lote (100) = 1000 solicitações | (1.000 solicitações * 0,5 segundo por solicitação) / 60 = 8,3 minutos |
| Variantes do produto | Variantes (produtos secundários) atribuídas aos produtos configuráveis (PV): 100000 | PV = 100000 | 100000 / Tamanho de Lote (100) = 1000 solicitações | (1.000 solicitações * 0,5 segundo por solicitação) / 60 = 8,3 minutos |
| Permissões de categoria | Contagem de todas as Permissões de Categoria + 4 registros de fallback (CP): 10000 | CP = 10000 | 10000 / Tamanho de Lote (100) = 100 solicitações | (100 solicitações * 0,5 segundo por solicitação) / 60 = 0,8 minuto (50 segundos) |
| Status do Estoque de Estoque | Produtos (P): 10000, Produtos de estoque atribuídos a (S): 5 (supondo que cada produto esteja atribuído a cada estoque) | P * S = 50000 | 50000 / Tamanho de Lote (100) = 500 solicitações | (500 solicitações * 0,5 segundo por solicitação) / 60 = 4,2 minutos |
| Ordens de Venda | Todos os registros de ordem (incluindo NFFs, entregas e assim por diante) (SO): 10000 | SO = 10000 | 10000 / Tamanho de Lote (100) = 100 solicitações | (100 solicitações * 0,5 segundo por solicitação) / 60 = 0,8 minuto (50 segundos) |
