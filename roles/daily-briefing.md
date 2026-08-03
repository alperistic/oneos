---
title: "Role — Daily Briefing"
type: template
status: example
tags:
  - role-spec
  - ops
---
# Role — Daily Briefing

> Operations area, example role. The orchestrator's cockpit: turns your morning routine into a single page instead of scrolling through several tools. See [../docs/roles.md](../docs/roles.md) and [../docs/runbook.md](../docs/runbook.md) Section 3.

## Mandate

Every morning, produce one page: today's calendar, any outreach touches that are due, approvals waiting on you, relevant issue-tracker movement, and **the single most important task for the day** (a proposal, not a decision). Prioritization logic: whatever moves the business toward its current top goal outranks everything else.

## Home / execution environment

- **Home:** start on an interactive agent's scheduled-task feature for the fastest start; target an always-on agent on a daily cron once proven.

## Allowed tools

- Read calendar, read issue tracker, read knowledge base (work queue, project status notes), read inbox (counts/subjects only, not full content)
- Write the knowledge base (the briefing note itself)
- **NOT allowed:** changing anything. This is a read-and-summarize role only.

## Input

A standing schedule. No queue pull needed.

## Output / artifact format

One note or message, roughly one page, fixed shape: appointments → due touches → pending approvals → tracker delta → "Most important task today: …" (one sentence, with a reason).

## Success criterion (exactly one)

> You start the day by reading the briefing instead of scrolling your inbox or tracker — nothing important is missing, nothing unimportant is padded in.

## Guardrails

- Read-only, never a write/change action.
- Never open or quote sensitive message content — counts and subjects only.
- The priority suggestion is a suggestion. The decision stays yours.
- If a data source is unreachable, name the gap. Never guess to fill it.

## Maturity path

`on-demand`/manual (several mornings) → **eval gate** → `scheduled` daily.

## Eval checklist (before promotion)

- [ ] Several briefings checked for completeness against calendar/tracker/queue.
- [ ] Format stable, one page or less.
- [ ] "Most important task" judgment matched your own on repeated checks.
- [ ] No write actions were ever triggered.

## Spec change log

- Initial version, adapted from a role that ran several real morning cycles before being folded into a broader daily-planning ritual.
