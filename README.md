# 📋 Organization .github Repository

This repository contains reusable workflows, issue templates, and community health files for the Phenotype ecosystem.

## 🚀 Quick Start

### Using Reusable Workflows

In your project's workflow, reference the reusable workflows:

```yaml
name: My Project CI
on: [push, pull_request]

jobs:
  rust-ci:
    uses: phenotype/.github/.github/workflows/ci-rust.yml@main
    with:
      rust-version: 'stable'
      run-coverage: true
    secrets:
      CODECOV_TOKEN: ${{ secrets.CODECOV_TOKEN }}
```

## 📁 Repository Structure

```
.github/
├── workflows/              # Reusable workflows
│   ├── ci-rust.yml         # Rust CI workflow
│   ├── ci-python.yml       # Python CI workflow
│   ├── ci-typescript.yml   # TypeScript/Node.js CI
│   ├── ci-go.yml           # Go CI workflow
│   ├── security.yml        # Security scanning
│   ├── publish.yml         # Package publishing
│   └── release.yml         # Release creation
├── workflow-templates/     # Starter workflows
├── ISSUE_TEMPLATE/         # Issue templates
├── CODE_OF_CONDUCT.md      # Community guidelines
├── CONTRIBUTING.md         # Contribution guide
├── FUNDING.yml            # Sponsorship info
└── pull_request_template.md # PR template
```

## 🔧 Available Reusable Workflows

### CI Workflows

| Workflow | Language | Purpose |
|----------|----------|---------|
| `ci-rust.yml` | Rust | Check, fmt, clippy, test, coverage |
| `ci-python.yml` | Python | Ruff, mypy, bandit, pytest |
| `ci-typescript.yml` | TypeScript | ESLint, Prettier, tsc, test |
| `ci-go.yml` | Go | vet, golangci-lint, test, race |

### Supporting Workflows

| Workflow | Purpose |
|----------|---------|
| `security.yml` | Snyk, Semgrep, CodeQL, Trivy, secret scanning |
| `publish.yml` | Multi-registry publishing (npm, PyPI, crates.io, Docker) |
| `release.yml` | GitHub release creation with artifacts |

## 📖 Usage Examples

### Rust Project

```yaml
name: CI
on: [push, pull_request]

jobs:
  ci:
    uses: phenotype/.github/.github/workflows/ci-rust.yml@main
    with:
      rust-version: '1.75'
      run-coverage: true
```

### Python Project with Security

```yaml
name: CI + Security
on: [push, pull_request]

jobs:
  ci:
    uses: phenotype/.github/.github/workflows/ci-python.yml@main
    with:
      python-version: '3.12'

  security:
    needs: ci
    uses: phenotype/.github/.github/workflows/security.yml@main
    with:
      languages: 'python'
      run-semgrep: true
```

### Full Pipeline

```yaml
name: Release Pipeline
on:
  push:
    tags: ['v*']

jobs:
  ci:
    uses: phenotype/.github/.github/workflows/ci-rust.yml@main

  security:
    needs: ci
    uses: phenotype/.github/.github/workflows/security.yml@main

  publish:
    needs: [ci, security]
    uses: phenotype/.github/.github/workflows/publish.yml@main
    with:
      language: 'crates'
      registry: 'crates.io'
    secrets:
      CARGO_TOKEN: ${{ secrets.CARGO_TOKEN }}

  release:
    needs: publish
    uses: phenotype/.github/.github/workflows/release.yml@main
    with:
      version: ${{ github.ref_name }}
      generate-notes: true
    secrets:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## 🤝 Contributing

See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

## 📄 License

MIT - See individual projects for their specific licenses.
