---
title: Ferramenta Migração de dados em massa
description: Saiba como usar a Ferramenta de migração de dados em massa para migrar dados da sua instância existente do Adobe Commerce na nuvem para o  [!DNL Adobe Commerce as a Cloud Service].
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
role: Architect
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: 131d3bdb7e6ef2622236ddf08f306639396d6ffa
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Ferramenta de migração de dados em massa

A ferramenta de migração de dados em massa segue uma arquitetura distribuída que permite a migração de dados segura e eficiente de PaaS para ambientes SaaS. Essa ferramenta foi projetada para que os implementadores de soluções migrem dados de uma instância existente do Adobe Commerce na nuvem (PaaS) para [!DNL Adobe Commerce as a Cloud Service] (SaaS). Para obter mais informações sobre o processo de migração, consulte a [Visão geral da migração](./overview.md).

>[!NOTE]
>
>A ferramenta de migração de dados em massa é compatível apenas com a migração de dados comerciais principais de terceiros. No momento, não há suporte para a migração de dados personalizada.

A imagem a seguir detalha a arquitetura e os principais componentes para usar a ferramenta Migração de dados em massa.

![Arquitetura da Ferramenta de Migração de Dados em Massa](../assets/bulk-data-diagram.png)

## Fluxo de trabalho de migração

O fluxo de trabalho de migração de dados em massa consiste nas seguintes etapas:

1. Configure um novo ambiente para sua migração.
1. Copie os dados do sistema antigo.
1. Mova seus dados para o novo sistema.
1. Disponibilize seu catálogo de produtos no novo sistema.
1. Confirme se os dados foram migrados corretamente.

As seções a seguir descrevem essas etapas em detalhes.

## Acessar a ferramenta de migração de dados em massa

A disponibilidade da ferramenta de migração de dados em massa é a seguinte:

- **T4 2025** - Para acessar a ferramenta de migração de dados em massa, envie um tíquete de suporte.
- **T4 2025** - A ferramenta de migração de dados em massa estará disponível publicamente e poderá ser acessada nesta página.

## Criar ambiente de destino

O implementador de soluções (SI) cria um ambiente de destino para a migração. Esse ambiente é usado para armazenar os dados migrados da instância de origem.

Primeiro, [crie uma nova instância [!DNL Adobe Commerce as a Cloud Service] (SaaS)](../getting-started.md#create-an-instance).

### Configurar ferramenta de extração

A ferramenta de extração é usada para extrair dados da instância de origem.

1. Baixe a ferramenta de extração no link fornecido pelo Adobe.
1. Defina as seguintes variáveis de ambiente na ferramenta de extração:
   - Detalhes da conexão com o banco de dados MySQL existente
   - A ID do locatário de destino para sua instância [!DNL Adobe Commerce as a Cloud Service]
   - Suas credenciais IMS, incluindo:
      - ID do cliente
      - Client secret
      - Escopos IMS
      - URL IMS - O URL de base. Por exemplo, `https://ims-na1.adobelogin.com/`.
      - IMS organization ID

   Para escopos IMS e outros valores, selecione seu tipo OAuth na seção **Credenciais** dentro do projeto na [Adobe Developer Console](https://developer.adobe.com/console/). Mais informações são fornecidas no arquivo `.example.env` incluído com a ferramenta de extração.

### Extrair dados

Antes de executar a ferramenta de extração, o implementador da solução deve estabelecer um túnel SSH para o banco de dados PaaS usando:

```bash
magento-cloud tunnel:open
```

Em seguida, execute a ferramenta de extração, que:

1. Conecte-se ao banco de dados PaaS, analise seu esquema e compare-o com os detalhes do esquema do locatário SaaS.
1. Gerar um plano de extração e transformação com base nos elementos de esquema comuns entre PaaS e SaaS.
1. Extraia os dados usando o Serviço de gerenciamento de dados de catálogo (CDMS).

### Carregar dados

Execute a ferramenta carregar dados fornecida pelo Adobe. Essa ferramenta irá:

1. Conecte-se ao banco de dados de locatários SaaS usando uma conta de migração.
1. Gerar um plano de carregamento.
1. Execute o plano, movendo dados para o banco de dados de locatários SaaS em lotes.
1. Processe a mídia do catálogo e transfira-a para o ambiente de destino.
1. Libera o cache SaaS Redis e invalida os índices de banco de dados do locatário.

### Assimilação de dados do catálogo

Depois que os dados são carregados, os dados do catálogo fluem automaticamente do banco de dados do locatário SaaS para o Serviço de catálogo.

O Serviço de catálogo compartilha esses dados com o Live Search e as Recomendações de produto. Nenhuma intervenção manual é necessária para esse processo. Os dados estarão disponíveis em todos os serviços quando a assimilação for concluída.

### Verificação da integridade dos dados

Após a migração, o CDMS executa as seguintes verificações automáticas de integridade de dados para garantir a precisão e a integridade dos dados migrados:

**Verificação baseada em API**

Durante a verificação, o CDMS compara as respostas da API REST e GraphQL de consultas executadas anteriormente com os registros correspondentes da instância de destino. Todas as discrepâncias são visíveis no status da migração.

**Verificação no nível do banco de dados**

Durante a verificação, o CDMS conta o número de registros extraídos e compara esse número à quantidade de registros carregados.

**Verificação sob demanda (opcional)**

Você também pode acionar manualmente a verificação abrangente de todos os registros do sistema:

>[!NOTE]
>
>Esse processo consome muitos recursos e só deve ser usado em ambientes de sandbox.

A verificação completa inclui:

- Verificação completa baseada em API usando todas as respostas pré-extraídas da REST e da API do GraphQL
- Relatório detalhado de todas as inconsistências encontradas
