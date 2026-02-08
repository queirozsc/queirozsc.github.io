# 📝 Guia Completo: Publicar Artigos com Jekyll Chirpy

## 🎯 Visão Geral

O Jekyll Chirpy é um tema moderno e elegante para blogs técnicos e profissionais. Vamos integrar um blog na seção "Artigos" do seu site.

## 📋 Pré-requisitos

Antes de começar, você precisa instalar:

### Windows:

1. **Ruby + Devkit**:
   - Baixe: [rubyinstaller.org](https://rubyinstaller.org/downloads/)
   - Escolha: Ruby+Devkit 3.2.X (x64)
   - Execute o instalador
   - Marque "Add Ruby to PATH"
   - No final, execute `ridk install` e escolha opção 3

2. **Verifique a instalação**:
   ```bash
   ruby -v
   gem -v
   ```

### macOS:

```bash
# Instale Homebrew (se não tiver)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Instale Ruby
brew install ruby

# Adicione ao PATH
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

### Linux (Ubuntu/Debian):

```bash
sudo apt-get update
sudo apt-get install ruby-full build-essential zlib1g-dev

# Adicione ao PATH
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## 🚀 Opção 1: Configuração Rápida (Recomendada)

### Passo 1: Usar o Template do Chirpy

1. Acesse: [github.com/cotes2020/chirpy-starter](https://github.com/cotes2020/chirpy-starter)
2. Clique em **"Use this template"** > **"Create a new repository"**
3. Nome do repositório: `blog`
4. Marque como **Public**
5. Clique em **"Create repository"**

### Passo 2: Clonar e Configurar Localmente

```bash
# Clone seu repositório
git clone https://github.com/seu-usuario/blog.git
cd blog

# Instale as dependências
bundle install

# Execute localmente para testar
bundle exec jekyll serve

# Acesse: http://localhost:4000
```

### Passo 3: Editar Configurações

Abra o arquivo `_config.yml` e edite:

```yaml
lang: pt-BR
timezone: America/La_Paz

title: Sergio Carvalho Queiroz Blog
tagline: Insights sobre Dados, Analytics e Transformação Digital
description: >-
  Blog profissional compartilhando conhecimento sobre Data Analytics,
  Business Intelligence, Transformação Digital e muito mais.

url: "https://seu-usuario.github.io"
baseurl: "/blog"

github:
  username: seu-usuario

social:
  name: Sergio Carvalho Queiroz
  email: queirozsc@gmail.com
  links:
    - https://www.linkedin.com/in/queirozsc/

avatar: /assets/img/avatar.png
```

### Passo 4: Adicionar Sua Foto

```bash
# Crie a pasta de assets
mkdir -p assets/img

# Copie sua foto
cp caminho/para/Gemini_Generated_Image_3n09fq3n09fq3n09.png assets/img/avatar.png
```

## ✍️ Como Criar um Novo Artigo

### Método 1: Manual

1. **Crie um arquivo na pasta `_posts`**:
   - Nome: `YYYY-MM-DD-titulo-do-artigo.md`
   - Exemplo: `2025-02-08-governanca-dados-saude.md`

2. **Adicione o Front Matter**:

```markdown
---
title: "Governança de Dados no Setor de Saúde: Guia Completo"
date: 2025-02-08 10:00:00 -0400
categories: [Data Governance, Healthcare]
tags: [dados, governança, saúde, hospital]
author: sergio
image:
  path: /assets/img/posts/governanca-dados.png
  alt: "Governança de Dados em Saúde"
---

## Introdução

Neste artigo, compartilho minha experiência implementando governança...

## Por que é Crítica?

1. **Qualidade dos Dados**
2. **Segurança**
3. **Conformidade**

```python
def validar_dados(dados):
    return True
```

## Conclusão

A governança não é opcional...
```

### Método 2: Usando Jekyll Compose

```bash
# Instale
bundle add jekyll-compose

# Crie novo post
bundle exec jekyll post "Título do Artigo"

# Crie rascunho
bundle exec jekyll draft "Título"

# Publique rascunho
bundle exec jekyll publish _drafts/titulo.md
```

## 📁 Estrutura de Pastas

```
blog/
├── _posts/                    # Artigos publicados
│   └── 2025-02-08-artigo.md
├── _drafts/                   # Rascunhos
├── _tabs/                     # Páginas
│   ├── about.md
│   └── archives.md
├── assets/
│   └── img/
│       ├── avatar.png
│       └── posts/
├── _config.yml
└── Gemfile
```

## 🎨 Front Matter Completo

```yaml
---
title: Título                      # OBRIGATÓRIO
date: 2025-02-08 10:30:00 -0400   # OBRIGATÓRIO
categories: [Cat1, Cat2]           # Máx 2
tags: [tag1, tag2]                 # Ilimitadas
author: sergio
image:
  path: /assets/img/posts/img.png
  alt: Texto alternativo
pin: true                          # Fixar no topo
math: true                         # Fórmulas matemáticas
mermaid: true                      # Diagramas
---
```

## 🚀 Publicar no GitHub Pages

### GitHub Actions (Recomendado)

1. **Settings > Pages > Source: GitHub Actions**

2. **Crie `.github/workflows/pages-deploy.yml`**:

```yaml
name: "Build and Deploy"
on:
  push:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: 3.2
          bundler-cache: true

      - name: Build
        run: bundle exec jekyll b
        env:
          JEKYLL_ENV: production

      - name: Upload
        uses: actions/upload-pages-artifact@v3

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Deploy
        uses: actions/deploy-pages@v4
```

3. **Commit e push**:

```bash
git add .
git commit -m "Setup deployment"
git push
```

4. **Acesse**: `https://seu-usuario.github.io/blog`

## 🔗 Integrar com Site Principal

No `index.html`, o menu "Artigos" já está configurado.

Se blog em repositório separado, atualize:

```html
<li><a href="https://seu-usuario.github.io/blog">Artigos</a></li>
```

## 📝 Exemplos de Artigos

### Tutorial Técnico

```markdown
---
title: "Power BI: 5 DAX Patterns Essenciais"
date: 2025-02-10 14:00:00 -0400
categories: [BI, Tutorial]
tags: [powerbi, dax, analytics]
---

## Pattern 1: Time Intelligence

```dax
Sales YTD = 
CALCULATE(
    [Total Sales],
    DATESYTD('Calendar'[Date])
)
```
```

### Case Study

```markdown
---
title: "Governança de Dados: Case Clínica de las Américas"
date: 2025-02-15 10:00:00 -0400
categories: [Data Governance, Healthcare]
tags: [governança, case-study]
pin: true
---

Neste case, compartilho como estabelecemos governança...
```

## 🔧 Comandos Úteis

```bash
# Servidor local
bundle exec jekyll serve

# Com rascunhos
bundle exec jekyll serve --drafts

# Build produção
JEKYLL_ENV=production bundle exec jekyll build

# Novo post
bundle exec jekyll post "Título"

# Limpar cache
bundle exec jekyll clean
```

## 📊 Google Analytics

No `_config.yml`:

```yaml
google_analytics:
  id: 'G-XXXXXXXXXX'
```

## 🎨 Personalizar Cores

Edite `assets/css/style.scss`:

```scss
:root {
  --heading-color: #0066cc;
  --link-color: #00a3e0;
}
```

## ✅ Checklist de Publicação

- [ ] Ruby instalado
- [ ] Repositório criado no GitHub
- [ ] `_config.yml` configurado
- [ ] Avatar adicionado
- [ ] Primeiro artigo criado
- [ ] Testado localmente
- [ ] GitHub Actions configurado
- [ ] Deploy realizado
- [ ] Site acessível online
- [ ] Link integrado no site principal

## 🆘 Solução de Problemas

**Erro de bundle**:
```bash
bundle update
bundle install
```

**Servidor não inicia**:
```bash
bundle exec jekyll clean
bundle exec jekyll serve
```

**Build falha no GitHub**:
- Verifique logs em "Actions"
- Confirme `_config.yml` correto
- Verifique formato de datas nos posts

## 📚 Recursos

- [Documentação Chirpy](https://chirpy.cotes.page/)
- [Jekyll Docs](https://jekyllrb.com/docs/)
- [Markdown Guide](https://www.markdownguide.org/)

---

**Pronto para começar! 🚀**
