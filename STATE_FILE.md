---
verification_status: verified
verified_by: scribe
phase: 0
tags: [state, meta]
---

# STATE FILE

## TEMPLATE PURPOSE

Machine-readable state file for cold-start and cold-resume operation. This is the FIRST file any agent should read when beginning or resuming work. The Scribe maintains this file based on notifications from all agents.

**MAINTAINED BY:** Scribe (exclusively). No other agent modifies this file.

---

## Project Identity

- PROJECT_NAME: [FROM SCOPE DOCUMENT]
- PROJECT_ID: [FROM SCOPE DOCUMENT]
- PROJECT_STATUS: [ACTIVE / PAUSED / COMPLETED / KILLED]

---

## Current Position

- PHASE: [0-8]
- PHASE_NAME: [Human-readable phase name]
- STEP: [Step number within phase]
- STEP_STATUS: [NOT_STARTED / IN_PROGRESS / COMPLETE / BLOCKED]
- STEP_DESCRIPTION: [What is happening right now]
- SUBSTEP: [If within a multi-part step]

---

## Next Action

- NEXT_ACTION: [Specific next thing to do]
- NEXT_ACTION_OWNER: [Which agent should do it]
- NEXT_ACTION_REFERENCE: [Where in process docs this is defined]

---

## Pending Actions

- [ ] [ACTION 1 — assigned to AGENT]
- [ ] [ACTION 2 — assigned to AGENT]

---

## Active Delegated Tasks

| Task ID | Assigned To | Description | Status | Due |
|---|---|---|---|---|

---

## Completed Gates

| Gate | Result | Date | PI Approved | Notes |
|---|---|---|---|---|
| GATE_0 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_1 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_2 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_3 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_4 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_5 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_6 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |
| GATE_7 | [PASS/FAIL/NOT_EVALUATED] | [DATE] | [YES/NO/N/A] | |

---

## Blocking Issues

- [ISSUE AND WHAT'S NEEDED TO RESOLVE]

---

## Key Context for Cold Start

*5-10 sentences: what's happening right now, not a project summary.*

[WRITE HERE]

---

## Active Agents

| Role | Model | Provider | Status | Last Active |
|---|---|---|---|---|
| COO | [model] | [provider] | [active/idle] | [timestamp] |
| Librarian | [model] | [provider] | [active/idle] | [timestamp] |
| Red Team | [model] | [provider] | [active/idle] | [timestamp] |
| Lab Tech | [model] | [provider] | [active/idle] | [timestamp] |
| Liaison | [model] | [provider] | [active/idle] | [timestamp] |
| Scout | [model] | [provider] | [active/idle] | [timestamp] |
| Scribe | [model] | [provider] | [active/idle] | [timestamp] |
| PM | [model] | [provider] | [active/idle] | [timestamp] |

---

## Recent Decisions (last 5)

*From DECISION_LOG.md — for quick context.*

1. [DATE — BRIEF SUMMARY]
2. [DATE — BRIEF SUMMARY]
3. [DATE — BRIEF SUMMARY]
4. [DATE — BRIEF SUMMARY]
5. [DATE — BRIEF SUMMARY]

---

## Last Updated

- TIMESTAMP: [ISO 8601]
- UPDATED_BY: scribe
- UPDATE_REASON: [What triggered this update]
