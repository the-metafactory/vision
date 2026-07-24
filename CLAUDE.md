# vision — the why-layer of metafactory

This repo is public and small on purpose. It carries the **why** — mission, strategy, process — while all code and task tracking live in the owning repos. Any agent working here is editing the project's public voice: precision and honesty over enthusiasm.

## The artifacts and their jobs

| Artifact | Job | Change cadence |
|---|---|---|
| `VISION.md` | Mission, principles, trust doctrine | Rarely; every word is load-bearing |
| `PLAN.md` | Strategy snapshot — the reasoning behind the phases | Per revision round |
| `ITERATION.md` | How the community engages with the plan | When the process changes |
| Pinned iteration-plan issue | The living map: task lists of cross-repo issue URLs that render with live state | Continuously; stewards edit the body |

**Division of labor is strict:** `PLAN.md` never carries owning-repo issue numbers — task-level truth belongs to the iteration-plan issue, which self-updates as linked issues close. When the snapshot and the map disagree, the map wins.

## Rules

1. **Everything lands by PR.** Main is protected (require-PR, no bypass — binds admins and agents alike). Community-facing documents stay open for community review; merge is the principal's call, not an agent's.
2. **No unverified claims.** Nothing enters any artifact as "broken" or "missing" without same-day verification against the owning repo's `origin/main`. This ecosystem ships fixes in hours; stale claims are the main source of wasted work.
3. **Held items are sacred.** ✋ entries on the plan block on a named decision owner. Never start them, never "helpfully" resolve them.
4. **Confidentiality.** This repo is public. No internal business figures, no private-repo contents, no personal data. Critique categories and patterns, not named people or companies.

## SOP: community feedback playback

When review feedback arrives on a PR here (or on the plan issue), the loop is:

1. **Digest** — pull every comment; classify each point adopt / adapt / decline. Decisions that change plan substance are ratified by the principal, not made by the agent.
2. **Revise** — apply adopted changes on the PR branch, one commit per review round, commit message crediting the round.
3. **Respond** — reply on the PR, per reviewer, by name: their point, the disposition, the commit SHA that carries it, and — where the reviewer is the right judge of whether the fix worked — the question back. Declines get reasons, not silence.
4. **Anchor** — adopted feedback that implies work becomes an issue in the repo that owns that work, credited to its proposer. Feedback must never survive only as a comment thread.
5. **Record** — update the iteration-plan issue body, then post the change to the plan's Discord channel using the changelog conventions: ✅ task completed · ➕/➖ plan body changed · ✋→✔ decision landed · 🔚 iteration close-out.

**The rule of three surfaces:** respond where the feedback was given, record where the plan lives, anchor where the work lives. All three, every round — a reviewer should never have to follow a second channel to learn what happened to their point.

## Discord conventions

- **#iteration-plan** is the plan's changelog, not the record: if it matters, it has an issue. Posts follow the prefixes above.
- **#general** hears about the plan only at open and close of an iteration — announcements are ephemeral, the ledger is append-only, GitHub is ground truth.
- Substantive community posts carry attribution: *written by <agent>, reviewed by <principal>*.

### How #iteration-plan posts work as the iteration goes on

**Event-driven, never scheduled.** A post happens because a ledger event happened — an issue closed, the plan body changed, a decision landed. Silence means nothing changed; the map self-updates, so there are no heartbeat posts and no "still working on it" filler.

**Post shapes** (a receipt link is mandatory — no post without one):

- `✅ <repo>#<n> — <what shipped, one line> · <how it was verified> · <PR link>` — when a plan-linked issue closes.
- `➕/➖ Plan body changed — <what and why, itemized> · <revision sha> · map link` — when a steward applies ADD/REMOVE proposals or absorbs a review round. Credits proposers by name.
- `✋→✔ <decision> — <what was decided> by <owner> · unblocks <items>` — when a held item resolves.
- `🏃 <wave n> complete, <wave n+1> started` — milestone-level only, never per-task.
- `🔚 Iteration close-out — shipped / moved / dropped-and-why · link to the close-out comment on the plan issue` — once per iteration.

**Batching:** events landing the same day go out as one combined post — the channel reads as a ledger, not a ticker. A busy day gets one itemized digest, not ten pings.

**Threading:** the post is the ledger entry and stays clean; discussion happens in a thread off the post. When a thread reaches a conclusion, the conclusion exits as an issue or an ADD/REMOVE proposal — threads are where conclusions are reached, never where they live.

**Corrections are append-only.** A wrong post is never silently edited or deleted: post a correction naming what the earlier post got wrong. The ledger's value is that it can be trusted backwards.

**Who posts:** whoever applied the change — steward or their agent — with the attribution footer on agent posts. One event, one post: another repo's release is only announced here if it changes the plan.

## Provenance

This SOP was extracted from the first live round: PR #3's three community reviews (two delivered agent-for-human), all adopted, played back across all three surfaces in one pass. The generic version for other projects is proposed to compass-core.
