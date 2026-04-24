# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository contains **end-user documentation only** for Sol.NET ERP (Hetosoft's ERP system). It is **not** a code repository — there is no build, no tests, and no source code to compile.

- Product source lives at https://github.com/hetosoft/ProjetosSol.NET/ (different repo; do not reference or attempt to pull internal/source-level details into docs).
- All content is written in **Brazilian Portuguese**. Do not mix languages.
- Target audience is end users, administrators, and support staff — **not developers**. Avoid source-code references or implementation internals.

## How the Site is Built and Published

The site is a Jekyll GitHub Pages site served from the `main` branch at https://hetosoft.github.io/documentacao-solnet.

- `_config.yml` — Jekyll config. Uses `kramdown` with GFM input and `permalink: pretty` (URLs end without `.html`). Plugins: `jekyll-optional-front-matter`, `jekyll-readme-index` (each folder's `README.md` becomes that folder's `index.html`), `jekyll-relative-links` (rewrites `.md` links to `.html` at build time), `jemoji`, `jekyll-seo-tag`.
- `_layouts/default.html` — wraps every page and includes Mermaid support.
- `_includes/mermaid.html` — loads Mermaid.js v10.9.1 from jsDelivr with `securityLevel: 'antiscript'`. **Do not lower this security level** — it was deliberately chosen over the default.
- There is no local preview script committed. Treat edits as published content; verify Mermaid changes against `TESTE_MERMAID.md` after deploy.

## Content Architecture

Top-level is a portal (`README.md`) that links into module folders. Each module folder follows the same 4-document pattern:

| File | Role |
|------|------|
| `README.md` | Section index (rendered as the folder's landing page via `jekyll-readme-index`). |
| `Documentacao <Tema>.md` | Full reference for the module. |
| `Guia Rapido.md` | Shortcut/checklist reference for daily operation. |
| `FAQ.md` | Categorized Q&A. |

Modules present today: `Financeiro/`, `Movimentacao/`, `RH/`, `SelfCheckout/`. Cross-module subjects (e.g. Reforma Tributária) live inside the most relevant module folder with their own Documentacao/Guia Rapido/FAQ trio.

Section `README.md` files use Jekyll front matter to set a clean permalink, e.g.:

```yaml
---
title: "Índice: Documentação Módulo Financeiro Sol.NET"
permalink: /Financeiro/
---
```

Keep front matter when editing these index files — removing it breaks the public URL.

## File Naming Conventions

- Use **spaces** in filenames, not hyphens or underscores (e.g. `Documentacao DRE.md`, `Guia Rapido.md`). URLs that link to these files must URL-encode spaces as `%20`.
- Capitalize the first letter of each significant word.
- `README.md` is reserved for folder indexes.
- Assets go in `/Assets/` at the repo root.

## Document Style (enforced across the portal)

The `.github/copilot-instructions.md` file codifies the house style. Key rules to preserve when editing:

- Every document opens with `# 📄 [Título] - Sol.NET` and uses emojis as section markers. Match the existing emoji vocabulary rather than inventing new ones.
- Structure: `## 🎯 Visão Geral` → main sections → `## 💡 Exemplos Práticos` → `## ❓ FAQ / Problemas Comuns` → metadata footer (`**Última atualização**`, `**Versão**`, `**Público-alvo**`).
- Prefer lists to tables; tables that do appear should stay narrow enough to read on mobile.
- When referring to the system use **"Sol.NET"** or **"Sol.NET ERP"**; modules are **"Módulo <Nome>"**; keyboard shortcuts use plain form (`F4`, `Ctrl+S`); menu paths use `Menu > Submenu > Opção`; field names go in quotes.
- When editing existing docs, add to existing sections rather than creating parallel ones, and keep the emoji/formatting pattern consistent with the file you're editing.

## Links Between Documents

- Use **relative `.md` links** between files (e.g. `[DRE](Financeiro/Documentacao DRE.md)`). `jekyll-relative-links` rewrites them to `.html` at build time, so both the GitHub repo view and the Pages site work.
- Anchors use kramdown's `auto_ids` — lowercase, hyphenated, emoji stripped. Test anchor links after renaming a heading.
- The portal `README.md` and every section `README.md` are the canonical entry points — when adding a new document, link it from the relevant index.

## Mermaid Diagrams

Mermaid is enabled site-wide. Fenced ```` ```mermaid ```` blocks render automatically on Pages but show as source on github.com's raw view.

- Reference `GUIA_MERMAID.md` for supported diagram types and syntax examples already in use.
- Before committing a new diagram, validate it on https://mermaid.live/ or by adding an example to `TESTE_MERMAID.md` — Mermaid is whitespace-sensitive and fails silently on syntax errors.
- Existing diagrams live in `RH/README.md`, `Movimentacao/README.md`, and `Financeiro/Documentacao Reforma Tributaria.md`; match their style.

## Git Workflow

- Commit messages in this repo are written in Portuguese (see `git log`). Match that style.
- This is a documentation repo — **never** add source code, binaries, or developer tooling config here. If a request would require those, it likely belongs in `ProjetosSol.NET` instead; flag it rather than creating scaffolding here.
