# Archive policy

## Status of this repository

`KooshaPari/.github` is **intentionally active and must not be archived**. It is the canonical source for account-wide community health files, workflow templates, and reusable GitHub Actions workflows.

## Archived repositories

During the 2026 archive migration, several legacy KooshaPari repositories were archived after their useful content was consolidated. Their shared CI templates, issue templates, and community files now live here—not in the archived repos.

Archived repositories may remain available for historical reference, but:

- Do not copy defaults back out of archived repos into active projects.
- Do not treat archived repos as SSOT for workflows or community files.
- Update this repository when adding or changing shared defaults.

## Relationship to member repos

Some active repositories (for example `phenotype-infra`) keep a local `.github/` directory for **repo-specific** automation (Terraform plans, infra lint, project CODEOWNERS paths). That is expected.

Shared, reusable pieces belong here. Project-specific workflows stay in the project repository.

## When to change this repo

Update `KooshaPari/.github` when you:

- Add or change a reusable workflow used by multiple projects
- Add or update a workflow template for the Actions UI
- Change default issue/PR templates or community guidelines
- Bump shared tool versions (Rust, Python, Node, Go) for reusable workflows

## When not to change this repo

Do not add:

- Single-repo infrastructure or deployment logic
- Secrets, tokens, or environment-specific configuration
- Content that only one repository will ever use

Last updated: 2026-06-16
