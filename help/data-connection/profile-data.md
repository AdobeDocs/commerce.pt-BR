---
title: Atualizar esquema de registro de perfil para assimilação de dados do Commerce
description: Saiba como criar um esquema, conjunto de dados e sequência de dados para coletar e enviar dados de registro de perfil do Commerce para a Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Atualizar esquema de registro de perfil para assimilação de dados do Commerce

Quando os compradores criam um perfil no site do Commerce, um registro de perfil é criado e os dados são capturados. Você deve criar um esquema e um conjunto de dados específicos para esse registro de perfil antes de poder transmitir esses dados de perfil para a Experience Platform.

1. [Crie](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas) um esquema e defina a classe como **Perfil Individual**.

1. [Adicione](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas) os seguintes grupos de campos específicos de perfil:

   - identityMap
   - Detalhes demográficos
   - Detalhes de contato pessoal
   - Detalhes da conta do usuário

1. [Habilitar](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas) o esquema para o Perfil.

   Quando um esquema é ativado para o Perfil, qualquer conjunto de dados criado a partir desse esquema participa do Real-Time CDP, que mescla dados de fontes diferentes para criar uma visualização completa de cada cliente.

1. [Crie um conjunto de dados](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform) com base no esquema que você criou ou atualizou.

   Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

1. Crie um [namespace personalizado](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces#create-namespaces) no Experience Platform com os seguintes valores:

   - **Nome para Exibição**: _ID de Cliente da Commerce_
   - **Símbolo de Identidade**: _CustomerId_
   - **Tipo**: _ID entre dispositivos individuais_

   ![Criar namespace personalizado](assets/custom-namespace.png){width="700" zoomable="yes"}

   Clique em **[!UICONTROL Create]**. Um namespace personalizado é usado pelo Serviço de perfil unificado para unir fragmentos de perfil.

Com o esquema, o conjunto de dados e o namespace personalizado configurados para os dados de registro do perfil do cliente, você pode [configurar](connect-data.md#data-collection) sua instância do Commerce para coletar e enviar esses dados para a Experience Platform.

Para criar um esquema, conjunto de dados e sequência de dados para dados de evento comportamentais e de back office, consulte [atualizar esquemas de evento de série temporal para assimilação de dados do Commerce](update-xdm.md).
