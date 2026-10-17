# Archive policy

## Status of this repository

`KooshaPari/.github` is **intentionally active and must not be archived**. It is the canonical source for account-wide community health files, workflow templates, and reusable GitHub Actions workflows.

## Archived repositories

During the 2026 archive migration, several legacy KooshaPari repositories were archived after their useful content was consolidated. Their shared CI templates, issue templates, and community files now live here—not in the archived repos.

Archived repositories may remain available for historical reference, but:

- Do not copy defaults back out of archived repos into active projects.
- Do not treat archived repos as SSOT for workflows or community files.
- Update this repository when adding or changing shared defaults.

## The "what happens to a sunset repo" pattern (canonical, copy-pasteable)

When retiring a KooshaPari repository:

1. **Consolidate first.** Pull reusable CI workflows, issue/PR
   templates, and community-health files into `KooshaPari/.github`
   **before** archiving the target.
2. **Add an `ARCHIVE_POLICY.md` line to the archived repo** that says:
   > This repository is archived. Shared defaults now live at
   > <https://github.com/KooshaPari/.github>. Do not copy defaults
   > back out of this archive into active projects.
3. **Archive at the GitHub settings level** (Settings → General →
   "Archive this repository"). A commit narrative alone is not a
   tombstone — it must be paired with the GitHub archive flag, or it
   is a contradiction (see the 2026-10-17 audit on this very repo).
4. **Do not unarchive** to change branch protection or to push fixes —
   the archived tag is the durable signal.

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

Last updated: 2026-10-17 (FWD-path reconciliation: this file is the canonical statement; root README points here; commit narrative "archived" labels are stale and not authoritative — see `docs/audits/2026-10-17/dotgithub-fwd-report.md`)
