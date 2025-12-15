---
title: Camada de catálogo
description: Saiba como as camadas de catálogo permitem modificar dados do produto sem alterar os dados de origem originais, para que você possa personalizar com segurança e reverter alterações a qualquer momento.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Somente SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."
source-git-commit: 4a904527af172a5e35b87410135d55484d07ad84
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Camada de catálogo

As camadas de catálogo permitem modificar os dados do produto sem alterar os dados de origem originais. As camadas aplicam alterações a atributos específicos do produto, como nome, descrição, imagens, links e metadados, criando uma camada na parte superior do catálogo base. Os dados originais do produto permanecem intactos, permitindo personalizar produtos com segurança e reverter alterações a qualquer momento.

![Camadas do catálogo](../assets/catalog-layers.png)

## Como as camadas de catálogo funcionam

Quando um cliente visualiza sua loja, o sistema combina os dados do catálogo base com as camadas do catálogo ativo para exibir as informações finais do produto. Veja como o processo funciona:

1. **Aplicativo de camada** — Quando uma solicitação é feita com uma ID de canal e uma ID de ambiente, o serviço de armazenamento recupera a exibição de catálogo relevante.

1. **Mesclagem de dados** — O sistema aplica camadas de catálogo aos dados do produto com base na ordem de prioridade das camadas.

1. **Tratamento de campo**—Tipos de campo diferentes são processados de forma diferente:

   - **Substituir campos** — Campos de texto como nome, descrição e metatítulos são substituídos pelos valores definidos na camada, com a camada de prioridade mais alta tendo precedência.
   - **Mesclar campos** — Campos de matriz como imagens, links e atributos são combinados de várias camadas, fornecendo uma resposta unificada.

1. **Resolução de prioridade** — O campo de ordem determina qual camada tem prioridade. Quando várias camadas modificam o mesmo campo, a camada com o número de ordem mais baixo tem prioridade mais alta (por exemplo, a ordem 1 é a mais alta).

## Casos de uso da camada de catálogo

As camadas de catálogo geralmente são usadas para:

- **Otimização de SEO**—Substitua os metatítulos e descrições do produto com base nas recomendações de IA do [Sites Optimizer](../manage-results/opportunities.md).
- **Campanhas sazonais** — Atualize temporariamente nomes de produtos, descrições ou imagens para promoções sem alterar os dados de origem.
- **Personalização regional**—Exiba informações de produtos diferentes com base na localização geográfica ou no idioma.
- **Teste A/B**—Teste diferentes apresentações de produtos para otimizar as taxas de conversão.
- **Gerenciamento de várias marcas** — Personalize atributos de produto para diferentes exibições do catálogo de marcas.

## Adicionar uma camada de catálogo por meio da assimilação de dados

É possível adicionar camadas de catálogo aos seus produtos durante o processo de assimilação de dados. Esse método é ideal para operações em massa ou fluxos de trabalho automatizados.

>[!NOTE]
>
>As camadas de catálogo são importadas usando a API de assimilação, mas a [definição da ordem](#manage-layer-priorities) das camadas é feita usando a interface.

**Pré-requisitos:**

- Credenciais da API com permissão para acessar o serviço de assimilação de dados
- SKUs do produto que já existem no catálogo base

**Etapas:**

1. Prepare os dados da camada no formato necessário com os atributos do produto que você deseja modificar.

1. Use o endpoint da API de camadas de produto para assimilar os dados da camada.

1. Verifique se a camada foi assimilada com êxito verificando a configuração de exibição do catálogo.

Para obter especificações detalhadas de API e exemplos de carga, consulte [Camadas de produto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) na documentação do desenvolvedor.

## Adicionar uma camada de catálogo manualmente na interface

>[!NOTE]
>
>Este recurso ainda não está disponível.

A interface de exibição de catálogo permite criar e gerenciar manualmente camadas, o que é particularmente útil para integrações como o Sites Optimizer que geram recomendações alimentadas por IA.

>[!NOTE]
>
>Se uma camada do Sites Optimizer não existir na visualização de catálogo, o recurso de correção automática no Sites Optimizer criará uma camada automaticamente e a atribuirá à ordem 1 (prioridade mais alta). Se você excluir essa camada, ela será recriada na próxima vez que o recurso de correção automática no Sites Optimizer for executado e mudará as camadas existentes para números de ordem mais baixos. Se a camada do Sites Optimizer já existir com um número de pedido diferente, o recurso de correção automática não alterará sua prioridade.

>[!TIP]
>
>Para operações de camada em massa, use o método de API de assimilação de dados [descrito acima](#add-a-catalog-layer-via-data-ingestion).

**Para criar uma camada manual:**

1. Navegue até **Configuração da loja** > **Exibições de catálogo**.

1. Selecione a exibição de catálogo na qual deseja aplicar a camada.

1. Na seção camadas do catálogo, clique em **Adicionar camada do catálogo**.

1. Configure as propriedades da camada:

   - **Nome da camada** — Digite um nome descritivo para identificar a finalidade da camada.
   - **Produtos**—Selecione os produtos aos quais esta camada se aplica.
   - **Atributos** — Escolha quais atributos de produto modificar (nome, descrição, imagens, metatags e assim por diante).
   - **Valores** — Insira os novos valores para cada atributo selecionado.

1. Clique em **Salvar** para criar a camada.

A nova camada é adicionada à visualização do catálogo e é automaticamente atribuída ao próximo número de pedido disponível.

## Visualizar efeitos de camada

>[!NOTE]
>
>Este recurso ainda não está disponível.

Antes de ativar camadas ou alterar prioridades, é possível visualizar como elas afetam os dados do produto.

**Para visualizar as alterações da camada:**

1. Navegue até **Configuração da loja** > **Exibições de catálogo**.

1. Selecione a exibição de catálogo com as camadas que deseja visualizar.

1. Na seção camadas do catálogo, selecione um produto específico ou use a função de visualização.

1. Revise os dados do produto combinados que mostram como as camadas modificam os valores do catálogo base.

1. Faça ajustes no conteúdo da camada ou na ordem de prioridade, conforme necessário.

## Ativar, desativar ou excluir camadas

É possível ativar ou desativar camadas de catálogo sem excluí-las, permitindo que você controle quando personalizações específicas são aplicadas.

**Para ativar ou desativar uma camada:**

1. Navegue até **Configuração da loja** > **Exibições de catálogo**.

1. Selecione a exibição de catálogo que contém a camada.

1. Na seção camadas do catálogo, localize a camada que deseja alternar.

1. Clique no botão de ativação para ativar ou desativar a camada.

   - **Ativo** — A camada é aplicada aos dados do produto.
   - **Inativo** — A camada é preservada, mas não aplicada aos dados do produto.

1. A alteração entrará em vigor imediatamente na loja.

**Para excluir uma camada:**

Use a API de assimilação de dados para [excluir uma camada de catálogo](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers).

## Gerenciar prioridades de camada

A ordem em que as camadas são aplicadas determina quais valores aparecem na loja quando várias camadas modificam o mesmo atributo de produto. O gerenciamento de prioridades garante que os dados corretos sejam exibidos.

**Noções básicas sobre a ordem de prioridade:**

- A cada camada é atribuído um número de ordem (1, 2, 3 e assim por diante)
- A ordem 1 tem a prioridade mais alta e substitui todas as outras camadas
- Quando várias camadas modificam o mesmo campo, a camada com o número de ordem mais baixo tem prioridade
- A prioridade se aplica somente a campos de substituição (nome, descrição, metatags)
- Campos de mesclagem (imagens, links, atributos) combinam dados de todas as camadas

**Para reordenar as prioridades de camada:**

1. Navegue até **Configuração da loja** > **Exibições de catálogo**.

1. Selecione a exibição do catálogo que contém as camadas que você deseja reordenar.

1. Na seção camadas do catálogo, localize a camada que deseja mover.

1. Arraste e solte a camada para alterar sua posição ou use os controles de reordenação.

1. O sistema atualiza automaticamente os números dos pedidos com base na nova sequência.

1. Clique em **Salvar** para aplicar a nova ordem de prioridade.

>[!IMPORTANT]
>
>As alterações na prioridade da camada têm efeito imediatamente e podem afetar o que os clientes veem em sua loja. Revise a visualização antes de salvar para garantir que os valores corretos sejam aplicados (**a visualização ainda não está disponível**).

## Práticas recomendadas

Siga estas recomendações ao trabalhar com camadas de catálogo:

- **Use nomes descritivos** — Nomeie camadas claramente para indicar sua finalidade (por exemplo, &quot;Campanha de Natal 2025&quot; ou &quot;Otimização de SEO - Páginas de Produto&quot;).

- **Limitar camadas**—Embora o sistema suporte várias camadas, o uso de muitas pode afetar o desempenho. Consolidar camadas quando possível.

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

- **Lógica de prioridade do documento**—Acompanhe quais camadas devem ter precedência para evitar substituições não intencionais.

- **Revisar camadas do Sites Optimizer**—Ao usar a correção automática do Sites Optimizer, o sistema cria camadas com a prioridade mais alta. Lembre-se de adicionar camadas manuais que podem substituir as recomendações de IA. Saiba mais sobre como usar o [Sites Optimizer](../manage-results/opportunities.md).

- **Monitorar desempenho** — Se você observar carregamentos lentos de páginas de produtos, revise sua configuração de camada e considere a consolidação de camadas.

## Veja mais aqui

- [Exibições de catálogo](catalog-view.md) - Configure exibições de catálogo para diferentes vitrines
- [Oportunidades](../manage-results/opportunities.md) - Saiba mais sobre a otimização baseada em IA usando camadas de catálogo
