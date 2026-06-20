# Complete Guide to Git Commits

---

## Table of Contents

1. [What is a Commit](#1-what-is-a-commit)
2. [What is a Commit For](#2-what-is-a-commit-for)
3. [Why Use Standardization (Conventional Commits)](#3-why-use-standardization-conventional-commits)
4. [Conventional Commits Standard Structure](#4-conventional-commits-standard-structure)
5. [Complete Table of Official Types](#5-complete-table-of-official-types)
6. [Detailed Explanation of Each Type](#6-detailed-explanation-of-each-type)
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
7. [Breaking Changes](#7-breaking-changes)
8. [Scope](#8-scope)
9. [Custom Types Used by Companies](#9-custom-types-used-by-companies)
10. [Quick Decision Table](#10-quick-decision-table)
11. [Professional History Example](#11-professional-history-example)
12. [Benefits of the Convention](#12-benefits-of-the-convention)
13. [How to Set Up in Your Project](#13-how-to-set-up-in-your-project)
14. [Automatic Validation Tools (Git Hooks)](#14-automatic-validation-tools-git-hooks)
15. [VS Code Extensions for Help and Automation](#15-vs-code-extensions-for-help-and-automation)

---

## 1. What is a Commit

In pure Git there is no official list of "commit types". A commit is a **snapshot of the project's changes** at a given moment. Each commit records who made the change, when it was made, and a descriptive message about what was changed.

The most adopted standard today is **Conventional Commits**, used by open source projects, GitHub, GitLab, Azure DevOps, Semantic Release, Commitlint, and many companies.

---

## 2. What is a Commit For

- Record the project's change history
- Document **what** was changed and **why**
- Enable traceability of bugs, features, and technical decisions
- Facilitate collaboration among team members
- Serve as a basis for changelog automation and semantic versioning

---

## 3. Why Use Standardization (Conventional Commits)

1. **Automation**: Tools like Semantic Release can read commits and automatically decide whether to bump the project version (Patch, Minor, or Major).
2. **Clean History**: Any new developer can understand what happened in the project just by reading the commit types.
3. **Easy Search**: If you need to find when a dependency was updated, just filter with `git log --grep="build"`.
4. **Changelog Generation**: Generate a CHANGELOG.md in seconds, listing all new features (feat) and fixes (fix) since the last version.
5. **Better `git log` readability**.
6. **Easier code reviews and onboarding**.
7. **Integration with tools like Commitlint, Husky, etc.**

In professional organizations, no one uses "updated screen" or "fixed bug". Using these prefixes allows the team to know exactly what someone did without reading the code, enables automatic changelog generation, and triggers CI/CD processes.

---

## 4. Conventional Commits Standard Structure

```
<type>(scope): description

[optional body]

[optional footer]
```

Extended format:

```
<type>[optional scope]!: <description>

[optional body]

[optional footer(s)]
```

**Basic example:**

```bash
feat(auth): add Google login
```

**Complete example:**

```bash
feat: change API response format

BREAKING CHANGE: the 'user_id' field is now called 'uuid'.
```

### Referencing Issues

In professional environments, it is common to link the commit to a task (Jira, GitHub Issues).

```bash
fix: fix rounding error (#123)
```

---

## 5. Complete Table of Official Types

**Note:** `feat` and `fix` have direct impact on SemVer (minor and patch). BREAKING CHANGE (or `!` after the type) indicates an incompatible change (major). Other types are allowed and recommended by the Angular convention (the most common).

| Type | Purpose | SemVer Impact | Practical Message Example |
|------|---------|---------------|---------------------------|
| **`feat`** | Introduces a **new feature** to the codebase | Minor (e.g., 1.2.0 → 1.3.0) | `feat(auth): add Google login` |
| **`fix`** | **Fixes a bug** or issue found in the system | Patch (e.g., 1.2.3 → 1.2.4) | `fix(api): fix 500 error when saving appointment` |
| **`docs`** | Changes **only to documentation** (Markdown, README, docstrings, wikis) | None | `docs(readme): update Docker installation instructions` |
| **`style`** | Changes that **do not affect code meaning** (formatting, spaces, semicolons, linting). *Not to be confused with CSS!* | None | `style(templates): fix indentation and remove extra spaces` |
| **`refactor`** | A code change that **neither fixes a bug nor adds a feature** (improves performance, readability, architecture) | None | `refactor(services): centralize date validation logic` |
| **`perf`** | A code change strictly intended to **improve performance** | None | `perf(db): add index to queries table` |
| **`test`** | Adds missing tests or **corrects/modifies existing tests** | None | `test(views): add unit tests for checkout flow` |
| **`build`** | Changes that affect the **build system**, compilation tools, or external dependencies (e.g., Poetry, npm, Dockerfile) | None | `build(poetry): add django-cors-headers library` |
| **`ci`** | Changes to **Continuous Integration configuration** files and scripts (e.g., GitHub Actions, GitLab CI, Travis) | None | `ci(github): add lint step to pull request workflow` |
| **`chore`** | Routine maintenance tasks that **do not modify production or test files** (e.g., updating `.gitignore`, manual deploy tasks) | None | `chore(gitignore): add VS Code folders (.vscode)` |
| **`revert`** | Indicates a **revert** of a previous commit that caused problems | None (usually follows the reverted commit) | `revert: feat(auth): add Google login` |

These are the types recommended by the Conventional Commits specification and the Angular convention.

---

## 6. Detailed Explanation of Each Type

### 6.1 feat (Feature)

**Purpose:** Add a new feature for the user.

**When to use:**
- ✅ New screen
- ✅ New API
- ✅ New endpoint
- ✅ New component

**Examples:**

```bash
feat(cart): add shopping cart
```

```bash
feat(auth): implement Google login
```

```bash
feat(api): create CSV export endpoint
```

---

### 6.2 fix (Bug Fix)

**Purpose:** Fix incorrect behavior.

**When to use:**
- ✅ Fix error
- ✅ Fix validation
- ✅ Fix exception
- ✅ Fix logic

**Examples:**

```bash
fix(auth): fix token expiration
```

```bash
fix(cart): prevent duplicate items
```

```bash
fix(payment): fix discount calculation
```

---

### 6.3 docs (Documentation)

**Purpose:** Change documentation only.

**When to use:**
- ✅ README
- ✅ Wiki
- ✅ Swagger/OpenAPI
- ✅ Explanatory comments

**Examples:**

```bash
docs(readme): add docker instructions
```

```bash
docs(api): document user endpoint
```

```bash
docs: fix usage examples
```

---

### 6.4 style

**Purpose:** Visual changes to code without changing behavior.

**When to use:**
- ✅ Spacing
- ✅ Indentation
- ✅ Line breaks
- ✅ Visual organization

**Examples:**

```bash
style: fix project formatting
```

```bash
style(component): align imports
```

```bash
style(css): reorganize style rules
```

---

### 6.5 refactor

**Purpose:** Improve code structure without changing behavior.

**When to use:**
- ✅ Extract methods
- ✅ Separate classes
- ✅ Improve architecture
- ✅ Reduce duplication

**Examples:**

```bash
refactor(auth): separate authentication rules
```

```bash
refactor(order): extract payment service
```

```bash
refactor(api): reorganize controllers
```

---

### 6.6 perf (Performance)

**Purpose:** Improve performance.

**When to use:**
- ✅ Slow queries
- ✅ Cache
- ✅ More efficient algorithms
- ✅ Lower memory consumption

**Examples:**

```bash
perf(database): optimize customer query
```

```bash
perf(cache): add redis cache
```

```bash
perf(images): reduce loading time
```

---

### 6.7 test

**Purpose:** Add or fix tests.

**When to use:**
- ✅ Unit tests
- ✅ Integration tests
- ✅ E2E tests

**Examples:**

```bash
test(auth): add authentication tests
```

```bash
test(api): cover user endpoint
```

```bash
test(payment): fix declined payment scenario
```

---

### 6.8 build

**Purpose:** Changes to the build system.

**When to use:**
- ✅ Maven
- ✅ Gradle
- ✅ Webpack
- ✅ Vite
- ✅ Dependencies

**Examples:**

```bash
build: update dependencies
```

```bash
build(npm): update react to v19
```

```bash
build(docker): optimize application image
```

---

### 6.9 ci (Continuous Integration)

**Purpose:** Change automated pipelines.

**When to use:**
- ✅ GitHub Actions
- ✅ GitLab CI
- ✅ Jenkins
- ✅ Azure Pipelines

**Examples:**

```bash
ci: add testing stage
```

```bash
ci(github): configure automatic deploy
```

```bash
ci(jenkins): fix build pipeline
```

---

### 6.10 chore

**Purpose:** Tasks that do not affect functionality.

**When to use:**
- ✅ Settings
- ✅ Scripts
- ✅ Simple updates
- ✅ Cleanup

**Examples:**

```bash
chore: update node version
```

```bash
chore: remove temporary files
```

```bash
chore(config): adjust eslint
```

---

### 6.11 revert

**Purpose:** Undo a previous commit.

**When to use:**
- ✅ Revert feature
- ✅ Revert bug
- ✅ Revert problematic deploy

**Examples:**

```bash
revert: feat(auth): login via Google
```

```bash
revert: fix(api): cache fix
```

---

## 7. Breaking Changes

When a change breaks compatibility with what previously existed (e.g., renaming a critical database field), we add an exclamation mark `!` after the type or a note in the commit footer.

This indicates a MAJOR version bump (1.x → 2.x).

### Form 1 — With exclamation `!`

```bash
git commit -m "feat(api)!: change authentication JSON response structure"
```

```bash
feat!: remove legacy endpoint
```

### Form 2 — With `BREAKING CHANGE` in the footer

```bash
feat(api): remove legacy endpoint

BREAKING CHANGE: /v1/users endpoint removed
```

### Corporate View

There is a special type of commit that organizations fear and need to clearly signal: **Breaking Changes**. This happens when you change something that will cause another team's system or the client's application to stop working if not updated.

**Example:** `feat(api)!: change route from /users to /v2/users`

What happens in the company: This commit signals to the company's automation that the next software version cannot be "1.x.x", it must jump to "2.0.0" (Semantic Versioning).

---

## 8. Scope

Beyond the initial term, organized companies use the **scope** (in parentheses) right after the prefix. This prevents the history from becoming a soup of letters.

**Structure:** `type(scope): message`

**Without scope (Bad):**
```
feat: add save button
```
(Save what? Where?)

**With scope (Good):**
```
feat(user-profile): add save button
```
(Now the team knows exactly which part of the system was modified.)

**Common scope examples:**
- `(auth)`
- `(database)`
- `(ui)`
- `(checkout)`
- `(payments)`
- `(email-service)`

Keeping the scope helps the team (and your future self) instantly identify which part of the project was impacted, without even opening the code.

---

## 9. Custom Types Used by Companies

Although not part of the official specification, many teams use custom types. These types are local conventions and need to be configured in tools like Commitlint or Commitizen.

| Type | Usage |
|------|-------|
| `hotfix` | Urgent fix in production |
| `release` | Release preparation |
| `security` | Security fixes |
| `deps` | Dependency updates |
| `config` | Configuration |
| `wip` | Work in Progress |
| `init` | Initial commit |
| `merge` | Branch merge |
| `improvement` | Improvements without new feature |

### Notes on extended types

- **`deps`**: A variation of `build` or `chore` focused only on dependency updates.
- **`wip`**: (Work In Progress) Indicates that work is still in progress (common in draft branches).
- **`init`**: Used specifically for the initial commit that starts the repository.

---

## 10. Quick Decision Table

| Situation | Type |
|-----------|------|
| New feature | `feat` |
| Fix bug | `fix` |
| Update README | `docs` |
| Fix indentation | `style` |
| Improve architecture | `refactor` |
| Improve performance | `perf` |
| Create tests | `test` |
| Update dependencies | `build` |
| Adjust GitHub Actions | `ci` |
| Update configurations | `chore` |
| Undo commit | `revert` |
| Break compatibility | `feat!` or `BREAKING CHANGE` |

---

## 11. Professional History Example

```bash
feat(auth): implement JWT login

fix(auth): fix token renewal

docs(api): document authentication endpoint

test(auth): add login tests

perf(auth): reduce database queries

refactor(auth): separate service layer

build(docker): update node 22 image

ci(github): add automatic deploy

chore(eslint): update lint rules

revert: feat(auth): Facebook login
```

This set covers practically **100% of professional scenarios found in modern Git projects**, following the Conventional Commits standard adopted by most of the industry.

---

## 12. Benefits of the Convention

- **Automatic changelog generation** (tools like `standard-version`, `semantic-release`)
- **Better `git log` readability**
- **Easier code reviews and onboarding** for new developers
- **Integration with tools** like Commitlint, Husky, etc.
- **Easy search**: filter with `git log --grep="build"` to find specific changes
- **Automated semantic versioning**: tools like Semantic Release can read commits and automatically decide whether to bump the project version (Patch, Minor, or Major)

---

## 13. How to Set Up in Your Project

1. **Install `commitlint` + `husky`** to validate commits automatically
2. **Use templates or VS Code extensions** (e.g., Conventional Commits)
3. Configure **Commitlint** with your team's rules (allowed types, scopes, etc.)
4. Use **Commitizen** to create commits interactively following the standard

---

## 14. Automatic Validation Tools (Git Hooks)

In top-tier organizations, no one relies on the developer's goodwill. They use **Git Robots (Git Hooks)**:

1. The developer types: `git commit -m "fixed the login screen"`
2. The robot (tool like **Commitlint + Husky**) **blocks the commit** and shows an error in the terminal: *"Error: Your commit does not follow the Conventional Commit standard. Use feat:, fix:, etc."*
3. The commit **is only saved in Git** if the developer types: `git commit -m "fix(login): fix email validation"`
4. When this commit reaches GitHub/GitLab, another robot reads `fix:` and automatically generates a ticket in Jira/Linear marking the bug as "Resolved".

---

## 15. VS Code Extensions for Help and Automation

Below are the main VS Code extensions that assist in creating standardized commits, from visual interfaces to automatic AI generation.

### 15.1 Conventional Commits (vivaxy)

**ID:** `vivaxy.vscode-conventional-commits`

Most popular extension for writing conventional commits manually with a visual interface.

**Features:**
- Visual interface to fill in type, scope, description, body, and footer
- Shortcut: `Ctrl+Shift+P` → "Conventional Commits"
- Automatic auto commit after completing the form (configurable)
- Breaking Changes support

**Relevant settings:**

| Setting | Description | Default |
|---|---|---|
| `conventionalCommits.autoCommit` | Controls whether to commit automatically after filling in the message | `true` |
| `conventionalCommits.silentAutoCommit` | Silent auto commit without focusing on the control panel | `false` |

**Recommended workflow:**
1. Activate the extension
2. Fill in the fields in the interface
3. The extension automatically adds the files, commits, and pushes

---

### 15.2 Git Auto Commit Message (MohitJangir)

**ID:** `MohitJangir.git-auto-commit-message`

Generates automatic commit messages using AI (Groq, Google Gemini, or Anthropic Claude).

**Features:**
- One-click generation (✨ icon in Source Control or Command Palette)
- Works with staged, unstaged, and untracked files
- 3 AI providers: Groq/Llama (free, fast), Google Gemini (free), Anthropic Claude (paid)
- Automatic model switching when changing provider
- Generates messages in `type(scope): description` format
- API keys stored in VS Code's encrypted SecretStorage
- Works globally in any Git repository

**Available commands:**

| Command | Description |
|---|---|
| `Auto Commit: Auto Generate Commit Message` | Generate commit message from current changes |
| `Auto Commit: Setup API Key` | Set or update API key |
| `Auto Commit: Reset API Key` | Clear stored API key |

**Settings:**

| Setting | Default | Description |
|---|---|---|
| `autoCommit.provider` | `groq` | AI provider: `groq`, `gemini` or `claude` |
| `autoCommit.model` | `meta-llama/llama-4-scout-17b-16e-instruct` | AI model (auto-switches when provider changes) |
| `autoCommit.maxDiffLength` | `10000` | Maximum diff characters sent to AI |

**Available models:**

| Model | Provider | Free | Notes |
|---|---|---|---|
| `meta-llama/llama-4-scout-17b-16e-instruct` | Groq | Yes | Latest Llama (default) |
| `llama-3.3-70b-versatile` | Groq | Yes | Stable |
| `gemini-2.0-flash` | Gemini | Yes | Fast and stable |
| `gemini-2.5-flash` | Gemini | Yes | May be overloaded |
| `gemini-3-flash-preview` | Gemini | Yes | Latest Gemini |
| `claude-haiku-4-5-20251001` | Claude | No | Fast, best quality |
| `claude-sonnet-4-6-20260310` | Claude | No | Balanced |
| `claude-opus-4-6-20260310` | Claude | No | Highest quality |

---

### 15.3 Conventional Commit Builder (fletch-r)

**ID:** `fletch-r.conventional-commit-builder`

Simplified interface for building commits following the Conventional Commits standard.

**Features:**
- Input boxes and selection boxes for writing messages
- If there are no staged files, it asks which files to stage first
- Automatically detects issue numbers from the current branch
- Gitmoji support (emojis in commits)
- Support for per-project configuration file `.commitbuilderrc.json`
- Optional auto commit on completion

**Relevant settings:**

| Setting | Description | Default |
|---|---|---|
| `conventionalCommitBuilder.autoCommit` | Auto commit after filling in the prompts | `true` |
| `conventionalCommitBuilder.showCommit` | Show message in SCM for review before committing | `false` |

---

### 15.4 AI Commit Message Gen (Nolomon)

**ID:** `Nolomon.commit-message-gen-vs-x`

Generates commit messages with AI directly in the Source Control view.

**Features:**
- Button in Source Control to generate message with AI
- Multiple AI providers and models
- API keys stored in VS Code's SecretStorage
- Conventional Commits format

**Commands:**

| Command | Description |
|---|---|
| `AI Commit: Set Model` | Select AI model |
| `AI Commit: Set API Key` | Set API key |
| `AI Commit: Clear API Key` | Clear API key |

**Tip:** To keep the button visible without hovering, add to `settings.json`:
```json
"workbench.view.alwaysShowHeaderActions": true
```

---

### 15.5 Gemini Commits (midnightgb)

**ID:** `midnightgb.gemini-commits`

Generates conventional commits using Google Gemini AI with context analysis.

**Features:**
- Quick access button in Source Control
- Contextual analysis of changed code (not just file names)
- Multi-language support (English and Spanish)
- Editable messages before committing
- Smart Large Diff Handling: automatically handles large commits with compact summaries
- API keys stored in SecretStorage

**Configuration:**

```json
{
  "geminiCommits.model": "gemini-2.5-flash"
}
```

**Requirements:** VS Code 1.85.0+, Git repository, Gemini API key.

**Usage methods:**
1. **Source Control Button**: Click the ✨ icon in Source Control
2. **Command Palette**: `Ctrl+Shift+P` → "Generate Commit with Gemini"

---

### 15.6 Git Message Generator (ARGRABBI)

**ID:** `ARGRABBI.git-message-generator-by-arg-rabbi`

Generates conventional commit messages **without needing an API key** — 100% local.

**Features:**
- No AI, no API key — works locally
- Multi-signal analysis (path + diff + metadata)
- Intelligent scope detection (`auth`, `deps`, etc.)
- Confidence-aware messages (high confidence = greater precision)
- Support for multi-line body commits
- "Explain" command to inspect why a message was generated
- Large diff fallback

**Relevant settings:**

| Setting | Default | Description |
|---|---|---|
| `commitGen.maxHeaderLength` | `72` | Maximum header length |
| `commitGen.includeBody` | `true` | Include body in message |
| `commitGen.bodyMaxLines` | `12` | Maximum body lines |
| `commitGen.messageStyle` | `balanced` | Verbosity: `concise`, `balanced`, `verbose` |
| `commitGen.showConfidence` | `true` | Confidence notification |
| `commitGen.profile` | `balanced` | Profile: `balanced`, `frontend`, `backend`, `infra` |

---

### 15.7 ZeroDrop (Siranjeevan)

**ID:** `Siranjeevan.zerodrop`

Complete commit automation with auto-save, AI, and synchronization.

**Features:**
- **Auto-save lifecycle**: Automatically commits and pushes when closing VS Code
- **Intelligent AI commits**: Generates "Conventional Commit" messages automatically using AI
- **Auto interval**: Automatically saves at configurable intervals (default: 30 min)
- **Default commit fix**: Replaces placeholder messages with AI messages
- **Standalone CLI**: `zerodrop run` command for manual backup
- Supports multiple providers: Groq, Google, Hugging Face, Cohere, xAI, Ollama, etc.
- Battery monitoring: automatically commits if battery is low

**Main settings:**

| Setting | Default | Description |
|---|---|---|
| `zeroDrop.enableAutoPush` | `false` | Auto push on close |
| `zeroDrop.enableAICommitMessage` | `true` | Generate messages with AI |
| `zeroDrop.aiProvider` | `groq` | AI provider |
| `zeroDrop.enableAutoInterval` | `false` | Periodic auto-save |
| `zeroDrop.intervalMinutes` | `30` | Minutes between auto-saves |

**CLI commands:**

| Command | Description |
|---|---|
| `zerodrop run` | Silent manual backup |
| `zerodrop run --auto-push` | Manual backup with push |
| `zerodrop run --ai` | Backup with AI message generation |

---

### 15.8 Gemini Conventional Commit Writer (shawnchee)

**ID:** `shawnchee.vscode-gemini-commit-writer`

Extension focused on Gemini (free) for writing modular conventional commits.

**Features:**
- 100% free (uses Google Gemini free tier, no credit card required)
- Generation in seconds based on staged changes
- Choice between single-line or multi-line commit (with body and footer)
- Multiple models: Gemini 2.5 Flash and Flash Lite
- Keyboard shortcut: `Ctrl+Alt+G` (Windows/Linux) or `Cmd+Alt+G` (Mac)
- ✨ button in Source Control

**Settings:**

| Setting | Default | Description |
|---|---|---|
| Model | `gemini-2.5-flash` | Gemini model (all free) |
| Temperature | `0.1` | Creativity control (0.0 = consistent, 1.0 = creative) |
| Max Output Tokens | `500` | Maximum message length |
| Max Diff Length | `5000` | Maximum diff characters analyzed |

---

### Comparative Summary

| Extension | Auto Commit | AI | Free | Local | Visual Interface |
|---|---|---|---|---|---|
| Conventional Commits (vivaxy) | Yes | No | Yes | Yes | Yes |
| Git Auto Commit Message | No | Yes (Groq/Gemini/Claude) | Partial | No | No |
| Conventional Commit Builder | Yes | No | Yes | Yes | Yes |
| AI Commit Message Gen | No | Yes (multiple) | Partial | No | No |
| Gemini Commits | No | Yes (Gemini) | Partial | No | No |
| Git Message Generator | No | No | Yes | Yes | No |
| ZeroDrop | Yes | Yes (multiple) | Partial | No | No |
| Gemini Commit Writer | No | Yes (Gemini) | Yes | No | No |

---

## 🤝 Collaborate on this guide

This document was built based on research and can always grow.

**Missing something? Want to add more information, examples, tips, or corrections?**

Contribute by sending suggestions, opening issues, or making a pull request in the repository. Every contribution is welcome to make this guide increasingly complete and useful for the community.

> ✨ **Share knowledge. Grow together.**

---

> **Source:** Research compiled from multiple sources about Conventional Commits, Angular convention, and market practices, gathered into one file.

---
