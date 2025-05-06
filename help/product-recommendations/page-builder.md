---
title: Integração do [!DNL Page Builder]
description: Saiba como usar  [!DNL Product Recommendations]  unidades no Page Builder.
feature: Services, Recommendations, Page Builder
exl-id: 001e8e1d-3590-4b44-b5f8-dd8b9b61f370
badgePaas: label="Somente PaaS" type="Informative" url="https://experienceleague.adobe.com/pt-br/docs/commerce/user-guides/product-solutions" tooltip="Aplica-se somente a projetos do Adobe Commerce na nuvem (infraestrutura do PaaS gerenciada pela Adobe) e a projetos locais."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Integração do [!DNL Page Builder]

As Recomendações de produto podem ser integradas em qualquer conteúdo do Page Builder que você implanta no site.

>[!NOTE]
>
> Você pode ter até 25 unidades de recomendação em uma página nativa do Page Builder. As páginas não nativas do Page Builder podem ter até 5 unidades de recomendação. Consulte [Criar nova recomendação](create.md) para obter mais informações.

## Uso das recomendações de produto com conteúdo do Page Builder

1. Crie uma unidade de Recomendação na visualização de loja padrão de um site. Eles devem ser criados na exibição de loja padrão, mesmo que você planeje usá-los em diferentes exibições de loja.

   >[!NOTE]
   >
   >As métricas para unidades de recomendação do Page Builder aparecem somente na exibição de armazenamento padrão [!DNL Product Recommendations] do espaço de trabalho. Mesmo que você coloque uma unidade de recomendação do Page Builder em uma exibição de loja que não seja a exibição de loja padrão, as métricas relacionadas a essas unidades de recomendação do Page Builder não serão exibidas na exibição de loja não padrão [!DNL Product Recommendations] do espaço de trabalho. Para ver as métricas do Page Builder em um espaço de trabalho de exibição de repositório não padrão [!DNL Product Recommendations], abra e [edite](edit.md) a unidade de recomendação do Page Builder no modo de exibição de repositório não padrão e clique em [!UICONTROL **Salvar**]. As métricas do Page Builder agora aparecem no espaço de trabalho [!DNL Product Recommendations] na loja não padrão.

1. No Page Builder, selecione o widget de conteúdo das Recomendações de produto e coloque-o em seu site.

![Inserir unidade de recomendação](assets/pb-insert.png)

1. Clique em **Editar recomendação do produto**
1. Clique em **Selecionar**
1. Selecione a unidade de recomendação criada anteriormente e clique em **Adicionar seleção**

![Inserir unidade de recomendação](assets/pb-select.png)

1. Faça outras edições no conteúdo do Page Builder e salve as alterações.

No momento da renderização, o contexto e o escopo do conteúdo do Page Builder são respeitados pela unidade de recomendação.
