---
title: Instalar [!DNL Data Connection]
description: Saiba como instalar, atualizar e desinstalar a extensão  [!DNL Data Connection]  do Adobe Commerce.
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Instalar [!DNL Data Connection]

Antes de instalar a extensão, [revise os pré-requisitos](overview.md#prereqs).

## Instalar a extensão

A extensão [!DNL Data Connection] está disponível no [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html). Ao instalar esta extensão a partir da linha de comando do servidor, ela se conecta à instalação do Adobe Commerce como um [serviço](../landing/saas.md). Quando o processo for concluído, o **[!DNL Data Connection]** e o **Commerce Services Connector** aparecerão no menu **Sistema** em **Serviços** no Commerce _Admin_.

![[!DNL Data Connection] exibição de administrador da extensão](assets/epc-adminui.png)

>[!IMPORTANT]
>
>Embora o nome da extensão tenha sido alterado do conector do Experience Platform para [!DNL Data Connection], o nome do pacote permanece `experience-platform-connector` para oferecer suporte à compatibilidade com versões anteriores.

1. Para baixar o pacote `experience-platform-connector`, execute o seguinte na linha de comando:

   ```bash
   composer require magento/experience-platform-connector
   ```

   Este metapackage contém os seguintes módulos e extensões:

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. (Opcional) Para incluir dados do [!DNL Live Search], que incluem [eventos de pesquisa](events.md#search-events), instale a extensão [[!DNL Live Search]](../live-search/install.md).

1. (Opcional) Para incluir dados B2B, que compreende [eventos de requisição](events.md#b2b-events), instale a [extensão B2B](#install-the-b2b-extension).

1. (Opcional) Se você for um comerciante do plano de saúde, instale a extensão [Data Services HIPAA](#install-the-data-services-hipaa-extension) para que seus dados de back office do [!DNL Commerce] estejam prontos para HIPAA.

### Instale o Adobe I/O Events e configure o módulo do conector do cliente

Após instalar a extensão `experience-platform-connector`, instale o Adobe I/O Events para Adobe Commerce e configure o módulo `customers-connector`.

As etapas a seguir se aplicam ao Adobe Commerce na infraestrutura em nuvem e às instalações locais.

1. Se você estiver executando o Commerce 2.4.4 ou 2.4.5, use o seguinte comando para carregar os módulos de evento:

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   O Commerce 2.4.6 e versões posteriores carregam esses módulos automaticamente.

1. Atualize as dependências do projeto.

   ```bash
   composer update
   ```

1. Ative os novos módulos:

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

Finalize a instalação com base no tipo de implantação: Adobe Commerce na infraestrutura em nuvem ou no local.

#### Na infraestrutura em nuvem

Na infraestrutura do Adobe Commerce na nuvem, habilite a variável global `ENABLE_EVENTING` em `.magento.env.yaml`. [Saiba mais](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html?lang=pt-BR#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

Confirme e envie por push os arquivos atualizados para o ambiente em nuvem. Quando a implantação for concluída, habilite o envio de eventos com o seguinte comando:

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### No local

Em ambientes locais, você deve habilitar manualmente a geração de código e os Eventos do Adobe Commerce:

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### Instalar a extensão B2B

Para comerciantes B2B, instale a seguinte extensão para incluir dados do evento [lista de requisições](events.md#b2b-events).

Baixe a extensão `magento/experience-platform-connector-b2b` executando o seguinte na linha de comando:

```bash
composer require magento/experience-platform-connector-b2b
```

### Instalar a extensão HIPAA do Data Services

Para comerciantes da área de saúde, instale a seguinte extensão para garantir que os dados de eventos de back office estejam prontos para HIPAA.

Baixe a extensão `magento/module-data-services-hipaa` executando o seguinte na linha de comando:

```bash
composer require magento/module-data-services-hipaa
```

## Atualizar a extensão [!DNL Data Connection] {#update}

Para atualizar a extensão [!DNL Data Connection], execute o seguinte a partir da linha de comando:

```bash
composer update magento/experience-platform-connector --with-dependencies
```

Ou, para os comerciantes B2B:

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

Para atualizar para uma versão principal, como de 2.0.0 para 3.0.0, edite o arquivo raiz do projeto [!DNL Composer] `.json` da seguinte maneira:

1. Abra o arquivo raiz `composer.json` e procure por `magento/experience-platform-connector`.

1. Na seção `require`, atualize o número da versão da seguinte maneira:

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **Salvar** `composer.json`. Em seguida, execute o seguinte a partir da linha de comando:

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   Ou, para os comerciantes B2B:

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## Desinstalar a extensão [!DNL Data Connection] {#uninstall}

Para desinstalar a extensão [!DNL Data Connection], consulte [desinstalar módulos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html?lang=pt-BR).
