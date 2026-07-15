---
title: Configurar o AEM Assets para o Commerce Optimizer
description: Saiba como configurar a Integração do AEM Assets para  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---


# Configurar o AEM Assets para [!DNL Adobe Commerce Optimizer]

[!BADGE Somente SaaS]{type=Positive tooltip="Aplicável somente a projetos do Adobe Commerce Optimizer."}

A integração do AEM Assets para [!DNL Adobe Commerce Optimizer] permite que os comerciantes usem o AEM Assets como a solução de gerenciamento de ativos digitais centralizada para imagens de produtos. Este guia aborda a configuração específica para [!DNL Commerce Optimizer].

O diagrama a seguir é uma visão geral da sincronização de produtos entre o [!DNL Adobe Commerce Optimizer] e a integração do AEM Assets.

![Fluxo do AEM Assets para [!DNL Commerce Optimizer]](../assets/aco-asset-sync-architecture.png){width="700"}

Essa integração tem dois fluxos de evento independentes. Ambos usam o [Adobe I/O Events](https://developer.adobe.com/events/docs/) para transferir eventos para o Serviço de Integração da Assets, mas cada direção usa seu próprio provedor de eventos:

* **Do AEM Assets para o Serviço de Integração da Assets**: quando um ativo é aprovado, rejeitado ou removido, o evento é entregue ao Serviço de Integração da Assets. O serviço corresponde ativos a produtos usando o `match-by-SKU` (orientado por metadados) ou o [correspondência personalizada (App Builder)](../synchronize/custom-match.md){target=_blank} e, em seguida, envia os mapeamentos do `product-asset` para o [!DNL Commerce Optimizer], onde eles são armazenados como camadas de produto.

  >[!NOTE]
  >
  >A camada de catálogo `AEM-Assets` usada pela integração é criada automaticamente durante a integração. Não é necessário criá-lo antecipadamente. Para obter informações sobre como as camadas do catálogo funcionam e como a camada AEM-Assets se comporta, consulte [Camada AEM-Assets](../../optimizer/setup/catalog-layer.md#aem-assets-layer).

* **De [!DNL Adobe Commerce Optimizer] para o Serviço de Integração da Assets**: quando um produto é atualizado em [!DNL Commerce Optimizer], o evento é entregue ao Serviço de Integração da Assets. O serviço sincroniza todos os mapeamentos de ativos correspondentes de volta para [!DNL Commerce Optimizer].

## Limitação

A integração do [!DNL Commerce Optimizer] tem as seguintes limitações:

### Restrições relacionadas à camada

* Use uma camada dedicada para o conteúdo do AEM Assets.

  Cargas enviadas do AEM Assets preenchem uma camada de catálogo do Commerce Optimizer. Os valores nessa camada substituem os atributos do catálogo base onde os campos são fornecidos. Quando a integração omite um campo na carga, os valores correspondentes nessa camada podem ser substituídos por valores vazios. O compartilhamento de uma camada com fluxos de trabalho não relacionados do Commerce, ou a reutilização de uma camada que já armazena dados de produtos que não são da AEM e da Assets, pode causar **perda involuntária de dados** ou substituições confusas. Reserve o nome da camada (por exemplo, o **`AEM-Assets`** padrão) principalmente para a sincronização de imagens de produtos orientada pela AEM.

* A integração oferece suporte a uma origem de catálogo por locatário: uma única localidade e uma camada nomeada. No momento, não há suporte para a configuração de várias camadas ou localidades AEM-Assets para o mesmo locatário.

* Reutilizar uma camada existente ou compartilhar uma camada com fluxos de trabalho não relacionados é uma causa frequente de casos de suporte evitáveis.

### Outras restrições

* **Somente imagens**: a integração não oferece suporte a vídeo ou outros tipos de mídia neste estágio.
* **Nenhuma imagem de categoria**: a sincronização de imagem de categoria não está disponível. Imagens de categoria do AEM Assets para o Seletor de Assets (inserção da interface do usuário) não são compatíveis.
* **Nenhuma distinção entre vários sites**: a integração não trata de vários sites; uma imagem associada a um produto é mostrada da mesma forma em todos os canais e políticas.
* **Posição/ordem da imagem**: não há suporte para a posição e a ordem da imagem.
* **O produto deve existir**: se o produto não existir em [!DNL Commerce Optimizer], a camada não será criada para esse mapeamento de ativos do produto.

## Pré-requisitos

Antes de configurar a integração, verifique se você tem:

* Uma instância [!DNL Adobe Commerce Optimizer] ativa com o direito **Visuais de Produto** (inclui o Dynamic Media com recursos OpenAPI + [AEM Assets Prime](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-prime)) ou uma licença AEM Assets fornecida pelo cliente (por exemplo, **AEM Assets Ultimate**) com o Dynamic Media habilitado.
* Acesso a um ambiente do AEM Assets as a Cloud Service.
* O [!DNL Commerce Optimizer] e o AEM Assets na mesma Organização do Adobe IMS.
* Dynamic Media com OpenAPI habilitado no seu ambiente do AEM Assets (consulte [Configurar o projeto do AEM Assets](configure-aem.md#prerequisites) para ver as etapas de habilitação).

### Configurar o AEM Assets primeiro

Para oferecer suporte à integração, configure o projeto e os ambientes do AEM Assets antes de iniciar o processo para integrar a Integração do AEM Assets com o [!DNL Commerce Optimizer]. Isso inclui ativar o Dynamic Media com recursos OpenAPI e disponibilizar os esquemas de metadados, eventos e a interface do Commerce no seu projeto do AEM.

* [!BADGE Recomendado]{type=Positive} Na versão `2026.5.26309` e posterior do AEM, habilite a integração do Cloud Manager sem implantação de código. Siga [Habilitar a integração do Commerce (autoatendimento)](configure-aem.md#enable-aem-commerce-self-service).

* Em versões anteriores do AEM, implante o pacote `assets-commerce` manualmente.
Siga [Instalar o pacote assets-commerce manualmente](configure-aem.md#install-the-assets-commerce-package-manually).

>[!TIP]
>
> Verifique a versão atual do AEM no menu superior direito: **[!UICONTROL Help]** > **[!UICONTROL About AEM]**.

## Integração

>[!IMPORTANT]
>
>Antes de enviar um tíquete de suporte para habilitar a integração com o [!DNL Commerce Optimizer], conclua o processo para [Configurar o AEM Assets](#configure-aem-assets-first). O suporte requer que os ambientes e o projeto do AEM Assets sejam configurados para serem compatíveis com a integração do AEM Commerce, incluindo a implantação do pacote `assets-commerce` (ou equivalente de autoatendimento) para metadados e eventos. Abrir um tíquete antes da configuração do AEM pode atrasar a integração.

Para integrar a Integração do AEM Assets com o [!DNL Commerce Optimizer], o Suporte da Adobe deve registrar sua instância do Adobe Commerce Optimizer no Serviço de Integração da Assets e assiná-la em:

* Eventos do AEM Assets (ativo aprovado, atualizado, removido)
* [!DNL Commerce Optimizer] eventos de catálogo (produto criado, atualizado)

Para iniciar este processo, [crie um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) que inclua as seguintes informações:

* **[!DNL Adobe Commerce Optimizer]ID do Locatário** (ID da Instância) encontrada na sua URL [!DNL Commerce Optimizer] ou na interface do Commerce Cloud Manager.
* **ID de Programa e ID de Ambiente do AEM** configurados quando você [configurou o AEM Assets](#configure-aem-assets-first) para a integração.
* **Regra de correspondência**: corresponder por SKU ou [correspondência externa (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Camada**: o nome da camada do catálogo com o qual registrar o locatário (consulte **Restrições relacionadas à camada**). Especifique um nome personalizado somente se for intencional; caso contrário, o padrão **`AEM-Assets`** será usado.
* **Localidade**: a localidade de origem do catálogo na qual registrar o locatário (por exemplo, `en-US`). Essa localidade deve corresponder à localidade usada na exibição do catálogo e nos dados do catálogo de produtos.

### Configurar a visualização do catálogo

Depois que o locatário do [!DNL Commerce Optimizer] for registrado, configure sua exibição de catálogo para que a loja e as APIs apresentem dados de imagem orientados pela AEM:

* **Selecione a origem do catálogo (localidade)** — Selecione a mesma localidade especificada no tíquete de suporte (por exemplo, **`en-US`**). A integração registra um local por locatário; uma incompatibilidade impede que imagens sincronizadas apareçam na exibição de catálogo desejada.
* **Atribuir a camada do catálogo** — Atribua a camada **`AEM-Assets`** (ou o nome de camada personalizado do tíquete) a essa exibição de catálogo.

Se a localidade ou camada não for atribuída corretamente, os dados de imagem **não aparecerão** ou se comportarão inesperadamente, mesmo que a sincronização tenha êxito no upstream.

## Sincronização

Após configurada, a integração sincroniza mapeamentos de `product-asset` automaticamente.

Consulte [Correspondência automática personalizada](../synchronize/custom-match.md) para obter mais informações.

### Exemplo de fluxo de trabalho Corresponder por SKU

Um fluxo típico ao adicionar um ativo existente a um novo produto:

1. Crie o produto em [!DNL Commerce Optimizer] (via API ou assimilação de dados). Inicialmente, o produto pode existir sem imagens.

1. No AEM Assets, abra o ativo que deseja mapear para o produto.

1. Adicione o SKU do produto aos metadados do **commerce:skus** e atribua funções de imagem (por exemplo, `thumbnail`, `image`).

1. Aprovar o ativo para entrega. Isso aciona o evento que o serviço de integração do Assets processa.

1. O Serviço de Integração da Assets envia o mapeamento de imagem do produto para [!DNL Commerce Optimizer]. O produto em [!DNL Commerce Optimizer] é atualizado com as imagens do ativo.

1. Verifique se a imagem está visível. Aguarde alguns minutos para que a sincronização seja concluída e, em seguida, verifique o produto na interface do usuário do [!DNL Commerce Optimizer] ou consulte as APIs da loja para confirmar se a imagem foi retornada.

## Manuseio de função da imagem

Quando um produto tem vários ativos usando a mesma função de imagem (por exemplo, dois ativos com a função `thumbnail`), a integração garante que apenas um ativo mantenha essa função para evitar funções duplicadas na camada [!DNL Commerce Optimizer] e comportamento inesperado da loja.

**Comportamento:** quando uma atualização é enviada do AEM Assets, o ativo atualizado mais recentemente recebe a função de imagem (por exemplo, `thumbnail`), e a função é removida do ativo anterior que o tinha. Isso impede que funções de imagem duplicadas apareçam na loja.

## Veja mais aqui

* [Visuais do produto](../../optimizer/setup/product-visuals.md)
* [Configurar o projeto do AEM Assets](configure-aem.md)
* [Correspondência automática personalizada](../synchronize/custom-match.md)
* [Visão geral da integração do AEM Assets](../overview.md)
