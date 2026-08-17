# CLAUDE.md

Persistent instructions for working in this repository. Read this before making
architectural, kernel, or capability-model decisions.

## What this repo is

LanternOS: a clean-slate, capability-based, AI-native microkernel OS. Architecture-first —
documentation and RFCs precede code. Start at [`README.md`](./README.md) and
[`lantern-docs/wiki/Home.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Home.md)
if unfamiliar with the project.

## Two vision documents apply at once

- [`lantern-docs/wiki/Vision.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Vision.md)
  — the near-term engineering thesis: why a clean-slate capability microkernel beats
  retrofitting a 1970s kernel with modern security primitives.
- [`Lantern OS — Vision and Architectural Context.md`](<./Lantern OS — Vision and Architectural Context.md>)
  — the long-term product vision: intent over applications, Contexts over files, a Personal
  Agent, local AI as trust anchor, agent-to-agent computing, interfaces beyond a monitor.
  Condensed into the wiki as
  [`lantern-docs/wiki/Intent-Model.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Intent-Model.md).

The long-term document is explicit that **the current job is still just the kernel**. It
exists so near-term primitive choices don't foreclose the long-term model — not as a signal
to start building agents, intent interfaces, or Contexts now. Check
[`lantern-docs/wiki/Roadmap.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Roadmap.md)
for the current phase's exit criteria before proposing work, and don't build ahead of it.

## Working here

- Governance and RFC/ADR process: [`GOVERNANCE.md`](./GOVERNANCE.md),
  [`lantern-rfcs/README.md`](https://github.com/lantern-os/lantern-rfcs/blob/main/README.md).
  Decisions that fix a trust boundary get an RFC; the wiki describes, RFCs decide. If a wiki
  page and a repo's `ARCHITECTURE.md` disagree, that's a bug.
- Six non-negotiable principles, in priority order when they collide:
  [`lantern-docs/wiki/Principles.md`](https://github.com/lantern-os/lantern-docs/blob/main/wiki/Principles.md).
- Every `lantern-*` component repo carries its own `README.md`, `ARCHITECTURE.md`,
  `THREAT_MODEL.md`, `STATUS.md` — read the target component's before editing it.
- LanternOS is organised as 14 separate `lantern-*` repositories plus this one (`.github`)
  under the `lantern-os` org, not a monorepo — that's why cross-repo links here use absolute
  GitHub URLs. Confirm which repo's remote a change is destined for before pushing.

## When a decision touches the long-term vision

Ask the three questions from the architectural-context document's closing section:

1. Does this make the kernel smaller, safer, and easier to reason about?
2. Can an agent use this capability without being unnecessarily trusted?
3. Does this support both humans and agents through the same deterministic interface, rather
   than creating a separate privileged "AI path"?
