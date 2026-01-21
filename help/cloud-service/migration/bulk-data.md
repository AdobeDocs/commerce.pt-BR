---
title: Ferramenta de migração de dados em massa
description: Aprenda a usar a ferramenta de migração de dados em massa para migrar dados dos Adobe Systems existentes Comércio na Cloud instância [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a Adobe Systems Comércio como Cloud Service e somente projetos Adobe Systems Comércio Optimizer (infraestrutura SaaS gerenciados Adobe Systems)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# ferramenta de migração de dados em massa

A migração de dados em massa ferramenta segue uma arquitetura distribuída que permite a migração de dados seguros e eficientes dos ambientes PaaS para SaaS. Esta ferramenta ajuda os implementadores de soluções a migrar dados de um Adobe Systems existente Comércio no Cloud instância (PaaS) para [!DNL Adobe Commerce as a Cloud Service] o (SaaS). Para obter mais informações sobre o processo de migração, consulte a visão geral[ da ](./overview.md)migração.

>[!NOTE]
>
>A migração de dados em massa ferramenta suporta a migração apenas de dados principais de comércio primários. Atualmente, a migração de dados personalizados não é suportada.

A imagem a seguir detalha a arquitetura e os principais componentes para usar a migração de dados em massa ferramenta.

![Diagrama da arquitetura da ferramenta de migração de dados em massa mostrando o fluxo de dados PaaS para SaaS](../assets/bulk-data-diagram.png){zoomable="yes"}

## fluxo de Trabalho de migração

A migração de dados em massa fluxo de Trabalho consiste nas seguintes etapas:

1. Configure um novo ambiente para a migração.
1. Copie seus dados do seu sistema antigo.
1. Mova seus dados para o novo sistema.
1. Disponibilize seu catálogo de produtos no novo sistema.
1. Confirme se seus dados migraram corretamente.

As seções a seguir descrevem essas etapas detalhadamente.

## Acesse o ferramenta de migração de dados em massa

A disponibilidade da ferramenta de migração de dados em massa é a seguinte:

- **Primeiro trimestre de 2026** (ainda não disponível) - Após a versão inicial da migração de dados em massa ferramenta, você poderá acessá-la enviando um ticket de suporte.
- **Primeiro trimestre de 2026** (ainda não disponível) - Após o lançamento público da migração de dados em massa ferramenta, ele estará acessível a partir desta página.

## ambiente de Criar Direcionamento

O implementador de soluções (SI) cria uma Direcionamento ambiente para a migração. Essa ambiente armazena os dados migrados do instância de origem.

Primeiro, [crie uma nova [!DNL Adobe Commerce as a Cloud Service]  instância (SaaS).](../getting-started.md#create-an-instance)

### Configurar extração ferramenta

Use a extração ferramenta para extrair os dados do instância de origem.

1. Baixe as ferramenta de extração do link fornecidas a você por Adobe Systems.
1. Defina as seguintes variáveis de ambiente na ferramenta de extração:
   - Detalhes de conexão ao banco de dados MySQL existente
   - A Direcionamento ID do inquilino do seu [!DNL Adobe Commerce as a Cloud Service] instância
   - Suas credenciais do IMS, incluindo:
      - ID do cliente
      - Segredo do cliente
      - Escopos IMS
      - IMS URL- A URL base. Por exemplo, `https://ims-na1.adobelogin.com/`.
      - ID da organização de IMS

   Para escopos de IMS e outros valores, selecione seu tipo OAuth na seção Credenciais dentro do **seu projeto no** console Adobe Systems desenvolvedor[.](https://developer.adobe.com/console/) Mais informações são fornecidas no `.example.env` arquivo incluído na ferramenta de extração.

### dados do Extract

Antes de executar o ferramenta de extração, o implementador de soluções deve estabelecer um túnel SSH para o banco de dados PaaS usando:

```bash
magento-cloud tunnel:open
```

Em seguida, execute o ferramenta de extração, que irá:

1. Conecte-se ao banco de dados PaaS, analise suas schema e compare-o com o inquilino do SaaS schema detalhes.
1. Gere um plano de extração e transformação com base nos elementos schema comuns entre PaaS e SaaS.
1. Extract os dados usando o Catalog Data Management Service (CDMS).

### Carregar dados

Execute os ferramenta de dados de carregamento fornecidos pelo Adobe Systems. Essa ferramenta irá:

1. Conecte-se ao banco de dados do locatário do SaaS usando um conta de migração.
1. Gere um plano de carregamento.
1. Execute o plano, movendo dados para o banco de dados do locatário do SaaS em lotes.
1. Processe as mídia do catálogo e transfira-as para o ambiente de Direcionamento.
1. Libere o cache do SaaS Redis e invalide os índices de banco de dados do inquilino.

### Ingestão de dados de catálogo

Depois que os dados são carregados, os dados do catálogo fluem automaticamente do banco de dados do locatário do SaaS para o Serviço de catálogo.

O Serviço de catálogo compartilha esses dados com o Live Search e o Product recomendações. Nenhuma intervenção manual é necessária para este processo. Os dados ficam disponíveis em todos os serviços após a conclusão da ingestão.

### Verificação de integridade de dados

Após a migração, o CDMS realiza as seguintes verificações automáticas de integridade de dados para garantir a precisão e a completitude dos dados migrados:

**Verificação baseada em API**

Durante a verificação, o CDMS compara as respostas da REST e da API GraphQL de consultas anteriores com os registros correspondentes do Direcionamento instância. Quaisquer discrepâncias estão visíveis no status da migração.

**Verificação no nível do banco de dados**

Durante a verificação, o CDMS conta o número de registros extraídos e compara esse número com a quantidade de registros carregados.

**Verificação sob demanda (opcional)**

Você também pode acionar manualmente uma verificação abrangente de todos os registros do sistema:

>[!NOTE]
>
>Esse processo é intensivo em recursos e deve ser usado apenas em ambientes de área de segurança.

A verificação completa inclui:

- Todos os Apps a verificação baseada em API usando todas as respostas da API REST e GraphQL pré-extraídas
- Relatório detalhado de quaisquer inconsistências encontradas
