---
title: Migrar arquivos de mídia para o AEM
description: Migre os arquivos de mídia do Adobe Commerce ou de uma fonte externa para o AEM Assets DAM.
feature: CMS, Media, Integration
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# Migrar arquivos de mídia para o AEM Assets DAM

O Adobe Commerce e o Adobe Experience Manager (AEM) fornecem recursos integrados para simplificar a migração de arquivos de mídia do Commerce para o **sistema de gerenciamento de ativos digitais (DAM)** da AEM Assets. Você também pode migrar arquivos de mídia de outras fontes.

## Pré-requisitos

| Categoria | Requisito |
|----------|-------------|
| **Requisitos do sistema** | <ul><li>Ambiente do AEM as a Cloud Service provisionado com o AEM Assets</li><li>Capacidade de armazenamento suficiente</li><li>Largura de banda de rede para transferências de arquivos grandes</li></ul> |
| **Permissões e acesso necessários** | <ul><li>Acesso de administrador ao AEM Assets as a Cloud Service</li><li>Acesso ao sistema de origem onde os arquivos de mídia são armazenados (Adobe Commerce ou sistema externo)</li><li>Permissões apropriadas para acessar serviços de armazenamento na nuvem</li></ul> |
| **Conta de Armazenamento na Nuvem** | <ul><li>Conta de armazenamento AWS S3 ou Azure Blob</li><li>Configuração privada de container/bucket</li><li>Credenciais de autenticação</li></ul> |
| **Conteúdo do Source** | <ul><li>Arquivos de mídia organizados prontos para migração</li><li>Arquivos de imagem e vídeo em <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">formatos com suporte no AEM Assets</a>.</li><li>Ativos limpos e duplicados</li></li> |
| **Preparação de Metadados** | <ul><li><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Perfil de metadados do AEM Assets configurado para ativos do Commerce</a></li><li>Valores de metadados mapeados para cada ativo</li><li>Editor de arquivos CSV (por exemplo, Microsoft Excel)</li></ul> |

## Práticas recomendadas de migração

1. Prepare ativos antes da migração, removendo conteúdos não utilizados e duplicados.

1. Organize ativos logicamente por tamanho, formato ou caso de uso.

1. Considere dividir grandes migrações em lotes menores.

1. Agendar importações que consomem muitos recursos fora das horas de pico.

1. Valide o mapeamento de metadados antes da importação completa.

## Fluxo de trabalho de migração

Siga o fluxo de trabalho de migração para exportar arquivos de mídia do Adobe Commerce ou outro sistema externo e importá-los para o DAM do AEM Assets.

### Etapa 1: exportar conteúdo da fonte de dados existente

[!BADGE Somente PaaS]{type=Informative tooltip="Aplicável a projetos do Adobe Commerce na nuvem somente (infraestrutura do PaaS gerenciada pela Adobe)."}

Para os comerciantes do Adobe Commerce, o **módulo de Armazenamento remoto** pode facilitar as importações e exportações de arquivos de mídia. Esse módulo permite que as empresas armazenem e gerenciem arquivos de mídia usando serviços de armazenamento remoto, como o AWS S3. Para configurar o armazenamento remoto para sua instância do Commerce, consulte [Configurar Armazenamento Remoto](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3) no **Guia de Configuração do Commerce**.

Se você tiver arquivos de mídia armazenados fora do Adobe Commerce, carregue-os diretamente para uma das [fontes de dados](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites) compatíveis com o AEM as a Cloud Service.

### Etapa 2: criar um arquivo CSV para mapeamento de metadados

Depois de exportar os arquivos de mídia, crie um arquivo CSV para mapear esses ativos com os metadados necessários para automação. O CSV deve incluir campos do **produto**, **posição** e **mapeamento de funções**, garantindo o alinhamento com o [perfil de metadados do AEM Assets](configure-aem.md#configure-a-metadata-profile).

Para cada arquivo de mídia que você planeja migrar, forneça valores para os campos de metadados incluídos no [perfil de metadados do AEM Assets para ativos do Commerce](configure-aem.md), conforme descrito na tabela a seguir.

| Metadados | Descrição | Valor |
|-------|-------------|--------|
| assetPath | O caminho completo onde o ativo será armazenado no repositório do AEM Assets.<br><br>Use o caminho para criar subpastas para organizar ativos do Commerce, por exemplo `content/dam/commerce/<brand>/<type>`. | `/content/dam/commerce/<sub-folder>/..<filename>` |
| comércio:posições | A posição/ordem do ativo em galerias de produtos | Vários valores numéricos separados por barra vertical (consulte o arquivo csv) |
| commerce:isCommerce | Sinalizador que indica se o ativo é usado no comércio | `Yes` |
| comércio:skus | SKUs de produto associadas a este ativo | Vários valores de string separados por barra vertical (consulte o arquivo csv) |
| comércio:funções | As funções ou tipos de imagens para o ativo (por exemplo, `thumbnail`, `main image`, `swatch`) | Vários valores separados por ponto e vírgula (por exemplo, &quot;miniatura; imagem; imagem_amostra; imagem_pequena&quot;) |

+++código CSV

Use este exemplo de código CSV para criar o arquivo em um editor de código ou aplicativo de planilha, como o Microsoft Excel.

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### Etapa 3: Importação em massa do Assets para o AEM Assets

Depois de criar o arquivo de mapeamento de metadados, use a Ferramenta de importação em massa do AEM Assets para importar os ativos.

Veja a seguir uma visão geral de alto nível sobre o uso da ferramenta.

1. [Faça logon no ambiente de criação do AEM Assets as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem).

1. Na exibição Ferramentas do Experience Manager, selecione **[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**.

   ![criação no AEM Assets](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. Nas Configurações de Importação em Massa, selecione **[!UICONTROL Create]** para abrir o formulário de configuração.

   ![criação no AEM Assets](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. Defina e salve a configuração.

   Você precisará de:

   * Credenciais de autenticação para sua fonte de dados
   * A pasta de destino no AEM Assets onde os arquivos importados serão armazenados
   * Opcional. Informações sobre os tipos MIME, o tamanho do arquivo e outros parâmetros para personalizar a configuração de importação
   * O caminho para o arquivo CSV de mapeamento de metadados carregado na instância de armazenamento na nuvem.

   Para obter etapas detalhadas, consulte [Configurar a ferramenta Importação em Massa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool) no *Guia do Usuário do AEM Assets as a Cloud Service*.

1. Depois de salvar a configuração, use as ferramentas de importação em massa para testar e executar a operação de importação.

>[!MORELIKETHIS]
>
> [Demonstração de vídeo da ferramenta de importação em massa](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> > [Dicas, práticas recomendadas e limitações](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> > [Carregar ou assimilar ativos usando APIs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
