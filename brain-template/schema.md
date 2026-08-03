---
title: "Knowledge Base Schema"
type: schema
status: active
tags:
  - knowledge-base
  - llm-wiki
  - schema
---
# Knowledge Base Schema

This schema defines how agents and humans maintain this vault as a Karpathy-style **LLM-maintained Markdown wiki**.

## Design goal

The vault should be a compounding knowledge artifact, not just a pile of retrieved documents.

- Raw material is preserved as source evidence.
- Durable knowledge is compiled into canonical Markdown notes.
- Whatever retrieval tooling you use (semantic search, grep, an index) reads the compiled vault.
- Agents keep the wiki maintained as they work on the business, its projects, research, and operations.

## Layer model

### 1. Inbox layer

Temporary landing zone.

- Path: `inbox/`
- Purpose: untriaged captures, imports, quick notes.
- Rule: should be processed into `sources/` or a domain note; do not let it become a permanent knowledge base by default.

### 2. Source layer

Raw or near-raw evidence.

- Path: `sources/`
- Purpose: original documents, copied source text, transcripts, imported files, source summaries.
- Rule: preserve source meaning. Do not silently rewrite a source as if it were compiled knowledge.
- Suggested subfolders: `sources/research/`, `sources/projects/`, `sources/meetings/`.

### 3. Compiled wiki layer

Distilled, linked knowledge that agents keep current.

- Project-specific: `projects/<project>/`
- Decisions: `decisions/`
- Ops/runbooks: `ops/`

This is the main layer to query and maintain.

### 4. Agent protocol layer

Rules for AI agents.

- `WORKFLOW.md` — full operating rules.
- `schema.md` — this file.
- `AGENTS.md` — concise protocol for agents.

## Note types

Use `type:` in YAML frontmatter where possible. Common values:

- `index` — folder home or navigation page.
- `context` — durable background/context page.
- `status` — current state and next bottlenecks.
- `source` — raw or near-raw imported evidence.
- `source-index` — index of source material.
- `decision` — decision record.
- `runbook` — repeatable ops/procedure note.
- `research` — research synthesis or finding.
- `template` — reusable prompt/protocol/template.

## Frontmatter standard

Minimum for new durable notes:

```yaml
---
title: "Readable Title"
created: YYYY-MM-DD
type: context
status: active
---
```

Recommended optional fields:

```yaml
updated: YYYY-MM-DD
tags:
  - project-name
source_refs:
  - "[[sources/example-source]]"
supersedes:
  - "[[old-note]]"
superseded_by: "[[new-note]]"
confidence: medium
---
```

## Canonical page pattern

For long-running projects, maintain these pages where useful:

```text
README.md              # folder index
context.md             # durable background and positioning
status.md              # current state, blockers, next actions
decisions.md           # decision log if decisions are frequent
research/README.md     # market/user/research synthesis
ops/README.md          # runbooks, infrastructure, recurring ops
```

Not every project needs all pages. Create only what is useful.

## Ingest rule

When a new source arrives:

1. Put the raw material in `inbox/` or `sources/`.
2. Identify which compiled wiki notes it affects.
3. Patch existing canonical notes before creating new duplicates.
4. Create a new compiled note only when no canonical page fits.
5. Add source links for traceability when a decision or claim depends on the source.
6. Update the nearest README/index.
7. Verify with a diff before committing.

## Writing rules

- Be factual, concise, and direct.
- Separate current status from historical context.
- Distinguish facts, assumptions, open questions, and decisions.
- Prefer bullet lists and dated sections for evolving state.
- Use wikilinks for important relationships.
- Do not store secrets or private credentials.
- Do not save temporary task progress that will be stale within a week.
