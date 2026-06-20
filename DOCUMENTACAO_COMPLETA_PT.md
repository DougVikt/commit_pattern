# Documentação Completa sobre Commits Git
---

## Índice

1. [O que é um Commit](#1-o-que-é-um-commit)
2. [Para que serve um Commit](#2-para-que-serve-um-commit)
3. [Por que usar padronização (Conventional Commits)](#3-por-que-usar-padronização-conventional-commits)
4. [Estrutura Padrão do Conventional Commits](#4-estrutura-padrão-do-conventional-commits)
5. [Tabela Completa de Tipos Oficiais](#5-tabela-completa-de-tipos-oficiais)
6. [Explicação Detalhada de Cada Tipo](#6-explicação-detalhada-de-cada-tipo)
   - [6.1 feat (Feature)](#61-feat-feature)
   - [6.2 fix (Bug Fix)](#62-fix-bug-fix)
   - [6.3 docs (Documentation)](#63-docs-documentation)
   - [6.4 style](#64-style)
   - [6.5 refactor](#65-refactor)
   - [6.6 perf (Performance)](#66-perf-performance)
   - [6.7 test](#67-test)
   - [6.8 build](#68-build)
   - [6.9 ci (Continuous Integration)](#69-ci-continuous-integration)
   - [6.10 chore](#610-chore)
   - [6.11 revert](#611-revert)
7. [Breaking Changes (Mudanças Disruptivas)](#7-breaking-changes-mudanças-disruptivas)
8. [Escopo (Scope)](#8-escopo-scope)
9. [Tipos Customizados Usados por Empresas](#9-tipos-customizados-usados-por-empresas)
10. [Tabela de Decisão Rápida](#10-tabela-de-decisão-rápida)
11. [Exemplo de Histórico Profissional](#11-exemplo-de-histórico-profissional)
12. [Benefícios da Convenção](#12-benefícios-da-convenção)
13. [Como Configurar no Seu Projeto](#13-como-configurar-no-seu-projeto)
14. [Ferramentas de Validação Automática (Git Hooks)](#14-ferramentas-de-validação-automática-git-hooks)
15. [Extensões VS Code para Ajuda e Automação](#15-extensões-vs-code-para-ajuda-e-automação)

---

## 1. O que é um Commit

No Git puro não existe uma lista oficial de "tipos de commit". Um commit é uma **captura instantânea (snapshot) das alterações do projeto** em um determinado momento. Cada commit registra quem fez a alteração, quando foi feita e uma mensagem descritiva sobre o que foi alterado.

O padrão mais adotado atualmente é o **Conventional Commits**, utilizado por projetos open source, GitHub, GitLab, Azure DevOps, Semantic Release, Commitlint e diversas empresas.

---

## 2. Para que serve um Commit

- Registrar o histórico de alterações do projeto
- Documentar **o que** foi alterado e **por quê**
- Permitir rastreabilidade de bugs, features e decisões técnicas
- Facilitar a colaboração entre membros da equipe
- Servir como base para automação de changelogs e versionamento semântico

---

## 3. Por que usar padronização (Conventional Commits)

1. **Automação**: Ferramentas como o Semantic Release podem ler os commits e decidir se devem subir a versão do projeto (Patch, Minor ou Major) automaticamente.
2. **Histórico Limpo**: Permite que qualquer desenvolvedor novo entenda o que aconteceu no projeto apenas lendo os tipos de commit.
3. **Busca Facilitada**: Se você precisa encontrar quando uma dependência foi atualizada, basta filtrar por `git log --grep="build"`.
4. **Geração de Changelog**: É possível gerar um arquivo CHANGELOG.md em segundos, listando todas as novas funcionalidades (feat) e correções (fix) desde a última versão.
5. **Melhor legibilidade do `git log`**.
6. **Facilita code reviews e onboarding**.
7. **Integração com ferramentas como Commitlint, Husky, etc.**

Em empresas e organizações sérias, ninguém usa "atualizei a tela" ou "arrumei o bug". O uso desses prefixos permite que o time saiba exatamente o que o outro fez sem precisar ler o código, permite a geração automática de logs de atualização (Changelogs) e acionam ou não processos de deploy contínuo (CI/CD).

---

## 4. Estrutura Padrão do Conventional Commits

```
<tipo>(escopo): descrição

[corpo opcional]

[rodapé opcional]
```

Formato estendido:

```
<tipo>[escopo opcional]!: <descrição>

[corpo opcional]

[rodapé(s) opcional(is)]
```

**Exemplo básico:**

```bash
feat(auth): adicionar login com Google
```

**Exemplo completo:**

```bash
feat: alterar formato de resposta da API

BREAKING CHANGE: o campo 'user_id' agora se chama 'uuid'.
```

### Referenciando Issues

Em ambientes profissionais, é comum linkar o commit a uma tarefa (Jira, GitHub Issues).

```bash
fix: corrigir erro de arredondamento (#123)
```

---

## 5. Tabela Completa de Tipos Oficiais

**Observação:** `feat` e `fix` têm impacto direto no SemVer (minor e patch). BREAKING CHANGE (ou `!` após o tipo) indica mudança incompatível (major). Outros tipos são permitidos e recomendados pela convenção Angular (a mais comum).

| Tipo | Para que serve? (Escopo / Objetivo) | Impacto no SemVer | Exemplo Prático de Mensagem |
|------|-------------------------------------|-------------------|-----------------------------|
| **`feat`** | Introduz uma **nova funcionalidade** no código (equivalente a uma nova *feature*) | Minor (ex: 1.2.0 → 1.3.0) | `feat(auth): adiciona login com Google` |
| **`fix`** | **Corrige um bug** ou problema encontrado no sistema | Patch (ex: 1.2.3 → 1.2.4) | `fix(api): corrige erro 500 ao salvar agendamento` |
| **`docs`** | Alterações **apenas na documentação** (Markdown, README, docstrings, wikis) | Nenhum | `docs(readme): atualiza instruções de instalação com Docker` |
| **`style`** | Mudanças que **não afetam o sentido do código** (formatação, espaços, ponto e vírgula, linting). *Não confunda com CSS!* | Nenhum | `style(templates): corrige indentação e remove espaços extras` |
| **`refactor`** | Uma alteração no código que **nem corrige um bug nem adiciona uma feature** (melhoria de performance, legibilidade, arquitetura) | Nenhum | `refactor(services): centraliza lógica de validação de datas` |
| **`perf`** | Uma mudança de código que serve estritamente para **melhorar a performance/desempenho** | Nenhum | `perf(db): adiciona índice na tabela de consultas` |
| **`test`** | Adiciona testes que faltavam ou **corrige/modifica testes existentes** | Nenhum | `test(views): adiciona testes unitários para o fluxo de checkout` |
| **`build`** | Mudanças que afetam o **sistema de construção** (build), ferramentas de compilação ou dependências externas (ex: Poetry, npm, Dockerfile) | Nenhum | `build(poetry): adiciona biblioteca django-cors-headers` |
| **`ci`** | Alterações em arquivos e scripts de **Configuração de Integração Contínua** (ex: GitHub Actions, GitLab CI, Travis) | Nenhum | `ci(github): adiciona step de lint no workflow de pull request` |
| **`chore`** | Tarefas rotineiras de manutenção que **não modificam arquivos de produção ou testes** (ex: atualizar `.gitignore`, tarefas de deploy manuais) | Nenhum | `chore(gitignore): adiciona pastas do VS Code (.vscode)` |
| **`revert`** | Indica o **refluxo ou reversão** de um commit anterior que causou problemas | Nenhum (geralmente segue o commit revertido) | `revert: feat(auth): adiciona login com Google` |

Esses são os tipos recomendados pela especificação Conventional Commits e pela convenção Angular.

---

## 6. Explicação Detalhada de Cada Tipo

### 6.1 feat (Feature)

**Objetivo:** Adicionar uma nova funcionalidade para o usuário.

**Quando usar:**
- ✅ Nova tela
- ✅ Nova API
- ✅ Novo endpoint
- ✅ Novo componente

**Exemplos:**

```bash
feat(cart): adicionar carrinho de compras
```

```bash
feat(auth): implementar login com Google
```

```bash
feat(api): criar endpoint de exportação CSV
```

---

### 6.2 fix (Bug Fix)

**Objetivo:** Corrigir comportamentos incorretos.

**Quando usar:**
- ✅ Corrigir erro
- ✅ Corrigir validação
- ✅ Corrigir exceção
- ✅ Corrigir lógica

**Exemplos:**

```bash
fix(auth): corrigir expiração do token
```

```bash
fix(cart): impedir itens duplicados
```

```bash
fix(payment): corrigir cálculo de desconto
```

---

### 6.3 docs (Documentation)

**Objetivo:** Alterar apenas documentação.

**Quando usar:**
- ✅ README
- ✅ Wiki
- ✅ Swagger/OpenAPI
- ✅ Comentários explicativos

**Exemplos:**

```bash
docs(readme): adicionar instruções docker
```

```bash
docs(api): documentar endpoint de usuários
```

```bash
docs: corrigir exemplos de uso
```

---

### 6.4 style

**Objetivo:** Alterações visuais no código sem mudar comportamento.

**Quando usar:**
- ✅ Espaçamento
- ✅ Identação
- ✅ Quebra de linhas
- ✅ Organização visual

**Exemplos:**

```bash
style: corrigir formatação do projeto
```

```bash
style(component): alinhar imports
```

```bash
style(css): reorganizar regras de estilo
```

---

### 6.5 refactor

**Objetivo:** Melhorar estrutura do código sem alterar comportamento.

**Quando usar:**
- ✅ Extrair métodos
- ✅ Separar classes
- ✅ Melhorar arquitetura
- ✅ Reduzir duplicação

**Exemplos:**

```bash
refactor(auth): separar regras de autenticação
```

```bash
refactor(order): extrair service de pagamento
```

```bash
refactor(api): reorganizar controllers
```

---

### 6.6 perf (Performance)

**Objetivo:** Melhorar desempenho.

**Quando usar:**
- ✅ Queries lentas
- ✅ Cache
- ✅ Algoritmos mais eficientes
- ✅ Menor consumo de memória

**Exemplos:**

```bash
perf(database): otimizar consulta de clientes
```

```bash
perf(cache): adicionar cache redis
```

```bash
perf(images): reduzir tempo de carregamento
```

---

### 6.7 test

**Objetivo:** Adicionar ou corrigir testes.

**Quando usar:**
- ✅ Testes unitários
- ✅ Testes integração
- ✅ Testes E2E

**Exemplos:**

```bash
test(auth): adicionar testes de autenticação
```

```bash
test(api): cobrir endpoint de usuários
```

```bash
test(payment): corrigir cenário de pagamento recusado
```

---

### 6.8 build

**Objetivo:** Mudanças no sistema de build.

**Quando usar:**
- ✅ Maven
- ✅ Gradle
- ✅ Webpack
- ✅ Vite
- ✅ Dependências

**Exemplos:**

```bash
build: atualizar dependências
```

```bash
build(npm): atualizar react para v19
```

```bash
build(docker): otimizar imagem da aplicação
```

---

### 6.9 ci (Continuous Integration)

**Objetivo:** Alterar pipelines automatizados.

**Quando usar:**
- ✅ GitHub Actions
- ✅ GitLab CI
- ✅ Jenkins
- ✅ Azure Pipelines

**Exemplos:**

```bash
ci: adicionar etapa de testes
```

```bash
ci(github): configurar deploy automático
```

```bash
ci(jenkins): corrigir pipeline de build
```

---

### 6.10 chore

**Objetivo:** Tarefas que não afetam funcionalidades.

**Quando usar:**
- ✅ Configurações
- ✅ Scripts
- ✅ Atualizações simples
- ✅ Limpeza

**Exemplos:**

```bash
chore: atualizar versão do node
```

```bash
chore: remover arquivos temporários
```

```bash
chore(config): ajustar eslint
```

---

### 6.11 revert

**Objetivo:** Desfazer commit anterior.

**Quando usar:**
- ✅ Reverter feature
- ✅ Reverter bug
- ✅ Reverter deploy problemático

**Exemplos:**

```bash
revert: feat(auth): login via Google
```

```bash
revert: fix(api): correção de cache
```

---

## 7. Breaking Changes (Mudanças Disruptivas)

Quando uma alteração quebra a compatibilidade com o que já existia (ex: mudar o nome de um campo crucial no banco), adicionamos uma exclamação `!` após o tipo ou uma nota no rodapé do commit.

Isso indica aumento de versão MAJOR (1.x → 2.x).

### Forma 1 — Com exclamação `!`

```bash
git commit -m "feat(api)!: altera a estrutura de retorno do JSON de autenticação"
```

```bash
feat!: remover endpoint legado
```

### Forma 2 — Com `BREAKING CHANGE` no rodapé

```bash
feat(api): remover endpoint legado

BREAKING CHANGE: endpoint /v1/users removido
```

### Visão Corporativa

Existe um tipo especial de commit que as organizações temem e precisam sinalizar claramente: a **Quebra de Compatibilidade**. Isso ocorre quando você muda algo que vai fazer o sistema de outro time ou o aplicativo do cliente parar de funcionar se não for atualizado.

**Exemplo:** `feat(api)!: muda rota de /usuarios para /v2/usuarios`

O que acontece na empresa: Esse commit sinaliza aos robôs da empresa que a próxima versão do software não pode ser "1.x.x", ela obrigatoriamente tem que pular para "2.0.0" (Versionamento Semântico).

---

## 8. Escopo (Scope)

Além do termo inicial, empresas organizadas usam o **escopo** (entre parênteses) logo após o prefixo. Isso impede que o histórico vire uma sopa de letrinhas.

**Estrutura:** `tipo(escopo): mensagem`

**Sem escopo (Ruim):**
```
feat: adiciona botão de salvar
```
(Salvar o quê? Onde?)

**Com escopo (Bom):**
```
feat(user-profile): adiciona botão de salvar
```
(Agora o time sabe exatamente em qual parte do sistema mexeu.)

**Exemplos de escopos comuns:**
- `(auth)`
- `(database)`
- `(ui)`
- `(checkout)`
- `(payments)`
- `(email-service)`

Manter o escopo ajuda a equipe (e a você mesmo no futuro) a identificar instantaneamente qual parte do projeto foi impactada, sem nem precisar abrir o código.

---

## 9. Tipos Customizados Usados por Empresas

Embora não façam parte da especificação oficial, muitas equipes utilizam tipos customizados. Esses tipos são convenções locais e precisam ser configurados em ferramentas como Commitlint ou Commitizen.

| Tipo | Uso |
|------|-----|
| `hotfix` | Correção urgente em produção |
| `release` | Preparação de release |
| `security` | Correções de segurança |
| `deps` | Atualização de dependências |
| `config` | Configurações |
| `wip` | Work in Progress |
| `init` | Commit inicial |
| `merge` | Merge de branches |
| `improvement` | Melhorias sem nova feature |

### Observações sobre tipos estendidos

- **`deps`**: Uma variação do `build` ou `chore` focada apenas em atualização de dependências.
- **`wip`**: (Work In Progress) Indica que o trabalho ainda está em andamento (comum em branches de rascunho).
- **`init`**: Utilizado especificamente para o commit inicial que inicia o repositório.

---

## 10. Tabela de Decisão Rápida

| Situação | Tipo |
|----------|------|
| Nova funcionalidade | `feat` |
| Corrigir bug | `fix` |
| Atualizar README | `docs` |
| Corrigir indentação | `style` |
| Melhorar arquitetura | `refactor` |
| Melhorar performance | `perf` |
| Criar testes | `test` |
| Atualizar dependências | `build` |
| Ajustar GitHub Actions | `ci` |
| Atualizar configurações | `chore` |
| Desfazer commit | `revert` |
| Quebrar compatibilidade | `feat!` ou `BREAKING CHANGE` |

---

## 11. Exemplo de Histórico Profissional

```bash
feat(auth): implementar login JWT

fix(auth): corrigir renovação de token

docs(api): documentar endpoint de autenticação

test(auth): adicionar testes de login

perf(auth): reduzir consultas ao banco

refactor(auth): separar camada de serviço

build(docker): atualizar imagem node 22

ci(github): adicionar deploy automático

chore(eslint): atualizar regras de lint

revert: feat(auth): login por Facebook
```

Esse conjunto cobre praticamente **100% dos cenários profissionais encontrados em projetos Git modernos**, seguindo o padrão Conventional Commits adotado pela maior parte da indústria.

---

## 12. Benefícios da Convenção

- **Geração automática de changelogs** (ferramentas como `standard-version`, `semantic-release`)
- **Melhor legibilidade do `git log`**
- **Facilita code reviews e onboarding** de novos desenvolvedores
- **Integração com ferramentas** como Commitlint, Husky, etc.
- **Busca facilitada**: filtrar por `git log --grep="build"` para encontrar mudanças específicas
- **Versionamento semântico automatizado**: ferramentas como Semantic Release podem ler os commits e decidir se devem subir a versão do projeto (Patch, Minor ou Major) automaticamente

---

## 13. Como Configurar no Seu Projeto

1. **Instale `commitlint` + `husky`** para validar commits automaticamente
2. **Use templates ou extensões do VS Code** (ex: Conventional Commits)
3. Configure o **Commitlint** com as regras do seu time (tipos permitidos, escopos, etc.)
4. Use o **Commitizen** para criar commits interativamente seguindo o padrão

---

## 14. Ferramentas de Validação Automática (Git Hooks)

Em organizações de ponta, ninguém confia na boa vontade do programador. Eles usam **Robôs de Git (Git Hooks)**:

1. O dev digita: `git commit -m "arrumei a tela de login"`
2. O robô (ferramenta como o **Commitlint + Husky**) **barra o commit** e dá um erro no terminal do dev: *"Erro: Seu commit não segue o padrão Conventional Commit. Use feat:, fix:, etc."*
3. O commit **só é salvo no Git** se o dev digitar: `git commit -m "fix(login): corrige validação de e-mail"`
4. Quando esse commit sobe para o GitHub/GitLab, outro robô lê o `fix:` e automaticamente gera um cartão no Jira/Linear marcando o bug como "Resolvido".

---

## 15. Extensões VS Code para Ajuda e Automação

Abaixo estão as principais extensões do VS Code que auxiliam na criação de commits padronizados, desde interfaces visuais até geração automática com IA.

### 15.1 Conventional Commits (vivaxy)

**ID:** `vivaxy.vscode-conventional-commits`

Extensão mais popular para escrever commits convencionais manualmente com uma interface visual.

**Funcionalidades:**
- Interface visual para preencher tipo, escopo, descrição, corpo e rodapé
- Atalho: `Ctrl+Shift+P` → "Conventional Commits"
- Auto commit automático ao finalizar o formulário (configurável)
- Suporte a Breaking Changes

**Configurações relevantes:**

| Configuração | Descrição | Padrão |
|---|---|---|
| `conventionalCommits.autoCommit` | Controla se faz o commit automaticamente após preencher a mensagem | `true` |
| `conventionalCommits.silentAutoCommit` | Auto commit silencioso, sem focar no painel de controle | `false` |

**Fluxo de trabalho recomendado:**
1. Ativar a extensão
2. Preencher os campos na interface
3. A extensão automaticamente adiciona os arquivos, executa o commit e faz push

---

### 15.2 Git Auto Commit Message (MohitJangir)

**ID:** `MohitJangir.git-auto-commit-message`

Gera mensagens de commit automáticas usando IA (Groq, Google Gemini ou Anthropic Claude).

**Funcionalidades:**
- Geração com um clique (ícone ✨ no Source Control ou Command Palette)
- Funciona com arquivos staged, unstaged e untracked
- 3 provedores de IA: Groq/Llama (gratuito, rápido), Google Gemini (gratuito), Anthropic Claude (pago)
- Troca automática de modelo ao mudar de provedor
- Gera mensagens no formato `tipo(escopo): descrição`
- Chaves de API armazenadas no SecretStorage criptografado do VS Code
- Funciona globalmente em qualquer repositório Git

**Comandos disponíveis:**

| Comando | Descrição |
|---|---|
| `Auto Commit: Auto Generate Commit Message` | Gera mensagem de commit a partir das alterações atuais |
| `Auto Commit: Setup API Key` | Configurar ou atualizar a chave de API |
| `Auto Commit: Reset API Key` | Limpar a chave de API armazenada |

**Configurações:**

| Configuração | Padrão | Descrição |
|---|---|---|
| `autoCommit.provider` | `groq` | Provedor de IA: `groq`, `gemini` ou `claude` |
| `autoCommit.model` | `meta-llama/llama-4-scout-17b-16e-instruct` | Modelo de IA (auto-switch ao mudar de provedor) |
| `autoCommit.maxDiffLength` | `10000` | Máximo de caracteres do diff enviados para IA |

**Modelos disponíveis:**

| Modelo | Provedor | Gratuito | Notas |
|---|---|---|---|
| `meta-llama/llama-4-scout-17b-16e-instruct` | Groq | Sim | Llama mais recente (padrão) |
| `llama-3.3-70b-versatile` | Groq | Sim | Estável |
| `gemini-2.0-flash` | Gemini | Sim | Rápido e estável |
| `gemini-2.5-flash` | Gemini | Sim | Pode estar sobrecarregado |
| `gemini-3-flash-preview` | Gemini | Sim | Gemini mais recente |
| `claude-haiku-4-5-20251001` | Claude | Não | Rápido, melhor qualidade |
| `claude-sonnet-4-6-20260310` | Claude | Não | Balanceado |
| `claude-opus-4-6-20260310` | Claude | Não | Maior qualidade |

---

### 15.3 Conventional Commit Builder (fletch-r)

**ID:** `fletch-r.conventional-commit-builder`

Interface simplificada para construir commits seguindo o padrão Conventional Commits.

**Funcionalidades:**
- Input boxes e selection boxes para escrever mensagens
- Se não houver arquivos staged, pergunta quais arquivos stage antes
- Detecta automaticamente números de issue da branch atual
- Suporte a Gitmoji (emojis nos commits)
- Suporte a arquivo de configuração `.commitbuilderrc.json` por projeto
- Auto commit opcional ao finalizar

**Configurações relevantes:**

| Configuração | Descrição | Padrão |
|---|---|---|
| `conventionalCommitBuilder.autoCommit` | Commit automático após preencher os prompts | `true` |
| `conventionalCommitBuilder.showCommit` | Mostrar mensagem no SCM para revisão antes de commitar | `false` |

---

### 15.4 AI Commit Message Gen (Nolomon)

**ID:** `Nolomon.commit-message-gen-vs-x`

Gera mensagens de commit com IA diretamente na visualização do Source Control.

**Funcionalidades:**
- Botão no Source Control para gerar mensagem com IA
- Múltiplos provedores e modelos de IA
- Chaves de API armazenadas no SecretStorage do VS Code
- Mensagens no formato Conventional Commits

**Comandos:**

| Comando | Descrição |
|---|---|
| `AI Commit: Set Model` | Selecionar modelo de IA |
| `AI Commit: Set API Key` | Configurar chave de API |
| `AI Commit: Clear API Key` | Limpar chave de API |

**Dica:** Para manter o botão visível sem precisar passar o mouse, adicione ao `settings.json`:
```json
"workbench.view.alwaysShowHeaderActions": true
```

---

### 15.5 Gemini Commits (midnightgb)

**ID:** `midnightgb.gemini-commits`

Gera commits convencionais usando Google Gemini AI com análise de contexto.

**Funcionalidades:**
- Botão de acesso rápido no Source Control
- Análise contextual do código alterado (não apenas nomes de arquivos)
- Suporte a múltiplos idiomas (inglês e espanhol)
- Mensagens editáveis antes de commitar
- Smart Large Diff Handling: lida automaticamente com commits grandes usando sumários compactos
- Chaves de API armazenadas no SecretStorage

**Configuração:**

```json
{
  "geminiCommits.model": "gemini-2.5-flash"
}
```

**Requisitos:** VS Code 1.85.0+, repositório Git, chave de API Gemini.

**Métodos de uso:**
1. **Botão Source Control**: Clique no ícone ✨ no Source Control
2. **Command Palette**: `Ctrl+Shift+P` → "Generate Commit with Gemini"

---

### 15.6 Git Message Generator (ARGRABBI)

**ID:** `ARGRABBI.git-message-generator-by-arg-rabbi`

Gera mensagens de commit convencionais **sem necessidade de API key** — funciona 100% local.

**Funcionalidades:**
- Sem IA, sem API key — funciona localmente
- Análise multi-sinal (caminho + diff + metadados)
- Detecção inteligente de escopo (`auth`, `deps`, etc.)
- Mensagens com nível de confiança (high confidence = precisão maior)
- Suporte a commits com body multi-linha
- Comando "Explain" para inspecionar por que determinada mensagem foi gerada
- Fallback para diffs grandes

**Configurações relevantes:**

| Configuração | Padrão | Descrição |
|---|---|---|
| `commitGen.maxHeaderLength` | `72` | Tamanho máximo do cabeçalho |
| `commitGen.includeBody` | `true` | Incluir corpo na mensagem |
| `commitGen.bodyMaxLines` | `12` | Máximo de linhas no corpo |
| `commitGen.messageStyle` | `balanced` | Verbosidade: `concise`, `balanced`, `verbose` |
| `commitGen.showConfidence` | `true` | Notificação de confiança |
| `commitGen.profile` | `balanced` | Perfil: `balanced`, `frontend`, `backend`, `infra` |

---

### 15.7 ZeroDrop (Siranjeevan)

**ID:** `Siranjeevan.zerodrop`

Automação completa de commit com salvamento automático, IA e sincronização.

**Funcionalidades:**
- **Auto-save lifecycle**: Commita e faz push automaticamente ao fechar o VS Code
- **AI commits inteligentes**: Gera mensagens "Conventional Commit" automaticamente usando IA
- **Auto interval**: Salva automaticamente em intervalos configuráveis (padrão: 30 min)
- **Fix de commits padrão**: Substitui mensagens placeholder por mensagens com IA
- **CLI standalone**: Comando `zerodrop run` para backup manual
- Suporte a múltiplos provedores: Groq, Google, Hugging Face, Cohere, xAI, Ollama, etc.
- Monitoramento de bateria: commita automaticamente se a bateria estiver baixa

**Configurações principais:**

| Configuração | Padrão | Descrição |
|---|---|---|
| `zeroDrop.enableAutoPush` | `false` | Push automático ao fechar |
| `zeroDrop.enableAICommitMessage` | `true` | Gerar mensagens com IA |
| `zeroDrop.aiProvider` | `groq` | Provedor de IA |
| `zeroDrop.enableAutoInterval` | `false` | Auto-save periódico |
| `zeroDrop.intervalMinutes` | `30` | Minutos entre auto-saves |

**Comandos CLI:**

| Comando | Descrição |
|---|---|
| `zerodrop run` | Backup manual silencioso |
| `zerodrop run --auto-push` | Backup manual com push |
| `zerodrop run --ai` | Backup com geração de mensagem IA |

---

### 15.8 Gemini Conventional Commit Writer (shawnchee)

**ID:** `shawnchee.vscode-gemini-commit-writer`

Extensão focada em Gemini (gratuito) para escrever commits convencionais modulares.

**Funcionalidades:**
- 100% gratuito (usa Google Gemini free tier, sem cartão de crédito)
- Geração em segundos baseada nas alterações staged
- Escolha entre commit de uma linha ou multi-linha (com body e footer)
- Múltiplos modelos: Gemini 2.5 Flash e Flash Lite
- Atalho de teclado: `Ctrl+Alt+G` (Windows/Linux) ou `Cmd+Alt+G` (Mac)
- Botão ✨ no Source Control

**Configurações:**

| Configuração | Padrão | Descrição |
|---|---|---|
| Model | `gemini-2.5-flash` | Modelo Gemini (todos gratuitos) |
| Temperature | `0.1` | Controle de criatividade (0.0 = consistente, 1.0 = criativo) |
| Max Output Tokens | `500` | Tamanho máximo da mensagem |
| Max Diff Length | `5000` | Máximo de caracteres do diff analisado |

---

### Resumo Comparativo

| Extensão | Auto Commit | IA | Gratuito | Local | Interface Visual |
|---|---|---|---|---|---|
| Conventional Commits (vivaxy) | Sim | Não | Sim | Sim | Sim |
| Git Auto Commit Message | Não | Sim (Groq/Gemini/Claude) | Parcial | Não | Não |
| Conventional Commit Builder | Sim | Não | Sim | Sim | Sim |
| AI Commit Message Gen | Não | Sim (múltiplos) | Parcial | Não | Não |
| Gemini Commits | Não | Sim (Gemini) | Parcial | Não | Não |
| Git Message Generator | Não | Não | Sim | Sim | Não |
| ZeroDrop | Sim | Sim (múltiplos) | Parcial | Não | Não |
| Gemini Commit Writer | Não | Sim (Gemini) | Sim | Não | Não |

---

## 🤝 Colabore com este guia

Este documento foi construído com base em pesquisas e pode sempre crescer.

**Faltou algo? Quer complementar com mais informações, exemplos, dicas ou correções?**

Contribua enviando sugestões, abrindo issues ou fazendo um pull request no repositório. Toda contribuição é bem-vinda para tornar este guia cada vez mais completo e útil para a comunidade.

> ✨ **Compartilhe conhecimento. Evolua junto.**

---

> **Fonte:** Pesquisa compilada de múltiplas fontes sobre Conventional Commits, convenção Angular e práticas de mercado, reunida em um só arquivo.

---