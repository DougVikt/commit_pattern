## COMMIT PATTERN

> **Standardized Git commits — clear, objective, and professional.**

This repository contains a complete guide on how to write meaningful and standardized Git commits using the **Conventional Commits** specification — the most widely adopted convention in the global market, used by open source projects, GitHub, GitLab, Azure DevOps, and thousands of companies.

---

## 📋 What you will find here

| Topic | Description |
|-------|-------------|
| **What is a commit** | Fundamental concept and why it matters |
| **Commit structure** | Anatomy of a Conventional Commit: `type(scope): description` |
| **Official types** | 11 standardized types (`feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`) |
| **Breaking Changes** | How to signal incompatible changes (`!` and `BREAKING CHANGE`) |
| **Scope usage** | How to organize commits by project modules |
| **Custom types** | Extended types used by companies (`hotfix`, `release`, `security`, `deps`, etc.) |
| **Quick decision table** | Immediate reference: situation → type |
| **Real-world examples** | Professional commit history example |
| **Benefits** | Changelog automation, SemVer, cleaner history, easier onboarding |
| **Git Hooks setup** | How to enforce standards with Commitlint + Husky |
| **VS Code extensions** | 8 extensions for visual commit building and AI-powered automation |

---

## 🌐 Choose your language

| PT | EN | ES |
|---|---|---|
| [Português](DOCUMENTACAO_COMPLETA_PT.md) | [English](DOCUMENTACAO_COMPLETA_EN.md) | [Español](DOCUMENTACAO_COMPLETA_ES.md) |
| Documentação completa em português sobre commits padronizados, tipos, exemplos e ferramentas. | Full documentation in English about standardized commits, types, examples, and tools. | Documentación completa en español sobre commits estandarizados, tipos, ejemplos y herramientas. |

---

## 💡 Why Conventional Commits?

Simply put: **consistency at scale.**

- **`feat`** and **`fix`** automatically drive semantic versioning (minor / patch)
- **`BREAKING CHANGE`** triggers major version bumps
- Tools like `semantic-release` parse your history to generate changelogs automatically
- New team members understand the project history at a glance
- CI/CD pipelines can react to specific commit types

> "In professional organizations, no one uses 'updated screen' or 'fixed bug'. These prefixes let the team know exactly what changed without reading the code." — *from the research compiled in this repository*

---

## 📁 Repository structure

```
commit_pattern/
├── README.md                       ← You are here (language selector)
├── DOCUMENTACAO_COMPLETA.md        ← Portuguese version
├── DOCUMENTACAO_COMPLETA_EN.md     ← English version
├── DOCUMENTACAO_COMPLETA_ES.md     ← Spanish version
├── conteudo.txt                    ← Raw research source
├── LICENSE
```

---

## 🤝 Contribute

This guide is built from community research and can always grow.

**Missing something? Found an error? Want to add more examples or tips?**

Open an issue, submit a pull request, or share your suggestions.

> ✨ **Share knowledge. Grow together.**

---

## 📚 Reference

- [Conventional Commits 1.0.0](https://www.conventionalcommits.org/)
- [Angular Commit Convention](https://github.com/angular/angular/blob/main/CONTRIBUTING.md#commit)
- [Semantic Versioning](https://semver.org/) 
