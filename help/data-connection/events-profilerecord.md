---
title: Registros de perfil
description: Saiba quais dados um registro de perfil captura.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection] Registros do Perfil

A tabela a seguir descreve os dados de registro de perfil do Commerce que estão disponíveis quando você instala a extensão [!DNL Data Connection]. Os dados nos registros de perfil são enviados para a Adobe Experience Platform.

## Registro de perfil

As atualizações de registro de perfil estão disponíveis na Experience Platform quando um novo perfil é criado, atualizado ou excluído.

### Dados coletados do registro do perfil

A seguir estão os dados capturados para um registro de perfil.

| Campo | Descrição |
|---|---|
| `channel` | Contém informações sobre a fonte de dados. `_id` e `_type` contêm [valores com namespace](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/schema/namespaces). |
| `channel._id` | O identificador exclusivo do canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica a origem dos dados do canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Contém informações sobre o cliente. |
| `person.name` | Contém informações sobre o nome do cliente. |
| `person.name.firstName` | Contém o nome do cliente. |
| `person.name.lastName` | Contém o sobrenome do cliente. |
| `person.birthDate` | Data de nascimento do comprador. |
| `personalEmail` | Um endereço de email pessoal. |
| `personalEmail.address` | O endereço técnico, por exemplo, `name@domain.com`, conforme comumente definido em RFC2822 e padrões subsequentes. |
| `billingAddress` | O endereço postal de cobrança. |
| `billingAddress.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua. |
| `billingAddress.street2` | Segunda linha opcional de informações da rua. |
| `billingAddress.city` | O nome da cidade. |
| `billingAddress.state` | O nome do estado. Este é um campo de forma livre. |
| `billingAddress.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `billingAddress.primary` | Indica se este é o endereço de cobrança principal. O valor é sempre `False`. |
| `billingAddressPhone` | O número de telefone associado ao endereço de cobrança. |
| `billingAddressPhone.number` | O telefone. Observe que o número de telefone é uma cadeia de caracteres e pode incluir caracteres significativos, como colchetes `()`, hifens `-` ou caracteres para indicar identificadores de submarcação como extensões `x`, por exemplo, `1-353(0)18391111` ou `+613 9403600x1234`. |
| `billingAddressPhone.primary` | Indica se este é o número de telefone principal do endereço de cobrança. O valor é sempre `False`. |
| `shippingAddress` | O endereço postal de remessa. |
| `shippingAddress.street1` | Informações no nível da rua principal, número do apartamento, número da rua e nome da rua. |
| `shippingAddress.street2` | Segunda linha opcional de informações da rua. |
| `shippingAddress.city` | O nome da cidade. |
| `shippingAddress.state` | O nome do estado. Este é um campo de forma livre. |
| `shippingAddress.country` | O nome do território administrado pelo governo. Além de `xdm:countryCode`, este é um campo de forma livre que pode ter o nome do país em qualquer idioma. |
| `shippingAddress.primary` | Indica se este é o endereço de entrega principal. O valor é sempre `False`. |
| `shippingAddressPhone` | O número de telefone associado ao endereço para entrega. |
| `shippingAddressPhone.number` | O telefone. Observe que o número de telefone é uma cadeia de caracteres e pode incluir caracteres significativos, como colchetes `()`, hifens `-` ou caracteres para indicar identificadores de submarcação como extensões `x`, por exemplo, `1-353(0)18391111` ou `+613 9403600x1234`. |
| `shippingAddressPhone.primary` | Indica se este é o número de telefone principal do endereço para entrega. O valor é sempre `False`. |
| `userAccount` | Indica detalhes de fidelidade, preferências, processos de logon e outras preferências de conta. |
| `userAccount.startDate` | A data em que o perfil foi criado pela primeira vez. |

>[!NOTE]
>
>Cada registro de perfil também inclui o campo [`identityMap`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/field-groups/profile/identitymap), que inclui a ID de cliente da Commerce gerada pelo sistema como o identificador principal do perfil e uma ID de email usada como um identificador secundário.

Saiba como [criar um esquema específico de registro de perfil](profile-data.md) que possa assimilar os dados de seus registros de perfil.
