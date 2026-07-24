# metafactory — The Plan (July 2026)

**Status: PROPOSAL — community input wanted.** Comment on this PR, or in Discord. Nothing here is final until it survives your review.

This is the honest version. We audited ourselves — architecture, install experience, security posture, and the market — and this document is what came out. It leans on what our field testers taught us in the last week, which was more than any internal review found.

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
- Capability declarations are **reviewed at publish time, not yet enforced at execution time**. By our own standard, declaration without enforcement isn't done. Closing that gap is on this plan, not behind it.
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

An adversarial README/claims review from the community is in progress right now and will feed Phase 0/1 below.

## The plan

### Phase 0 — Correctness before promotion (days)

Nothing gets promoted while the advertised path has holes.

- Fix surface-adapter dependency resolution so a bare cortex install can't end up with zero adapters (missing `repo:` fields in the manifest).
- Fix `arc install` of governance-type packages (arc#361 — first fresh install of compass-core crashed).
- Fix luna-lite's dead `dependencies:` manifest key and its broken README install URL.
- Close the release-gate integrity issues: macOS healthy-boot gate reading the wrong log path (cortex#2282), config-fix re-runs not restarting the daemon (cortex#2283), owns-declarations so `arc purge` fully applies to cortex (cortex#2338).
- Wire or remove the unwired guard hook found in field testing (cortex#2331).
- Rehearse the registry-install path end-to-end against the actually-published artifact — not just the git-URL path.

### Phase 1 — One command to magic (weeks)

The mass-market gate. Target: **fresh machine → agent replies, under 15 minutes**, measured on every release.

- **A real arc installer** (`curl | sh`, brew) — no more clone-and-link.
- **One advertised command per persona**: luna-lite for chat, luna-stack for the coding tier. Names settled once, everywhere.
- **A guided onboarder**: interactive prompts for bot token / guild / channel (accept pasted URLs), open the pre-filled OAuth invite, explain every secret it asks for, and provision or supervise NATS instead of requiring it to pre-exist.
- **Collapse the dual config tree.** One canonical directory, before more users form habits.
- **`arc doctor` / `cortex doctor`.** Every silent failure a tester hit becomes a check.
- **Stock the shelf**: publish the foundation set (cortex, the surface adapters, luna-lite, luna-stack, compass-core, the discord bundle) to the live registry. A curated foundation, not an empty pipe.

### Phase 2 — Own the trust axis (1–2 months)

Close the distance between the trust story and its enforcement:

- **Execution-time enforcement**: a deterministic filesystem/exec boundary around agent sessions — path containment first, kernel sandbox as target. "Declared capabilities, enforced" becomes literally true.
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

*This plan is a snapshot. Issues referenced live in the public repos ([cortex](https://github.com/the-metafactory/cortex), [arc](https://github.com/the-metafactory/arc)) and are the source of truth for status.*
