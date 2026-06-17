# KooshaPari community profile (`.github`)

This is the **KooshaPari account community profile repository**. GitHub uses it to provide default community health files and workflow starter templates to member repositories that do not define their own copies.

**This repo is the single source of truth (SSOT)** for org-wide defaults. Do not treat archived repos or per-project `.github/` folders as the canonical source for shared templates.

## What this repo provides

| Path | Purpose |
|------|---------|
| `CONTRIBUTING.md` | Default contribution guidelines for member repos |
| `CODE_OF_CONDUCT.md` | Default community standards |
| `pull_request_template.md` | Default pull request template |
| `ISSUE_TEMPLATE/` | Default issue templates (bug, feature, docs) |
| `FUNDING.yml` | Default sponsorship links |
| `workflow-templates/` | Starter workflows shown in **Actions → New workflow** |
| `.github/workflows/` | Reusable workflows callable from member repos |
| `docs/` | Shared documentation and journey guides |

Member repos inherit these files automatically when they omit local equivalents. Repo-specific overrides (for example `phenotype-infra/.github/workflows/terraform-plan.yml`) stay in those repositories.

## Quick start: reusable workflows

Reference reusable workflows from member repo workflows:

```yaml
name: My Project CI
on: [push, pull_request]

jobs:
  rust-ci:
    uses: KooshaPari/.github/.github/workflows/ci-rust.yml@main
    with:
      rust-version: 'stable'
      run-coverage: true
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

## Quick start: workflow templates

When creating a workflow in a member repo, choose a template from this repository under **Actions → New workflow**. Templates in `workflow-templates/` wrap the reusable workflows above.

## Repository layout

```
.github/                          # This repo root
├── .github/workflows/            # Reusable workflows (workflow_call)
│   ├── ci-rust.yml
│   ├── ci-python.yml
│   ├── ci-typescript.yml
│   ├── ci-go.yml
│   ├── security.yml
│   ├── publish.yml
│   └── release.yml
├── workflow-templates/           # Starter workflows + properties.json
├── ISSUE_TEMPLATE/
├── docs/
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── ARCHIVE_POLICY.md
└── pull_request_template.md
```

## Available reusable workflows

### CI

| Workflow | Language | Checks |
|----------|----------|--------|
| `ci-rust.yml` | Rust | fmt, clippy, test, optional coverage |
| `ci-python.yml` | Python | ruff, mypy, bandit, pytest |
| `ci-typescript.yml` | TypeScript | ESLint, Prettier, tsc, test |
| `ci-go.yml` | Go | vet, golangci-lint, test, race |

### Supporting

| Workflow | Purpose |
|----------|---------|
| `security.yml` | Snyk, Semgrep, CodeQL, Trivy, secret scanning |
| `publish.yml` | Multi-registry publishing (npm, PyPI, crates.io, Docker) |
| `release.yml` | GitHub release creation with artifacts |

## Example: full release pipeline

```yaml
name: Release Pipeline
on:
  push:
    tags: ['v*']

jobs:
  ci:
    uses: KooshaPari/.github/.github/workflows/ci-rust.yml@main

  security:
    needs: ci
    uses: KooshaPari/.github/.github/workflows/security.yml@main

  publish:
    needs: [ci, security]
    uses: KooshaPari/.github/.github/workflows/publish.yml@main
    with:
      language: 'crates'
      registry: 'crates.io'
    secrets:
      CARGO_TOKEN: ${{ secrets.CARGO_TOKEN }}

  release:
    needs: publish
    uses: KooshaPari/.github/.github/workflows/release.yml@main
    with:
      version: ${{ github.ref_name }}
      generate-notes: true
    secrets:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Maintenance

See [ARCHIVE_POLICY.md](./ARCHIVE_POLICY.md) for archive/migration context, [docs/STACK_POLICY_POINTER.md](./docs/STACK_POLICY_POINTER.md) for canonical stack and domain policy (SSOT in phenotype-registry), and [CONTRIBUTING.md](./CONTRIBUTING.md) for change guidelines.

Last reviewed: 2026-06-16
