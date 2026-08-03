---
title: "Work Queue"
type: template
status: active
tags:
  - agents
  - queue
---
# Work Queue

The central inbox for agent work. See [../docs/runbook.md](../docs/runbook.md) Section 1a. Agents read open entries with `for-role == them`, claim them, do the work, then set `status: done` and fill in `output`. Both humans and agents may add entries.

## Schema

```
- id: Q-YYYYMMDD-NN
  for-role: <role>
  requested-by: <human/role>
  task: <one scoped task>
  status: open | claimed | done | blocked
  output: <link to the result, once done>
```

## Open

The two entries below are fictional examples showing the expected shape — replace them with your own.

```
- id: Q-20260115-01
  for-role: research-digest
  requested-by: you
  task: Eval run 1 — a first weekly digest of real work (source-control history +
    knowledge-base status). Sourced, draft-only.
  status: open
  output:

- id: Q-20260115-02
  for-role: bug-triage
  requested-by: you
  task: Eval run 1 — triage the three oldest unresolved errors in the error
    tracker as a dry run, using historical data.
  status: open
  output:
```

## Done

Move completed entries here once `output` is filled in, so `Open` stays short and scannable.
