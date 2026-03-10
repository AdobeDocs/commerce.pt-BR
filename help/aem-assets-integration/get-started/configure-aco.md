---
title: Configurar o AEM Assets para o Commerce Optimizer
description: Saiba como configurar a Integração do AEM Assets para  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 7f0970648663331fea2af19b981c4fd3b3aedcaa
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---


# Configurar o AEM Assets para [!DNL Adobe Commerce Optimizer]

[!BADGE Somente SaaS]{type=Positive tooltip="Aplicável somente a projetos do Adobe Commerce Optimizer."}

A integração do AEM Assets para [!DNL Adobe Commerce Optimizer] permite que os comerciantes usem o AEM Assets como a solução de gerenciamento de ativos digitais centralizada para imagens de produtos. Este guia aborda a configuração específica para [!DNL Commerce Optimizer].

Ao contrário do Adobe Commerce (PaaS) ou Adobe Commerce as a Cloud Service (ACCS), o [!DNL Commerce Optimizer] não tem uma interface de configuração de administrador. Para habilitar a integração, crie um tíquete de suporte com seus detalhes do [!DNL Adobe Commerce Optimizer] e do AEM Assets. O Suporte da Adobe configura a integração e registra seu locatário no Serviço de integração da Assets.

O diagrama a seguir é uma visão geral da sincronização de produtos entre o [!DNL Adobe Commerce Optimizer] e a integração do AEM Assets.

![Fluxo do AEM Assets para [!DNL Commerce Optimizer]](../assets/aco-asset-sync-architecture.png){width="700"}

Essa integração tem dois fluxos principais:

* **Do AEM Assets**: quando um ativo é aprovado, rejeitado ou removido, o evento flui pelo Pipeline do Adobe para o Serviço de Integração do Assets. O serviço corresponde ativos a produtos usando o `match-by-SKU` (orientado por metadados) ou o [correspondência personalizada (App Builder)](../synchronize/custom-match.md){target=_blank} e, em seguida, envia os mapeamentos do `product-asset` para a Commerce Optimizer, onde eles são armazenados como camadas de produto.

* **De[!DNL Adobe Commerce Optimizer]**: quando um produto é atualizado em [!DNL Commerce Optimizer], o evento flui pelo Pipeline do Adobe para o Serviço de Integração da Assets. O serviço sincroniza todos os mapeamentos de ativos correspondentes de volta para o [!DNL Adobe Commerce Optimizer].

## Pré-requisitos

Antes de configurar a integração, verifique se você tem:

* Uma instância [!DNL Adobe Commerce Optimizer] ativa com direito a Visuais de Produto ou qualquer licença do AEM Assets com Dynamic Media.
* Acesso a um ambiente do AEM Assets as a Cloud Service.
* O [!DNL Commerce Optimizer] e o AEM Assets na mesma Organização do Adobe IMS.
* Dynamic Media com OpenAPI ativada no ambiente do AEM Assets.

## Integração

Para integrar a Integração do AEM Assets com o [!DNL Commerce Optimizer], você deve [Criar um tíquete de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

O Suporte da Adobe usa as informações no tíquete para registrar o locatário no Serviço de integração da Assets e configurar a integração.

Inclua as seguintes informações no tíquete de suporte:

* **[!DNL Adobe Commerce Optimizer]ID do Locatário** (ID da Instância) encontrada na sua URL [!DNL Commerce Optimizer] ou na interface do Commerce Cloud Manager.
* **ID do Programa AEM**.
* **ID de Ambiente AEM**.
* **Regra de correspondência**: corresponder por SKU ou [correspondência externa (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Camada**: o nome da camada de catálogo com o qual registrar o locatário. Especifique um nome personalizado, se necessário. Caso contrário, o padrão `AEM-Assets` será usado.
* **Localidade**: a localidade de origem do catálogo na qual registrar o locatário (por exemplo, `en-US`).

>[!IMPORTANT]
>
> A integração oferece suporte a uma origem por locatário, que é a combinação de uma localidade e uma camada.

Depois que o Suporte da Adobe processar seu tíquete, a integração será configurada e seu locatário será registrado no Serviço de integração da Assets.

Quando a integração estiver concluída:

1. **Registro com o Assets Integration Service**: seu locatário do [!DNL Commerce Optimizer] está registrado com o Assets Integration Service usando a ID de Locatário do [!DNL Adobe Commerce Optimizer], a ID do Programa AEM, a ID de Ambiente AEM e o locatário.

1. **Assinatura de evento**: o Serviço de Integração da Assets assina:

   * Eventos do AEM Assets (ativo aprovado, atualizado, removido)
   * [!DNL Commerce Optimizer] eventos de catálogo (produto criado, atualizado)

### Limitação

A integração do [!DNL Commerce Optimizer] tem as seguintes limitações:

* **Camada única por comerciante** — A Integração do AEM Assets oferece suporte a uma camada AEM-Assets por comerciante (uma origem por locatário). No momento, não há suporte para a configuração de várias camadas por comerciante.
* **Somente imagens**—A integração não oferece suporte a vídeo ou outros tipos de mídia.
* **Nenhuma imagem de categoria**—A sincronização de imagem de categoria não está disponível. Imagens de categoria do AEM Assets para o Seletor de Assets (inserção da interface do usuário) não são compatíveis.
* **Nenhuma distinção entre vários sites**—A integração não trata de vários sites; uma imagem associada a um produto é mostrada da mesma forma em todos os canais e políticas.
* **Posição/ordem da imagem**—A posição e a ordem da imagem não são suportadas.
* **O produto deve existir**—Se o produto não existir em [!DNL Commerce Optimizer], a camada não será criada para esse mapeamento de ativos do produto.
* **Substituição de campo de camada** — Os valores em uma camada substituem o catálogo base. Se um campo não for enviado na carga da camada, ele poderá ser substituído por um valor vazio. Use uma camada dedicada para conteúdo do AEM Assets; a reutilização de uma camada existente para outros fins pode resultar em perda não intencional de dados.

### Configurar o AEM Assets

O processo de instalação e configuração do AEM Assets para [!DNL Commerce Optimizer] é o mesmo do Adobe Commerce as a Cloud Service. Consulte [Configurar o projeto do AEM Assets para oferecer suporte aos metadados do Commerce](configure-aem.md) para obter as etapas completas.

Verifique se o ambiente do AEM Assets está pronto:

1. **Configuração do AEM Assets**: configurar o perfil de metadados do Commerce. Consulte [Configurar um perfil de metadados](configure-aem.md#configure-a-metadata-profile).

1. **Habilitação do Dynamic Media**: verifique se o Dynamic Media com recursos OpenAPI está habilitado no seu ambiente do AEM Assets.

## Configurar AEM Assets

Para habilitar a sincronização de ativos de produtos, configure o ambiente do AEM Assets.

### Etapa 1: Habilitar o Dynamic Media com OpenAPI

O Dynamic Media com OpenAPI deve estar ativado no ambiente do AEM Assets. As Visualizações de produto e as novas licenças do AEM Assets permitem que você as ative de maneira automatizada por meio do Cloud Manager. Licenças mais antigas da AEM Assets exigem o Suporte da Adobe para serem ativadas. Consulte [Configurar o projeto do AEM Assets](configure-aem.md#prerequisites) para ver as etapas de habilitação.

### Etapa 2: Opcional. Configurar perfil de metadados do Commerce

Configure o perfil de metadados no AEM Assets para armazenar metadados específicos do Commerce.

Consulte [Configurar um perfil de metadados](configure-aem.md#step-2-optional-configure-a-metadata-profile) para obter instruções detalhadas.

### Etapa 3: Aplicar metadados a ativos

Adicione metadados do Commerce às imagens do produto no AEM Assets.

Consulte o [conteúdo do pacote do AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents) para definições de campo e [Configurar um perfil de metadados](configure-aem.md#step-2-optional-configure-a-metadata-profile) para as etapas de instalação.

O ativo deve estar em um status **aprovado** para que a sincronização de dados seja acionada. Salvar metadados sozinho não aciona o evento.

>[!CAUTION]
>
> Atribua a camada `AEM-Assets` à sua [exibição de catálogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view). Se a camada não for atribuída, os dados da imagem do produto poderão ser substituídos inesperadamente.

## Sincronização

Após configurada, a integração sincroniza mapeamentos de `product-asset` automaticamente.

Consulte [Correspondência automática personalizada](../synchronize/custom-match.md) para obter mais informações.

### Exemplo de fluxo de trabalho Corresponder por SKU

Um fluxo típico ao adicionar um ativo existente a um novo produto:

1. Crie o produto em [!DNL Commerce Optimizer] (via API ou assimilação de dados). Inicialmente, o produto pode existir sem imagens.

1. No AEM Assets, abra o ativo que deseja mapear para o produto.

1. Adicione o SKU do produto aos metadados do **commerce:skus** e atribua funções de imagem (por exemplo, `thumbnail`, `image`).

1. Aprovar o ativo para entrega. Isso aciona o evento que o Assets Integration Service processa.

1. O Serviço de Integração da Assets envia o mapeamento de imagem do produto para [!DNL Commerce Optimizer]. O produto em [!DNL Commerce Optimizer] é atualizado com as imagens do ativo.

1. Verifique se a imagem está visível. Aguarde a conclusão da sincronização (normalmente dentro de alguns minutos) e verifique o produto na interface do usuário do [!DNL Commerce Optimizer] (por exemplo, Sincronização de Dados ou exibição de catálogo) ou consulte as APIs da loja (Serviço de Catálogo, Live Search, API da GraphQL da Loja) para confirmar se a imagem foi retornada.

## Manuseio de função da imagem

Quando um produto tem vários ativos usando a mesma função de imagem (por exemplo, dois ativos com a função `thumbnail`), a integração garante que apenas um ativo mantenha essa função para evitar funções duplicadas na camada [!DNL Commerce Optimizer] e comportamento inesperado da loja.

**Comportamento:** quando uma atualização é enviada do AEM Assets, o ativo atualizado mais recentemente recebe a função de imagem (por exemplo, `thumbnail`), e a função é removida do ativo anterior que o tinha. Isso impede que funções de imagem duplicadas apareçam na loja.

## Veja mais aqui

* [Visuais do produto](../../optimizer/setup/product-visuals.md)
* [Configurar o projeto do AEM Assets](configure-aem.md)
* [Correspondência automática personalizada](../synchronize/custom-match.md)
* [Visão geral da integração do AEM Assets](../overview.md)
