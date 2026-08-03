---
title: "Knowledge Base Operating Rules"
type: workflow
status: active
tags:
  - knowledge-base
  - llm-wiki
  - agents
---
# Knowledge Base Operating Rules

This vault is the durable shared knowledge layer for every agent and every human working on the company — whatever environments those agents run in (desktop, server, browser).

It follows a Karpathy-style **LLM Wiki pattern**: raw sources are preserved, and agents compile durable knowledge into structured, interlinked Markdown notes that compound over time instead of being rediscovered from scratch every session.

## Core model

```text
inbox/      -> temporary untriaged captures
sources/    -> immutable or minimally edited source material
wiki notes  -> distilled, linked, agent-maintained knowledge in projects/, decisions/, ops/, etc.
schema.md   -> conventions agents must follow when reading/writing the vault
AGENTS.md   -> short operational protocol for agents
```

The important rule: **do not make an agent rediscover everything from raw documents every time it runs.** Ingest a source once, then update the durable wiki pages it affects.

## What goes where

- **Agent memory (if your tooling has one):** stable working preferences, recurring conventions — not durable business knowledge.
- **This vault:** notes, plans, references, project context, decisions, and evolving knowledge. This is the actual asset.
- **Sources:** raw or near-raw evidence that should not be silently rewritten.
- **Any skills/playbooks your agents use:** repeatable workflows and troubleshooting procedures, kept separate from the knowledge itself.

## Directory map

Adjust this to your own business, but keep the separation between raw and compiled:

- `projects/<project>/` — project-specific compiled wiki: context, status, decisions, ops, research, technical notes.
- `decisions/` — decision records and rationale.
- `ops/` — infrastructure, runbooks, monitoring, recurring operational notes.
- `sources/` — raw imports, snapshots, transcripts, documents, source indexes.
- `inbox/` — untriaged captures, waiting to be filed.

## Operating rules

1. **Search first.** Before answering or writing about existing context, search the vault.
2. **Do not guess durable context.** If the vault does not resolve an ambiguity, ask the human.
3. **Keep sources and synthesis separate.** Raw documents go in `sources/` or temporary `inbox/`; distilled knowledge goes into the compiled wiki pages.
4. **Prefer updating canonical pages over creating duplicates.** Patch existing project indexes, status pages, and context notes when they already exist, instead of adding a new note that says almost the same thing.
5. **Link related notes.** Use wikilinks for important relationships.
6. **Archive, don't destroy, unique context.** A superseded note with unique details moves to an archive location with a `superseded_by` note, rather than being deleted.
7. **No secret storage.** Never store API keys, tokens, passwords, or private credentials in the vault.
8. **No machine dumps.** Do not dump whole folders, logs, repos, or exports into the vault. Import curated material and add a routing/index note instead.
9. **After changes, verify.** Check the diff before committing.

## Ingest workflow

For any substantial new source:

1. Save or locate the raw input under `inbox/` or `sources/`.
2. Identify which canonical notes it affects.
3. Extract durable facts, decisions, dates, open questions, and relationships.
4. Patch or create compiled wiki notes in the appropriate domain.
5. Add links back to the source material when the source needs to remain traceable.
6. Update the nearest README/index if you created a new page worth finding later.
7. Check git status/diff before committing.

## Compiled note standards

Good compiled notes are:

- stable and reusable across sessions
- short enough to scan
- explicit about current status vs. historical evidence
- linked to related notes
- sourced when a claim matters
- updated in place instead of duplicated

Bad compiled notes are:

- raw transcript dumps
- one-off logs with no lasting structure
- duplicated versions with no canonical page
- unsourced claims that read as if they were verified
- stale plans with no status marker

## Multi-writer convention

If more than one agent (or agent environment) writes to this vault, the rule that keeps them from colliding is simple: **each area has one place that owns writes to it, and everyone else reads.** Scope folders by functional area (see [architecture.md](../docs/architecture.md) for the areas), and pick one agent environment as the git owner if more than one exists — see [runbook.md](../docs/runbook.md) Section 0 for a worked example of a two-environment split.
