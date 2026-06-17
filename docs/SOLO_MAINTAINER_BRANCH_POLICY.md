# Solo-maintainer branch protection policy

**Account:** KooshaPari is the sole maintainer. Branch rules must not require external PR reviewers.

## Active repos (`main`)

- **No required approving reviews** on pull requests
- **`enforce_admins`: false** — admin can merge without bypass friction
- **Keep** rulesets that block force-push and branch deletion (see per-repo `Main` ruleset)
- **Optional:** required status checks (CI) remain per-repo

## Apply to new repos

When bootstrapping a repo, set branch protection with:

```json
{
  "required_pull_request_reviews": null,
  "enforce_admins": false,
  "allow_force_pushes": false,
  "allow_deletions": false
}
```

Template: `solo-maintainer-branch-protection.json` in phenotype-org-governance.

## Archived repos

Do not unarchive solely to change protection. Rules are irrelevant while archived.

_Last updated: 2026-06-17. Fleet sweep applied to 16+ active repos._