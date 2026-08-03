# Runbook

This is the execution layer. [architecture.md](architecture.md) explains the org and system design; [roles.md](roles.md) explains the role catalog and how roles mature. This document answers: how do you actually build this, step by step — who does what, what foundations you set up once, the repeatable recipe per role, and the order to roll it out in.

## Section 0 — Division of labor

If you're running agents in more than one environment, decide the split explicitly and write it down. A common and effective split is a **desktop agent** you drive interactively, and an **always-on server agent** that runs unattended. The exact tools don't matter; the boundary does.

| Actor | Can | Cannot | Role in the build |
|---|---|---|---|
| **Desktop agent** (interactive, you're at the keyboard) | Write and edit knowledge-base content — specs, templates, eval checklists — research, draft artifacts | Own git history end-to-end, run on a schedule, run unattended | **Author of the foundations and specs.** Writes the durable templates into the knowledge base. |
| **Server agent** (always-on, unattended) | git operations, scheduling, running unattended, webhooks | Take outside-impact actions without approval | **Operator.** Pulls specs via git, sets up schedules, executes, commits results back. |
| **You** | Direction, approval, hard calls | — | **Orchestrator.** Approve specs, pass the eval gate, approve outside-impact actions. |

Basic flow: **desktop agent drafts a spec into the knowledge base → you review it → the server agent pulls it and operationalizes it → the server agent commits the result → you approve promotion.**

> If your setup only has one agent environment, collapse this to: draft on-demand, review, promote to scheduled once trustworthy. The principle — draft first, prove it, then automate — doesn't change with the number of environments.

## Section 1 — The foundations (build once, keep small)

Two conventions are enough to get started. You don't need a framework or a queue service.

### 1a. A work queue

One file as the central inbox. See [templates/work-queue.md](../templates/work-queue.md) for the exact format. Every entry looks like:

```
- id: Q-YYYYMMDD-NN
  for-role: <role>            # who should do this
  requested-by: <you/a role>  # who filed it
  task: <one scoped task>
  status: open | claimed | done | blocked
  output: <link to the result artifact, once done>
```

Agents read their own open entries (`for-role == me`, `status: open`), claim them, do the work, set `done` + `output`.

### 1b. The handoff artifact

Every handoff is a knowledge-base note (or a tracker ticket) with a fixed closing block — so the next agent, or the next you, can pick up work without live coordination. See [templates/handoff.md](../templates/handoff.md):

```
## Handoff
- Done: <what's finished>
- Open: <what's still missing>
- Next step: <concrete>
- Owner: <role/human>
- Confidence / sources: <evidence, uncertainties>
```

Product/engineering work uses a ticket in your issue tracker with the same fields in the description, instead of a knowledge-base note.

## Section 2 — The repeatable role recipe

Identical for **every** role. Doing one role for real beats ten half-built ones.

1. **Write the spec** (desktop agent, into `roles/<role>.md`): mandate, execution environment, allowed tools, input/output, **one** success criterion, guardrails, maturity path, eval checklist. Use [templates/role-spec.md](../templates/role-spec.md).
2. **Approve** (you): does the spec hold up?
3. **Run it on-demand** (server or desktop agent): 3–5 real runs, output filed into the knowledge base, each with a handoff block.
4. **Pass the eval gate** (you, checklist from Section 5): reliable enough?
5. **Promote** (server agent): a scheduled job **or** an event trigger. Never before.
6. **Log it** (server agent): commit the result; update the honesty column in [architecture.md](architecture.md).

## Section 3 — Rollout sequence across functional areas

You build **one role after another**, each gated on real proof it works. Match roles to whichever agent environment makes sense for their nature.

**The home rule:** *whatever needs you, or runs while you're already at the keyboard, lives with your interactive agent. Whatever needs to run without you, at any time or on any event, lives with your always-on agent.* The knowledge base is the shared substrate no matter where the compute runs; the always-on agent stays the owner of git, while the interactive agent only produces drafts into the vault.

| # | Area / role | Home | First concrete task | Target mode |
|---|---|---|---|---|
| 1 | Insights / research | server (prototype interactively first) | A weekly "building in public" digest from real work | scheduled (weekly) |
| 2 | Market / competitor monitor | server | Market/competitor digest into the knowledge base | scheduled |
| 3 | Bug triage | server | Error report → prioritized ticket | event-triggered |
| 4 | QA / test author | interactive coding agent | Missing tests for untested logic | on-demand |
| 5 | Analytics insight | server or interactive | Funnel drop-offs → "where are we losing users" | scheduled |
| 6 | Daily briefing | server or interactive | Morning: calendar, open tickets, priorities | scheduled (daily) |
| 7 | Backlog hygiene | server | Keep the tracker clean, propose prioritization | scheduled |
| 8 | Lead research & enrichment | interactive | Find and enrich target accounts | on-demand |
| 9 | Outreach drafting | interactive | Personalized sequences (draft only) | on-demand, **sending = human** |
| 10 | Inbox triage & reply drafting | server | Sort inbox, propose replies | event-triggered |
| 11 | Content repurposing | interactive | One insight → multiple formats | on-demand |
| 12 | Weekly report / metrics | server | KPI scorecard | scheduled |

> Promotion (scheduled/event) only happens after the eval gate. Until then, every role stays on-demand. **Home isn't fixed:** proving a role interactively and later moving it to your always-on agent once it's earned trust is the normal path, not an exception.

## Section 4 — Bringing the first role live

A worked walkthrough, using insights/research as the example (see [roles/research-digest.md](../roles/research-digest.md) for the full spec):

1. Write the spec and a queue entry.
2. Approve the spec.
3. Run 3–5 on-demand cycles → drafts filed into the knowledge base.
4. Pass the eval (Section 5). Publication stays human-gated regardless of eval outcome.
5. Set up the recurring schedule.

## Section 5 — The eval gate (what "reliable enough" means)

Lightweight, but mandatory. A role gets promoted when, across 3–5 runs:

- **Correctness:** no fabricated facts; claims are sourced or evidenced.
- **Format:** output matches the artifact format from the spec, including the handoff block.
- **Guardrails:** no outside-impact action was triggered, no sensitive personal data appeared in prompts or output.
- **Usefulness:** you would use the output with no rework, or only minimal rework.

Passes → promote to scheduled/event. Fails → sharpen the spec, stay on-demand. There is no partial credit here — a role that fails one of these criteria is not "mostly ready," it's not ready.

## Section 6 — Handing this off to an always-on agent

If you're briefing a separate always-on agent to operationalize a role, the brief is short: pull the relevant spec and queue entries, read them, run the on-demand cycles into the correct knowledge-base folder, commit after each run, wait for your explicit eval approval before setting up any schedule or trigger, and report back what was done and what's open after each cycle.

The one rule that matters more than the syntax: **never automate before the human says the eval passed.**

## Section 7 — Status tracking

Keep a running checklist per role somewhere durable (a knowledge-base note, or the tracker):

- [ ] Spec written and approved
- [ ] Recipe run (foundations in place: work queue, handoff format)
- [ ] On-demand runs complete
- [ ] Eval gate passed
- [ ] Promoted (scheduled or triggered)
- [ ] Next role in the sequence started

## See also

- [architecture.md](architecture.md) — the org and system design this runbook executes
- [roles.md](roles.md) — the full role catalog and guardrails
- [improvement-loop.md](improvement-loop.md) — what happens after a role is running: how it gets better over time
