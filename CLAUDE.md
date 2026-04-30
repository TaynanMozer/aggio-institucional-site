# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

Institutional website for AGGIO Engenharia — a single self-contained file with no build tools, no dependencies, and no external frameworks. Everything lives in `index.html`.

## Architecture

The entire site is one file: `index.html` (~2050 lines) structured as:

- **`<head>`** — all CSS in a single `<style>` block, organized by numbered sections (1–15 + responsive breakpoints)
- **`<body>`** — semantic HTML sections in this order:
  - Header (sticky, with desktop nav + mobile checkbox-toggle nav)
  - Hero (two-column grid with abstract dashboard visual built entirely from CSS)
  - Diagnóstico (problem framing cards)
  - Por que a AGGIO (`#por-que`)
  - Como atuamos (`#como-atuamos`) — 5-step process
  - Serviços (`#servicos`) — 10 service cards
  - Área do Cliente (`#area-cliente`) — 4 portal cards
  - Resultados (`#resultados`)
  - Nossa História (`#historia`)
  - Trabalhe conosco (`#trabalhe-conosco`)
  - Contato (`#contato`) — contact form (currently `action="#"`, no backend wired)
  - Footer

## CSS design system (CSS custom properties in `:root`)

| Variable | Value | Use |
|---|---|---|
| `--verde-principal` | `#17413C` | Primary brand green |
| `--verde-secundario` | `#70A545` | Accent green (CTAs, badges) |
| `--verde-profundo` | `#0E2D2A` | Dark green (headings, footer bg) |
| `--verde-claro` | `#E8F1EC` | Light green tints |
| `--amarelo-tecnico` | `#D8A735` | Yellow accent (hero highlights, indicators) |
| `--azul-petroleo` | `#173B57` | Petroleum blue (second result card border) |
| `--cinza-texto` | `#2E3836` | Body text |
| `--cinza-suave` | `#F5F7F6` | Section backgrounds |
| `--max-width` | `1180px` | Container max-width |

Button variants: `.btn-primary`, `.btn-dark`, `.btn-outline`, `.btn-outline-dark`, `.btn-yellow`, `.btn-sm`.

## Responsive breakpoints

- `≤980px` — hero becomes single column; history/contact grids stack; process grid goes 2-col
- `≤768px` — desktop nav hides; mobile nav (checkbox toggle `#nav-toggle`) activates; form rows stack
- `≤480px` — tighter container padding; hero visual adjustments

## Mobile navigation

Uses a pure-CSS pattern: hidden `<input type="checkbox" id="nav-toggle">` + `<label for="nav-toggle">` + sibling `.nav-mobile`. No JavaScript involved.

## Development

Open `index.html` directly in a browser — no server, build step, or install required. To preview changes live, any static file server works (e.g. `python -m http.server` or VS Code Live Server).

## External link

The only outbound URL in the site: `https://aggioengenharia.reportload.com` — used in service card #05 and the "Área do Cliente" portal card for operational performance reports.

## Contact form

The form (`action="#" method="post"`) has no backend wired. Submitting it does nothing — this needs integration (e.g. Formspree, a server endpoint, or JavaScript fetch) to become functional.

## GitHub repository

The project is version-controlled with Git and synced to GitHub automatically.

**Remote:** `https://github.com/mozer-eng/aggio-institucional-site` (configure with `git remote add origin <URL>` after creating the repo)

**Auto-sync:** A Claude Code `PostToolUse` hook in `.claude/settings.json` automatically commits and pushes to `origin` after every `Edit` or `Write` operation. No manual `git push` needed.

**Setup (one-time, if remote not yet configured):**
1. Install GitHub CLI: https://cli.github.com/
2. Run: `gh auth login`
3. Run: `gh repo create aggio-institucional-site --public --source=. --push`

After step 3 the remote is wired and auto-sync will push on every file change.
