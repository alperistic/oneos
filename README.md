# How Late runs

Late is run by one person with AI agents. This repository describes how
work, memory and decisions move inside Late, and holds the templates it
uses. The same description lives at
[late-systems.vercel.app/system](https://late-systems.vercel.app/system).

## The rule

**A model drafts, code checks, a person decides.**

Models read, research and write drafts. Code computes and checks: totals,
prices, formats, tests. A person makes every call that leaves the house:
sending, publishing, deploying, paying. Every other rule in this
repository is this one applied somewhere.

## The parts

1. **Memory is Markdown in Git.** One vault is the only shared memory.
   Decisions, research and project state are notes, filed by a written
   routing rule. A job on a server commits, rebases and pushes the vault
   every ten minutes, and stops on a conflict instead of resolving it.
   → [`brain-template/`](brain-template/)
2. **One agent, a library of skills.** Each skill is a file: what it is
   for, which tools it may use, where its output goes, its guardrails and
   its eval. The agent reads the skills that fit the task and works.
   → [`templates/role-spec.md`](templates/role-spec.md)
3. **The work queue is one file.** Each entry has an id, a skill, a
   status (open, claimed, done, blocked) and a link to its output.
   → [`templates/work-queue.md`](templates/work-queue.md)
4. **Every run ends with a handoff block.** Done, open, next step, who is
   up, confidence and sources. The next run, or the person, picks up from
   the note, not from a chat. → [`templates/handoff.md`](templates/handoff.md)
5. **The gates do not move.** No sending, publishing, deploying, calendar
   commitments or payments without the person. No customer names,
   addresses or phone numbers in prompts. A fact that cannot be checked is
   marked as missing, not filled in.
   → [`docs/architecture.md`](docs/architecture.md)

## Maturity

Counted from Late's skill library on 23 October 2026.

| Stage | Skills |
|---|---|
| Written | 13 |
| Parked | 1 |
| Started by a person, each run | 12 |
| Passed an eval on real work | 1 |
| Scheduled or event-triggered | 0 |
| Fully autonomous | 0 |

A skill moves onto a schedule only after it passes its eval on real work,
and only when the founder says so. None has been moved yet.

## What breaks

- **Memory drifts when filing stops.** A few days without notes and the
  vault no longer matches what happened. Everything written after that
  inherits the gap.
- **Plans get too cheap.** Agents make strategy notes so easy to write
  that planning replaces shipping. Late keeps a rule against it and has
  broken it.
- **Several writers, one repository.** The person, a desktop agent and a
  server job all write to the vault. Conflicts happen; the sync stops and
  the person resolves them.
- **Autonomy comes slower than expected.** The first runs left alone
  produced confident, wrong output. The eval gate exists because of them.

## In this repository

| Path | What it is |
|---|---|
| [`docs/architecture.md`](docs/architecture.md) | Principles, gates, eval loop, maturity stages |
| [`docs/roles.md`](docs/roles.md) | How a skill is written, run and promoted |
| [`docs/runbook.md`](docs/runbook.md) | Who does what: the person, a desktop agent, a server agent |
| [`docs/improvement-loop.md`](docs/improvement-loop.md) | How a failure turns into a rule |
| [`brain-template/`](brain-template/) | Vault skeleton: filing rules, note schema, routing, agent protocol |
| [`roles/`](roles/) | Four example specs, generalized from Late's own: lead verification, daily briefing, bug triage, research digest |
| [`templates/`](templates/) | Work queue, handoff block, empty spec |

The docs still call a skill a "role". The fields are the same.

## Using it

1. Copy [`brain-template/`](brain-template/) into a new Git repository.
2. Write one spec from [`templates/role-spec.md`](templates/role-spec.md)
   for a task that recurs.
3. Start every run by hand. End every run with the handoff block and a
   queue update.
4. Put it on a schedule only after it passes its eval on real work.

## License

[MIT](LICENSE). Open source by Late.
