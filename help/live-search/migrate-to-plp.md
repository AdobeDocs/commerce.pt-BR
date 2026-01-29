---
title: Migração do adaptador de pesquisa para o Widget do PLP
description: Saiba como migrar do adaptador de pesquisa obsoleto para o  [!DNL Live Search] Widget de página de listagem de produtos.
source-git-commit: 8811f0f271928fbc827e5a0164542da473c57224
workflow-type: tm+mt
source-wordcount: '2053'
ht-degree: 0%

---

# Migração do Adaptador de Pesquisa para o Widget do PLP

O adaptador de pesquisa foi [descontinuado](release-notes.md#live-search-400) a partir de [!DNL Live Search] 4.0.0 e receberá apenas atualizações de segurança. O [Widget da PLP (Página de Listagem de Produtos)](plp-styling.md) é a solução com suporte para todas as implementações de [!DNL Live Search] a partir de agora. Este guia ajuda você a entender quando a migração é simples e quando trabalho adicional é necessário.

## Pré-requisitos

Verifique se o ambiente atende a esses requisitos antes de iniciar o processo de migração.

Antes de iniciar a migração:

**Requisitos técnicos**:

- Adobe Commerce 2.4.4 ou superior.
- Extensão [!DNL Live Search] instalada.
- Acesso à linha de comando (CLI).
- Acesso ao administrador do Commerce.
- Ambiente de preparo ou controle de qualidade para testes.

**Backup e preparação**:

1. Faça backup do banco de dados e do código.
1. Documentar as personalizações atuais.
1. Revise os [Limites e Limites](boundaries-limits.md) para garantir que o widget PLP atenda às suas necessidades.
1. Agendar migração durante um período de tráfego baixo.
1. Notifique as partes interessadas sobre possíveis alterações no comportamento da loja.

**Revise a implementação atual**:

- Verifique sua versão atual do [!DNL Live Search].
- Documente quais facetas estão em uso e suas configurações.
- Teste toda a funcionalidade de pesquisa e os comportamentos esperados do documento.
- Capture capturas de tela da apresentação de resultados da pesquisa atual.

**Compatibilidade de versão**:

- Execução do Adobe Commerce 2.4.4 ou mais recente.
- Pronto para atualizar para [!DNL Live Search] 4.0.0 ou superior.

## Cenários de migração

### Migração simples (não é necessário trabalho adicional)

Você pode migrar diretamente para o widget PLP se a sua implementação atender a TODOS os seguintes critérios:

**Loja padrão baseada em Luma**:

- Você está usando o tema Luma ou um tema que herda do Luma com personalizações mínimas.
- Você não fez modificações personalizadas em layouts ou modelos do PLP.
- Você não fez extensões personalizadas do JavaScript que interagem com os resultados da pesquisa.

**Catálogo de produtos padrão**:

- Todos os atributos de produto usam modelos de origem padrão (não modelos de origem personalizados).
- Não há tipos de produto personalizados que exijam uma lógica de renderização especial.
- Seu catálogo usa apenas facetas padrão e filtragem.

**Integrações padrão**:

- Você não está usando o Google Tag Manager (GTM) para análise.
- Você não está usando extensões de terceiros que modificam o comportamento da pesquisa.

Se sua implementação corresponder a estes critérios, prossiga para [Etapas de migração padrão](#standard-migration-steps).

### Migração que requer trabalho adicional

Será necessário trabalho adicional se sua implementação tiver QUALQUER UM dos seguintes itens:

**Modificações de tema personalizadas**:

- Layouts PLP personalizados que substituem modelos Luma.
- CSS ou JavaScript personalizados direcionados a elementos específicos do adaptador de pesquisa.
- Modificações de modelos personalizados no PLP ou em arquivos relacionados.
- O tema não é herdado do Luma (por exemplo, tema personalizado do zero).

**Atributos de produto personalizados**:

- Atributos de produto com modelos de origem personalizados usados como facetas.
- Tipos de produto personalizados com requisitos especiais de exibição.
- Atributos programáticos com `"is_user_defined": false`.

**Integrações avançadas**:

- O Gerenciador de tags da Google (GTM) é usado ativamente para rastreamento.
- Ferramentas de análise ou personalização de terceiros integradas à pesquisa.
- Rastreamento de evento personalizado ou implementação da camada de dados.
- Integração com mecanismos externos de pesquisa ou recomendação.

**Implementações headless ou PWA**:

- Uso de arquitetura headless (por exemplo, PWA Studio, Vue Storefront).
- Estrutura personalizada de front-end (React, Vue, Angular).
- Uso do GraphQL exclusivamente para consultas de catálogo.
- Implementação de eventos de vitrine personalizados.

**Código de widget personalizado**:

- Personalizado anteriormente o código do adaptador de pesquisa.
- Hospedagem de versões personalizadas de widgets em seu próprio CDN.
- Extensões personalizadas do JavaScript para funcionalidade de pesquisa.

Se sua implementação tiver um desses cenários, consulte [Cenários de migração complexos](#complex-migration-scenarios).

## Etapas de migração padrão

Para implementações sem personalizações especiais, siga estas etapas:

### Etapa 1: Atualizar [!DNL Live Search]

Atualize sua extensão do [!DNL Live Search] para a versão 4.0 ou superior para acessar o widget PLP.

**Função**: comerciante ou parceiro

1. Verifique sua versão atual do [!DNL Live Search]:

   ```bash
   composer show magento/live-search | grep version
   ```

1. Se a versão for 3.x ou anterior, habilite o módulo AdvancedSearch antes de atualizar:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

1. Atualize `composer.json` para exigir [!DNL Live Search] 4.0 ou superior:

   ```json
   "require": {
      "magento/live-search": "^4.0"
   }
   ```

1. Execute a atualização:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Execute a atualização e a recompilação da instalação:

   ```bash
   bin/magento setup:upgrade
   bin/magento setup:di:compile
   ```

1. Implante conteúdo estático, se necessário:

   ```bash
   bin/magento setup:static-content:deploy
   ```

### Etapa 2: Ativar o dispositivo PLP

Configure o widget PLP no Administrador do Commerce.

**Função**: Comerciante

O widget PLP é habilitado por padrão para novas instalações do [!DNL Live Search] 4.0.0+. Se estiver atualizando de uma versão anterior:

1. Vá para **[!UICONTROL Stores]** > Configurações > **[!UICONTROL Configuration]**.
1. Navegue até **[!UICONTROL Live Search]** > **[!UICONTROL Storefront Features]**.
1. Expanda a seção **[!UICONTROL Storefront Features]**.
1. Defina **[!UICONTROL Enable Product Listing Widgets]** como **Sim**.
1. Clique em **[!UICONTROL Save Config]**.
1. Liberar o cache: **[!UICONTROL System]** > Ferramentas > **[!UICONTROL Cache Management]** > **[!UICONTROL Flush Magento Cache]**.

### Etapa 3: testar no preparo

Valide a migração em um ambiente de não produção antes de ativá-la.

**Função**: comerciante/parceiro

Antes de implantar na produção, teste completamente a funcionalidade de pesquisa:

**Teste funcional**:

- Verifique se os resultados da pesquisa aparecem corretamente.
- Testar todas as facetas configuradas.
- Verifique se a navegação da categoria funciona.
- Teste a paginação por meio dos resultados.
- Verifique se as opções de classificação funcionam conforme esperado.
- Teste a funcionalidade do carrinho de compras para produtos simples.

**Teste visual**:

- Confirme se as imagens do produto são exibidas corretamente.
- Verifique se os nomes e os preços dos produtos são renderizados corretamente.
- Testar amostras de cores (se usadas).
- Verifique o comportamento responsivo em dispositivos móveis.
- Verifique se o estilo corresponde à sua marca.

**Teste de desempenho**:

- Meça o tempo de carregamento da página.
- Teste com tamanho de catálogo realista.
- Monitorar o uso de recursos do servidor.
- Verifique se há erros de JavaScript no console do navegador.

### Etapa 4: implantar para produção

Mova a configuração validada para sua loja online.

**Função**: comerciante/parceiro

1. Programe a implantação durante a janela de manutenção, se possível.
1. Siga o processo de implantação padrão.
1. Habilite o dispositivo PLP na produção usando [Etapa 2: habilitar o dispositivo PLP](#step-2-enable-the-plp-widget).
1. Monitore problemas imediatamente após a implantação.
1. Ter um plano de reversão pronto se surgirem problemas críticos.

### Etapa 5: validar e monitorar

Acompanhe o desempenho da pesquisa e a experiência do cliente após a migração.

**Função**: Comerciante

Após a implantação, monitorar as métricas principais:

- Taxa de pesquisa de resultados zero
- Taxa de conversão da pesquisa em carrinho
- Desempenho de carregamento de página
- Feedback do cliente ou tíquetes de suporte
- Erros do JavaScript no console do navegador

## Cenários de migração complexos

Os cenários a seguir exigem planejamento adicional, desenvolvimento personalizado ou suporte especializado além das etapas de migração padrão.

### Tema personalizado com modificações de layout

Nesse cenário, você tem modelos ou layouts personalizados que substituem o comportamento padrão da lista de produtos.

**Função**: desenvolvedor/parceiro

1. **Personalizações de auditoria**:
   - Documente todos os arquivos XML de layout personalizados no seu tema.
   - Revise todas as modificações do modelo personalizado nas páginas de listagem de produtos ou nos arquivos relacionados.
   - Identifique as classes CSS personalizadas usadas para estilo.
   - Documentar interações personalizadas do JavaScript.

1. **Migrar para personalizações baseadas em CSS**:
   - O widget PLP usa classes CSS específicas (consulte [guia de estilo PLP](plp-styling.md)).
   - Recrie personalizações visuais usando classes CSS do widget PLP.
   - Teste se os estilos personalizados se aplicam corretamente.

1. **Remover personalizações conflitantes**:
   - Remova o XML de layout que modifica a estrutura da lista de produtos.
   - Limpe o JavaScript que segmenta os elementos específicos do adaptador de pesquisa.
   - Atualizar substituições de modelo que estão em conflito com a renderização do widget.

1. **Testar completamente**:
   - Verifique se todas as personalizações visuais funcionam com o widget PLP.
   - Verifique se não há conflitos de layout.
   - Teste em todos os pontos de interrupção e dispositivos.

### Atributos de produto com modelos de origem personalizados

Nesse cenário, há facetas que usam atributos de produto com modelos de origem personalizados que não são compatíveis com o adaptador de pesquisa, mas são compatíveis com o widget PLP.

**Função**: Comerciante (Configuração de administrador)

1. **Identificar atributos afetados**:
   - Revise os atributos do produto usados como facetas.
   - Identificar qual usa modelos de origem personalizados.
   - Documentar a configuração atual das facetas.

1. **Atualizar e habilitar o widget PLP**:
   - Siga [Etapas de migração padrão](#standard-migration-steps).
   - O widget PLP suporta atributos de modelo de origem personalizados.

1. **Reconfigurar aspectos**:
   - Vá para **[!UICONTROL Marketing]** > SEO &amp; Search > **[!UICONTROL Live Search]**.
   - Revise a configuração das facetas para os atributos afetados.
   - Os aspectos de teste funcionam corretamente com modelos de origem personalizados.

1. **Validar**:
   - Testar a filtragem com facetas de modelo de origem personalizado.
   - Verifique se todos os valores de atributo aparecem corretamente.
   - Certifique-se de que o desempenho seja aceitável.

### Integração do Google Tag Manager (GTM)

Neste cenário, há um problema conhecido em que ativar o dispositivo PLP pode causar falha no GTM.

**Função**: Desenvolvedor/Parceiro + Engenharia de Cliente

**Opção 1: Continuar com o adaptador de pesquisa (apenas temporário)**

- Mantenha o adaptador de pesquisa ativado se o GTM for essencial para os negócios.
- Saiba que você só receberá atualizações de segurança.
- Planejar a migração quando a compatibilidade do GTM for resolvida.
- Entre em contato com o Suporte da Adobe para obter atualizações sobre a compatibilidade com o GTM.

**Opção 2: migrar o rastreamento GTM para uma abordagem alternativa**

1. **Implementar uma coleção de eventos personalizada**:

   - Use o [SDK de Eventos da Loja](https://developer.adobe.com/commerce/services/shared-services/storefront-events/).
   - Capture eventos de pesquisa e interação com o produto.
   - Enviar eventos para a camada de dados do GTM manualmente.

1. **Conclua as seguintes etapas**:

   - Auditoria de requisitos atuais de rastreamento do GTM.
   - Mapear eventos do GTM para Eventos da loja.
   - Implementar ouvintes de eventos personalizados.
   - Testar fluxo de dados para GTM.
   - Validar relatórios de análise.

**Opção 3: substituir o GTM pelo Adobe Analytics**

- Considere migrar para o [Adobe Analytics](https://business.adobe.com/products/adobe-analytics.html), se aplicável.
- Entre em contato com o departamento de engenharia de clientes para obter orientação.

**Com quem entrar em contato**: envie um tíquete de suporte para obter atualizações de compatibilidade do GTM ou assistência de engenharia do cliente.

### Cenário: implementação headless ou PWA

Neste cenário, você tem uma loja headless ou PWA que requer uma coleção de eventos personalizada e não pode usar a interface de widget PLP padrão.

**Função**: desenvolvedor/parceiro

1. **Revisar implementações de referência**:
   - Estude o [código-fonte do widget PLP](https://github.com/adobe/storefront-product-listing-page).
   - Consulte a documentação da API do [[!DNL Live Search] GraphQL](graphql.md).
   - Compreender as [consultas do Serviço de Catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).

1. **Implementar uma interface personalizada**:
   - Use a API do GraphQL [!DNL Live Search] para consultas.
   - Criar componentes personalizados de lista de produtos.
   - Implemente a interface do usuário para facetas.
   - Lidar com paginação e classificação.

1. **Implementar coleção de eventos**:
   - Revise a [documentação de Eventos da vitrine](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search).
   - Implemente os eventos necessários:
      - `search-request-sent`
      - `search-response-received`
      - `search-results-view`
      - `product-page-view`
      - `add-to-cart`
   - Testar o fluxo de dados do evento para o Adobe Commerce.

1. **Configurar classificação de facetas**:
   - Para implementações headless, as facetas podem ser classificadas por contagem.
   - Configurar no **[!UICONTROL Live Search]** > **[!UICONTROL Facets]** espaço de trabalho.
   - Defina **[!UICONTROL Sort Type]** como **Count** para um UX melhor.

1. **Teste e validação**:
   - Verifique a precisão dos resultados da pesquisa.
   - Funcionalidade de faceta de teste.
   - Confirme se os eventos estão sendo rastreados corretamente.
   - Monitorar métricas de desempenho.
   - Validar o funcionamento de recursos de merchandising inteligentes.

### Cenário: modificações no código do widget personalizado

Nesse cenário, você personalizou anteriormente o adaptador de pesquisa ou código do widget e precisa migrar as personalizações.

**Função**: desenvolvedor/parceiro

1. **Personalizações existentes do documento**:
   - Listar todas as personalizações feitas no adaptador de pesquisa.
   - Identificar os requisitos de negócios que orientam cada personalização.
   - Determine se as personalizações ainda são necessárias.

1. **Verifique se os recursos internos atendem às suas necessidades**:
   - Revise os [recursos do widget PLP](plp-styling.md#widget-features).
   - Verifique se a personalização baseada em CSS é suficiente.
   - Testar o comportamento padrão do dispositivo PLP.

1. **Se o código personalizado ainda for necessário**:
   - Clona o [repositório de widgets PLP](https://github.com/adobe/storefront-product-listing-page).
   - Implemente suas personalizações.
   - Hospede em seu próprio CDN.
   - Atualize a configuração do Commerce para usar o widget personalizado.

   >[!WARNING]
   >
   >Se você personalizar o widget PLP usando o código do repositório, será responsável pela manutenção e atualizações. Os novos recursos de widget PLP do Adobe podem ser incompatíveis com suas personalizações.

1. **Testar completamente**:
   - Teste toda a funcionalidade personalizada.
   - Verifique se as atualizações do Commerce não interrompem as personalizações.
   - Documente sua implementação personalizada.
   - Planeje a manutenção contínua.

## Limitações conhecidas e casos de borda

Esteja ciente dessas limitações ao migrar:

**Limitações do widget PLP**:

- **Direção da ordem de classificação**: quando o widget PLP está habilitado, a direção da ordem de classificação nas páginas de listagem de produtos não pode ser alterada (crescente/decrescente).
- **Adicionar ao carrinho**: os botões Adicionar ao carrinho só estão disponíveis para produtos simples no widget.
- **Preços de camada**: não suportado no widget PLP.
- **Exibição de VAT**: os preços incluem VAT, mas VAT não pode ser exibido como um valor separado.

**Diferenças de recursos do adaptador de pesquisa**:

- **Amostras de cor**: o atributo `color` deve ser escrito exatamente como `color` (não &quot;cor&quot; ou nomes personalizados) para que as amostras funcionem corretamente.
- **Estilo do tema**: as classes de tema personalizadas não são herdadas pelo widget; devem ter como alvo as classes CSS específicas do widget.
- **Tipos de produto personalizados**: não há suporte no widget.

**Considerações sobre desempenho**:

- Catálogos grandes (mais de 50.000 produtos) podem enfrentar carregamentos de página iniciais mais longos.
- Várias facetas com muitos valores podem afetar o desempenho.
- O desempenho do dispositivo móvel pode variar de acordo com o tamanho do catálogo.

**Problemas de compatibilidade**:

- Problema de compatibilidade do Google Tag Manager (consulte [Cenário de GTM](#google-tag-manager-gtm-integration)).
- Algumas extensões de terceiros podem entrar em conflito com o widget PLP.
- As extensões de check-out personalizadas podem precisar de atualizações.

## Obtendo ajuda

Entre em contato com o recurso apropriado com base em suas necessidades específicas.

O **Suporte da Adobe** pode ajudar com:

- Procedimentos de migração padrão do Live Search
- Problemas de configuração do dispositivo PLP
- Problemas de indexação de facetas ou atributos
- Problemas de desempenho com implementações padrão
- Erros de atualização

**Parceiros de desenvolvimento/integradores de sistemas** devem ser contatados para:

- Modificações de tema personalizadas
- Implementações de código de widget personalizado
- Compatibilidade com extensões de terceiros
- Implementações headless ou PWA
- Rastreamento de evento personalizado

Para contatar o Suporte da Adobe, consulte o [Guia do Usuário da Central de Ajuda](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).

## Perguntas frequentes

Encontre respostas para perguntas comuns sobre a migração do adaptador de pesquisa para o widget PLP.

**P: O adaptador de pesquisa receberá correções de erros ou atualizações de recursos?**

R: Não. O adaptador de pesquisa está obsoleto e só receberá atualizações de segurança. Correções de erros, melhorias de desempenho e novos recursos só estão disponíveis no widget PLP. Se você encontrar problemas com o adaptador de pesquisa, a migração para o dispositivo PLP é a solução recomendada.

**P: a migração interromperá minha loja?**

R: Se você seguir os procedimentos de teste adequados no preparo, a migração deverá ser contínua. Ter um plano de reversão pronto para a implantação em produção.

**P: Quanto tempo leva a migração?**

R: Para implementações padrão: 1 a 2 horas. Para implementações personalizadas: 1 a 4 semanas, dependendo da complexidade.

**P: minhas regras de merchandising de pesquisa ainda funcionarão?**

R: Sim, todas as regras de merchandising de pesquisa, sinônimos e aspectos configurados no espaço de trabalho [!DNL Live Search] continuam a funcionar com o widget PLP.

**P: Preciso reconfigurar minhas facetas?**

R: Geralmente não, mas se você estava limitado por atributos de modelo de origem personalizados com o adaptador de pesquisa, agora é possível usá-los com o widget PLP.

**P: E quanto ao meu CSS personalizado?**

R: Você precisa atualizar o CSS para direcionar as classes de widget do PLP. Consulte a [referência de classes CSS](plp-styling.md#css-classes).

**P: Isso afetará meu desempenho de pesquisa?**

R: O dispositivo PLP foi projetado para ter desempenho. A maioria dos comerciantes vê um desempenho igual ou melhor. Catálogos grandes devem ser testados no preparo.
