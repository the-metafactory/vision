# metafactory — Vision

## Mission

**Every way agents do work can be captured, shared, and improved.**

metafactory is a distribution hub for agentic processes — the skills, tools, workflows, and standard operating procedures that teach AI agents how to do real work. Not just code packages. The recipes, the playbooks, the hard-won knowledge of what actually works.

## The Insight

Businesses are graphs of algorithms.¹ Every organization runs on processes — code review, incident response, onboarding, deployment, compliance, customer support. These have always been locked in people's heads, in wikis nobody reads, in tribal knowledge that walks out the door when someone leaves.

¹ *Concept from Daniel Miessler, creator of [PAI](https://github.com/danielmiessler/PAI) and [Fabric](https://github.com/danielmiessler/fabric).*

At the same time, companies are becoming APIs. Every business surface — payments, identity, logistics, communication — is becoming a callable interface. This creates an explosion of tools: API wrappers, SDK integrations, protocol adapters. Toolsheds fill up with ways to call these interfaces — as skills, as tools, as MCP servers.

But tools alone don't do work. **You wire them together into processes.** A tool calls Stripe. A skill knows how to reconcile invoices. A process orchestrates the tool, the skill, and a human approval gate into an end-to-end workflow that actually receipts an invoice. The value isn't in any single component — it's in the composition.

Agentic AI makes this possible. When an agent does work, that work is recorded. Every session is a trace — tool calls, decisions, corrections, outcomes. The process becomes observable, extractable, shareable.

**The act of doing work through agentic tools IS the process mining.** You don't need a separate observation step. The work itself generates the data. The data becomes the recipe. The recipe becomes a distributable artifact. Others run it, generating new traces. The recipe evolves.

This is the "meta" in metafactory: a factory that observes its own production lines and codifies them.

## What We Distribute

Components that teach agents how to work — at every level of abstraction:

| Level | Artifact | What It Does | Example |
|-------|----------|-------------|---------|
| **Capability** | Skill | Teaches an agent HOW to do something | Research, SpecFlow, Code Review |
| **Capability** | Tool | Gives an agent something to do it WITH | pii-pseudonymizer, session-harvester |
| **Capability** | Agent | A specialized persona with domain expertise | Architect, Pentester, Designer |
| **Invocation** | Prompt | A single-shot instruction template | explain-code, summarize-pr |
| **Orchestration** | Playbook | An ordered sequence of tasks with gates | SpecFlow Development, PR Review |
| **Knowledge** | Process | An extracted, evolved workflow from real traces | fix-bug, deploy-service, onboard-engineer |

Skills are capabilities. Processes are workflows. You install a skill to gain an ability. You install a process to gain a recipe. The process uses skills as ingredients.

## The Feedback Loop

```
DO WORK ──────► TRACES RECORDED ──────► PATTERNS EXTRACTED
   ^                                           │
   │                                           v
   └──── OTHERS RUN THE PROCESS ◄──── PROCESS PUBLISHED
```

This is what makes metafactory different from a package registry. npm distributes code. We distribute *how agents do work* — and that knowledge improves every time someone uses it.

## Why Trust Is Foundational

Distributing processes is more dangerous than distributing code. A malicious package can steal your credentials. A malicious process can make your agent *believe* harmful actions are correct. It shapes judgment, not just capability.

This is why we start closed. Debian, not npm. Every publisher known personally. Every component reviewed by humans. Trust earned through proven contributions, never self-declared. Reputation built over months, destroyed in seconds.

Closed is a publish-side stance, not a consumer-side one. **Like Debian: a curated repository with one-command install.** Curation gates who publishes; apt-grade ease is what installers get. Mass-market means consumers, not contributors.

Trust is not the product. Trust is what makes the product safe enough to exist.

## The Three Layers

```
Layer 3: PROCESS COMPOSER                          ← The vision
  Capture, compose, and evolve agentic workflows
  Businesses as graphs of executable processes

Layer 2: THE MARKETPLACE                           ← Grows at the speed of trust
  Discover, trust, install, review, endorse
  Public registry with agent-native API

Layer 1: RUNTIME ADAPTERS                          ← The foundation
  Claude Code + PAI today
  Any harness tomorrow
```

The foundation is open and installable today; the marketplace grows at the speed of trust. The mission is Layer 3.

## What Success Looks Like

- An engineer installs a battle-tested code review process. Their agent follows it. Their execution traces improve the process for everyone.
- A team publishes their incident response workflow. Other teams adapt it. The community's collective IR knowledge compounds.
- Someone figures out a brilliant way to onboard agents to a new codebase. They publish it. It becomes the standard.
- The processes that run metafactory itself are published on metafactory. Dog-fooding at every level.

## Principles

1. **Start closed, grow open** — Know every publisher. Review every component. Don't optimize for scale you don't have.
2. **Trust is earned** — Proven contributions, not self-declaration. MFA is the floor.
3. **The work IS the mining** — Every agent session generates traces. Every trace is potential knowledge.
4. **Composability over monoliths** — Small, focused components that combine into workflows.
5. **Dog-food everything** — Build metafactory using the processes metafactory distributes.
6. **Harness-neutral by design** — Phase 1 is Claude Code + PAI. Architecture supports any agent runtime.

---

*Andreas Aastroem & Jens-Christian Fischer, 2026*
