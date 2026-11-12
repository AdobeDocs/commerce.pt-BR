---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%
---
As camadas de catálogo permitem modificar os dados do produto sem alterar os dados de origem originais. As camadas modificam atributos do produto, como nome, descrição, imagens, links e metadados, criando uma camada na parte superior do catálogo base. Os dados originais do produto permanecem intactos, permitindo personalizar produtos com segurança e reverter alterações a qualquer momento.

![Camadas do catálogo](/help/assets/ccdm-shared/setup/catalog-layers.png)

## Acessar o espaço de trabalho de exibições do Catálogo

Você gerencia camadas de catálogo no espaço de trabalho *Exibições de catálogo* selecionando uma exibição de catálogo. A forma como você abre o espaço de trabalho depende do produto usado:

- **Administrador do Adobe Commerce** (Adobe Commerce as a Cloud Service)—Selecione *Catálogo* > **Exibições de catálogo**.
- **Adobe Commerce Optimizer Studio**—Selecione *Configuração de armazenamento* > **Exibições de catálogo**.

## Como as camadas de catálogo funcionam

Quando um cliente visualiza sua loja, o sistema combina os dados do catálogo base com as camadas do catálogo ativo para exibir as informações finais do produto. O processo funciona da seguinte maneira:

1. **Aplicativo de camada** — Quando uma solicitação é feita com uma ID de canal e uma ID de ambiente, o serviço de armazenamento recupera a exibição de catálogo relevante.

1. **Mesclagem de dados** — O sistema aplica camadas de catálogo aos dados do produto com base na ordem de prioridade das camadas.

1. **Tratamento de campo**—Tipos de campo diferentes são processados de forma diferente:

   * **Substituir campos** — Campos de texto como nome, descrição e metatítulos são substituídos por valores de camada, e a camada de prioridade mais alta tem precedência.
   * **Mesclar campos** — Campos de matriz como imagens, links e atributos são combinados de várias camadas, fornecendo uma resposta unificada.

1. **Resolução de prioridade** — O campo de ordem determina qual camada tem prioridade. Quando várias camadas modificam o mesmo campo, a camada com o número de ordem mais alto tem prioridade mais alta (por exemplo, a ordem 10 é a mais alta).

## Casos de uso da camada de catálogo

As camadas de catálogo geralmente são usadas para:

* **Otimização de SEO**—Substitua os metatítulos e descrições do produto com base nas recomendações de IA do [Sites Optimizer](../manage-results/opportunities.md).
* **Campanhas sazonais** — Atualize temporariamente nomes de produtos, descrições ou imagens para promoções sem alterar os dados de origem.
* **Personalização regional**—Exiba informações de produtos diferentes com base na localização geográfica ou no idioma.
* **Teste A/B**—Teste diferentes apresentações de produtos para otimizar as taxas de conversão.
* **Gerenciamento de várias marcas** — Personalize atributos de produto para diferentes exibições do catálogo de marcas.
* **Visualizações de Produto**—Aplique imagens de produto do AEM Assets como uma camada sobre o catálogo base.

## Camada AEM-Assets

Essa camada contém imagens de produtos sincronizadas do AEM Assets. Como outras camadas de catálogo, ele é preenchido por meio da [API de Camadas de Produto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}. O Serviço de integração do Assets transforma os metadados de ativos do AEM e os URLs de entrega no formato da API e envia os dados automaticamente quando os ativos são aprovados no AEM Assets.

A integração oferece suporte a uma origem por locatário (uma localidade + uma camada).

### Como a camada AEM-Assets funciona

1. **Criação automática**: a camada é criada quando a Integração do AEM Assets é configurada para sua instância.

1. **Sincronização de imagem**: quando os ativos são aprovados no AEM Assets, o Serviço de Integração da Assets transforma os dados de ativos e atualiza a camada `AEM-Assets` por meio da API de Camadas de Produto.

1. **Atribuição de camada**: atribua a camada `AEM-Assets` às exibições de catálogo nas quais você deseja que as imagens do AEM Assets apareçam.

### Atribuir a camada AEM-Assets a uma exibição de catálogo

>[!CAUTION]
>
> Atribua a camada AEM-Assets à visualização do catálogo. Se a camada não for atribuída, os dados da imagem do produto serão substituídos inesperadamente.

Para exibir imagens do AEM Assets em sua loja:

1. No espaço de trabalho Exibições de catálogo, selecione a exibição de catálogo à qual deseja aplicar a camada.

1. Na seção de camadas do catálogo, localize a camada **AEM-Assets**.

1. Para ativar a camada para esta exibição de catálogo, ative-a.

1. Clique em **[!UICONTROL Save]** para aplicar as alterações.

Depois de atribuídas, as APIs dos Serviços de merchandising e da GraphQL da loja retornam as imagens base do catálogo e as imagens da AEM Assets para os produtos.

## Adicionar uma camada de catálogo por meio da assimilação de dados

É possível adicionar camadas de catálogo aos seus produtos durante o processo de assimilação de dados. Esse método é ideal para operações em massa ou fluxos de trabalho automatizados. As camadas de catálogo são importadas usando a API de assimilação, mas a [definição da ordem](#manage-layer-priorities) das camadas é feita usando a interface.

**Pré-requisitos:**

* Credenciais da API com permissão para acessar o serviço de assimilação de dados
* SKUs do produto que já existem no catálogo base

**Etapas:**

1. Prepare os dados da camada no formato necessário com os atributos do produto que você deseja modificar.

1. Use o endpoint da API de camadas de produto para assimilar os dados da camada.

1. Verifique se a camada foi assimilada com êxito verificando a configuração de exibição do catálogo.

Para obter especificações detalhadas de API e exemplos de carga, consulte [Camadas de produto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank} na documentação do desenvolvedor.

## Adicionar uma camada de catálogo manualmente na interface

A interface de exibição de catálogo permite criar e gerenciar camadas manualmente, o que é particularmente útil para integrações como o Sites Optimizer que geram recomendações alimentadas por IA. Para operações de camada em massa, use o método de API de assimilação de dados [descrito acima](#add-a-catalog-layer-via-data-ingestion).

Se uma camada do Sites Optimizer não existir na visualização de catálogo, o recurso de correção automática no Sites Optimizer criará automaticamente uma camada e a atribuirá à prioridade mais alta (número mais alto). Se você excluir essa camada, ela será recriada na próxima vez que o recurso de correção automática no Sites Optimizer for executado e mudar as camadas existentes para números de ordem mais baixos. Se a camada do Sites Optimizer já existir em um número de pedido diferente, o recurso de correção automática não alterará sua prioridade.

**Para criar uma camada manual:**

1. No espaço de trabalho **[!UICONTROL Catalog views]**, selecione a exibição de catálogo à qual deseja aplicar a camada.

1. Na seção camadas do catálogo, clique em **Adicionar camada do catálogo**.

1. Configure as propriedades da camada:

   * **Nome da camada** — Digite um nome descritivo para identificar a finalidade da camada.
   * **Produtos**—Selecione os produtos aos quais esta camada se aplica.
   * **Atributos** — Escolha quais atributos de produto modificar (nome, descrição, imagens, metatags e assim por diante).
   * **Valores** — Insira os novos valores para cada atributo selecionado.

1. Clique em **[!UICONTROL Save]** para criar a camada.

A nova camada é adicionada à visualização do catálogo e é automaticamente atribuída ao próximo número de pedido disponível.

## Visualizar efeitos de camada


Antes de ativar camadas ou alterar prioridades, é possível visualizar como elas afetam os dados do produto.

**Para visualizar as alterações da camada:**

1. No espaço de trabalho **[!UICONTROL Catalog views]**, selecione a exibição de catálogo com as camadas que deseja visualizar.

1. Na seção camadas do catálogo, selecione um produto específico ou use a função de visualização.

1. Revise os dados do produto combinados que mostram como as camadas modificam os valores do catálogo base.

1. Faça ajustes no conteúdo da camada ou na ordem de prioridade, conforme necessário.

## Gerenciar ativação e exclusão de camadas

É possível ativar ou desativar camadas de catálogo sem excluí-las, permitindo que você controle quando personalizações específicas são aplicadas.

**Para ativar ou desativar uma camada:**

1. No espaço de trabalho **[!UICONTROL Catalog views]**, selecione a exibição de catálogo que contém a camada.

1. Na seção camadas do catálogo, localize a camada que deseja alternar.

1. Clique no botão de ativação para ativar ou desativar a camada.

   * **Ativo** — A camada é aplicada aos dados do produto.
   * **Inativo** — A camada é preservada, mas não aplicada aos dados do produto.

1. A alteração entrará em vigor imediatamente na loja.

**Para excluir uma camada:**

Use a API de assimilação de dados para [excluir uma camada de catálogo](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers){target=_blank}.

## Gerenciar prioridades de camada

A ordem em que as camadas são aplicadas determina quais valores aparecem na loja quando várias camadas modificam o mesmo atributo de produto. O gerenciamento de prioridades garante que os dados corretos sejam exibidos.

**Noções básicas sobre a ordem de prioridade:**

* A cada camada é atribuído um número de ordem (1, 2, 3 e assim por diante)
* Números mais altos indicam maior prioridade e substituem todas as outras camadas
* Quando várias camadas modificam o mesmo campo, a camada com o número de ordem mais alto tem prioridade
* A prioridade se aplica somente a campos de substituição (nome, descrição, metatags)
* Campos de mesclagem (imagens, links, atributos) combinam dados de todas as camadas

**Para reordenar as prioridades de camada:**

1. No espaço de trabalho **[!UICONTROL Catalog views]**, selecione a exibição de catálogo que contém as camadas que você deseja reordenar.

1. Na seção camadas do catálogo, localize a camada que deseja mover.

1. Arraste e solte a camada para alterar sua posição ou use os controles de reordenação.

1. O sistema atualiza automaticamente os números dos pedidos com base na nova sequência.

1. Clique em **[!UICONTROL Save]** para aplicar a nova ordem de prioridade.

>[!IMPORTANT]
>
>As alterações na prioridade da camada têm efeito imediatamente e afetam o que os clientes veem em sua loja. Revise a visualização antes de salvar para garantir que os valores corretos sejam aplicados.

## Práticas recomendadas

Siga estas recomendações ao trabalhar com camadas de catálogo:

* **Use nomes descritivos** — Nomeie camadas claramente para indicar sua finalidade (por exemplo, &quot;Campanha Natal 2025&quot; ou &quot;Otimização de SEO — Páginas de Produto&quot;).

* **Limitar camadas**—Embora o sistema suporte várias camadas, o uso de muitas pode afetar o desempenho. Consolidar camadas quando possível.


* **Lógica de prioridade do documento**—Acompanhe quais camadas têm precedência para evitar substituições não intencionais.

* **Revisar camadas do Sites Optimizer**—Ao usar a correção automática do Sites Optimizer, o sistema cria camadas com a prioridade mais alta. Lembre-se de adicionar camadas manuais que substituem as recomendações de IA. Saiba mais sobre como usar o [Sites Optimizer](../manage-results/opportunities.md).

* **Monitorar desempenho** — Se você observar carregamentos lentos de páginas de produtos, revise sua configuração de camada e considere a consolidação de camadas.

## Veja mais aqui

* [Exibições de catálogo](catalog-view.md) — Configure exibições de catálogo para diferentes vitrines
* [Visuais de Produtos](https://experienceleague.adobe.com/pt-br/docs/commerce/optimizer/setup/product-visuals)—Use o AEM Assets para imagens de produtos
* [Oportunidades](../manage-results/opportunities.md)—Saiba mais sobre a otimização baseada em IA usando camadas de catálogo
* [Chaves de acesso restrito](restricted-access-keys.md)—Proteja uma exibição de catálogo com autenticação de token assinado
