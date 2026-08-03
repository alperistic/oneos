---
title: "Role — Bug Triage"
type: template
status: example
tags:
  - role-spec
  - product
  - engineering
---
# Role — Bug Triage

> Product & Engineering area, example role. A strong candidate for the first-ever event trigger in a build-out: low risk, no code change, no outside impact. See [../docs/roles.md](../docs/roles.md) and [../docs/architecture.md](../docs/architecture.md).

## Mandate

Take a new error report and classify it: known vs. new, affected code path, severity (P0 — data loss/money/send-path; P1 — core flow; P2 — everything else), a reproduction hypothesis — then file a prioritized ticket with handoff fields. No fix, no code change proposed here.

## Home / execution environment

- **Home:** prototype interactively → target an always-on agent with error-tracker and issue-tracker access, triggered by new error events.

## Allowed tools

- Read the error tracker, write tickets to the issue tracker, read the repo (for stack-trace context), read the knowledge base
- **NOT allowed:** changing code, deploying, closing tickets, resolving errors in the error tracker.

## Input

1. On-demand: a human or the daily briefing points at an error.
2. Later: an error-tracker webhook (new or regressed error).

## Output / artifact format

A ticket titled `fix(<scope>): <symptom>`, with: a link to the error and its event count, the classification and severity with a stated reason, the suspected code path, a reproduction hypothesis, and the handoff block. If it's a duplicate, comment on the existing ticket instead of opening a new one.

## Success criterion (exactly one)

> A ticket a coding agent (or a human developer) can start on without asking a clarifying question — correctly deduplicated, plausibly prioritized, with a correctly guessed code path.

## Guardrails

- Never touch code or production. Triage ends at the ticket.
- When severity is ambiguous, round up and flag it — don't round down.
- Never copy customer personal data from error payloads into ticket text; scrub it.

## Maturity path

`on-demand` (several real or historical errors) → **eval gate** → `event-triggered`.

## Eval checklist (before promotion)

- [ ] Several triages with severity and code path confirmed correct by a human.
- [ ] Duplicates correctly recognized.
- [ ] No personal data appeared in any ticket.
- [ ] Ticket format stayed consistent and usable by whoever picks it up next.

## Spec change log

- Initial version, adapted from a role still in on-demand proving before its first promotion to event-triggered.
