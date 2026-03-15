---
verification_status: unverified
verified_by: null
phase: 0
tags: [meta, agents, registry]
---

# Agent Registry

## PURPOSE

Records current agent assignments: which model fills each role, which provider, prompt version, and status. Updated when agents are swapped, models are upgraded, or roles are added.

**MAINTAINED BY:** COO (on agent changes), PM (audits currency).

---

## Active Agents

| Role | Model | Provider | Prompt Version | Owned Directory | Status | Assigned Date | Notes |
|---|---|---|---|---|---|---|---|
| COO | [model] | [provider] | [version/date] | research/, writeups/ | [active] | [date] | |
| Librarian | [model] | [provider] | [version/date] | literature/ | [active] | [date] | |
| Red Team | [model] | [provider] | [version/date] | adversarial/ | [active] | [date] | MUST be different provider than COO |
| Lab Tech | [model] | [provider] | [version/date] | code/ | [active] | [date] | |
| Liaison | [model] | [provider] | [version/date] | liaison/ | [active] | [date] | |
| Scout | [model] | [provider] | [version/date] | scouting/ | [active] | [date] | OpenClaw instance |
| Scribe | [model] | [provider] | [version/date] | (none — shared docs) | [active] | [date] | |
| PM | [model] | [provider] | [version/date] | _meta/ | [active] | [date] | Cron schedule: [interval] |

---

## Model Change History

| Date | Role | Old Model | New Model | Reason | Changed By |
|---|---|---|---|---|---|
| | | | | | |

---

## Provider Diversity Check

*Red Team MUST be a different provider than COO. Verify on every model change.*

- COO provider: [PROVIDER]
- Red Team provider: [PROVIDER]
- Providers match: [YES = VIOLATION / NO = OK]
