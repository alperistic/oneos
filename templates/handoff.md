---
title: "Handoff Block"
type: template
status: active
tags:
  - agents
  - handoff
---
# Handoff Block

Append this block to the end of every artifact an agent hands off — a knowledge-base note or an issue-tracker ticket. It's what lets the next agent, or the next you, pick up the work without needing live coordination. See [../docs/architecture.md](../docs/architecture.md) Part B, Section 4.

```
## Handoff
- Done: <what's finished>
- Open: <what's still missing>
- Next step: <concrete, actionable>
- Owner: <role or human responsible for the next step>
- Confidence / sources: <evidence backing the claims above, and any real uncertainties>
```

## Notes on filling it in well

- **Done** is a fact, not a summary of effort. "Verified the contact email against the company's published imprint" is a done fact. "Worked on verification" is not.
- **Open** should be specific enough that the next reader doesn't have to reread the whole artifact to find the gap.
- **Next step** names an action, not a vague direction. "Escalate to a human for the ICP judgment call" is a next step. "Follow up" is not.
- **Owner** is a single name or role — a handoff with no clear owner is a handoff that stalls.
- **Confidence / sources** is where you admit what you don't know. A handoff that hides uncertainty is worse than one that states it plainly, because the next step will be built on a false floor.
