---
title: Verificar atualizações de extensão
description: Saiba como o Adobe Commerce verifica e notifica os administradores sobre novas versões de extensão da Integração do AEM Assets, incluindo a verificação manual da CLI.
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# Verificar atualizações de extensão

Com a extensão de integração do AEM Assets versão 1.4.6 e posterior, o Adobe Commerce verifica automaticamente se uma versão mais recente da extensão está disponível e notifica os administradores no Administrador. Essa verificação é executada de forma assíncrona como parte do processamento agendado e não bloqueia a renderização da página de administração.

## Como funciona a verificação de atualização

* A verificação de atualização compara a versão do pacote `aem-assets-integration` instalada com a versão mais alta compatível disponível em [repo.magento.com](https://repo.magento.com/admin/dashboard).
* Os resultados são armazenados em cache. O carregamento de uma página de Administrador lê o resultado mais recente em cache, em vez de acionar uma solicitação de rede em tempo real.
* Se `repo.magento.com` não estiver disponível ou os metadados retornados forem inválidos, o Commerce manterá o último resultado em cache bem-sucedido e não bloqueará o Administrador.

>[!NOTE]
>
>A verificação de atualização destina-se ao Adobe Commerce em implantações na nuvem e locais.

## Exibir notificações de atualização

Os administradores podem ver uma notificação de atualização disponível em ambos os locais:

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* A lista suspensa Notificação de administrador

Cada notificação é exibida:

* A versão instalada
* A versão disponível
* A classificação de versão
* Um link para as notas de versão

Selecione **[!UICONTROL Remind me later]** para adiar a notificação para esta instância do Commerce ou recusar totalmente as notificações de atualização.

## Executar uma verificação de atualização manual

Para verificar se há uma atualização disponível imediatamente, execute o seguinte comando no diretório raiz do Commerce:

```bash
bin/magento aem:assets:check-update
```

Esse comando só verifica e relata uma atualização disponível. Ele não modifica arquivos do Composer nem implanta uma atualização. Para instalar uma atualização, siga as instruções do Composer em [Instalar pacotes do Adobe Commerce](configure-commerce.md).

## Metadados de versão para pacotes de extensão

A verificação de atualização lê os metadados da versão da seção `extra` do arquivo `composer.json` do pacote instalado:

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/pt-br...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## Próxima etapa

* [Instalar pacotes do Adobe Commerce](configure-commerce.md)
