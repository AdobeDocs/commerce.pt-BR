---
title: Preparação para HIPAA para  [!DNL Commerce] serviços
description: Saiba como usar a  [!DNL Data Connection] extensão para compartilhar [!DNL Commerce] dados com a Experience Platform e manter a conformidade com a HIPAA.
role: Admin, Leader
feature: Security, Compliance
exl-id: 8851e6d2-c466-4d8e-bfa4-20d0ad6522b5
source-git-commit: 290e3310bd7940c4ccd11317d273b75cc974223b
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Disponibilidade para HIPAA para [!DNL Commerce] Serviços

A extensão [!DNL Data Connection] permite compartilhar [!DNL Commerce] dados de eventos de back office com a Experience Platform e manter a conformidade com a HIPAA.

>[!IMPORTANT]
>
>Como os eventos de vitrine são gerados no lado do cliente, é responsabilidade do comerciante [não enviar dados do evento de vitrine](connect-data.md#data-collection) para a Experience Platform.

Neste artigo, você aprenderá:

- O que instalar
- Como garantir que os dados enviados para o Experience Platform estejam prontos para HIPAA
- Criptografia de dados em [!DNL Commerce]

## Instalação

Se você adquiriu o complemento de plano de saúde para o Adobe [!DNL Commerce], provavelmente já instalou a [extensão HIPAA-Ready](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation). Para garantir que os dados do evento de back office do [!DNL Commerce] estejam prontos para HIPAA, você também precisa instalar a extensão [!DNL Data Connection] com a extensão adicional **HIPAA** do Data Services. A extensão HIPAA **do** Data Services garante que todos os dados de back-office enviados para a Experience Platform estejam prontos para HIPAA. Saiba [como instalar a extensão](install.md#install-the-data-services-hipaa-extension).

>[!IMPORTANT]
>
>Quando você instala a extensão HIPAA **do** Data Services, os dados do evento da loja usados pelo Live Search e pelas Recomendações de Produto não são mais capturados. Isso ocorre porque os dados do evento da loja são gerados no lado do cliente. Para continuar capturando e enviando dados do evento da loja, reative a coleta de eventos para esses serviços. Consulte [configuração geral](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services) para saber mais.

## Como garantir que os dados enviados para o Experience Platform estejam prontos para HIPAA

Todos os dados de eventos de back office que a extensão [!DNL Data Connection] envia para a Experience Platform são considerados confidenciais em [!DNL Commerce]. No entanto, é de responsabilidade do comerciante aplicar rótulos de uso de dados ao esquema [!DNL Commerce] no Experience Platform para identificar explicitamente dados específicos como confidenciais. Ao aplicar rótulos de uso de dados diretamente a um esquema, eles são propagados para todos os conjuntos de dados existentes e futuros baseados nesse esquema.

Para obter uma visão geral dos rótulos de uso de dados e sua função na estrutura de Governança de dados, consulte a [visão geral dos rótulos de uso de dados](https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-governance/labels/overview) na documentação do Experience Platform.

### Aplicar rótulos de uso de dados a [!DNL Commerce] campos

Siga as etapas do tutorial [gerenciar rótulos de uso de dados para um esquema](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/labels) para saber como aplicar rótulos ao seu esquema [!DNL Commerce].

Consulte o [glossário de rótulos confidenciais](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/labels/reference#sensitive) para saber mais sobre os rótulos disponíveis que você pode aplicar aos campos no esquema [!DNL Commerce]. Por exemplo, o rótulo `RHD` identifica informações de saúde protegidas (PHI) ou informações sobre um paciente que você tem permissão contratual do Adobe para carregar.

Quando os dados do [!DNL Commerce] são rotulados como confidenciais, você pode aplicar políticas para impedir operações de dados que constituam violações de política. Saiba mais sobre [imposição de política](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/enforcement/overview) no Experience Platform.

## Criptografia de dados no Commerce

O Adobe [!DNL Commerce] usa criptografia em nível de bloco. Para armazenamento, [!DNL Commerce] usa o Amazon Elastic Block Store (EBS). Todos os volumes EBS são criptografados usando o algoritmo AES-256, o que significa que os dados são criptografados em repouso. [!DNL Commerce] dados em trânsito são conduzidos em conexões seguras e criptografadas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

>[!IMPORTANT]
>
>A Commerce não oferece suporte à criptografia em nível de coluna ou linha quando os dados não estão em repouso ou não estão em trânsito entre servidores.

### Criptografia de dados no Experience Platform

Quando os comerciantes enviam seus dados para o Experience Platform, esses dados são enviados usando HTTPS TLS v1.2. Saiba mais sobre como o [Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/encryption) criptografa dados.

## Como o [!DNL Commerce] lida com solicitações de privacidade

Saiba como o [!DNL Commerce] [lida com solicitações de privacidade](handle-privacy-request.md).
