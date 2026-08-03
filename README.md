# oneOS

**The operating system of a one-person company.**

*I run a software company alone — a German B2B SaaS with real users, real
GDPR constraints, and real production incidents. What makes that workable
isn't one heroic AI assistant. It's an operating system: a shared memory,
a handful of defined roles, and rules about what agents may and may not do.
This repo is that system, extracted as a template — including the parts
that don't work yet.*

## The problem nobody tells you about

Everyone shows you the demo where an agent writes code. Nobody shows you
week three, when you have five chat histories with five different
"assistants", none of them knows what the others did, and you've become a
full-time messenger between your own tools.

The bottleneck of a one-person company was never typing speed. It's state:
who knows what, what's decided, what's next. A human team solves this with
meetings and shared context. My agents don't attend meetings. So they need
something better.

## The one rule everything follows

> **Agents research, draft and prepare. Deterministic systems calculate and
> check. The human decides everything that touches the outside world.**

This came out of building my product, where an LLM extracts a customer
request but is never allowed to invent a price — prices come from a
database, totals from tested code. Generalized, it became the constitution
of the whole company. Every rule in this repo is this rule applied
somewhere.

## A real day

Morning: I read a briefing an agent assembled from the work queue, the
issue tracker and the pipeline — and decide the one thing that matters
today. During the day: I dispatch tasks in plain language; roles do their
work and file artifacts; git commits accumulate in the Brain. Evening: I
review and approve what wants to leave the building — an outreach draft, a
PR, a post. My calendar has almost no execution left in it. What remains is
judgment.

That's the end state this template points at. You won't start there, and
neither did I — see the maturity path below.

## Getting started

Day one, in four steps. Don't skip ahead.

1. **Create your Brain.** Copy [`brain-template/`](brain-template/) into a
   fresh git repo. This becomes the only shared memory: every decision,
   research note and project state lives here as a markdown file, filed by
   a written routing rule. If it's not in the Brain, it didn't happen.
2. **Spec one role.** Copy [`templates/role-spec.md`](templates/role-spec.md)
   and fill it in for the most annoying recurring task you have. One
   mandate, allowed tools, one success criterion, hard guardrails. Steal
   from the four examples in [`roles/`](roles/).
3. **Run it on-demand.** You start it, you watch it, it ends every run by
   writing a handoff note ([`templates/handoff.md`](templates/handoff.md))
   and updating the work queue
   ([`templates/work-queue.md`](templates/work-queue.md)).
4. **Make it earn its promotion.** After a few real runs, score it against
   the eval checklist in its spec. Only a role that passes on real work
   gets scheduled. Until then it stays supervised.

## The architecture, in one diagram

```
        Me — direction, approvals, hard calls
                        │
        ┌───────────────┼────────────────┐
   orchestration: dispatch · eval · brain steward
        │               │                │
  Knowledge/Research  Product/Eng     Go-to-Market
  Insights/Content    Operations
        │               │                │
        └────────── the Brain ───────────┘
        (git-backed markdown, the only shared memory)
```

Five things carry the system:

1. **The Brain — one memory, under version control.** A plain markdown
   vault, git-backed, synced between my laptop, an always-on server agent,
   and my notes app. No agent "remembers" anything privately. Agents are
   disposable; the Brain is the asset. →
   [`docs/architecture.md`](docs/architecture.md)
2. **Handoffs are artifacts, not conversations.** Agents never talk to each
   other live. One finishes by writing a note with a fixed closing block —
   *what's done, what's open, next step, who's up, confidence* — and the
   next one reads it. Any agent (or I) can pick up any thread cold, weeks
   later. Amnesia becomes a feature. →
   [`templates/handoff.md`](templates/handoff.md)
3. **A work queue that is just a file.** No queue service, no framework.
   One markdown file: task, role, status, output link. I can read my
   company's entire backlog in one screen. →
   [`templates/work-queue.md`](templates/work-queue.md)
4. **Roles with a maturity path.** Every role starts as a spec, then has to
   earn autonomy: on-demand (I start it, I watch it) → eval gate (does it
   pass real checks on real work?) → scheduled (it runs without me). Never
   automate a role that hasn't earned it. → [`docs/roles.md`](docs/roles.md)
5. **Hard boundaries the system stops at.** Every send, publish, deploy and
   payment requires me. Customer master data never enters a prompt (GDPR
   isn't optional in Germany). Money is handled by code with decimals,
   never by a model. When an agent isn't confident, its job is to mark and
   escalate, not to guess. → [`docs/architecture.md`](docs/architecture.md)

## The honest part

Current state of my own instance of this system:

| Stage | Roles |
|---|---|
| Specified | 13 |
| Running for real (on-demand, supervised) | 4 |
| Scheduled / event-triggered | 0 |
| Fully autonomous | 0 |

The four that run: coding, brain-stewardship, research digests, and lead
verification — the last one passed its eval gate on three batches of live
work. Most "agent company" posts skip this column. I think the maturity
path *is* the product.

## What breaks (so you don't have to find out)

- **The system rots without daily use.** Skip three days of filing and the
  Brain drifts from reality; every artifact after that inherits the drift.
  Git discipline — pull, small commits, push — is the actual load-bearing
  habit, and it's boring.
- **Concept production is a failure mode.** Agents make writing strategy
  documents so cheap that "planning" becomes procrastination with extra
  steps. I had to write an explicit rule: after this note, ship code or
  nothing. I've broken it more than once.
- **Autonomy is earned slower than you want.** My promotion pipeline exists
  precisely because the first "just let it run" experiments produced
  confident garbage.
- **Three writers, one repo, real merge conflicts.** Me, a desktop agent
  and a server agent share the vault. The only fix is discipline: rebase
  before, push after, and a human resolves conflicts.

One of my favorite failures: a research agent couldn't find a repo it
expected, and instead of hallucinating progress, it labeled every claim it
couldn't check as "unverified". That's the system working.

## What's in this repo

| Path | What it is |
|---|---|
| [`docs/architecture.md`](docs/architecture.md) | The full system: principles, boundaries, eval loop, maturity stages |
| [`docs/roles.md`](docs/roles.md) | How roles are defined, operated and promoted |
| [`docs/runbook.md`](docs/runbook.md) | Division of labor between you, a desktop agent and a server agent; rollout sequence |
| [`docs/improvement-loop.md`](docs/improvement-loop.md) | How the system learns from its own failures |
| [`brain-template/`](brain-template/) | The Brain skeleton: filing rules, note schema, routing, agent protocol |
| [`roles/`](roles/) | Four worked example specs, generalized from real roles in the catalog: lead verification, daily briefing, bug triage, research digest |
| [`templates/`](templates/) | Work queue, handoff block, empty role spec |

## Why I published this

Frameworks answer "how do I orchestrate agents in code". Almost nobody
answers "how do I run a company with an agent team" — with the file
structure, the role specs, the queue, the handoff format, the eval
checklist. So I extracted mine: an opinionated template, zero
configuration, exactly the way I run it. Not because it's perfect —
because it's real, and it built a real product.

Take it, run one role on-demand this week, and make it earn its promotion.

*Built solo, in public.*

## License

[MIT](LICENSE)
