# Lantern OS — Vision and Architectural Context

## Purpose of this document

This document defines the long-term product and architectural vision for Lantern OS.

Use it as persistent context when designing, implementing, reviewing, or refactoring Lantern.

Lantern is **not intended to become another conventional desktop operating system**.

The existing work on a small, secure kernel remains fundamental. Continue building a robust, minimal and secure operating-system foundation, but make architectural decisions with the longer-term computing model described here in mind.

Do not attempt to implement the entire vision immediately.

Instead:

1. Build the kernel correctly.
2. Preserve architectural flexibility.
3. Introduce the necessary primitives gradually.
4. Avoid unnecessary assumptions inherited from Windows, macOS, Linux desktop environments, Android or iOS.
5. Continually ask whether an abstraction makes sense for an intent-centric, agent-centric operating system rather than merely reproducing an application-centric OS.

---

# 1. The central idea

Lantern explores a different model of personal computing.

Traditional desktop computing is based around:

**User → Applications → Files → Operating System**

Lantern should move toward:

**Human → Intent → Personal Agent → Capabilities → Operating System**

The primary abstraction presented to a human should eventually be neither the application nor the file.

It should be **intent and context**.

A user should increasingly be able to express what they want rather than manually determining which application, service, file or workflow will accomplish it.

For example, instead of:

> Open Excel → find budget.xlsx → modify assumptions → update formulas → create graph.

The user might say:

> Show me what happens to our budget if income falls by 20%.

Lantern determines which data, computational capabilities and visual representation are appropriate.

A spreadsheet may still exist underneath, and the user must be able to inspect it when useful, but manipulating spreadsheet software isn't necessarily the primary interaction.

---

# 2. Inspiration from early personal computers

Early home computers such as the Commodore 64 and ZX Spectrum booted directly into a programmable environment.

The machine effectively said:

> READY.

The user was immediately at the machine's command surface.

Modern computers instead boot into a collection of applications created by other people.

Lantern should recover something important from early personal computing:

> **The computer is something the user can instruct, explore and create with directly.**

Natural language and AI make it possible to revisit this idea without requiring every user to learn BASIC or a shell.

Lantern's spiritual successor to the BASIC prompt is therefore an **Intent Interface**.

However, it must not simply look like a terminal or an empty chatbot.

---

# 3. Intent, not applications

Applications remain useful implementation mechanisms, but should not necessarily be Lantern's fundamental user-facing abstraction.

Consider capabilities such as:

- text editing
- document layout
- calculation
- structured data manipulation
- databases
- image manipulation
- video processing
- communication
- web access
- code compilation
- search
- mapping
- visualisation

Lantern should increasingly make these capabilities available to the user's agent.

Instead of requiring:

> User → find application → operate application → manipulate information

Lantern should support:

> User → express intent → system composes appropriate capabilities

Traditional applications can continue to exist and must remain usable where they provide the best interface.

The objective is not to prohibit applications.

The objective is to stop assuming that launching an application is always the first step in accomplishing something.

---

# 4. Contexts rather than files

Files remain necessary for persistence, compatibility, interchange and low-level system operation.

But humans frequently think in terms of activities and subjects rather than filenames.

Lantern should therefore investigate a higher-level abstraction called a **Context**.

Examples:

- Catalyst
- Lantern development
- Family finances
- Moving house
- Holiday planning
- University
- Photography

A Context could eventually associate:

- structured information
- files
- conversations
- people
- history
- decisions
- tasks
- external services
- permissions
- AI memory
- capabilities
- agent state
- provenance

The user might say:

> Continue working on Lantern.

Lantern should understand the relevant context without requiring the user to manually reopen six applications and locate eight files.

Files should remain inspectable and portable.

Do not create an architecture in which critical user information exists only as opaque AI state.

---

# 5. The Personal Agent

A central long-term component of Lantern is a **Personal Agent**.

This is not merely a chatbot bundled with the OS.

It acts as an intelligent intermediary between the human and the computing environment.

Conceptually:

**Human**

↓

**Personal Agent**

↓

**Intent / Context / Policy**

↓

**Capabilities**

↓

**Kernel / Hardware / Network**

The Personal Agent should eventually be able to:

- understand user intent;
- understand current context;
- find information;
- invoke capabilities;
- compose capabilities;
- create temporary interfaces;
- create persistent workflows;
- interact with external agents;
- manage permissions;
- protect private information;
- explain what it has done;
- request human judgement when necessary.

The agent should augment deterministic operating-system primitives rather than replace them.

---

# 6. Local AI as the trust anchor

Privacy and security are fundamental.

Lantern should assume that a meaningful level of AI inference will be available locally.

The local Personal Agent is the user's **trust boundary**.

Private context should remain local wherever practical.

More powerful external models may still be useful.

The architecture should therefore support something conceptually similar to:

**Private local context**

↓

**Local agent**

↓

**Policy / privacy filter**

↓

**Sanitised external request**

↓

**External AI**

↓

**Result**

↓

**Local agent combines result with private context**

A cloud AI should not automatically receive the user's entire digital life merely because a task requires powerful inference.

Local AI should decide what information needs to leave the machine.

---

# 7. Agent-to-agent computing

Lantern should anticipate an Internet in which people, organisations and services increasingly expose intelligent agents.

A user's Personal Agent could communicate with:

- another person's Personal Agent;
- an employer's agent;
- a hotel agent;
- an airline agent;
- a retailer agent;
- a bank agent;
- a government agent;
- specialist AI services;
- devices;
- other Lantern systems.

The emerging model becomes:

**Human → Personal Agent → Agent Network → Organisation/Service Agent**

Agents should exchange structured intents and results rather than simply pretending to be humans operating websites.

This suggests future protocol requirements around:

- identity;
- discovery;
- authentication;
- authorisation;
- capability negotiation;
- intent representation;
- payments;
- provenance;
- trust;
- delegation;
- revocation;
- selective disclosure.

Do not hard-code these concepts prematurely, but consider them when defining kernel security, IPC, identity and capability primitives.

---

# 8. Minimum necessary disclosure

Agent interaction should follow a strong principle:

> **Reveal the minimum information necessary to fulfil an intent.**

For example, finding hotel availability may require:

- dates;
- number of travellers;
- approximate location;
- requirements;
- budget.

It should not automatically reveal:

- identity;
- employer;
- home address;
- complete calendar;
- email history;
- unrelated preferences.

Lantern should eventually support different levels of identity, including:

- anonymous;
- pseudonymous;
- verified attribute;
- verified person;
- authorised representative.

Where possible, the system should be able to prove facts without revealing unnecessary underlying information.

Example:

> Prove that the user is over 18.

rather than:

> Send the user's complete passport.

This philosophy should influence the security model from the beginning.

---

# 9. The kernel remains fundamental

The existing Lantern kernel work remains relevant and important.

Continue pursuing a **small, secure, comprehensible kernel**.

The future AI experience should sit above strong deterministic foundations.

AI must not become the security boundary.

The kernel should ultimately provide trustworthy primitives upon which agents operate.

Particular architectural areas worth considering include:

- strong process isolation;
- capability-based security where appropriate;
- explicit permissions;
- secure IPC;
- identity;
- resource ownership;
- device isolation;
- auditable operations;
- revocable authority;
- sandboxing;
- secure storage;
- cryptographic primitives;
- trusted execution boundaries;
- networking;
- deterministic system services.

An AI agent should operate through constrained capabilities granted by the OS.

Do not simply give an AI process unrestricted root access.

---

# 10. AI actions must be inspectable

Natural language is probabilistic.

System operations should not be.

If the user says:

> Back up my projects every Friday.

The AI can interpret the request, but should convert it into an explicit system object such as:

**Backup Policy**

- Source: Projects
- Destination: NAS
- Schedule: Friday
- Failure behaviour: notify
- Retention: defined policy

The user should be able to:

- inspect it;
- modify it;
- disable it;
- delete it;
- see its history;
- understand which permissions it possesses.

The principle is:

> **AI interprets intention; deterministic components execute authority-bearing operations.**

---

# 11. Progressive disclosure

Lantern should work for both ordinary users and highly technical users.

Interfaces should therefore be progressively revealable.

An ordinary user might say:

> Make this photo brighter.

An advanced user might inspect the exact transformation.

A developer might inspect the underlying API invocation or implementation.

Conceptually:

**Intent**

↓

**Result**

↓

**Details**

↓

**Operations**

↓

**API / Shell**

↓

**Implementation**

Do not hide the computer from technically sophisticated users in the name of simplicity.

Lantern should make simple things simple while allowing users to descend through abstraction layers.

---

# 12. The Intent Interface

Lantern should eventually boot into an **Intent Environment**, rather than assuming that the first thing a user needs is a traditional desktop.

However, avoid presenting an intimidating blank prompt.

The initial experience should combine:

- natural-language input;
- voice;
- visual suggestions;
- recent Contexts;
- current activities;
- relevant events;
- important exceptions;
- traditional navigation when wanted.

Conceptually:

> Good morning.

> What would you like to do?

Possible visual affordances might include:

**Continue · Find · Create · Explore · Communicate**

alongside recent Contexts.

The interface should teach users what is possible rather than expecting them to know what commands to type.

---

# 13. Interfaces should be generated according to the task

A permanent desktop full of windows should not be assumed.

The system should present visual complexity according to need.

For example:

> How much did we spend last month?

may require only:

**£4,820**

Whereas:

> Let me investigate our spending.

might create a rich financial workspace containing charts, transactions, filters and tables.

And:

> Show me the raw data.

might expose a conventional spreadsheet.

Therefore:

> **The interface should expand to match the task.**

Visual interfaces remain extremely important.

The goal is not to eliminate GUIs.

The goal is to make them contextual rather than permanent.

---

# 14. Beyond the screen

Lantern should not assume that a rectangular monitor will always be the primary computing interface.

The same Personal Agent and Context model should eventually operate through:

- voice;
- audio;
- phones;
- conventional monitors;
- keyboards;
- televisions;
- AR glasses;
- spatial displays;
- cameras;
- environmental sensors.

The interaction mode should adapt to the user's circumstances.

Possible hierarchy:

**Ambient → Conversational → Visual → Spatial → Workstation**

Examples:

Walking:

**audio + minimal visual information**

At home:

**voice + environmental displays**

AR glasses:

**audio + vision + contextual spatial information**

Desk:

**large displays + keyboard + pointing devices**

Deep technical work:

**rich multi-window/multi-display workspace**

The underlying Context remains the same as the user moves between interfaces.

---

# 15. Vision as context

With user permission, visual perception could provide contextual input.

Instead of:

> Search for information about this object.

the user could simply look at something and ask:

> What is that?

Or:

> How do I repair this?

Or:

> Connect to that computer.

Or:

> Remember this.

Vision supplies context while speech supplies intent.

Conceptually:

**Eyes → Context**

**Voice → Intent**

**Agent → Interpretation**

**OS → Controlled action**

Visual sensing must follow explicit privacy policies and should favour local processing.

Continuous recording of a user's life should NOT be assumed.

---

# 16. Attention is a scarce resource

A major goal of Lantern should be to return human attention to the human.

Modern knowledge workers spend enormous amounts of time:

- checking email;
- checking chat;
- navigating applications;
- finding files;
- copying information;
- filling forms;
- updating tickets;
- scheduling;
- chasing responses;
- producing status reports;
- monitoring systems.

Agents should handle routine coordination and escalate **decisions, exceptions and genuinely important information**.

Lantern should optimise not merely for:

> How much work can this human perform?

but also:

> How little of this human's attention does the computer need to consume?

Technology should enable people to spend more time living, thinking, creating and interacting with other people.

---

# 17. Mobile work is a first-class use case

Work should not necessarily mean sitting in front of a laptop running work applications.

A user might ask while walking:

> Anything important at work?

Their Personal Agent can communicate with a separate authorised work agent and return:

> The overnight build failed. The team has a fix. One decision requires you.

The user makes the decision.

Later, when detailed investigation becomes necessary, Lantern can create a full visual workspace.

This means computing follows the person rather than requiring the person to remain at the computer.

---

# 18. Personal and work boundaries

Personal and organisational agents must have explicit trust boundaries.

A work agent should not automatically gain access to private personal Contexts.

Likewise, a Personal Agent should only interact with organisational systems through explicitly granted capabilities.

Lantern should make these boundaries understandable and auditable.

The user should be able to answer questions such as:

- What does my employer's agent know about me?
- What can it access?
- What has it requested?
- What information did my Personal Agent disclose?
- What actions can it perform?
- Can I revoke that authority?

---

# 19. The Internet as an agent mesh

The long-term vision extends beyond Lantern itself.

The first Internet connected computers.

The Web connected documents.

Social networks connected people.

An emerging agent network may connect **representatives of people, organisations, services and machines**.

Lantern should be designed so that it could participate naturally in such an environment.

Potential future architecture:

**People / Organisations**

↓

**Trusted Agents**

↓

**Agent Protocol**

↓

**Services / Knowledge / Markets / Devices**

↓

**Existing Internet**

This does not require replacing today's Internet.

It creates another semantic and transactional layer above it.

---

# 20. Do not recreate the desktop accidentally

When implementing Lantern, continually challenge inherited assumptions.

Before introducing an abstraction, ask:

> Is this fundamental to computing, or merely fundamental to the desktop metaphor?

Examples worth questioning include:

- applications as destinations;
- files as the primary user abstraction;
- desktop icons;
- taskbars;
- application launchers;
- system trays;
- notification centres;
- separate application settings;
- application-owned data;
- manual copy/paste between programs;
- fixed windows;
- application-specific AI assistants.

Some of these will remain useful.

But they should survive because they solve a genuine problem, not because existing operating systems contain them.

---

# 21. Compatibility is different from architecture

Lantern may eventually need compatibility with conventional software, file formats and network protocols.

Compatibility should not force Lantern's native conceptual model to become identical to existing operating systems.

For example, Lantern might support:

- conventional files;
- POSIX-like APIs;
- existing network protocols;
- containers;
- virtualisation;
- Web applications;
- existing document formats.

These can be bridges into the existing computing world.

Lantern's native experience can still be based around Intent, Context and Capabilities.

---

# 22. Development philosophy

When working on Lantern, prioritise:

1. **Security before convenience**
2. **Small understandable components**
3. **Explicit authority**
4. **Local-first operation**
5. **User ownership of information**
6. **Interoperability**
7. **Inspectable AI behaviour**
8. **Deterministic execution beneath probabilistic reasoning**
9. **Progressive disclosure**
10. **Interfaces appropriate to context**
11. **Minimal demands on human attention**
12. **Freedom from unnecessary legacy assumptions**

Avoid building large amounts of speculative infrastructure solely because it might eventually be useful.

Instead, ensure today's architectural choices do not unnecessarily prevent tomorrow's model.

---

# 23. Near-term kernel guidance

The immediate objective is NOT to build the complete AI/AR/agent environment.

The immediate objective remains building a high-quality operating-system foundation.

When making kernel decisions, however, favour primitives that would support the future architecture.

In particular, investigate whether Lantern's kernel architecture can naturally support:

- capabilities as first-class security objects;
- strongly isolated services;
- secure message passing;
- explicit delegation of authority;
- revocable capabilities;
- strong process identity;
- secure local agent execution;
- sandboxed external code;
- resource quotas;
- secure storage;
- auditable privileged operations;
- device permissions;
- trustworthy time;
- cryptographic identity;
- protected user secrets.

Do not implement these merely because they appear in this list.

Evaluate them against Lantern's existing kernel architecture and current development stage.

---

# 24. Architectural question to keep asking

For significant design decisions, consider three questions:

### Does this make the kernel smaller, safer and easier to reason about?

If not, determine whether the complexity belongs outside the kernel.

### Can an agent use this capability without being unnecessarily trusted?

Prefer explicit, constrained and revocable authority.

### Does this architecture support both humans and agents?

Future Lantern services should ideally expose deterministic interfaces that can be used by:

- conventional GUIs;
- shells;
- programs;
- automation;
- Personal Agents.

This avoids creating a separate privileged "AI path" through the operating system.

---

# 25. What Lantern is not

Lantern is not:

**Linux + chatbot**

It is not:

**a desktop environment with an LLM search box**

It is not:

**an AI that has unrestricted control of a computer**

It is not:

**a collection of cloud AI APIs disguised as an operating system**

And it is not:

**an attempt to remove every conventional interface simply because it is old.**

Lantern should instead explore what a personal computer would look like if it were being invented now, with AI, local inference, modern cryptography, ubiquitous networking, spatial computing and decades of operating-system knowledge available from the beginning.

---

# 26. The long-term experience

The ideal Lantern system should increasingly feel less like a device demanding to be operated and more like a trusted extension of the user.

It is:

**invisible when unnecessary;**

**conversational when conversation is sufficient;**

**visual when information benefits from visualisation;**

**spatial when the user needs space;**

**a workstation when deep work demands one;**

**programmable when the user wants control;**

**and inspectable when trust matters.**

The system should be capable of acting on the user's behalf while remaining bounded by explicit authority.

The computer should consume less of the user's life, not more.

---

# 27. The guiding statement

Early personal computers booted and effectively said:

> READY.

Desktop computers boot and effectively say:

> Here are your applications.

Smartphones say:

> Here are your apps and notifications.

Lantern should ultimately feel as though it says:

> **I'm here. Tell me what you want to accomplish — or go live your life, and I'll be here when you need me.**

Build the kernel and architecture that can make that model of computing possible.