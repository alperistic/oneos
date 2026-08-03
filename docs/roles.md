# Roles

This is the role catalog: the menu of jobs an agent team can hold in a one-person company, how each role matures, and the guardrails that apply to every single one of them regardless of function. For the org-level picture these roles sit inside, see [architecture.md](architecture.md). For example specs, see [roles/](../roles/) and the blank [templates/role-spec.md](../templates/role-spec.md).

## The role catalog principle

A role is not "an agent." It's a written mandate: what it's for, what it's allowed to touch, what counts as success, and what it must never do. You write the mandate once, as a spec, before you run it for real. The spec is the durable artifact; the agent executing it is replaceable.

Treat this the way you'd treat hiring: define the job before you fill it. A vague role produces vague, unverifiable output. A specific one — one clear input, one clear output, one success criterion — is something you can actually evaluate and trust.

## Three modes of operation

Every role runs in one of three modes, and every role starts at the bottom:

1. **On-demand / copilot** — you start it, you stay in the loop. Lowest risk, usable immediately. This is where every role begins, no exceptions.
2. **Scheduled / recurring** — runs on a timer without you (a morning briefing, a weekly digest). Reliable copilots graduate here.
3. **Event-triggered / autonomous** — reacts to an event (a new error, an inbound reply). Highest leverage, highest required care.

**Maturity path per role:** prove it on-demand → if reliable, promote to scheduled or triggered. Never automate an immature role, no matter how tempting the leverage looks. The failure mode of skipping this step is not "the role does slightly worse work" — it's "a mistake now happens without anyone watching."

## Guardrails that apply to every role

These are not per-role decisions. They apply uniformly, and a role spec that contradicts one of these is wrong, not exceptional.

- **No sensitive personal data in prompts.** Names, addresses, phone numbers, anything that identifies a real customer or private individual, stays out of agent prompts and outputs unless the role's entire purpose is handling that data under a defined lawful basis — and even then, minimize what's exposed.
- **A human is in the loop for anything with outside impact.** Sending (email/outreach), production deploys, legal or financial steps are approved by you, never triggered autonomously.
- **No money movement, ever.** A role touching bookkeeping-adjacent work can prepare and categorize. It never executes a payment or a transfer.
- **Every promoted role needs a quality check.** A simple eval that confirms output quality — otherwise you can't trust the role internally, and you definitely can't claim it externally (see the honesty principle in [architecture.md](architecture.md)).

## The role catalog

Organized by functional area. This is the full menu of *possible* roles — not all of them need to exist in your setup at once. See the honesty column in [architecture.md](architecture.md) for what "exists" should actually mean.

### A) Knowledge & Research

| Role | What it does | Needs | Maturity |
|---|---|---|---|
| **Market / competitor monitor** | Watches your market, competitors, industry news; produces a short digest into the knowledge base | Web search, knowledge base | on-demand → scheduled |
| **Knowledge-base steward** | Files and deduplicates durable knowledge per your filing rules, keeps an index current | Knowledge base (git-backed) | on-demand |
| **Insights / content research** | Sources evidence, examples, and use cases for building in public | Web search, knowledge base | on-demand → scheduled |

### B) Product & Engineering

| Role | What it does | Needs | Maturity |
|---|---|---|---|
| **Coding agent** | Feature work, bug fixes, refactors, following your project's own conventions | Coding tools, source control | on-demand |
| **Code / security review** | Checks changes for common failure classes before merge | Source control, repo | event (change proposed) |
| **QA / test author** | Writes missing tests, reproduces bugs as failing tests first | Repo, test runner | on-demand |
| **Bug triage** | Turns an error report into a prioritized, well-formed ticket | Error tracker, issue tracker | event-triggered |
| **Analytics insight** | Turns product usage data into "where are we losing users" | Analytics tool | scheduled (weekly) |
| **Release / deploy checklist** | Checks CI, migrations, health before a release — never deploys itself | Source control, repo | on-demand |
| **Tech-debt / dependency watcher** | Finds stale dependencies and risky areas, files them to the backlog | Repo | scheduled |

### C) Go-to-Market & Sales

| Role | What it does | Needs | Maturity |
|---|---|---|---|
| **Lead research & enrichment** | Finds and enriches target accounts against your ideal-customer profile | Web search, enrichment tools | on-demand |
| **Outreach drafting** | Personalized outbound sequences, drafted only — you send | Knowledge base, message templates | on-demand, **sending = human** |
| **Inbox triage & reply drafting** | Sorts inbound messages, proposes replies | Inbox access | on-demand → event |
| **CRM hygiene** | Keeps pipeline data current | CRM | scheduled |
| **SEO / content for your own site** | Keyword gaps, on-page suggestions | SEO tooling | on-demand |

### D) Operations & Admin

| Role | What it does | Needs | Maturity |
|---|---|---|---|
| **Daily briefing** | Morning summary: calendar, open tickets, priorities | Calendar, issue tracker, knowledge base | scheduled (daily) |
| **Backlog / project hygiene** | Keeps your issue tracker clean, proposes prioritization | Issue tracker | scheduled |
| **Meeting notes → action items** | Transcript to tasks, filed into the tracker or knowledge base | Notes/transcript tool, issue tracker | event |
| **Weekly report / metrics digest** | KPIs as a scorecard | Analytics, issue tracker, knowledge base | scheduled |
| **Bookkeeping prep** | Categorizes receipts, prepares reports — **no money movement** | Bookkeeping tool | on-demand |

### E) Insights / Content

| Role | What it does | Needs | Maturity |
|---|---|---|---|
| **"Building in public" log** | Turns real weekly work into shareable material | Knowledge base, source-control history | scheduled |
| **Content repurposing** | One piece of insight into multiple formats/channels | Knowledge base | on-demand |
| **Publishing-cadence keeper** | Reminds/stages scheduled publications | Calendar | scheduled |

### F) Meta / Orchestration

- **Founder-as-orchestrator.** You set direction and approve; agents execute. This is the actual shift in what your job looks like day to day — not "fewer tasks," but a different kind of task.
- **Eval / quality harness.** Measures whether promoted agents stay reliable — the precondition for claiming any role externally.

## Recommended build order

1. **Start with insights/research or the function with the most immediate, low-risk recurring demand in your business.** Look for double leverage: something that produces visible material *and* internal usefulness, with low risk if it's imperfect.
2. **Then product agents** (bug triage, QA, analytics) if you have a live product — these compound the fastest because engineering work is already artifact-based.
3. **Then GTM** (lead research, outreach drafts) — sending stays human-approved throughout.
4. **Ops runs continuously in the background** (daily briefing, backlog hygiene) — promote each piece once it's reliable.

> Don't stand up all of these at once. Get one role genuinely productive, document it honestly, then move to the next. That sequencing discipline — not the size of the catalog — is what makes "big ambition, narrow surface" actually true of how you operate, not just how you talk about it.

## See also

- [runbook.md](runbook.md) — the step-by-step rollout recipe for turning a role from spec to running
- [roles/](../roles/) — four worked example specs
- [templates/role-spec.md](../templates/role-spec.md) — the blank template to write your own
