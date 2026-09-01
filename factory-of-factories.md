# The factory of factories — the meta-model under metafactory

*Concept doc. Companion to [VISION.md](VISION.md) — it makes one line
of the vision precise: "This is the 'meta' in metafactory: a factory
that observes its own production lines and codifies them." Status:
living document — pushback welcome via issues.*

---

## Why this document

"Factory of factories" has been used as a slogan. It is actually a
precise structural claim, and two mature bodies of engineering
knowledge — object-oriented design and the OMG meta-modeling stack —
tell us exactly what the claim commits us to, what it buys, and where
it goes wrong. This doc borrows their results so we don't rediscover
them the hard way.

## The two towers we inherit

**From OOP.** A class is a factory for instances. The Factory Method
pattern hides *which* concrete thing gets built behind an interface;
the Abstract Factory pattern produces whole *families* of related
products behind one contract, so code written against the contract
works with any concrete factory that honors it. And in languages where
classes are objects (Smalltalk, Python, CLOS), the tower goes one
step higher: a metaclass manufactures classes. The metaclass is the
literal factory of factories — and its power is definitional: it says
what all classes *are*, what it means to instantiate, inherit,
conform.

**From MOF/UML.** OMG formalized the same tower as four layers, each
an instance of the one above:

| Layer | What it holds | Example |
|-------|---------------|---------|
| M0 | The running world | An actual deployed system, a live session |
| M1 | Models | A schema, a class diagram, a workflow definition |
| M2 | The metamodel | UML — defines what "Class" and "Association" mean |
| M3 | The meta-metamodel | MOF — defines what a metamodel is; defined in itself |

The tower stops at M3 because MOF is self-describing. And the payoff
was never philosophical: because every metamodel conforms to MOF, one
set of generic machinery — repositories, serialization, transformation
engines — works over *any* modeling language, including ones the tool
authors never saw. **A metamodel is what makes heterogeneous things
comparable, storable, and composable by strangers' machinery.**

## The metafactory tower

Map it and the architecture we already have snaps into place:

| Layer | metafactory | Already named as |
|-------|-------------|------------------|
| M0 | Agents doing real work — sessions, traces, outcomes | "Every session is a trace" |
| M1 | Published components — a process is a *model of how work is done* | Skills, tools, prompts, playbooks, processes |
| M2 | The schema that defines what a publishable component *is* — manifest, the type stack (tool → skill → process → agent → graph, DD-49), capability declarations, trust tiers, review gates, receipts | The trust architecture + manifest schema |
| M3 | The schema applied to itself — metafactory built from metafactory components, its own processes published on the registry | Principle 5: dog-food everything |

Two things fall out immediately:

- **"The work IS the mining" is the M0→M1 arrow.** Process extraction
  from traces is not a feature bolted onto a registry; it is the
  tower's defining transition — instances observed, models codified.
  npm distributes M1 artifacts too, but code models *computation*;
  our M1 artifacts model *work*.
- **Dog-fooding is not culture, it's closure.** MOF needs no M4
  because it describes itself. metafactory needs no external
  authority over its schema because the registry's own processes run
  on the registry. Self-description is the structural argument for
  why the tower is complete.

## Factories, precisely

A **factory** is a member-operated production capability: an operator,
their agents, and their installed stack, able to turn models into
outcomes — a website factory that ships production sites, a document
factory, an assessment factory. Factories live at the factory layer.
They produce products.

**metafactory produces no products.** Its job is the layer above:
define what a factory *is* — how one is described (capability
declaration), trusted (tiers, review, sponsorship), verified
(receipts), found (discovery), and composed (contracts) — so that
factories built by strangers can trust, find, and invoke one another.
Not a bigger factory, not a holding company of factories: **the layer
that makes factories legible to each other.**

The Abstract Factory lesson applies verbatim to composition: a
consumer depends on the *contract* — the declared capability, the
definition of done, the receipts — never on whose workshop does the
building. Which concrete factory fulfills a request is a matchmaking
decision at composition time, exactly as which concrete class gets
instantiated is the factory's business, not the caller's.

## What the meta layer must earn

MOF mattered because one schema bought generic machinery for every
language. The equivalent test here is concrete:

> **Adding the Nth factory must require no new machinery — only a new
> capability declaration.**

Discovery, matchmaking, trust evaluation, receipt verification, and
composition must work for a factory the platform authors never
imagined, purely because it conforms to the schema. When onboarding
factory number two costs a schema entry instead of an integration
project, the meta layer is earning its keep. When it costs an
integration project, we have built a portal, not a metamodel.

## The warning label

The OOP world paid dearly for one lesson: **meta layers are only
worth anything when the base layer ships.** MOF mattered because UML
tools shipped real systems; metaclass frameworks built for their own
elegance became architecture astronautics. The base layer here is
real components delivering real outcomes for real consumers. The meta
layer is judged by one number: whether it makes the *second* factory
and the *second* outcome cheaper than the first. Every schema
decision that doesn't serve that number is tower-building for its own
sake, and we should decline it.

## Relation to the three layers

VISION.md's stack restated in tower terms:

- **Layer 1 — Runtime adapters** is M0 territory: where models
  execute and traces are born, harness by harness.
- **Layer 2 — The marketplace** is M1 distribution governed by the
  M2 schema: models published, trusted, discovered, installed.
- **Layer 3 — Process composer** is the generic machinery the
  metamodel buys: composition, transformation, and evolution over
  models — the MOF payoff, applied to work instead of software
  models.

The mission line survives translation intact: *every way agents do
work can be captured (M0→M1), shared (M1 under M2 governance), and
improved (the loop closing through M0 again).*

## The example that makes it concrete: one verdict, three factories

The tower stops being abstract at a single line of test output. The
[assay](https://github.com/the-metafactory/assay) runner stamps every
corpus verdict with `cortex@<sha> · env@<digest>`: which build of the
software under test, standing on which environment.

Each half of that stamp is a factory speaking:

- The **software factory** produced the `cortex@<sha>` — a checkout
  installed at an exact pin by
  [arc](https://github.com/the-metafactory/arc), and the install
  proves the pin rather than trusting it.
- The **infrastructure factory**
  ([crucible](https://github.com/the-metafactory/crucible)) produced
  the `env@<digest>` — a VM manufactured from a spec, fingerprinted,
  and identified by nothing mutable: destroy it, rebuild it, and the
  digest either matches or the environment must explain itself.
- The **test factory** (assay) consumed both and issued the receipt:
  a verdict that names the exact software and the exact floor it
  stood on, so a finding that fails to reproduce elsewhere is
  *environment drift on the record*, not an argument.

In tower terms: the run is M0, the stamped receipt is that trace
captured into an M1 model, and the interchange contract between the
factories —
[`environments/README.md`](https://github.com/the-metafactory/assay/blob/main/environments/README.md),
which defines the file one factory writes and the other reads — is M2
doing its one job: letting factories built by different people, on
different providers, stay legible to each other at a seam instead of
an integration project.

This is also the honest state of the warning label: the wiring is
tracked in
[crucible#24](https://github.com/the-metafactory/crucible/issues/24),
and until the first factory-built run lands, the example above is a
contract, not yet a receipt. The base layer ships first; this
document gets to cite the receipt only after it exists.
