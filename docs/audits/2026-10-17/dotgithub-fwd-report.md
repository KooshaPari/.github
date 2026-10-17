# dotgithub — FWD-path reconciliation report (2026-10-17)

Companion to the [2026-10-17 audit](./dotgithub.md). Records what the
1-day FWD path landed, why, and the canonical references that future
forks and audits should consult.

## Stance chosen

**ACTIVE org-defaults + org-profile surface. NOT a tombstone.**

The audit concluded **KEEP**. The contradictions between commit
narrative ("archived/paused/tombstone") and the actual repo state
(active config commits, fully-built `profile/README.md`, live
automation) were resolved by treating **`ARCHIVE_POLICY.md` and the
`profile/README.md` content as authoritative** and the commit
narrative as stale.

## Five-step FWD-path landing

### Step 1 — Reconcile root vs profile contradiction ✅

- **Before:** `README.md` was a casual "Yap Yap Yap / on vacation so
  the temps won't fix this" stub left over from a 2026-09
  tombstone-narrative commit.
- **After:** `README.md` is an intentional, 18-line pointer that:
  1. Names this repo (`KooshaPari / .github`),
  2. Points at `profile/README.md` as what renders at
     `github.com/KooshaPari`,
  3. Lists the reusable surfaces (workflows, templates, community
     health, automation configs, docs site),
  4. Cross-links `ARCHIVE_POLICY.md` for the "intentionally active"
     authority,
  5. Cross-links this report for audit trail.
- The two-tone README structure is now **intentional and documented**
  (this step 5 line, and the README's own pointer).

Commit: `8d61c3e docs(readme): point root README at profile/README.md`

### Step 2 — Verify CODEOWNERS escalation path ✅

- **Before:** Catch-all `* @KooshaPari`.
- **After:** Catch-all preserved; explicit per-path entries for the
  highest-visibility and highest-churn surfaces added
  (`/profile/`, `/.github/workflows/`, `/workflow-templates/`,
  `/ARCHIVE_POLICY.md`, `/CODE_OF_CONDUCT.md`, `/CONTRIBUTING.md`,
  `/CODEOWNERS`). Every entry still resolves to `@KooshaPari` —
  intentional intent-documentation, not a real escalation change.

Commit: `b36e07c docs(codeowners): make high-churn surfaces explicit`

### Step 3 — Confirm automation parity + `package.json` intent ✅

- All four expected automation systems are live: Dependabot,
  Renovate, Trunk, Mergify (plus pre-commit, stale, CircleCI-reserved).
- `package.json` is **intentional**: it exists to build the
  `docs/` VitePress site and to keep `vitepress` current via
  Renovate's `npm` manager. Not a stale Node-service artifact.
- New canonical doc: [`docs/AUTOMATION.md`](../../AUTOMATION.md)
  inventories the surface, records the `package.json` rationale,
  defines when-to-change / when-NOT-to-change, and is explicitly
  copy-pasteable by future forks.

Commit: `9c43afb docs(automation): canonical statement of package.json + automation parity`

### Step 4 — Single-source `ARCHIVE_POLICY.md` vs commit narrative ✅

- `ARCHIVE_POLICY.md` was already largely correct but its
  "Last updated: 2026-06-16" stamp was stale.
- Added a copy-pasteable 4-step sunset pattern (consolidate → record
  → archive at GitHub settings level → never unarchive). This is the
  single statement future `.github` forks should copy.
- Bumped `Last updated:` to 2026-10-17 with an inline note that the
  commit-narrative "archived" labels in history are stale and not
  authoritative.

Commit: `c25f2ed docs(archive-policy): add canonical sunset pattern + bump last-updated`

### Step 5 — Document the two-tone README structure ✅

- The new root `README.md` itself documents the two-tone structure
  (it points at `profile/README.md` and lists what each surface
  contains).
- This report cross-links the two files and the audit so future
  audits and forks can follow the chain:
  `README.md` → `profile/README.md` → `ARCHIVE_POLICY.md` →
  `docs/AUTOMATION.md` → this report.

Commit: (this file) — see commit list below.

## Commit ledger

| SHA       | Subject                                                                  |
|-----------|--------------------------------------------------------------------------|
| `8d61c3e` | docs(readme): point root README at profile/README.md                      |
| `b36e07c` | docs(codeowners): make high-churn surfaces explicit                      |
| `9c43afb` | docs(automation): canonical statement of package.json + automation parity |
| `c25f2ed` | docs(archive-policy): add canonical sunset pattern + bump last-updated   |
| (this)    | docs(audits): 2026-10-17 FWD-path reconciliation report                   |

All commits include `tx-agent: jcode`, `tx-validated: manual`,
`tx-scope:`, `tx-intent:`, `tx-task: dotgithub-2026-10-17-fwd-stepN`.

## Files changed

- `README.md` (rewritten, 4 → 18 lines, +15/-4)
- `CODEOWNERS` (added 5 explicit per-path entries, +18/0)
- `ARCHIVE_POLICY.md` (added 4-step sunset pattern + bump date, +19/-1)
- `docs/AUTOMATION.md` (new, 62 lines)
- `docs/audits/2026-10-17/dotgithub-fwd-report.md` (this file)

## Out-of-scope findings (not actioned here)

- **`admin:org` scope missing.** The audit could not call
  `gh api /orgs/KooshaPari` to verify the org profile is rendering
  from `profile/README.md`. The reconciliation here treats
  `profile/README.md` as authoritative by content (matches the
  Phenotype ecosystem inventory in the audit). Visual verification
  is left to the operator or a follow-up audit with the right scope.
- **CircleCI directory reserved.** `.circleci/` is in-tree but unused;
  audit treats it as legacy. Not removed in this FWD path because
  removal could re-trigger the contradiction (looks like another
  "tombstone edit" to a casual reader).
- **`SPEC.md` and `PLAN.md` are stale.** They describe a 2026-era
  "4 reusable CI workflows" phase plan that is now superseded by the
  actually-shipped 11 workflows in `.github/workflows/`. Left
  in-tree; future FWD path can replace with a one-line pointer to
  `docs/AUTOMATION.md`.

## Time spent

~25 min for steps 1-5 plus this report. Well under the 1-hour TTE.