# KooshaPari / .github

Canonical organization defaults for the **KooshaPari** GitHub org.

> 👋 The org profile lives at **[`profile/README.md`](profile/README.md)** — that's what renders at <https://github.com/KooshaPari>.

This repository is **intentionally active** (see [`ARCHIVE_POLICY.md`](ARCHIVE_POLICY.md)). It holds the reusable, org-wide surface:

- Org profile (rendered from `profile/README.md`)
- Reusable GitHub Actions workflows (`.github/workflows/`) and the `workflow-templates/` UI tiles
- Community health files (`CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `CODEOWNERS`, `FUNDING.yml`)
- Issue & PR templates (`ISSUE_TEMPLATE/`, `pull_request_template.md`)
- Shared automation configs (`dependabot.yml`, `renovate.json`, `trunk.yaml`, `.mergify.yml`, `.pre-commit-config.yaml`)
- Docs site skeleton (`docs/` — built with VitePress via `npm run docs:build`)

Member repos inherit from here unless they override with their own `.github/` directory.

_Last reconciled: 2026-10-17. See `docs/audits/2026-10-17/dotgithub-fwd-report.md` for the audit + FWD-path rationale._