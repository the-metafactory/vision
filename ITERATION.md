# How the iteration plan works

The iteration plan is the umbrella across all metafactory repos — one pinned issue in this repo that maps the current push (right now: [Factory MVP, #4](https://github.com/the-metafactory/vision/issues/4)) as task lists linking issues and epics in the repos that own the work. Modeled on VS Code's iteration plans.

**The linked issues are ground truth. The plan is the map.** Nothing is "on the plan" without a real issue behind it, and the plan never says more than the issues do.

## How it renders

Each task is a bare issue URL in a task list. GitHub renders these with the issue's live title and open/closed state — so **the plan updates itself as work merges**. Sections group by theme; two markers carry meaning:

- 🏃 — in progress
- ✋ — **held**: needs a named decision before anyone starts it. Held items list their decision owner. Do not "helpfully" pick these up.

## How to engage

### Complete a task
Do the work where it lives: PR in the owning repo, through that repo's review gate, closing the linked issue. The plan checks itself off. There is nothing to update here — closing the real issue *is* updating the plan.

**Community PRs are first-class.** Anyone can pick up a plan task and open the PR — and every PR, community or core, goes through the same rigour: the owning repo's tests, its review contract, and the adversarial lanes where the work touches trust paths. One bar, not two. That's respect, not gatekeeping: your merged work carries the same guarantees as ours because it survived the same gates. Those gates have held our own work back before merge — expect the same, and expect the findings to make the work better.

### Add a task
1. Open an issue in the repo that owns the work (the more executor-grade, the faster it moves: context, current state with evidence, steps, binary acceptance criteria, verification commands).
2. Comment on the plan issue: `ADD: <issue-url> — <one line why it belongs in this iteration>` and name the section.
3. A steward adds it to the body. Silence for a few days = ping in Discord.

### Remove a task
Comment on the plan issue: `REMOVE: <issue-url> — <why>` (superseded, refuted, out of iteration). Removal needs a steward ack and leaves a trail: the comment stays, and refuted items get a note. Precedent: four of the original nine Phase 0 items were dropped after adversarial re-verification showed them already fixed — dropping refuted work loudly is a feature of this process, not a failure.

### Question a decision
Held (✋) items and their decisions belong to the named owner. Argue the case in a comment on the plan issue or the linked issue — decisions change through discussion, not through someone starting the work.

## Rules of the map

1. **No unverified claims.** Anything entering the plan as "broken" or "missing" gets verified against `origin/main` of the owning repo first — this ecosystem ships fixes in hours, and stale claims create duplicate work.
2. **No duplicates.** Search the owning repo's issues before filing. An existing issue gets linked, not cloned.
3. **Cross-repo work lives where the code lives.** The plan links out; it never becomes a second tracker.
4. **Holds are sacred.** ✋ items block on their decision, full stop.
5. **Honest exits.** When an iteration ends, the plan issue gets a close-out summary — what shipped, what moved, what was dropped and why — and the next iteration's plan links back to it.

## Changing the plan itself vs. changing this process

- **Plan content** (the issue body): stewards edit it, driven by ADD/REMOVE comments and closing issues. Issue bodies aren't PR-able — that's why the comment protocol exists.
- **This process doc**: PR to this repo. Main is protected; all changes land by pull request, community PRs welcome.

## Where to talk

Plan-level discussion → comments on the plan issue, or Discord's **#iteration-plan** channel — the plan's changelog, where completions (✅), body changes (➕/➖), landed decisions (✋→✔) and close-outs (🔚) are announced. Work-level discussion → the linked issue, or the repo's own channel. Direction-level → #general. The plan issue is not a chat: comments that aren't ADD/REMOVE/decision-discussion may be minimized to keep the trail readable — and #iteration-plan is the changelog, not the record: if it matters, it has an issue.

**What to expect from #iteration-plan as work goes on:** posts are event-driven, never scheduled — silence means nothing changed, and the plan issue self-updates regardless. Every post carries a receipt link (issue, PR, or revision). Same-day events arrive batched as one itemized post, not a ticker stream. Want to discuss a post? Thread off it — and if the thread reaches a conclusion, the conclusion exits as an issue or an `ADD:`/`REMOVE:` proposal, because threads are where conclusions are reached, never where they live. Corrections are append-only: a wrong post gets a follow-up naming the error, never a silent edit — the ledger must be trustable backwards.
