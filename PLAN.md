# metafactory — The Plan (July 2026)

**Status: PROPOSAL — community input wanted.** Comment on this PR, or in Discord. Nothing here is final until it survives your review. *(Revised 2026-07-25: the Factory named as the product; Phase 0 corrected after adversarial re-verification.)*

**This document is the why.** The living plan — what's actually in flight, linked to real issues that check themselves off — is the [iteration plan](https://github.com/the-metafactory/vision/issues/4), and [ITERATION.md](ITERATION.md) explains how to engage with it. When this snapshot and the iteration plan disagree, the iteration plan wins.

This is the honest version. We audited ourselves — architecture, install experience, security posture, and the market — and this document is what came out. It leans on what our field testers taught us in the last week, which was more than any internal review found.

---

## The product: the Factory

For months this was "a collection of tools looking for a product" — a community tester's words, and he was right. The product crystallized in one exchange: **the Factory — a software factory you install.** cortex (the runtime) + a surface bundle (Discord first) + compass-core (governance) + an agent bundle (Luna, the worker). Composed, installed through arc, and — just as non-negotiable — **untangled through arc**: one command in, one command out, nothing left behind but your own data.

Metafactory is the factory of factories. The MVP is the first factory off the line: install it, and you're holding the thing that builds the things. From this product flows the chain a tester asked for — product → features → user stories → tests — so that "ready" means something you can validate, not something we feel.

Everything below serves that release.

---

## Where we stand

**What's real:**

- The trust platform is shipped and live: registry with publisher tiers, MFA-gated publishing, content-addressed immutable storage, static capability auditing, content scanning. This is not vaporware — it's running at meta-factory.ai.
- Cortex v6.11.0 is a genuinely sophisticated runtime: deny-by-default capabilities, secrets that never touch config files, signed envelope chains, a deterministic-shell brain model where the LLM can be limited to rendering words while code decides every effect.
- `cortex quickstart` is one idempotent command with a healthy-boot gate. `arc purge` / `arc files` shipped within 24 hours of a field tester showing us uninstall left residue.
- The feedback loop works: field-test finding → issue → fix → release has been running at ~24-hour latency.

**What's honest:**

- The path from a fresh machine to an agent replying in Discord is today **~16 manual steps across 4 tools**, plus a Discord Developer Portal detour.
- The live registry holds **one published package**. The distribution pipe is hardened; the shelf is nearly empty.
- Capability declarations are **reviewed at publish time, not yet enforced at execution time**. By our own standard, declaration without enforcement isn't done. Closing that gap is now in flight — a community security review confirmed it, and the execution-boundary hardening ladder is the response, being built fail-closed and held at the gate by its own adversarial reviews.
- There is no `doctor` command. A silent bot has no first-class diagnostic.

## The bar (mid-2026)

The self-hosted personal agent category has exploded. The current bar, set by the incumbents:

- **One line + a guided onboarder, ~5 minutes to first magic moment.** A README of manual steps now reads as dated.
- **An "npm for skills" registry** with search and one-verb install.
- **And an open wound: trust.** The most popular entrant has had tens of thousands of instances exposed to the open internet and hundreds of malicious skills found on its hub. Security vendors are writing the category's obituary-warnings weekly.

Nobody currently combines an effortless install with an enforceable trust story. That seat is open. It is the seat we've been building for — we just haven't finished the effortless part.

## Positioning

> **Curated like Debian for publishers, effortless like npm for installers.**
> Mass-market means consumers, not contributors.

And the framing for where we are on the journey:

> **The foundation is open and installable today; the marketplace grows at the speed of trust.**

Curation gates who publishes, never who installs. We will not race anyone on catalog size. We intend to win on "your agent is not a security incident waiting to happen" — and to make installing it boring.

## What field testing taught us

Our community testers (you know who you are — thank you) found more real issues in a week than any internal pass:

1. **Fail-closed gates earn trust.** "The installer stops before writing anything and prints the exact fix" changed the emotional temperature of testing. Keep this property everywhere.
2. **The installer must explain itself.** A secrets questionnaire that doesn't say what it's doing, or asks for two near-identical tokens, erodes the trust the gates earned.
3. **Uninstall symmetry is part of the trust story.** `arc remove` → `arc purge` → `arc files` came directly from a tester's reset script. What gets installed must be listable and reversible.
4. **Permission recipes are owed up front.** Fine-grained GitHub tokens can't split "can propose" from "can land" — the safeguard is a branch ruleset, not a credential scope. Testers shouldn't have to discover this by hitting a 403.
5. **Docs must be copy-paste executable.** Commands with `<slug>` placeholders fail; commands with `$CTX_SLUG` just work.
6. **One digest post beats a wall of text.** How we communicate to testers is part of the product.

Two community adversarial reviews have since landed and been absorbed: the security/architecture review (no auth bypass found, core rated security-mature; every finding tracked on the hardening ladder) and the README claims review (every claim now has an issue holding it to tester experience).

## The plan

*(The task-level truth lives in the [iteration plan](https://github.com/the-metafactory/vision/issues/4); this section is the shape and the reasoning.)*

### Phase 0 — Correctness before promotion (days)

Nothing gets promoted while the advertised path has holes.

A lesson worth keeping from this phase: our own first draft listed nine correctness items, and **adversarial re-verification against main killed four of them within a day** — already fixed by in-flight work we hadn't seen. This ecosystem moves fast enough that stale claims are the main source of wasted work, which is why nothing enters the plan unverified.

The shape of what remains: the governance-package install path, the starter bundle's manifest and README defects, owns-declarations so `arc purge` fully untangles runtime state (install symmetry is part of the trust story), advertised claims brought in line with tester experience, and — last, because it validates everything above — rehearsing the registry-install path end-to-end against the actually-published artifact rather than the git-URL path. The live task list is section 2 of the iteration plan.

### Phase 1 — One command to magic (weeks)

The mass-market gate. Target: **fresh machine → agent replies, under 15 minutes**, measured on every release — and the command that gets measured is the Factory's.

- **A real arc installer** (`curl | sh`, brew) — no more clone-and-link.
- **The Factory as one command**: `arc install <factory>` stands up the full composition with a single combined capability review — and `arc purge <factory>` reverses it completely. luna-lite (chat) and luna-stack (coding tier) remain the per-persona entries; names settled once, everywhere.
- **A guided onboarder**: interactive prompts for bot token / guild / channel (accept pasted URLs), open the pre-filled OAuth invite, explain every secret it asks for, and provision or supervise NATS instead of requiring it to pre-exist.
- **Collapse the dual config tree.** One canonical directory, before more users form habits.
- **`arc doctor` / `cortex doctor`.** Every silent failure a tester hit becomes a check.
- **Stock the shelf**: publish the foundation set (cortex, the surface adapters, luna-lite, luna-stack, compass-core, the discord bundle) to the live registry. A curated foundation, not an empty pipe.

### Phase 2 — Own the trust axis (1–2 months)

Close the distance between the trust story and its enforcement:

- **Execution-time enforcement** *(in flight — section 4 of the iteration plan)*: a deterministic filesystem/exec boundary around agent sessions — path containment first, kernel sandbox as the real boundary. Built fail-closed: the first code slice has been held at the merge gate while adversarial reviews killed four bypasses that green tests missed. "Declared capabilities, enforced" becomes literally true — the hard way, on purpose.
- **Audit the Mission Control surface** (the largest not-yet-audited component) and make the prompt filter fail closed.
- **Signing end-to-end**: finish the Sigstore/provenance work and verify signatures on install.
- **Publish the security story** as plain-language content. The ecosystem is drowning in "personal agents are a security nightmare" headlines; we're building the counterexample and should say so, with receipts.

### Phase 3 — Supply and ecosystem (this quarter and beyond)

- **Tester → publisher pipeline.** The sponsored-trust model needs throughput; our field testers are its first candidates. Formalize what the last week proved: digest posts, fail-closed gates, 24-hour fix loops, the machine-account + ruleset recipe as a first-class doc.
- **Portable skill format interop** so skills aren't locked in — the trust gate lives at publish time, not in a proprietary format.
- **Then the mining loop** (traces → recipes → published processes) — the Layer 3 mission, built on a foundation people already run.

## Open questions for the community

1. What was the single worst moment of your install experience? (Be brutal — that moment is the roadmap.)
2. What would it take for you to install an agent pack published by *someone other than us*? What proof would you want to see?
3. luna-lite (chat) vs luna-stack (coding tier): does the split make sense from the outside? Do the names?
4. What's missing from this plan that you expected to find?

---

*This plan is a snapshot — the why. The living map is the [iteration plan](https://github.com/the-metafactory/vision/issues/4) ([how to engage](ITERATION.md)); the linked issues in the owning repos ([cortex](https://github.com/the-metafactory/cortex), [arc](https://github.com/the-metafactory/arc), and friends) are the source of truth for status. We also hold the MVP against external critiques on their merits: [WSFF](https://github.com/the-metafactory/vision/issues/5) (why software factories fail) and a [provider-terms exposure review](https://github.com/the-metafactory/vision/issues/6) for honest user documentation.*
