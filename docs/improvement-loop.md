# Improvement Loop

The [architecture.md](architecture.md) heartbeat loop (wake → read → do → verify → write → sleep) ends at "write result, escalate on failure." That's enough to run a role reliably. It is not enough to make the role *get better* over time. This document is the missing layer: how failures turn into sharper specs, without skipping the maturity gates in [roles.md](roles.md).

## Why this layer is easy to skip

An eval gate is a one-time check: did this role pass 3–5 runs? Once passed, nothing forces you to keep looking at it. Roles quietly drift — a spec that was right for the first five runs stops matching what the role actually encounters by run fifty. Without a deliberate loop, you only notice when the output quality has already degraded enough to annoy you.

## Two additions, deliberately small

### 1. A failure log

Every run that fails, or that you substantially had to rework by hand, gets a short note: which role, what went wrong, what the spec should have said instead. This is a writing convention, not a tool — a few lines in the knowledge base next to the role's other output is enough.

### 2. A weekly review

Once a week (or whatever cadence fits your volume), read the failure notes across all active roles and turn recurring patterns into **spec update proposals**. You approve the changes; nothing edits its own spec unsupervised. This is the same escalation discipline as everywhere else in the system — the loop closes back through your approval, not around it.

Add a short "spec change log" — one dated line per change — at the bottom of each role spec. That makes the learning visible and auditable instead of invisible tribal knowledge.

## The deliberate limit

It is tempting, once you see this pattern, to want an agent that watches its own failures and ships its own fixes overnight, unsupervised. Resist that for as long as your eval infrastructure is thin. The maturity path in [roles.md](roles.md) — on-demand → eval → scheduled → event-triggered — is the disciplined version of self-improvement. Skipping the gate to get overnight autonomy faster is exactly how a small mistake becomes a large, unnoticed one. Add this layer on top of roles that are already running well. Don't use it as a shortcut past the gate itself.
