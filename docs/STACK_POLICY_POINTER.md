# Stack policy pointer

This repo does **not** define org-wide language or domain policy. The canonical single source of truth (SSOT) lives in [phenotype-registry](https://github.com/KooshaPari/phenotype-registry):

| Document | Purpose |
|----------|---------|
| [STACK_POLICY.md](https://github.com/KooshaPari/phenotype-registry/blob/main/docs/rationalization/STACK_POLICY.md) | Core stack: Rust, Zig, and Mojo; edge languages require explicit justification |
| [DOMAIN_ROLES.md](https://github.com/KooshaPari/phenotype-registry/blob/main/docs/rationalization/DOMAIN_ROLES.md) | Domain-oriented repo roles — organize by capability, not language buckets |
| [boundary-shaping.md](https://github.com/KooshaPari/phenotype-registry/blob/main/docs/rationalization/boundary-shaping.md) | Boundary and ownership shaping across the fleet |

**Summary:** Rust/Zig/Mojo form the core stack. Additional languages at the edge need documented justification. Repositories are grouped by domain responsibility, not by primary programming language.

_Last updated: 2026-06-16_
