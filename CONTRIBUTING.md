# Contributing to LanternOS

Thank you for your interest in LanternOS. We are at **Phase 0 (Foundations)**, which
means the most valuable contributions today are not code — they are **architecture,
threat models, critique, and RFCs**.

## The contribution ladder

1. **Read first.** Start with [`lantern-docs/wiki/Home.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Home.md),
   then [`Principles.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Principles.md) and
   [`Threat-Model.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Threat-Model.md). Understanding the *why* is
   a prerequisite for proposing the *what*.
2. **Discuss.** Open a GitHub issue or discussion to float an idea. Cheap, early
   feedback saves everyone time.
3. **RFC.** For anything non-trivial (see [`GOVERNANCE.md`](./GOVERNANCE.md) for the
   list), open an RFC in [`lantern-rfcs`](https://github.com/lantern-os/lantern-rfcs) using the template.
4. **Prototype.** Once an RFC is accepted, a throwaway prototype often de-risks the
   design before production implementation.
5. **Implement.** Production code lands last, against an accepted RFC, with tests and an
   updated threat model.

We deliberately put documentation and architecture *above* implementation. See
[Architecture First](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Architecture.md#architecture-first).

## What we are looking for right now

- Critique of the architecture and threat models. **Adversarial review is welcome.**
- RFCs for the foundational decisions still open (see open RFCs in `lantern-rfcs/rfcs/`).
- Prior-art surveys: seL4, CHERI, Fuchsia/Zircon, Redox, Barrelfish, Tock, Hubris,
  KataOS, Tor, I2P, libp2p, IPFS, Nym, age/PASETO, DID/VC specs.
- Hardware research: RISC-V extensions, secure enclaves, NPUs, FPGA regions.

## Conventions

- **Language.** Rust is the primary language. See
  [ADR-0001](https://github.com/lantern-os/lantern-rfcs/blob/main/adr/0001-rust-as-primary-language.md). Tooling may use
  TypeScript. `unsafe` must be isolated, justified in-comment, and reviewed.
- **Docs as code.** Every architectural repo carries `ARCHITECTURE.md`,
  `THREAT_MODEL.md`, and `STATUS.md`. Keep them current in the same PR as the change.
- **Commit messages.** Imperative mood, scoped: `kernel: add capability derivation note`.
- **Every component declares its TCB membership and threat model.** No exceptions.

## Pull request checklist

- [ ] Linked to an issue, RFC, or ADR where required by governance.
- [ ] Threat model updated if the change affects trust boundaries or the TCB.
- [ ] Documentation updated in the same PR.
- [ ] No new ambient authority introduced; new capabilities are explicit and minimal.
- [ ] `unsafe` blocks (if any) are justified and isolated.

## Reporting security issues

Do **not** open a public issue for vulnerabilities. Follow [`SECURITY.md`](./SECURITY.md).

## Licensing of contributions

By contributing you agree that your contributions are licensed under the repository's
licence — documentation under CC BY 4.0, code under the MIT/Apache-2.0 dual licence
(see [`LICENSE`](./LICENSE)). Include a `Signed-off-by` line (DCO) on commits.
