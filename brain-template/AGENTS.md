# AGENTS.md — Knowledge Base Protocol

This repository is a durable Markdown knowledge-base vault. Treat it as an LLM-maintained wiki, not a dump folder.

## Prime directive

Before answering or modifying durable project/business context, search the vault first. Do not guess facts that may already be recorded.

## Layer model

- `inbox/` — temporary untriaged captures.
- `sources/` — raw or near-raw evidence; preserve meaning, do not silently rewrite.
- `projects/`, `decisions/`, `ops/` — compiled wiki notes; update these when knowledge changes.
- `WORKFLOW.md` and `schema.md` — full rules.

## Editing rules

1. Patch canonical notes before creating duplicates.
2. Keep raw sources separate from compiled synthesis.
3. Use YAML frontmatter for new durable notes.
4. Use wikilinks for important relationships.
5. Never store secrets, tokens, passwords, or private credentials.
6. Do not dump whole folders, logs, repos, caches, or generated artifacts.
7. If a note is superseded but contains unique context, archive/link it instead of deleting it.
8. After edits, check the diff before committing.

## For project work

If code or project work changes durable knowledge, update the relevant vault note in the same work session — don't let it drift out of sync until someone notices. Start with a project's own `context.md`, `status.md`, and `README.md` before going wider.
