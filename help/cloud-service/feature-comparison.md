---
title: Comparação entre SaaS e PaaS da Adobe Commerce
description: Compare os modelos SaaS e PaaS da Adobe Commerce para determinar a melhor abordagem de implementação para suas necessidades de negócios.
role: Architect
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: da142209a5d0f565550ff6193ac029b0dded973f
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Comparação de recursos

{{accs-early-access}}

A Adobe Commerce oferece três modelos de implantação:

- [!BADGE Somente SaaS]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplicável somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE Somente PaaS]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."} [Adobe Commerce na Nuvem](https://experienceleague.adobe.com/pt-br/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-operations/installation-guide/overview) (local)

Essa comparação enfoca as diferenças entre os modelos de software como serviço (SaaS) e plataforma como serviço (PaaS), que fornecem diferentes níveis de personalização, extensibilidade e controle sobre a implementação comercial.

>[!NOTE]
>
>O modelo local compartilha recursos semelhantes com o modelo PaaS, portanto, essa comparação também se aplica ao considerar SaaS versus implementações locais.

## Recursos de gerenciamento de loja

A [Interface do Administrador do Commerce](https://experienceleague.adobe.com/pt-br/docs/commerce-admin/systems/guide-overview) é a principal interface para acessar recursos para gerenciar operações de armazenamento de back-end, inventário, preços, promoções e interações com clientes. No entanto, o [!DNL Adobe Commerce as a Cloud Service] oferece soluções exclusivas que substituem alguns dos recursos conhecidos disponíveis no Adobe Commerce em nuvem e em projetos locais.

A tabela a seguir descreve os recursos e as soluções de substituição disponíveis no [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Modelo PaaS [!BADGE PaaS only]{type=Informative url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se a projetos do Adobe Commerce na nuvem (infraestrutura PaaS gerenciada pela Adobe) e somente a projetos locais."}</th>
            <th>Modelo SaaS [!BADGE SaaS only]{type=Positive url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce as a Cloud Service e do Adobe Commerce Optimizer (infraestrutura SaaS gerenciada pela Adobe)."}</th>
            <th>Detalhes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Gerenciamento de ativos digitais</a></td>
            <td><a href="../product-visuals/overview.md">Visuais do produto</a></td>
            <td>Um sistema robusto de gerenciamento de ativos digitais (DAM) que se integra ao Adobe Experience Manager para gerenciar conteúdo de mídia avançada. Como alternativa, o recurso de gerenciamento de arquivos e ativos digitais padrão fornece ferramentas básicas de gerenciamento de ativos para armazenar e gerenciar ativos digitais.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/guide-overview">Sistema de gerenciamento de conteúdo (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/?lang=pt-BR">Construtor de vitrines</a></td>
            <td rowspan="3">Um CMS que permite aos usuários criar e gerenciar conteúdo da loja facilmente usando a criação de documentos ou um Editor visual e inclui recursos nativos de experimentação.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/page-builder/guide-overview">Page Builder</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">Substituições de URL</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/content-design/staging/content-staging">Preparo de conteúdo</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">Serviço de catálogo</a></td>
            <td rowspan="2">Um serviço de modelo de exibição avançado (somente leitura) para gerenciar dados de catálogo e renderizar experiências da loja relacionadas ao produto.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/stores-sales/payments/payments">Pagamentos</a></td>
            <td><a href="../payment-services/guide-overview.md">Payment Services</a></td>
            <td>Um serviço de pagamento integrado que facilita transações seguras e eficientes.</td>
        </tr>
    </tbody>
</table>

## Extensibilidade e recursos da plataforma

A tabela a seguir compara os recursos da plataforma e os recursos de extensibilidade para ajudá-lo a entender as diferenças e tomar uma decisão acertada sobre qual modelo se adapta melhor às necessidades da sua empresa antes de iniciar uma implementação.

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
            <td>Funcionalidade B2B</td>
            <td>Recursos B2B completos disponíveis após a instalação</td>
            <td>Pré-instalado com recursos B2B principais<sup>1</sup></td>
        </tr>
        <tr>
            <td>Experimentação</td>
            <td>Complemento para determinados níveis</td>
            <td>Teste A/B para otimizar o envolvimento e a conversão</td>
        </tr>
        <tr>
            <td>Atualizações de recursos e segurança</td>
            <td>Requer atualização e correção manuais</td>
            <td>Implantado automaticamente</td>
        </tr>
        <tr>
            <td>Infraestrutura de hospedagem</td>
            <td>Locatário único</td>
            <td>Multilocatário</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personalização de administração do Commerce</strong></td>
        </tr>
        <tr>
            <td>Telas principais de administração extensíveis</td>
            <td>Personalização completa de layout e funcionalidade</td>
            <td>Filtros predefinidos, controles de visibilidade</td>
        </tr>
        <tr>
            <td>Novas telas de administrador extensíveis</td>
            <td>Integração da interface do administrador padrão e injeção do aplicativo externo (SDK da interface do administrador)</td>
            <td>Inserção de aplicativo externo (SDK de interface do usuário do administrador)</td>
        </tr>
        <tr>
            <td>Tema de administração personalizável</td>
            <td>Estrutura de temas extensível</td>
            <td>Sem estrutura de temas</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibilidade</strong></td>
        </tr>
        <tr>
            <td>Modelo de extensibilidade</td>
            <td>Em processo (personalização do PHP) e fora de processo (APIs, eventos, App Builder)</td>
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
            <td>Atributos personalizados para entidades principais e B2B<sup>2</sup></td>
        </tr>
        <tr>
            <td>Tecnologias</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Nó</td>
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
            <td>Biblioteca de estado do App Builder (somente arquivo)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> Os <a href="https://experienceleague.adobe.com/pt-br/docs/commerce-admin/b2b/guide-overview">recursos B2B</a> principais, como gerenciamento e cotação da empresa, estão disponíveis prontamente no SaaS. No entanto, as personalizações específicas do setor podem exigir considerações adicionais de implementação.
                <br><br>
                <sup>2</sup> A extensibilidade do modelo de dados no SaaS oferece suporte a <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">entidades principais de extensão</a> além do produto e do cliente, incluindo entidades B2B. No entanto, os modelos de dados específicos do setor (por exemplo, atributos específicos do revendedor) podem exigir considerações arquitetônicas adicionais.
                <br><br>
                <sup>3</sup> O Adobe está trabalhando ativamente na integração do Banco de Dados de Documentos para atender às necessidades persistentes de armazenamento de SaaS. Atualmente, as implementações que exigem armazenamento de dados de longo prazo podem precisar provisionar e manter infraestruturas adicionais.
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
>- Considere a API Mesh para estender a funcionalidade da API.
>- Monitore a evolução contínua da plataforma da Adobe e as novas versões de recursos.
>- Avaliar os requisitos de modelo de dados específicos do setor em relação às opções de extensibilidade disponíveis.
>- Considere adotar [Serviços de merchandising fornecidos por Canais e políticas](../optimizer/catalog/overview.md).
