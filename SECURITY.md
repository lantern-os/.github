# LanternOS Security Policy

Security is not a feature of LanternOS; it is the architecture. That makes the integrity
of our process as important as the integrity of our code.

## Reporting a vulnerability

**Please do not report security vulnerabilities through public GitHub issues,
discussions, or pull requests.**

At Phase 0 there is no deployed software to exploit, but the policy is established now so
it is reflexive later:

- Email the security stewards at **security@lanternos.org** (placeholder until the org
  email is provisioned), encrypted to the published age/PGP key when available.
- Include: affected component/repo, a description, reproduction steps or proof of
  concept, and the impact you believe it has on the threat model.
- You will receive an acknowledgement within 72 hours and a triage assessment within
  7 days.

## Coordinated disclosure

- We operate a **90-day disclosure window** by default, negotiable for complex issues.
- We will credit reporters who wish to be credited.
- Embargoed fixes are developed in private and released with an advisory and an updated
  [`THREAT_MODEL.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Threat-Model.md).

## Scope and the Trusted Computing Base

The severity of an issue is judged against its position in the TCB. The smaller and more
trusted the component, the more severe a flaw in it is:

1. **Boot / root of trust** ([`lantern-boot`](https://github.com/lantern-os/lantern-boot)) — highest severity.
2. **Microkernel** ([`lantern-kernel`](https://github.com/lantern-os/lantern-kernel)) — highest severity.
3. **Capability runtime** ([`lantern-capabilities`](https://github.com/lantern-os/lantern-capabilities)).
4. **Cryptographic services** ([`lantern-crypto`](https://github.com/lantern-os/lantern-crypto)).
5. **System services** (filesystem, network) — confined; severity bounded by capabilities.
6. **Applications / agents** — confined by design; escapes from confinement are in scope.

A core security claim of LanternOS is that **a compromised application or agent cannot
exceed the capabilities it was granted**. Demonstrating a confinement escape — ambient
authority, capability amplification, or TCB code execution — is always in scope and
high severity.

## What we consider a vulnerability

- Any path to executing code in the kernel or TCB from a lower-privilege component.
- Capability forgery, amplification, or confused-deputy attacks.
- Cryptographic weaknesses: weak primitives, nonce reuse, key extraction, downgrade.
- Privacy regressions: unintended telemetry, metadata leakage, cross-identity linkage.
- Bypass of measured boot or hardware-backed trust.

## Security review process

No change to the TCB is merged without:

- review by at least one kernel/crypto steward,
- an updated threat model for the affected trust boundary,
- and, for cryptographic changes, an RFC (see [`GOVERNANCE.md`](./GOVERNANCE.md)).
