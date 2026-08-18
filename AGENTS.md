# AGENTS.md

## Repository Purpose
This repository contains documentation for the INGenious testing application, built as a MkDocs Material site.

## First Files To Read
- `mkdocs.yml` (site config, navigation, theme/plugins, markdown extensions)
- `docs/index.md` (landing page and high-level positioning)
- `docs/gettingstarted.md` (user setup expectations and prerequisites)
- `.github/workflows/deploy.yml` (authoritative build/deploy behavior)

## Fast Commands
Run from repository root:

```bash
python3 -m pip install mkdocs-material
mkdocs serve
mkdocs build
```

Deployment command used in CI:

```bash
mkdocs gh-deploy --config-file mkdocs.yml --force
```

## Editing Rules For Agents
- Edit docs under `docs/` and supporting assets under `docs/img/`, `docs/ing.css`, or `overrides/`.
- Do not edit generated site output under `site/` unless explicitly asked.
- Preserve the existing nav/document taxonomy in `mkdocs.yml` (Browser Testing, Mobile App Testing, API Testing, etc.).
- Prefer linking to existing docs over duplicating content.
- Keep page style consistent with existing docs: concise explanations, usage tables, and concrete examples where relevant.

## Markdown/Docs Conventions
- This repo uses MkDocs Material extensions configured in `mkdocs.yml` (admonitions, tabbed content, superfences, emoji, attr lists).
- Many action pages use tabbed blocks for usage and corresponding code examples; follow nearby pages as templates (for example under `docs/playwrightActions/`).
- Keep image paths relative to the current page, usually using files from `docs/img/<topic>/`.

## CI/CD Notes
- Do not update any CI/CD files
<!-- - GitHub Actions workflow `.github/workflows/deploy.yml` deploys from `main` to GitHub Pages (`gh-pages`).
- CI currently installs only `mkdocs-material`; avoid adding plugin-only syntax without also updating build dependencies. -->

## Known Pitfalls
- `mkdocs.yml` is the source of truth for docs navigation. Broken paths here will break site build/navigation.
- The file currently contains repeated top-level keys such as `extra` and `features`; when modifying config, verify final key intent carefully.

## Scope Reminder
- This repository documents INGenious behavior; it is not the INGenious runtime codebase itself.
- For product implementation details, link out to the main INGenious repository/docs rather than inventing internals here.
