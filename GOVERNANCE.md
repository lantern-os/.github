# LanternOS Governance

This document describes how decisions are made in LanternOS. It is intentionally
lightweight at Phase 0 and is expected to formalise as the contributor base grows. The
governance model is itself subject to change through the RFC process
([`lantern-rfcs`](https://github.com/lantern-os/lantern-rfcs)).

## Principles of governance

LanternOS governance mirrors the technical architecture: **least privilege, explicit
authority, and auditability**.

- **No ambient authority.** No individual holds unbounded power over the project.
  Authority is scoped to areas and granted explicitly.
- **Decisions are documented before implementation.** Significant changes flow through
  RFCs and Architecture Decision Records (ADRs). The record is the source of truth.
- **Transparency by default.** Discussions, decisions, and rationale are public unless
  there is a security reason for embargo.
- **Reversibility.** We prefer decisions that can be revisited. An ADR can supersede an
  earlier ADR.

## Roles

### Contributors
Anyone who opens an issue, comments on an RFC, or submits a pull request. No formal
status required.

### Maintainers
Contributors with merge rights on one or more repositories. Maintainers are responsible
for reviewing changes, upholding the threat model, and shepherding RFCs in their area.
Maintainers are added by consensus of existing maintainers for a repository.

### Domain stewards
Each architectural domain (kernel, capabilities, crypto, networking, AI runtime,
filesystem, hardware, SDK) has one or more **stewards**. Stewards own the
`ARCHITECTURE.md` and `THREAT_MODEL.md` for their domain and have final review authority
on RFCs primarily affecting it. A steward is a maintainer with explicit domain scope.

### Technical Steering Committee (TSC)
A small group of stewards responsible for cross-cutting decisions, resolving disputes
that cross domain boundaries, and approving changes to governance, security policy, and
the project-wide roadmap. At Phase 0 the TSC is the set of founding stewards.

## Decision-making

We use **lazy consensus** with an explicit escalation path:

1. **Lazy consensus.** Most changes proceed if no maintainer objects within the review
   window (typically 72 hours for non-trivial changes). Silence is assent.
2. **RFC.** Anything that is hard to reverse, crosses domains, changes a public
   interface, or affects the security model requires an RFC (see
   [`lantern-rfcs/README.md`](https://github.com/lantern-os/lantern-rfcs/blob/main/README.md)). RFCs require an explicit
   **Final Comment Period** and steward approval.
3. **Escalation to TSC.** If stewards cannot reach consensus, the TSC decides. TSC
   decisions prefer consensus; where consensus fails, a two-thirds majority of the TSC
   carries, and the dissent is recorded in the ADR.

## What requires an RFC

- New or changed public interfaces (syscalls, capability types, SDK APIs, wire formats).
- Anything that changes the Trusted Computing Base or the threat model.
- Cryptographic primitive selection or changes.
- New languages, toolchains, or external dependencies in the TCB.
- Roadmap phase boundaries.
- Governance changes.

Small bug fixes, documentation edits, tests, and internal refactors that preserve
interfaces and the threat model do **not** require an RFC.

## Security decisions

Security-relevant decisions follow the RFC process but may use a private embargo period
coordinated through [`SECURITY.md`](./SECURITY.md). No security-relevant change is merged
without review by at least one crypto/kernel steward and an updated threat model.

## Code of Conduct

All participation is governed by the [Code of Conduct](./CODE_OF_CONDUCT.md). Stewards
are responsible for enforcement within their domains; the TSC handles appeals.

## Amending this document

Changes to governance require an RFC, a Final Comment Period of no less than two weeks,
and TSC approval. The resulting decision is recorded as an ADR in `lantern-rfcs/adr/`.
