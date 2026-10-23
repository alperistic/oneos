# How Late runs

Late is run by one person with AI agents. This repository describes the
setup as it runs today and holds a template for its memory. The short
version lives at
[late-systems.vercel.app/system](https://late-systems.vercel.app/system).

## Memory: Markdown in Git

- One vault is the only shared memory: decisions, research, project
  state. Notes are filed by written rules (`AGENTS.md`, `WORKFLOW.md`,
  `schema.md`).
- Three writers: the founder in Obsidian, Claude Code on the Mac, and
  Hermes on a server. Each pulls with rebase before it writes.
- On the server, a job commits, rebases and pushes the vault every ten
  minutes, then re-indexes it for search. On a conflict it stops and
  reports instead of resolving it.
- Agents search the vault before they answer. What is not in the vault
  is not known.

→ [`brain-template/`](brain-template/)

## Building: Claude Code

- Every repository has a `CLAUDE.md`: commands, deploy path,
  conventions, and the honesty rules that apply there. A global file on
  top sets language, autonomy and when to stop and ask.
- Models are split by job. The main session plans and reviews. Code is
  written by a subagent on Opus from a spec (files, constraints,
  definition of done). Searching and small edits go to Sonnet.
- A hook blocks code edits of more than five lines in the main session,
  so the split holds. The rest of the routing is written discipline.
- One session, one pull request. The pull request body is the handoff.
  Review and fixes run in a new, short session.
- Working preferences carry between sessions as small memory files per
  project.

## Review: a second model

- Pull requests in offerre's repository run CI: tests, migrations up and
  down, lint, end-to-end tests in a browser, and a weekly dependency
  audit.
- Codex, a model from another vendor, reviews most of them on GitHub.
  Claude addresses its comments; the founder merges by hand.
- A local Codex review is kept for large or risky changes. Its findings
  are checked against the code before anything is changed.

## Running: Hermes

- Hermes is an agent on a rented server, reached over Telegram. Its
  dashboard is only reachable inside a private network.
- It works in profiles by domain: personal, business, inbox, ops,
  research and others. Profiles that face the outside, such as inbox
  and outreach, only write drafts.
- Scheduled jobs: the vault sync every ten minutes, a daily encrypted
  backup with a tested restore, and a daily check of the vault's Git
  state.

## Gates

- Human in the loop: nothing is merged, sent, published, deployed or
  paid without the person.
- No customer names, addresses or phone numbers in prompts.
- A fact that cannot be checked is marked as missing, not filled in.
- Pages and repositories claim only what runs. Planned things are
  labelled planned.

## Counted on 23 October 2026

| Count | Number |
|---|---|
| Notes in the vault | 712 |
| Vault commits in the last 30 days | 92 |
| Repositories with a CLAUDE.md | 11 |
| Hermes profiles | 13 |
| Agent skills written | 13 |
| Agent skills on a schedule | 0 |

## Written, barely used

Late also keeps a library of 13 skills for one central agent: lead
verification, outreach drafts, a weekly report, bug triage and others.
Each is started by hand, none runs on a schedule, and the last queue
entry is from August 2026. The specs and templates in this repository
come from that library.

## What breaks

- **Backups failed quietly.** From early August to 21 October the daily
  backup did not run, while the runbook said it did. A health check
  found it; the restore is now tested.
- **Memory drifts when filing stops.** A few days without notes and the
  vault no longer matches what happened.
- **Plans get too cheap.** Agents make strategy notes so easy to write
  that planning replaces shipping. Late keeps a rule against it and has
  broken it.
- **Several writers, one repository.** Conflicts happen. The sync stops
  and the person resolves them.

## In this repository

| Path | What it is |
|---|---|
| [`brain-template/`](brain-template/) | Vault skeleton: filing rules, note schema, routing, agent protocol |
| [`docs/`](docs/) | Architecture, gates and the eval path, written for the skill library |
| [`roles/`](roles/) | Four example specs from the skill library, generalized |
| [`templates/`](templates/) | Work queue, handoff block, empty spec |

## License

[MIT](LICENSE). Open source by Late.
