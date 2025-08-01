---
title: Commerce Services Connector
description: Saiba como integrar sua instância do Adobe Commerce ou Magento Open Source a serviços usando chaves de API de produção e sandbox.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: d7cf4898d5f44ab73017eb0a16b10856f0c4fc75
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Alguns recursos do Adobe Commerce e do Magento Open Source são viabilizados pelo [!DNL Commerce Services] e implantados como SaaS (software como serviço). Para usar esses serviços, você deve conectar sua instância do [!DNL Commerce] usando chaves de API de sandbox e produção e especificar o espaço de dados na [configuração](#saas-configuration). Você só precisa configurar a conexão uma vez para cada instância.

## Serviços disponíveis {#availableservices}

Veja a seguir uma lista dos recursos do [!DNL Commerce] que você pode acessar por meio do [!DNL Commerce Services Connector]:

| Serviço | Disponibilidade |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) ativado por Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) ativado por Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | ADOBE COMMERCE e MAGENTO OPEN SOURCE |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Arquitetura

Em um nível superior, o [!DNL Commerce Services Connector] é composto dos seguintes elementos principais:

![Arquitetura do Commerce Services Connector](assets/saas-config-sync-workflow.png)

As seções a seguir discutem cada um desses elementos com mais detalhes.

## Credenciais {#apikey}

As chaves de API de sandbox e produção são geradas a partir da conta [!DNL Commerce] do [proprietário da licença](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). A conta do Commerce é identificada por um identificador exclusivo [!DNL Commerce] (MageID). O proprietário da licença da organização do comerciante pode gerar chaves de API para serviços como Recomendações de produto ou Live Search, desde que a conta esteja em bom estado.

As chaves podem ser compartilhadas com base no &quot;conhecimento necessário&quot; com o integrador de sistemas ou a equipe de desenvolvimento que gerencia projetos e ambientes em nome do titular da licença. Os desenvolvedores aos quais o proprietário da licença concedeu [!DNL Shared Access] não podem gerar as chaves em seu nome, mesmo que a organização do comerciante esteja presente na lista suspensa [!DNL Switch Accounts] em sua conta.

Além disso, os integradores de soluções também podem usar o [!DNL Commerce Services]. Se você for um integrador de soluções, o signatário do contrato de parceiro [!DNL Commerce] deve gerar as chaves de API.

>[!NOTE]
>Os identificadores de chave *Produção* e *Sandbox* não se referem ao seu ambiente. Use o mesmo conjunto de chaves de API para cada um dos ambientes, por exemplo, local, de desenvolvimento, de armazenamento temporário ou de produção.
>
>O proprietário da licença normalmente é o contato principal na conta da Adobe Commerce e nem sempre é o mesmo Proprietário do projeto Adobe Commerce na infraestrutura em nuvem.

### Gerar as chaves de API de produção e sandbox {#genapikey}

1. Faça logon em sua conta do [!DNL Commerce] em [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Na guia **Magento**, selecione **Portal de API** na barra lateral.

1. No menu _Ambiente_, selecione **Produção** ou **Sandbox**.

   >[!NOTE]
   >
   >*Produção* e *Sandbox* referem-se aos ambientes de espaço de dados em que os dados são armazenados em sistemas back-end SaaS do Adobe. Não se refere aos ambientes de comércio nos quais você usará as chaves.

1. Insira um nome na seção _Chaves de API_ e clique em **Adicionar novo** para abrir a caixa de diálogo para baixar a nova chave.

   ![Baixar chave privada](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Esta caixa de diálogo fornece a única oportunidade que você tem para copiar ou baixar suas chaves.

1. Clique em **Baixar** e em **Cancelar**.

1. Repita as etapas acima para cada ambiente (produção e sandbox).

   A seção **Chaves de API** agora exibe suas chaves de API (Públicas). Você precisa de todas as quatro chaves (tanto as chaves de produção quanto de sandbox, Público+Privado) ao [selecionar ou criar um projeto SaaS](#createsaasenv) em qualquer um dos ambientes ou instalações associados à licença.

## Configuração SaaS {#saasenv}

[!DNL Commerce] instâncias devem ser configuradas com um projeto SaaS e um espaço de dados SaaS para que [!DNL Commerce Services] possa enviar os dados para o local correto. Um projeto SaaS agrupa todos os espaços de dados SaaS. Os espaços de dados SaaS são usados para coletar e armazenar dados que permitem que o [!DNL Commerce Services] funcione. Alguns desses dados podem ser exportados da instância [!DNL Commerce] e outros podem ser coletados do comportamento do comprador na loja. Esses dados são mantidos para proteger o armazenamento na nuvem.

Para [!DNL Product Recommendations], o espaço de dados SaaS contém dados de catálogo e comportamentais. Você pode apontar uma instância [!DNL Commerce] para um espaço de dados SaaS ao [selecioná-la](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) na configuração [!DNL Commerce].

>[!WARNING]
>
> Use seu **espaço de dados SaaS de produção** somente em sua instalação de produção [!DNL Commerce] para evitar colisões de dados. Caso contrário, você corre o risco de poluir os dados do site de produção com dados de teste, o que causa atrasos de implantação. Por exemplo, os dados do produto de produção podem ser substituídos por engano dos dados de preparo, como URLs de preparo.
> &#x200B;> Se isso acontecer, [envie uma solicitação de suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) para solicitar limpeza de dados.

Se não conseguir encontrar campos de configuração do LiveSearch no Painel de administração, verifique se você inseriu a chave de API SaaS correta.  Certifique-se de ter adicionado a chave SaaS de produção ao configurar o espaço de dados de produção e de ter adicionado a chave de preparo ao configurar o espaço de dados de preparo. Se você configurar a chave incorreta, os serviços SaaS, como o LiveSearch, não estarão disponíveis no ambiente do Adobe Commerce.

### Provisionamento de espaço de dados SaaS

Todos os comerciantes do Adobe Commerce podem acessar um espaço de dados de produção e dois espaços de dados de teste por projeto SaaS.

Você pode usar os espaços de dados de teste em qualquer ambiente de não produção, desde que não use o mesmo espaço de dados em vários ambientes ao mesmo tempo. Para usar o espaço de dados de teste em um ambiente diferente, execute uma limpeza de dados antes de selecionar e configurar o espaço de dados nesse ambiente.

Para projetos da Adobe Commerce Cloud Pro com vários ambientes de preparo, você pode solicitar espaços de dados de teste adicionais para cada ambiente de preparo [enviando uma solicitação de suporte](https://experienceleague.adobe.com/home?support-tab=home#support). No entanto, se você tiver apenas um ambiente de preparo e exigir espaços de dados de teste adicionais, terá as seguintes opções:

- Entre em contato com a equipe de Sucesso do cliente ou com o Gerente de sucesso do cliente designado para solicitar um ambiente de preparo adicional.

- [Envie uma solicitação de suporte](https://experienceleague.adobe.com/home?support-tab=home#support) para solicitar o espaço de dados de teste adicional e indicar a justificativa comercial para o espaço de dados extra. Esta solicitação está sujeita a aprovação.

Os clientes do Magento Open Source que usam os Serviços de pagamento da Adobe também podem solicitar um espaço de dados adicional. Entre em contato com a equipe de Pagamentos para obter aprovação prévia dos espaços de dados adicionais antes de enviar uma [Solicitação de suporte](https://experienceleague.adobe.com/home?support-tab=home#support) para solicitar o espaço de dados de teste.

Os clientes que possuem vários projetos na nuvem ou instalações locais (live/production) também podem solicitar espaços de dados adicionais de produção e teste para cada projeto ou instância por [enviar uma solicitação de suporte](https://experienceleague.adobe.com/home?support-tab=home#support).

### Selecionar ou criar um projeto SaaS {#createsaasenv}

Para selecionar ou criar um projeto SaaS, solicite a chave de API [!DNL Commerce] ao proprietário da licença [!DNL Commerce] da sua loja:

>[!NOTE]
>
> Se você não vir a seção **[!UICONTROL Commerce Services Connector]** na configuração [!DNL Commerce], instale os módulos [!DNL Commerce] do [[!DNL Commerce] serviço](#availableservices) desejado.

1. Na barra lateral _Admin_, vá para **System** > Services > **Commerce Services Connector**.

   Se você não vir a seção **[!UICONTROL Commerce Services Connector]** na configuração [!DNL Commerce], instale os módulos [!DNL Commerce] do [[!DNL Commerce] serviço](#availableservices) desejado. Além disso, verifique se o pacote `magento/module-services-id` está instalado.

1. Nas seções _[!UICONTROL Sandbox API Keys]_&#x200B;e_[!UICONTROL Production API Keys]_, cole seus valores de chave.

   - As chaves privadas devem incluir `----BEGIN PRIVATE KEY---` no início da chave e `----END PRIVATE KEY----` no final da chave.
   - Se você não tiver uma cópia das chaves reais, peça ao Proprietário da conta que as informe e, em seguida, conecte os valores à configuração.

   >[!WARNING]
   >
   > Se você adicionar valores-chave consultando um backup de banco de dados ou snapshot e colando os valores na configuração, uma camada adicional de criptografia será aplicada e as chaves não funcionarão.

1. Clique em **Salvar**.

Qualquer projeto SaaS associado às suas chaves é exibido no campo **Projeto** da seção **Identificador SaaS**.

1. Se não existirem projetos SaaS, clique em **Criar projeto**. Em seguida, no campo **Projeto**, digite um nome para o projeto SaaS.

>[!NOTE]
>
>Para evitar confusão, não use um Serviço Commerce específico como o nome do seu projeto, por exemplo *Live Search*, *Recomendações de Produto* ou *Conexão de Dados*.  A menos que sua licença tenha sido provisionada para vários projetos SaaS, você poderá usar o mesmo projeto SaaS para vários serviços.

1. Selecione o **Espaço de Dados** a ser usado para a configuração atual do seu repositório [!DNL Commerce].

>[!NOTE]
>
>Se você tiver instâncias separadas para integrar com os Serviços Commerce, [envie um tíquete de Suporte](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) para solicitar um novo projeto SaaS para cada instância adicional. Depois que o suporte tiver criado o projeto SaaS, configure a integração dos Serviços da Commerce para a instância usando a mesma chave de API e selecionando o novo projeto SaaS para o espaço de dados.

>[!WARNING]
>
> Se você gerar novas chaves na seção Portal de API de Minha conta, atualize imediatamente as chaves de API na configuração de Administrador. Se você gerar novas chaves e não atualizá-las no Admin, suas extensões SaaS não funcionarão mais e você perderá dados valiosos.

Para alterar os nomes do projeto SaaS ou do espaço de dados, clique em **Renomear**. Alterar o nome não afeta seu serviço porque o nome é apenas um rótulo que ajuda a identificar e diferenciar entre projetos e espaços de dados.

## Organização IMS (opcional) {#organizationid}

Para conectar sua instância do Adobe Commerce à Adobe Experience Platform, faça logon em sua conta da Adobe usando sua Adobe ID. Depois de fazer logon, a organização IMS associada à sua conta da Adobe é exibida nesta seção.

## Exportação de dados SaaS

Quando a instância do [!DNL Commerce] é conectada com êxito ao [!DNL Commerce Services], o processo de exportação de dados SaaS exporta os dados do Commerce do servidor [!DNL Commerce] para o [!DNL Commerce SaaS Services] para que ele possa ser sincronizado com os Commerce Services conectados. No Administrador, você pode verificar o status da sincronização usando o [painel de Gerenciamento de Dados](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Para obter detalhes, consulte o [Guia de Exportação de Dados SaaS](../data-export/overview.md).
