---
title: Configurar o AEM Assets para o Commerce Optimizer
description: Saiba como configurar a Integração do AEM Assets para  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 2cc7b70a6923687c74fe3f4b88448eaada6d16af
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---


# Configurar o AEM Assets para [!DNL Adobe Commerce Optimizer]

[!BADGE Somente SaaS]{type=Positive tooltip="Aplicável somente a projetos do Adobe Commerce Optimizer."}

A integração do AEM Assets para [!DNL Adobe Commerce Optimizer] permite que os comerciantes usem o AEM Assets como a solução de gerenciamento de ativos digitais centralizada para imagens de produtos. Este guia aborda a configuração específica para [!DNL Commerce Optimizer].

Ao contrário do Adobe Commerce (PaaS) ou [!DNL Adobe Commerce as a Cloud Service], [!DNL Commerce Optimizer] não tem uma interface de configuração de administrador. Para habilitar a integração, crie um tíquete de suporte com seus detalhes do [!DNL Adobe Commerce Optimizer] e do AEM Assets. O Suporte da Adobe configura a integração e registra seu locatário no Serviço de integração da Assets.

**Prepare o AEM Assets antes de enviar o tíquete.** O registro do locatário presume que o lado do AEM é utilizável para o Commerce. Por exemplo, após implantar o pacote `assets-commerce` do AEM Commerce, os metadados e eventos funcionam conforme explicado. **Abrir um tíquete antes da configuração do AEM pode atrasar a integração.**

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
* Dynamic Media com OpenAPI habilitado no seu ambiente do AEM Assets (consulte [Configurar o projeto do AEM Assets](configure-aem.md#prerequisites) para ver as etapas de habilitação).

## Configurar o AEM Assets primeiro

Conclua as etapas do AEM Assets **antes** para [abrir um tíquete de suporte](#onboarding) para registro de locatário. O padrão de instalação corresponde ao Adobe Commerce as a Cloud Service — consulte [Configurar o projeto do AEM Assets para oferecer suporte aos metadados do Commerce](configure-aem.md).

### Etapa 1: implantar o pacote do AEM Commerce

Instale e implante o pacote `assets-commerce` em seu projeto do AEM para que os esquemas de metadados, os eventos e a interface do usuário do Commerce estejam disponíveis.

Conclua o procedimento completo em [Instalar o `assets-commerce` pacote](configure-aem.md#step-1-install-the-assets-commerce-package). Antes de abrir um tíquete de suporte, siga estas etapas:

1. Clonar o repositório Git do Cloud Manager e copiar o [código do repositório Commerce do AEM Assets](https://github.com/ankumalh/assets-commerce) no projeto.

1. Em todos os arquivos `filter.xml` e `pom.xml` do seu projeto, substitua todas as ocorrências de &lt;my-app> pelo nome do seu aplicativo.

1. Confirme, envie, execute o pipeline de implantação e valide se a guia **[!UICONTROL Commerce]** aparece nas propriedades do ativo.

Consulte [Instalar o pacote `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package) para obter capturas de tela, etapas do pipeline e soluções de problemas do Cloud Manager se a guia **[!UICONTROL Commerce]** estiver ausente.

### Etapa 2: Habilitar o Dynamic Media com OpenAPI

O Dynamic Media com recursos OpenAPI deve estar ativado em seu ambiente do AEM Assets. Os caminhos de autoatendimento (por exemplo, Cloud Manager para Visuais de Produto) e as rotas de Suporte da Adobe são descritos em [Configurar o projeto do AEM Assets](configure-aem.md#prerequisites).

### Etapa 3: Aplicar metadados do Commerce e aprovar ativos

Adicione metadados do Commerce às imagens do produto no AEM Assets. Para obter definições de campo, consulte [conteúdo do pacote do AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents).

O ativo deve estar em um status **aprovado** para que a sincronização de dados seja acionada. Salvar metadados sozinho não aciona o evento.

### Etapa 4: opcional — configurar um perfil de metadados do Commerce

Se você optar por usar perfis de metadados do AEM para simplificar a criação, configure-os **depois** que o pacote for implantado e sua equipe entender os campos obrigatórios do Commerce — mesmo padrão opcional que **Configurar o projeto do AEM Assets**.

Consulte [Configurar um perfil de metadados](configure-aem.md#step-2-optional-configure-a-metadata-profile).

## Limitação

A integração do [!DNL Commerce Optimizer] tem as seguintes limitações:

### Restrições relacionadas à camada

Leia esta seção **antes** e escolha um nome de camada de catálogo no tíquete de suporte. Escolher ou compartilhar camadas sem esse contexto é uma causa frequente de casos de suporte evitáveis.

**Use uma camada dedicada para o conteúdo do AEM Assets.** Cargas enviadas do AEM Assets preenchem um catálogo do Commerce Optimizer **layer**. Valores nessa camada **substituem** atributos de catálogo base onde os campos são fornecidos. Quando a integração omite um campo na carga, os valores correspondentes nessa camada podem ser substituídos por valores vazios. O compartilhamento de uma camada com fluxos de trabalho não relacionados do Commerce, ou a reutilização de uma camada que já armazena dados de produtos que não são da AEM e da Assets, pode causar **perda involuntária de dados** ou substituições confusas. Planeje a opção de camada **antes** de abrir o tíquete de suporte e reserve esse nome de camada (por exemplo, o **`AEM-Assets`** padrão) principalmente para a sincronização de imagem de produto orientada pela AEM.

>[!IMPORTANT]
>
>A integração oferece suporte a **uma origem de catálogo por locatário**: uma única localidade e **uma camada nomeada**. No momento, não há suporte para a configuração de várias camadas ou localidades AEM-Assets para o mesmo locatário.

### Outras restrições

* **Somente imagens**: a integração não oferece suporte a vídeo ou outros tipos de mídia neste estágio.
* **Nenhuma imagem de categoria**: a sincronização de imagem de categoria não está disponível. Imagens de categoria do AEM Assets para o Seletor de Assets (inserção da interface do usuário) não são compatíveis.
* **Nenhuma distinção entre vários sites**: a integração não trata de vários sites; uma imagem associada a um produto é mostrada da mesma forma em todos os canais e políticas.
* **Posição/ordem da imagem**: não há suporte para a posição e a ordem da imagem.
* **O produto deve existir**: se o produto não existir em [!DNL Commerce Optimizer], a camada não será criada para esse mapeamento de ativos do produto.

## Integração

Para integrar a Integração do AEM Assets com o [!DNL Commerce Optimizer], você deve [Criar um tíquete de suporte](https://experienceleague.adobe.com/pt-br/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

O Suporte da Adobe usa as informações no tíquete para registrar o locatário no Serviço de integração da Assets e configurar a integração.

Verifique se você concluiu [Configurar AEM Assets primeiro](#configure-aem-assets-first) antes de enviar o tíquete.

Inclua as seguintes informações no tíquete de suporte:

* **[!DNL Adobe Commerce Optimizer]ID do Locatário** (ID da Instância) encontrada na sua URL [!DNL Commerce Optimizer] ou na interface do Commerce Cloud Manager.
* **ID do Programa AEM**.
* **ID de Ambiente AEM**.
* **Regra de correspondência**: corresponder por SKU ou [correspondência externa (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Camada**: o nome da camada do catálogo com o qual registrar o locatário (consulte **Restrições relacionadas à camada**). Especifique um nome personalizado somente se for intencional; caso contrário, o padrão **`AEM-Assets`** será usado.
* **Localidade**: a localidade de origem do catálogo na qual registrar o locatário (por exemplo, `en-US`). Deve corresponder à localidade utilizada na visualização do catálogo e nos dados do catálogo de produtos.

Depois que o Suporte da Adobe processar seu tíquete, a integração será configurada e seu locatário será registrado no Serviço de integração da Assets.

Quando a integração estiver concluída:

1. **Registro com o Assets Integration Service**: seu locatário do [!DNL Commerce Optimizer] está registrado com o Assets Integration Service usando sua ID de Locatário do [!DNL Adobe Commerce Optimizer], ID do Programa AEM, ID do Ambiente AEM, regra de correspondência, localidade e nome da camada fornecidos no tíquete.

1. **Assinatura de evento**: o Serviço de Integração da Assets assina:

   * Eventos do AEM Assets (ativo aprovado, atualizado, removido)
   * [!DNL Commerce Optimizer] eventos de catálogo (produto criado, atualizado)

Configure sua [visualização de catálogo](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/setup/catalog-view) para que as vitrines e APIs apresentem dados de imagem orientados pela AEM:

* **Origem do catálogo (localidade)** — Selecione a mesma localidade especificada no seu tíquete de suporte (por exemplo, **`en-US`**). A integração registra um local por locatário; uma incompatibilidade impede que imagens sincronizadas apareçam na exibição de catálogo desejada.
* **Camada do catálogo** — Atribua a camada **`AEM-Assets`** (ou o nome de camada personalizado do tíquete) a essa exibição do catálogo.

Se a localidade ou camada não for atribuída corretamente, os dados da imagem podem **não aparecer** ou podem se comportar inesperadamente, mesmo que a sincronização tenha êxito no upstream.

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
