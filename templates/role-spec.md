---
title: "Role — <Name>"
type: template
status: draft
tags:
  - role-spec
---
# Role — <Name>

> <Functional area> area. See [../docs/roles.md](../docs/roles.md) (catalog) and [../docs/architecture.md](../docs/architecture.md) (area mandate).

## Mandate

<One paragraph: what this role does, in concrete terms. What does it turn into what? What does it explicitly not do?>

## Home / execution environment

- **Home:** <interactive agent / always-on agent / either, with a note on which>

## Allowed tools

- <tool 1>
- <tool 2>
- **NOT allowed:** <explicit list of what this role must never touch>

## Input

1. <where work comes from — a queue, a schedule, an event>

## Output / artifact format

<Exact shape of what this role produces: file location/naming, required frontmatter, required closing handoff block>

## Success criterion (exactly one)

> <A single sentence a human could check a finished output against. Not a list — one criterion, precise enough to fail on.>

## Guardrails

- <Guardrail 1 — usually inherited from the catalog-wide guardrails in roles.md, plus anything specific to this role>
- <Guardrail 2>

## Maturity path

`on-demand` (<N> runs) → **eval gate** → `<scheduled | event-triggered>`.

## Eval checklist (before promotion)

- [ ] <Correctness check specific to this role>
- [ ] <Format check>
- [ ] <Guardrail check>
- [ ] <At least one output a human confirmed was usable with no rework>

## Spec change log

- <date> — <what changed and why, one line>
