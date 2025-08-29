---
source-git-commit: 39977196f322cac571ecdb0219f006970aff3575
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---
# Ganchos de pré-confirmação para otimização de imagem

Esse diretório contém ganchos de pré-confirmação que otimizam automaticamente as imagens antes de serem confirmadas no repositório.

## O que os ganchos fazem

- **Detectar automaticamente** arquivos de imagem preparados (PNG, JPG, JPEG, GIF, SVG)
- **Execute`image_optim`** para compactar e otimizar imagens
- **Repreparar imagens otimizadas** automaticamente
- **Verifique se todas as imagens confirmadas** estão corretamente otimizadas

## Benefícios

- Tamanho reduzido do repositório
- Carregamentos de página mais rápidos para a documentação
- Qualidade de imagem consistente em todos os colaboradores
- Não é necessária otimização manual

## Pré-requisitos

- Ruby 3.0 ou superior
- Pacote
- Git

## Configuração

### Configuração automática (recomendada)

```bash
.githooks/setup-hooks.sh
```

### Configuração manual

```bash
git config core.hooksPath .githooks
chmod +x .githooks/*
```

### Concluir configuração do projeto

1. Clonar o repositório:

   ```bash
   git clone <repository-url>
   cd commerce-admin.en
   ```

2. Ativar ganchos de pré-confirmação:

   ```bash
   .githooks/setup-hooks.sh
   ```

3. Instalar dependências do Jekyll:

   ```bash
   cd _jekyll
   bundle install
   ```

## Teste dos ganchos

1. Adicionar um arquivo de imagem ao repositório
2. Preparo: `git add <image-file>`
3. Tentar confirmar: `git commit -m 'test'`
4. O gancho deve otimizar automaticamente a imagem

### Saída esperada

```bash
Found 1 staged image(s). Running optimization...
Optimizing: path/to/your/image.png
Re-staged optimized image: path/to/your/image.png
Image optimization complete!
```

## Diretrizes de imagem

- **PNG**: usar para capturas de tela e elementos da interface do usuário (será otimizado automaticamente)
- **SVG**: usar para ícones e elementos gráficos simples (otimização desabilitada por padrão)
- **JPEG**: usar para fotografias (será otimizado automaticamente)
- **GIF**: usar para animações (será otimizado automaticamente)

Os ganchos de pré-confirmação otimizarão automaticamente todas as imagens na confirmação.

## Otimização manual

Para otimização manual de imagens:

```bash
cd _jekyll
bundle exec rake images:optimize path=../path/to/images
```

## Configuração

Os ganchos usam o arquivo de configuração `_jekyll/.image_optim` para personalizar as configurações de otimização:

- **PNG**: usa `advpng`, `optipng` e `pngquant`
- **JPEG**: Usa `jhead`, `jpegoptim` e `jpegtran`
- **GIF**: Usa `gifsicle`
- **SVG**: a otimização para SVG está desabilitada por padrão (pode quebrar animações e gráficos vetoriais complexos)

## Solução de problemas

### Gancho não está em execução

- Verificar configuração de gancho: `git config core.hooksPath`
- Verifique se o arquivo de gancho é executável: `chmod +x .githooks/pre-commit`
- Verifique se você está no repositório correto com o diretório `_jekyll`

### Falhas de otimização

- Verificar se `bundle install` foi executado no diretório `_jekyll`
- Verifique se as gems `image_optim` e `image_optim_pack` estão instaladas
- Revise o arquivo de configuração `.image_optim`

### Problemas de desempenho

- Ajustar contagem de threads em `_jekyll/.image_optim`
- Defina a variável de ambiente `DEBUG=1` para obter informações detalhadas sobre o erro

## Como funciona

1. **Acionador de pré-confirmação**: quando você executa o `git commit`, o gancho é executado automaticamente
2. **Detecção de imagem**: verifica arquivos preparados em busca de extensões de imagem
3. **Otimização**: Executa `image_optim` em cada imagem preparada
4. **Repreparo**: adiciona automaticamente imagens otimizadas de volta à área de preparo
5. **Continuação da confirmação**: se a otimização tiver êxito, a confirmação continuará normalmente

## Formatos de imagem compatíveis

- **PNG** (`.png`) - Compactação sem perdas e com perdas
- **JPEG** (`.jpg`, `.jpeg`) - Compactação com perda com limpeza de metadados
- **GIF** (`.gif`) - Otimização de animação e estática
- **SVG** (`.svg`) - Otimização de vetor (desabilitada por padrão)

## Práticas recomendadas

1. **Testar o gancho**: tente confirmar uma imagem pequena primeiro para garantir que ela funcione
2. **Revisar alterações**: verifique a diferença do Git para ver os resultados da otimização
3. **Monitorar desempenho**: imagens grandes podem demorar para serem otimizadas
4. **Controle de versão**: ganchos são armazenados neste diretório `.githooks/`

## Suporte

Para problemas com os ganchos de pré-confirmação:

1. Verifique se há mensagens de erro na saída do gancho
2. Verifique se a configuração do `image_optim` está funcionando
3. Testar primeiro com as tarefas manuais do rake
4. Revise os registros e a configuração do gancho
5. Verifique a configuração do gancho: `git config core.hooksPath`
