# .github — Light Audit (2026-10-17)

## IDENTITY
GitHub organization profile / defaults repo for `KooshaPari` (ID `1199812615`, default branch `main`). Holds reusable org-level config: community health files, workflow templates, dependency automation, and the org-facing profile surface.

## INTENT
Per `AGENT-PROMPT.md`: "Account defaults and publication surface." KooshaPari owns its public profile/site; `.github` publishes appropriate reusable account defaults; PhenoRegistry supplies approved metadata. Consumers = every KooshaPari repo that inherits issue/PR templates, CODEOWNERS, Dependabot/Renovate config, and the org profile rendered at github.com/KooshaPari.

## CURRENT STATE
- **Metadata.** Topics `[devtools, docs, maintained, meta]`; description "Org Level Configs & Defaults"; `has_issues=true`; last push `2026-09-29T09:15:15Z`; last commit `2026-09-22T21:00:33Z` (sha `cd830c2`, "update readme.md"). Repo is NOT actually archived at the API level despite commit-history "tombstone" labels.
- **Root `README.md` (179 B).** Casual stub: "Yap Yap Yap / on vacation so the temps won't fix this :( / not paused - strict name stability and use/consumption for organization level repo Defaults." Does NOT point at the profile.
- **`profile/README.md` (2421 B).** Fully-built org profile: Phenotype ecosystem table (10 active repos), architecture diagram, principles, stats (459 crates, 23,890 files, 40+ model providers, 85 Pheno crates). This is what github.com/KooshaPari actually renders.
- **Community health files present.** `CODEOWNERS`, `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md`, `FUNDING.yml`, `ISSUE_TEMPLATE/`, `pull_request_template.md`, `ARCHIVE_POLICY.md`, `SPEC.md`, `PLAN.md`.
- **Automation present.** `dependabot.yml`, `renovate.json`, `trunk.yaml`, `.mergify.yml`, `.pre-commit-config.yaml`, `.circleci/`, `.trunk/`, `.github/workflows/`, `workflow-templates/`. Also a tiny `package.json` + `package-lock.json` (suggests Node-based tooling check, size 87 KB).
- **Conflict (the durable issue).** Commit history narrates a tombstone arc: `2026-07-29 archived: tombstone commit - repo archived and migrated` → `2026-09-13 tombstone: mark as archived/retired` → `2026-09-15 add standardized zz-pause header to readme` → `2026-09-16 feat: add org profile readme for kooshapari` → `2026-09-22 update readme.md`. STATE.md labels this `SOURCE_CONFIRMED_INSTRUCTION_CONFLICT` — narrative says retired, repo is actively receiving config commits and now hosts a real profile.
- **Authority.** `gh api /orgs/KooshaPari` returned 404 (`admin:org` scope missing). Org profile rendering was not directly verified via the org endpoint.

## FWD PATH TO FINISH
1. **Reconcile the contradiction.** Pick one stance (active defaults+profile vs paused tombstone) and either rewrite the root `README.md` to point at `profile/README.md`, or mark the repo genuinely archived at the GitHub settings level. This is the only real defect.
2. **Verify CODEOWNERS.** Confirm `@KooshaPari` owners are still the right escalation path; tighten if needed.
3. **Confirm automation parity.** Dependabot + Renovate + Trunk configs all enabled — sanity-check that the `package.json` presence is intentional (Node tooling) and not a stale artifact from a prior experiment.
4. **Single-source ARCHIVE_POLICY.md vs the commit narrative.** Pick one canonical statement of "what happens to a sunset repo" so future .github forks can copy it cleanly.
5. **Document the two-tone README in this repo.** A 3-line root README pointing at `profile/README.md` is fine; it just must be intentional and consistent.

## TIME-TO-FINISH
~20-40 min for steps 1, 4, 5 (the reconciliation); ~10 min for steps 2, 3 (verification). Total under 1 hour, dominated by operator decision on stance.

## SUNSET/KEEP CALL
**KEEP.** Repo is the canonical org-defaults surface, profile is already built and substantial, automation configs are live, and recent commits show active maintenance. The root-vs-profile contradiction is cosmetic, not structural. Sunset would lose the only place the Phenotype org profile, CODEOWNERS, and shared templates live.

## CONFIDENCE
Medium. Read-only API audit, no clone, no local worktree inspection, did not exercise downstream inheritance (a sample KooshaPari repo pulling ISSUE_TEMPLATE/dependabot). Org-level `/orgs/KooshaPari` endpoint unreachable due to missing `admin:org` scope — org-profile rendering was inferred from `profile/README.md` contents, not directly observed at github.com/KooshaPari.