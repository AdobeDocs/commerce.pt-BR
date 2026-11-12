---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%
---
<!--This shared include file contains the conceptual and architecture overview of catalog views for Adobe Merchandising Services-->

Uma exibição de catálogo define os produtos e os preços que um cliente pode recuperar. Ele combina fontes de catálogo, camadas de catálogo, políticas e catálogos de preços para oferecer suporte a diferentes marcas, regiões, unidades de negócios ou canais.

## O que são visualizações de catálogo?

As exibições de catálogo definem como o catálogo de produtos é organizado e exibido. Eles atuam como filtros que determinam:

- **Quais produtos são visíveis** com base na estrutura comercial (marcas, regiões, revendedores)
- **Que preços são mostrados** por meio de catálogos de preços vinculados
- **Como os produtos são filtrados** usando políticas (atributos como marca, modelo, categoria)
- **Que [origem do catálogo](/help/optimizer/setup/catalog-sources.md) é usada** com base em atributos como localidade
- **Quem pode acessar os dados da exibição** por meio da [Proteção de Catálogo](private-catalog-view.md) e das [chaves de acesso restrito](restricted-access-keys.md)

Por exemplo, é possível criar exibições de catálogo separadas para:

- Uma marca ou unidade de negócios
- Uma região geográfica
- Um canal de revendedor ou parceiro
- Um segmento de cliente com preços específicos

## Visão geral da arquitetura

As exibições de catálogo são parte da estrutura de serviços da Adobe Merchandising que substitui a estrutura de site, loja e loja usada nas bases da Adobe Commerce por um modelo mais flexível:

Arquitetura ![[!DNL Merchandising Services]](/help/assets/ccdm-shared/setup/merchandising-svcs-architecture.png)

### Como funciona

**1. Assimilação de dados**
Os dados do catálogo de um back-end do Adobe Commerce ou de outro back-end de terceiros (por exemplo, PIM ou ERP) e de outros sistemas são assimilados na camada de dados dos Serviços da Adobe Merchandising. Cada SKU contém informações de local e atributos de produto que mapeiam para exibições de catálogo, políticas e locais. O processo de assimilação de dados depende do sistema de origem e do método de integração:

- **Infraestrutura Adobe Commerce** — O sistema exporta feeds de catálogo do Commerce, mapeia-os para o formato esperado pela API REST de assimilação de dados e sincroniza os dados de feed com a camada de dados dos Serviços da Adobe Merchandising. Nesse modelo, o Adobe Commerce gerencia a sincronização inicial e as atualizações subsequentes. Os feeds incluem produtos, categorias, atributos de produto, preços e catálogos de preços.

- **Back-end de terceiros ou sistema de origem** — Um conector ou serviço de integração recupera dados de catálogo da origem por meio de APIs, eventos ou feeds de exportação, mapeia e valida esses dados em relação ao esquema do modelo de dados de catálogo combinável (CCDM) e sincroniza os dados para a camada do Adobe Merchandising Services usando a API REST de Assimilação de Dados. A integração é responsável pela carga inicial e pelo envio de alterações posteriores. Um conector específico de plataforma, como o [Salesforce Commerce Connector](https://experienceleague.adobe.com/en/docs/commerce/optimizer/developer/salesforce-connector) da Adobe, pode fornecer um ponto de partida.

**2. Catálogo de base unificada**
Os dados assimilados criam um catálogo base unificado no pipeline de dados do Serviço de catálogo. Essa única fonte elimina a duplicação de dados nas unidades de negócios.

**3. Exibições do catálogo**
Várias exibições de catálogo representam unidades de negócios diferentes (por exemplo, &quot;Texas Retail&quot;, &quot;Texas Retail Seasonal&quot;). Locais, políticas e catálogos de preços podem ser compartilhados entre exibições de catálogo para maior flexibilidade.

**4. Entrega multicanal**
Os dados de catálogo filtrados são entregues a destinos como Edge Delivery Services, marketplaces, plataformas de publicidade e microlojas personalizadas. Para obter mais informações sobre a entrega de dados do catálogo, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/).

Quando uma exibição de catálogo tem **[!UICONTROL Catalog Protection]** habilitada, a entrega para esse destino requer um token assinado válido de uma [chave de acesso restrito](restricted-access-keys.md) atribuída; solicitações não autorizadas são negadas em vez de receber dados de catálogo.

### Componentes principais

| Componente | Finalidade | Exemplo |
|---|---|---|
| **Exibição de catálogo** | Unidade de negócios ou canal de distribuição | Rede de revendedores, Loja regional |
| **Política** | Filtro de produto com base em atributos | Marca, modelo, categoria |
| **Localidade** | Configuração de idioma/região | en-US, fr-CA, es-MX |
| **Catálogo de Preços** | Estrutura de preços | Varejo, Atacado, Funcionário |
| **Chave de acesso restrito** | Credencial de token assinado que dá acesso a uma exibição de catálogo protegida | Chave do portal do parceiro, chave de preços B2B |

### Fluxo de dados

1. **Assimilar** - dados de catálogo do back-end do Adobe Commerce
2. **Processo** - Aplicar exibições de catálogo, políticas e preços
3. **Entrega** - Veicula o catálogo filtrado em vitrines, marketplaces e assim por diante

## Principais recursos

| Recurso | Benefício |
|---|---|
| **Catálogo de Base Única** | Eliminar a duplicação de dados em unidades de negócios |
| **Preços flexíveis** | Vários catálogos de preços por SKU para diferentes segmentos de clientes |
| **Escalável** | Gerencie mais de 200 milhões de SKUs com eficiência |
| **Multicanal** | Oferece catálogos para vitrines, mercados e plataformas de publicidade |
| **Atualizações em tempo real** | Atualize rapidamente os dados do catálogo para promoções e campanhas |
| **Exibições de catálogo privado** | Restringir uma exibição de catálogo aos clientes autorizados usando a validação de token assinado |

## Casos de uso

### Conglomerado multimarcas

**Desafio**: gerenciar várias marcas, países e idiomas<br>
**Solução**: catálogo único com exibições de catálogo para cada combinação de marca/região

### Revendedor de peças automotivas

**Desafio**: 3.000 revendedores com os mesmos produtos, mas com preços diferentes<br>
**Solução**: um catálogo com exibições de catálogo e catálogos específicos de revendedores

### Retailer com vários locais

**Desafio**: preços e inventário diferentes por localização<br>
**Solução**: exibições de catálogo baseadas em localização com políticas específicas de região

>[!NOTE]
>
>Para obter informações detalhadas sobre a assimilação e a entrega de dados do catálogo, consulte a [documentação do desenvolvedor](https://developer.adobe.com/commerce/services/optimizer/).
