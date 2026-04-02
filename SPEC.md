# org-github Specification

## Architecture
```
┌─────────────────────────────────────────────────────┐
│            org-github (GitHub Org Templates)       │
├─────────────────────────────────────────────────────┤
│  ┌───────────────────────────────────────────────┐ │
│  │         Repository Templates                 │ │
│  │  ┌─────────────┐ ┌────────────────────────┐   │ │
│  │  │ ISSUE_TEMPLATE│ │ PULL_REQUEST_TEMPLATE │   │ │
│  │  └─────────────┘ └────────────────────────┘   │ │
│  │  ┌─────────────┐ ┌────────────────────────┐   │ │
│  │  │    docs/    │ │  CODE_OF_CONDUCT.md    │   │ │
│  │  └─────────────┘ └────────────────────────┘   │ │
│  └───────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────┘
```

## Templates

| Template | Purpose |
|----------|---------|
| ISSUE_TEMPLATE | Bug/feature report |
| PULL_REQUEST_TEMPLATE | PR description |
| CODE_OF_CONDUCT.md | Community guidelines |
| CONTRIBUTING.md | Contribution guide |
| FUNDING.yml | Funding options |

## Data Models

```yaml
issue:
  type: bug | feature
  priority: critical | high | medium | low
  area: api | docs | infra

pr:
  type: feat | fix | refactor | docs
  scope: none | breaking
```