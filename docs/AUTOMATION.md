# Automation parity & `package.json` intent

This document is the canonical statement of **what runs automatically**
in `KooshaPari/.github`, and **why a `package.json` exists** in what
otherwise looks like a config-only repo. Future forks (and audits) can
copy this file verbatim.

## Inventory (verified 2026-10-17)

| Tool         | File                  | Scope                                                                 |
|--------------|-----------------------|-----------------------------------------------------------------------|
| Dependabot   | `dependabot.yml`      | GitHub Actions only (this repo's only updatable ecosystem)            |
| Renovate     | `renovate.json`       | Cargo, npm, pip, gomod, github-actions, dockerfile; auto-merge non-major |
| Trunk        | `trunk.yaml` + `.trunk/trunk.yaml` | Unified lint+format across Rust/Python/Go/TS/Docker/YAML/Markdown/Sh |
| Mergify      | `.mergify.yml`        | Auto-merge on green CI + approved review; bot PR auto-merge           |
| pre-commit   | `.pre-commit-config.yaml` | Local hook orchestration                                        |
| CircleCI     | `.circleci/`          | Reserved (legacy)                                                      |
| stale        | `.github/stale.yml`   | Mark/close stale issues                                                |

## Why `package.json` exists

This repo hosts the **`docs/` VitePress site**. The site is built with
`npm run docs:build` (see `docs/.vitepress/`). Renovate's `matchManagers`
includes `npm` so `vitepress` is kept current.

- `package.json` is **not** a stale experiment and **not** leftover
  Node service code.
- Removing it would break the docs build and stop Renovate from
  updating `vitepress`.
- `private: true` is set so `npm publish` cannot accidentally publish it.

## Ecosystem scope (intentional)

- **Dependabot watches `github-actions` only** — this repo's only
  runtime ecosystem. Member repos with Cargo/Python/Go/Node codebases
  carry their own ecosystem entries locally.
- **Renovate is the heavier hammer**: it groups minor/patch across
  managers, requires manual review for majors, and enables
  vulnerability-alert automerge. The duplicate scope with Dependabot
  is intentional — Dependabot is a graceful fallback when Renovate is
  misconfigured or paused on a member repo.
- **Trunk is the lint/format SSOT.** Per-language linter configs
  (rustfmt, clippy, ruff, mypy, biome, prettier, …) live in member
  repos; `.trunk/` here is the org-default reference.

## When to change this surface

- Bump Dependabot/Trunk CLI versions: edit `trunk.yaml` and the
  Trunk plugin ref in `.trunk/trunk.yaml`.
- Add a new ecosystem (e.g. `pub` for Dart): add an entry in
  `dependabot.yml` and a `packageRules` block in `renovate.json`.
- Add a new reusable workflow: edit `.github/workflows/` and add a
  matching tile under `workflow-templates/`.

## When NOT to change this surface

- Do not add per-repo CI that only one member uses.
- Do not commit `node_modules/` (`.gitignore` covers this).
- Do not add secrets or environment-specific config — member repos own
  those.

_Last reconciled: 2026-10-17 (see `docs/audits/2026-10-17/dotgithub-fwd-report.md`)._