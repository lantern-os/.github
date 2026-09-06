# LanternOS

> An AI-native, privacy-first operating system built around capabilities, security, decentralisation, and open hardware.

LanternOS is a clean-slate operating system. It is **not** a Linux distribution, a
Unix clone, a Windows replacement, or a browser OS. It is an attempt to ask a single
question seriously:

> *If we designed an operating system today — with AI agents, cryptographic identity,
> decentralised networking, hardware isolation, open ISAs, and memory-safe languages
> available from the start — what would it look like?*

This repository is the **organisation root**. It contains no kernel code yet, and that
is deliberate. LanternOS is **architecture-first**. We write the documentation, the
threat models, and the RFCs before we write the code, because the quality of the
architecture matters more than the speed of implementation. The goal is a system that
can remain relevant for decades.

---

## The repositories

LanternOS is organised as a set of focused repositories under the
[`lantern-os`](https://github.com/lantern-os) organisation. Each repository owns one
layer of the architecture and maintains its own `ARCHITECTURE.md`, `THREAT_MODEL.md`,
and `STATUS.md`.

| Repository | Purpose | Layer |
| --- | --- | --- |
| [`lantern-rfcs`](https://github.com/lantern-os/lantern-rfcs) | RFC process, ADRs, governance — **start here** | Process |
| [`lantern-docs`](https://github.com/lantern-os/lantern-docs) | The project wiki: vision, principles, architecture | Docs |
| [`lantern-website`](https://github.com/lantern-os/lantern-website) | Public website and landing page | Docs |
| [`lantern-boot`](https://github.com/lantern-os/lantern-boot) | Boot, measured boot, root-of-trust handoff | Firmware |
| [`lantern-hal`](https://github.com/lantern-os/lantern-hal) | Hardware abstraction layer (x86-64 → RISC-V) | Hardware |
| [`lantern-kernel`](https://github.com/lantern-os/lantern-kernel) | Microkernel: scheduling, memory, IPC, capabilities | Kernel |
| [`lantern-capabilities`](https://github.com/lantern-os/lantern-capabilities) | Capability model, object capabilities, derivation | Security core |
| [`lantern-abi`](https://github.com/lantern-os/lantern-abi) | Confined-program syscall ABI + minimal `no_std` runtime (non-TCB) | Runtime |
| [`lantern-runtime`](https://github.com/lantern-os/lantern-runtime) | User-space service framework + WASM runtime | Runtime |
| [`lantern-filesystem`](https://github.com/lantern-os/lantern-filesystem) | Content-addressed, encrypted, capability-gated storage | Services |
| [`lantern-network`](https://github.com/lantern-os/lantern-network) | Decentralised, anonymity-capable networking | Services |
| [`lantern-crypto`](https://github.com/lantern-os/lantern-crypto) | Key management, signing, DIDs, verifiable credentials | Services |
| [`lantern-ai-runtime`](https://github.com/lantern-os/lantern-ai-runtime) | Local inference, model management, capability-scoped agents | Runtime |
| [`lantern-shell`](https://github.com/lantern-os/lantern-shell) | User shell, session, surfaces, agent supervision UI | Userland |
| [`lantern-sdk`](https://github.com/lantern-os/lantern-sdk) | Developer SDK, capability-aware APIs, tooling | Tooling |

---

## The architecture in one diagram

```
                         ┌───────────────────────────────┐
                         │  Applications & AI agents      │
                         ├───────────────────────────────┤
                         │  AI runtime  (lantern-ai-runtime)
                         ├───────────────────────────────┤
                         │  WASM runtime (lantern-runtime) │
                         ├───────────────────────────────┤
                         │  Capability runtime             │
                         │  (lantern-capabilities)         │
                         ├───────────────────────────────┤
                         │  User-space system services:    │
                         │  fs · net · crypto · drivers     │
                         ├───────────────────────────────┤
                         │  Microkernel (lantern-kernel):   │
                         │  sched · mem · IPC · caps · IRQ  │
                         ├───────────────────────────────┤
                         │  HAL (lantern-hal) · boot        │
                         ├───────────────────────────────┤
                         │  Hardware (x86-64 now, RISC-V)   │
                         └───────────────────────────────┘
```

Everything above the kernel line is unprivileged. Authority flows **downward as
explicit capabilities**, never as ambient permission.

---

## Core principles

1. **Security by architecture** — minimal TCB, no ambient authority, capabilities everywhere.
2. **Privacy by default** — users own identity, data, models, and keys; minimise telemetry and metadata.
3. **Local-first ownership** — the cloud is optional; the device is sovereign.
4. **Memory safety** — Rust first; `unsafe` is isolated, justified, and audited.
5. **Open hardware** — RISC-V, auditable firmware, open toolchains as the long-term target.
6. **AI-native** — AI is an OS capability, not an application; agents are capability-scoped and auditable.

See [`lantern-docs/wiki/Principles.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Principles.md) for the full text.

---

## Where to start

- **Understand the project** → [`lantern-docs/wiki/Home.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Home.md)
- **Understand the threat model** → [`lantern-docs/wiki/Threat-Model.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Threat-Model.md)
- **Propose a change** → [`lantern-rfcs/README.md`](https://github.com/lantern-os/lantern-rfcs/blob/main/README.md)
- **Understand how we decide** → [`GOVERNANCE.md`](./GOVERNANCE.md)
- **Contribute** → [`CONTRIBUTING.md`](./CONTRIBUTING.md)
- **Report a vulnerability** → [`SECURITY.md`](./SECURITY.md)

---

## Project status

**Phase 3 — Privacy, identity, networking, and AI.** Phase 2 (capability runtime & first
services) is complete, closed by
[RFC-0017](https://github.com/lantern-os/lantern-rfcs/blob/main/rfcs/0017-phase-2-to-phase-3-transition.md)/[ADR-0021](https://github.com/lantern-os/lantern-rfcs/blob/main/adr/0021-phase-2-complete-phase-3-opened.md):
its exit criterion — a third-party Wasm app runs confined, reads a file only via a granted
capability, and cannot touch anything it wasn't granted, demonstrated adversarially — is
met (`lantern-example-signer`, packaged by `lantern-sdk build`). `lantern-network`,
`lantern-ai-runtime`, and identity/wallet work are now open for prototype code, and the
first Phase 3 effort is the confined-execution port carried forward from Phase 2 (the
services and the runtime run in-process on a host target, not yet confined on the kernel).
See [`lantern-docs/wiki/Roadmap.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Roadmap.md).

## Licence

Documentation is licensed under [CC BY 4.0](./LICENSE-DOCS). Code is dual-licensed under
[MIT](./LICENSE-MIT) and [Apache-2.0](./LICENSE-APACHE) unless a repository states
otherwise. See [`LICENSE`](./LICENSE).
