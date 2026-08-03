---
title: "Role — Lead Verification & Enrichment"
type: template
status: example
tags:
  - role-spec
  - gtm
  - outreach
---
# Role — Lead Verification & Enrichment

> Go-to-Market area, example role. See [../docs/roles.md](../docs/roles.md) (catalog) and [../docs/architecture.md](../docs/architecture.md) (Go-to-Market area). This is a worked example of a role that reached eval-passed status — kept on-demand by deliberate choice, not promoted.

## Mandate

Take a raw lead entry and make it **outreach-ready**: fill in missing fields (a verifiable contact email, the decision-maker's name, a personalization hook), verify fit against your ideal-customer profile, and — where asked — research new candidates matching that profile. This role supplies the ammunition. It never sends anything.

## Home / execution environment

- **Home:** interactive agent (runs on-demand, while you're at the keyboard).
- Fallback if later moved to an always-on agent: a scoped profile with web research and CRM-write access only.

## Allowed tools

- Web search / page fetch (company website, public business registration data)
- Read/write the knowledge base (lead list), read/write your CRM
- **NOT allowed:** any form of sending or messaging, social-media scraping, private/non-public data sources.

## Input

1. Work-queue entries tagged for this role.
2. Entries in your lead list marked as incomplete.

## Output / artifact format

Updated entries in the lead list (knowledge base) and CRM, plus one short batch note per batch with a handoff block: what was verified, what couldn't be found, what was cleanly excluded as a non-fit.

## Success criterion (exactly one)

> After the run, a lead entry is outreach-ready without further research: a verifiable business contact email, a named decision-maker, and a sourced personalization hook are present — or the lead is cleanly excluded as a non-fit, with the reason stated.

## Guardrails

- **Only publicly listed business contacts**, sourced from a lawful public source (e.g., a company's own published registration/imprint data). Flag personal-looking addresses (free consumer email domains) rather than approving them; never scrape private sources.
- Never fabricate a missing data point — mark it missing, don't estimate it.
- No sending, no contact initiation of any kind — research only.

## Maturity path

`on-demand` (batches of real leads = eval runs) → **eval gate** → stays on-demand (this is a demand-driven role; move to scheduled only if you have a continuous, ongoing stream of new leads rather than periodic batches).

## Eval checklist (before promotion)

- [ ] Multiple batches with zero fabricated data; every field has a source.
- [ ] No private/personal addresses approved for outreach.
- [ ] Batch notes include the handoff block; knowledge base and CRM stay consistent.
- [ ] At least one batch marked by you as "outreach-ready with no rework."

## Spec change log

- Initial version, adapted from a role that passed its eval with real batches of prospect data.
