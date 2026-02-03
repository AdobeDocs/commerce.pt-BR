---
title: Comparação entre SaaS e PaaS da Adobe Commerce
description: Compare os modelos SaaS e PaaS da Adobe Commerce para determinar a melhor abordagem de implementação para suas necessidades de negócios.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: e8e0c9f6a14232abc1332b48df7ae8bc3b955900
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Comparação de recursos

A Adobe Commerce oferece três modelos de implantação:

- [!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."} [Adobe Commerce na Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/overview) (local)

Essa comparação enfoca as diferenças entre os modelos de software como serviço (SaaS) e plataforma como serviço (PaaS). Esses modelos fornecem diferentes níveis de personalização, extensibilidade e controle sobre a implementação do Commerce.

>[!NOTE]
>
>O modelo local compartilha recursos semelhantes com o modelo PaaS, portanto, essa comparação também se aplica ao considerar SaaS versus implementações locais.

## Recursos de gerenciamento de loja

A [Interface do Administrador do Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/guide-overview) é a principal interface para acessar recursos para gerenciar operações de armazenamento de back-end, inventário, preços, promoções e interações com clientes. No entanto, o [!DNL Adobe Commerce as a Cloud Service] oferece soluções exclusivas que substituem alguns dos recursos conhecidos disponíveis no [!DNL Adobe Commerce on Cloud] e em projetos locais.

A tabela a seguir descreve os recursos e as soluções de substituição disponíveis no [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Recurso</th>
            <th>Modelo PaaS [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a projetos do Adobe Commerce na nuvem (infraestrutura PaaS gerenciada pela Adobe) e somente a projetos locais."}</th>
            <th>Modelo SaaS [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Gerenciamento de ativos digitais</td>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Galeria de mídia</a></td>
            <td><a href="../aem-assets-integration/overview.md">Visuais do produto</a></td>
        </tr>
        <tr>
            <td>Gestão de conteúdo</td>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/guide-overview">Sistema de Gerenciamento de Conteúdo (CMS)</a>, <a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/page-builder/guide-overview">Page Builder</a>, <a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">regravações de URL</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=pt-BR">Construtor de vitrines</a></td>
        </tr>
        <tr>
            <td>Merchandising do catálogo</td>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/staging/content-staging">Preparo de conteúdo</a>, <a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Merchandiser Visual</a></td>
            <td><a href="../catalog-service/overview.md">Serviço de catálogo</a></td>
        </tr>
        <tr>
            <td>Pagamentos</td>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/payments/payments">Soluções de pagamento</a></td>
            <td><a href="../payment-services/guide-overview.md">Payment Services</a></td>
        </tr>
        <tr>
            <td>Funcionalidade B2B</td>
            <td>Recursos B2B completos disponíveis após a instalação</td>
            <td>Pré-instalado com recursos B2B principais<sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentação</td>
            <td>Complemento para determinados níveis</td>
            <td>Teste A/B nativo para otimizar o envolvimento e a conversão</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> Os <a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/b2b/guide-overview">recursos B2B</a> principais, como gerenciamento e cotação da empresa, estão disponíveis prontamente no SaaS. No entanto, as personalizações específicas do setor podem exigir considerações adicionais de implementação.
            </td>
        </tr>
    </tfoot>
</table>

## Extensibilidade e recursos da plataforma

A tabela a seguir compara os recursos da plataforma e os recursos de extensibilidade para ajudá-lo a entender as diferenças e decidir qual modelo se adapta melhor às necessidades da sua empresa antes de iniciar uma implementação.

<table>
    <thead>
        <tr>
            <th>Recurso</th>
            <th>Modelo PaaS [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a projetos do Adobe Commerce na nuvem (infraestrutura PaaS gerenciada pela Adobe) e somente a projetos locais."}</th>
            <th>Modelo SaaS [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Recursos da plataforma</strong></td>
        </tr>
        <tr>
            <td>Atualizações de recursos e segurança</td>
            <td>Requer atualização e correção manuais. Seis lançamentos de patch e uma versão menor por ano.</td>
            <td>Atualizado automaticamente pelo Adobe por meio de um modelo SaaS sem versão</td>
        </tr>
        <tr>
            <td>Infraestrutura de hospedagem</td>
            <td>Locatário único</td>
            <td>Multilocatário</td>
        </tr>
        <tr>
            <td>Desempenho e escalabilidade</td>
            <td>Dimensionamento automático horizontal para arquitetura dimensionada. Dimensionamento automático vertical para o nível da Web que está sendo implementado no acesso antecipado para todos os comerciantes, incluindo a arquitetura não dimensionada.</td>
            <td>Aplicativo nativo em nuvem para vários locatários com dimensionamento automático completo na pilha</td>
        </tr>
        <tr>
            <td>Observabilidade</td>
            <td>[!DNL New Relic] acesso para clientes monitorarem e gerenciarem o ambiente</td>
            <td>Adobe gerenciado. Os clientes podem usar o [!DNL OpenTelemetry] para [!DNL App Builder] aplicativos e painéis de RUM para vitrine. [!DNL New Relic] licença não incluída. Os clientes podem configurar o [!DNL API Mesh] e o [!DNL App Builder] para enviar dados para sua própria conta do [!DNL New Relic].</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] incluído</td>
            <td>CDN do Edge totalmente gerenciada, totalmente combinada com a Commerce Storefront. BYO-CDN também é compatível.</td>
        </tr>
        <tr>
            <td>Segurança e conformidade</td>
            <td>Certificações SOC2, PCI, ISO por provedor de hospedagem, HIPAA</td>
            <td>SOC2, PCI, ISO, GDPR HIPAA não disponível no momento.</td>
        </tr>
        <tr>
            <td>Recuperação de desastres e SLAs</td>
            <td>99,99% de infraestrutura, 99,9% de aplicativos (Managed Services)</td>
            <td>99,9% (infraestrutura e aplicativos), RPO/RTO mais rápidos</td>
        </tr>
        <tr>
            <td>Regiões de hospedagem</td>
            <td>Azure (24 localizações), AWS (22 localizações), GCP (8 localizações, não padrão)</td>
            <td>Disponível globalmente. Para obter informações sobre ambientes de produção em sua região, entre em contato com o representante de atendimento ao cliente. Locais adicionais implantados com base na demanda.</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personalização de administração do Commerce</strong></td>
        </tr>
        <tr>
            <td>Extensibilidade do Admin Console</td>
            <td>Personalização e tema do PHP, extensibilidade do App Builder (recomendado)</td>
            <td>Extensibilidade do App Builder</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibilidade</strong></td>
        </tr>
        <tr>
            <td>Modelo de extensibilidade</td>
            <td>Em andamento (personalização do PHP) e fora de processo (recomendado: APIs, eventos, App Builder)</td>
            <td>Somente fora do processo (APIs, eventos, App Builder)</td>
        </tr>
        <tr>
            <td>APIs da Web extensíveis</td>
            <td>Extensibilidade nativa de REST/GraphQL e API Mesh com resolvedores personalizados</td>
            <td>API Mesh com resolvedores personalizados</td>
        </tr>
        <tr>
            <td>Extensibilidade do modelo de dados</td>
            <td>Personalização completa do modelo de dados</td>
            <td>Atributos personalizados para entidades principais e B2B<sup>1</sup></td>
        </tr>
        <tr>
            <td>Tecnologias</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Nó</td>
        </tr>
        <tr>
            <td>Marketplace de aplicativos</td>
            <td>[Magento Marketplace](https://marketplace.magento.com/) (extensões PHP) e [Exchange Marketplace](https://commercemarketplace.adobe.com) para aplicativos [!DNL App Builder] (Recomendado)</td>
            <td>[!DNL App Builder] aplicativos de [[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com)</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Dados e armazenamento</strong></td>
        </tr>
        <tr>
            <td>Personalizações do índice de pesquisa</td>
            <td>Personalização de pesquisa nativa</td>
            <td>Requer soluções de terceiros</td>
        </tr>
        <tr>
            <td>Tipos de email personalizados</td>
            <td>Personalização completa de email</td>
            <td>Somente modelos de email padrão</td>
        </tr>
        <tr>
            <td>Armazenamento de dados personalizado</td>
            <td>BD, arquivo, cache, fila</td>
            <td>A biblioteca de estado do App Builder (somente arquivo)<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">O Armazenamento do Banco de Dados para o App Builder</a> está atualmente em Acesso Antecipado.</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> A extensibilidade do modelo de dados em SaaS oferece suporte a <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">entidades principais de extensão</a> além do produto e do cliente, incluindo entidades B2B. No entanto, os modelos de dados específicos do setor (por exemplo, atributos específicos do revendedor) podem exigir considerações arquitetônicas adicionais.
                <br><br>
                <sup>2</sup> O Adobe está trabalhando ativamente na integração do Banco de Dados de Documentos para atender às necessidades persistentes de armazenamento de SaaS. Atualmente, as implementações que exigem armazenamento de dados de longo prazo podem precisar provisionar e manter infraestruturas adicionais.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>Ao considerar a migração para SaaS, a Adobe recomenda:
>
>- Sempre que possível, mova a funcionalidade adequada para a extensibilidade fora do processo.
>- Reduza a área de superfície que requer transição.
>- Considere [!DNL API Mesh] para estender a funcionalidade da API.
>- Monitore a evolução contínua da plataforma da Adobe e as novas versões de recursos.
>- Avaliar os requisitos de modelo de dados específicos do setor em relação às opções de extensibilidade disponíveis.
>- Considere adotar os [Serviços de merchandising fornecidos pelas Exibições e políticas do catálogo](../optimizer/setup/catalog-view.md).
