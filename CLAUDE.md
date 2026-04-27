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
- `_layouts/default.html` — wraps every page, defines the persistent left sidebar (with full module navigation) and includes Mermaid support. The sidebar is fixed on desktop (≥ 900 px) and collapses into a hamburger drawer on mobile. When you add or move a document, **also update the sidebar markup in `_layouts/default.html`**.
- `_includes/mermaid.html` — loads Mermaid.js v10.9.1 from jsDelivr with `securityLevel: 'antiscript'`. **Do not lower this security level** — it was deliberately chosen over the default.
- There is no local preview script committed. Treat edits as published content; verify Mermaid changes against `teste_mermaid.md` after deploy.

## Content Architecture

Top-level is a portal (`README.md`) that links into module folders. Each module folder follows the same 4-document pattern:

| File | Role |
|------|------|
| `README.md` | Section index (rendered as the folder's landing page via `jekyll-readme-index`). |
| `documentacao_<tema>.md` | Full reference for the module. |
| `guia_rapido.md` (or `guia_rapido_<tema>.md` when the module covers multiple themes) | Shortcut/checklist reference for daily operation. |
| `faq.md` (or `faq_<tema>.md` when needed) | Categorized Q&A. |

Modules present today: `Financeiro/`, `Fiscal/`, `Movimentacao/`, `RH/`, `Agronomico/`, `SelfCheckout/`. Tributary topics (Reforma Tributária / CBS / IBS) live in **`Fiscal/`** — keep them there even if they touch finance, and cross-link from `Financeiro/README.md` when relevant.

Section `README.md` files use Jekyll front matter to set a clean permalink, e.g.:

```yaml
---
title: "Índice: Documentação Módulo Financeiro Sol.NET"
permalink: /Financeiro/
---
```

Keep front matter when editing these index files — removing it breaks the public URL.

## File Naming Conventions (snake_case)

**All `.md` files use `snake_case`:** lowercase only, words separated by underscores, no spaces, no accents, no diacritics, no hyphens. This produces clean, ASCII-only URLs that survive any browser, copy-paste, or CMS without percent-encoding.

- ✅ `documentacao_dre.md`, `guia_rapido.md`, `faq_reforma_tributaria.md`, `tabela_de_preco_fallback_preco_base.md`
- ❌ `Documentacao DRE.md`, `Guia-Rapido.md`, `Atualização de Custo.md`, `FAQ.md`

Two exceptions, kept as-is by convention:
- `README.md` — folder index (Jekyll/`jekyll-readme-index` convention).
- `CLAUDE.md` — this file (Claude Code convention).

**Folders** stay in their current PascalCase / capitalized form (`Financeiro/`, `Fiscal/`, `Movimentacao/`, `RH/`, `Agronomico/`, `SelfCheckout/`) so the public permalinks (`/Financeiro/`, `/Fiscal/`, etc.) are stable. Do not rename folders without coordinated permalink and sidebar updates.

When you rename a file, **always**: (1) update every Markdown link to it across the repo (search both the literal name and any `%20`-encoded form), (2) update the sidebar in `_layouts/default.html`, and (3) update the section `README.md` of the affected folder.

Assets go in `/Assets/` at the repo root (capitalized for legacy reasons; do not rename without auditing references).

## Document Style (enforced across the portal)

The `.github/copilot-instructions.md` file codifies the house style. Key rules to preserve when editing:

- Every document opens with `# 📄 [Título] - Sol.NET` and uses emojis as section markers. Match the existing emoji vocabulary rather than inventing new ones.
- Structure: `## 🎯 Visão Geral` → main sections → `## 💡 Exemplos Práticos` → `## ❓ FAQ / Problemas Comuns` → metadata footer (`**Última atualização**`, `**Versão**`, `**Público-alvo**`).
- Prefer lists to tables; tables that do appear should stay narrow enough to read on mobile.
- When referring to the system use **"Sol.NET"** or **"Sol.NET ERP"**; modules are **"Módulo <Nome>"**; keyboard shortcuts use plain form (`F1`, `Ctrl+S`) **only when validated against the source code** (see *Atalhos de Teclado* below); screens are referenced by name + numeric code accessed via the F1 search (see *Acesso a Telas* below); field names go in quotes.
- When editing existing docs, add to existing sections rather than creating parallel ones, and keep the emoji/formatting pattern consistent with the file you're editing.

## Atalhos de Teclado (Regra Obrigatória)

**NUNCA** documente um atalho de teclado se não for possível **validá-lo no código-fonte do Sol.NET**. Atalhos populares (`F4`, `F5`, `F6`, `F9`, `Enter` etc.) variam de tela para tela e podem ter sido alterados ou removidos entre releases — escrever atalhos por suposição produz documentação que confunde o usuário e gera retrabalho de suporte.

- A única referência de atalho confirmada de uso geral é **`F1`**, que abre a tela de pesquisa universal (ver *Acesso a Telas* abaixo). Pode ser usado em qualquer documento.
- Para qualquer outro atalho, antes de citá-lo na doc, **localize o handler no código** (ex.: `KeyDown`, `KeyPress`, `ShortCut`, `OnShortCut`, ações em `TActionList` com `ShortCut = ...`) na tela em questão. Se não for possível validar (sandbox sem acesso ao GitHub, falta de tempo, etc.), **NÃO** cite o atalho.
- Em vez de inventar atalhos, prefira frases como:
  - *"Acesse a tela `X` (código `NNN` na pesquisa F1)"*
  - *"Use a função `Y` da tela `X`"*
  - *"Confirme/Salve pelo botão equivalente"*
- Se a documentação atual já cita um atalho não validado, **remova ou substitua pela forma genérica** ao tocar no arquivo.

## Acesso a Telas (Convenção Obrigatória)

Toda tela do Sol.NET é acessada pela **tela de pesquisa universal**, aberta com o atalho **F1**. Cada tela tem um **código identificador** (numérico) que o usuário digita nessa pesquisa para abrir a função desejada.

- **NUNCA** documente acesso a telas usando caminhos do tipo `Menu > Submenu > Opção`. O Sol.NET não usa essa navegação como padrão de uso.
- **SEMPRE** referencie cada tela como: nome da tela + código identificador, indicando que o acesso é via pesquisa (F1). Exemplo: *"Tela `Receituário Agronômico` (código `142`) — abra pela pesquisa (F1) e digite o código ou parte do nome."*
- A fonte canônica dos códigos é o arquivo **`Sol.NET/Dal/ProcessosAtualizacao/uProcessosAtualizacaoPrincipal.pas`** do repositório [ProjetosSol.NET](https://github.com/hetosoft/ProjetosSol.NET/blob/develop/Sol.NET/Dal/ProcessosAtualizacao/uProcessosAtualizacaoPrincipal.pas) (branch `develop`). Os códigos aparecem nos comandos `INSERT INTO FORMULARIO` (tabela no **singular**); o parâmetro que carrega o código exibido na pesquisa F1 é **`ID_FORMULARIO`**, e o nome interno do formulário Delphi acompanha em `NOME_FORMULARIO`. Cada `VALUES` segue o padrão `(ID, ID_FORMULARIO, DESCRICAO, NAOEDITAR, NOME_FORMULARIO, PESQUISAR, HETOSOFT)` — o segundo campo é o código que o usuário digita.
- **Antes** de citar, criar ou alterar o código de qualquer tela na documentação, **consulte esse arquivo no `develop`**. Não invente códigos e não confie em memória de versões anteriores: a tabela é atualizada a cada release.
- Quando criar listas de telas relacionadas (ex.: "Cadastros do módulo X"), apresente em formato `Tela — código (ID_FORMULARIO) — descrição curta` e deixe claro que todas são abertas pela pesquisa (F1).
- **Como acessar o repositório privado**: `ProjetosSol.NET` é privado, então é necessário um **fine-grained PAT do GitHub** com a permissão **`Contents: Read`** sobre o repo (a permissão `Metadata: Read` sozinha — padrão dos PATs novos — devolve `403 "Resource not accessible by personal access token"` ao buscar arquivos). Com o token disponível, use `curl -H "Authorization: Bearer $GITHUB_TOKEN" -H "Accept: application/vnd.github.raw" "https://api.github.com/repos/hetosoft/ProjetosSol.NET/contents/<caminho>?ref=develop"` para baixar arquivos brutos, ou `https://api.github.com/search/code?q=<termo>+repo:hetosoft/ProjetosSol.NET` para pesquisar (lembre que o GitHub Code Search é exato — buscar `FORMULARIOS` no plural retorna zero; o termo correto é `FORMULARIO`). Se não houver token disponível na sessão, peça ao usuário para colar o trecho relevante na conversa.

## Links Between Documents

- Use **relative `.md` links** between files (e.g. `[DRE](Financeiro/documentacao_dre.md)` from the root, or `[Reforma Tributária](../Fiscal/documentacao_reforma_tributaria.md)` from another module). `jekyll-relative-links` rewrites them to `.html` at build time, so both the GitHub repo view and the Pages site work.
- Anchors use kramdown's `auto_ids` — lowercase, hyphenated, emoji stripped. Test anchor links after renaming a heading.
- The portal `README.md` and every section `README.md` are the canonical entry points — when adding a new document, link it from the relevant index **and** add it to the sidebar in `_layouts/default.html`.
- Because filenames are now ASCII snake_case, links should not contain `%20` or other percent-encoded characters. If you see one, it's a leftover from before the rename — fix it.

## Mermaid Diagrams

Mermaid is enabled site-wide. Fenced ```` ```mermaid ```` blocks render automatically on Pages but show as source on github.com's raw view.

- Before committing a new diagram, validate it on https://mermaid.live/ or by adding an example to `teste_mermaid.md` (excluded from publication via `_config.yml`) — Mermaid is whitespace-sensitive and fails silently on syntax errors.
- Existing diagrams live in `RH/README.md`, `Movimentacao/README.md`, and `Fiscal/documentacao_reforma_tributaria.md`; match their style.

## Git Workflow

- Commit messages in this repo are written in Portuguese (see `git log`). Match that style.
- This is a documentation repo — **never** add source code, binaries, or developer tooling config here. If a request would require those, it likely belongs in `ProjetosSol.NET` instead; flag it rather than creating scaffolding here.
- Massive renames (like the snake_case migration) should be committed as a single rename commit (so `git log --follow` continues working) followed by a separate commit for content changes.
