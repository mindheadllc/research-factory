# Research Factory: Process Design

## DOCUMENT PURPOSE

This is the **master orchestration document** for a solo-researcher virtual lab that uses AI language models as a multi-agent research team to conduct **computational interdisciplinary research**. It describes:

- The **research process**: phased pipeline from idea to publication-ready results.
- The **organizational layer**: agent roles, responsibilities, and coordination.
- The **infrastructure**: shared file tree, git workflow, task orchestration.
- The **quality system**: checklists, adversarial review, PI checkpoints, and external validation.

This document tells you **what to do, when, and in what order**. It references companion documents for detailed checklists, prompts, agent identity specs, and templates.

---

## HOW TO USE THIS DOCUMENT

**If you are the COO agent starting fresh (cold start):**

1. Read this entire document first.
2. Read the project's `STATE_FILE.md` (in the project's `research/` directory).
3. If no `STATE_FILE.md` exists, the project has not started. Begin at Intake.
4. Go to the relevant phase section, follow its instructions, and delegate to sub-agents as specified.

**If you are the COO agent resuming work (cold resume):**

1. Read this document.
2. Read `research/STATE_FILE.md` for current phase, step, and pending actions.
3. Read `research/DECISION_LOG.md` (last 10 entries) for recent context.
4. Check your task management system for any outstanding delegated tasks and their status.
5. Resume at the indicated step.

**If you are a sub-agent (Librarian, Red Team, Lab Tech, Liaison, Scout, Scribe, PM):**

1. Read your own identity document in `agents/[YOUR_ROLE].md` first.
2. Check your task management system for active tasks.
3. Read your own `_INDEX.md` in your owned directory for your working state.
4. Execute your tasks per your identity document's protocols.
5. You do NOT need to read this entire Process Design document — your identity document tells you what you need to know about the overall process. However, if you need process context beyond your role, this document is the authoritative source.

**If you are the PI (human researcher):**

This is your operations manual. The README provides the short version. This document is the detailed reference for when you want to understand what the team is doing and why.

---

## COMPANION DOCUMENTS

| Document | Location | Purpose |
|---|---|---|
| Phase Checklists | `01_PHASE_CHECKLISTS.md` | Step-by-step verification at each phase, with embedded adversarial review |
| Prompt Library | `02_PROMPT_LIBRARY.md` | All LLM prompts organized by phase and purpose |
| Domain Failure Modes | `03_PROJECT_DOMAIN_RISKS.md` | Known risks for the specific research domains (project-specific) |
| Agent: COO | `agents/COO.md` | COO identity, scope, protocols |
| Agent: Librarian | `agents/LIBRARIAN.md` | Librarian identity, scope, protocols |
| Agent: Red Team | `agents/RED_TEAM.md` | Red Team identity, scope, protocols |
| Agent: Lab Tech | `agents/LAB_TECH.md` | Lab Tech identity, scope, protocols |
| Agent: Liaison | `agents/LIAISON.md` | Liaison identity, scope, protocols |
| Agent: Scout | `agents/SCOUT.md` | Scout identity, scope, protocols |
| Agent: Scribe | `agents/SCRIBE.md` | Scribe identity, scope, protocols |
| Agent: PM | `agents/PM.md` | Project Manager identity, scope, protocols |
| Templates | `templates/` | Blank per-project documents |
| Spike Template | `templates/SPIKE.md` | Rapid feasibility assessment for Tier 1 |
| Expert Engagement Protocol | `templates/EXPERT_ENGAGEMENT.md` | How to seek, document, and act on external expert feedback |

---

## PART 1: ORGANIZATIONAL ARCHITECTURE

### Agent Roles

```
PI (Human)
  │
  ├── COO (frontier model — research reasoning, synthesis, PI interface)
  │     Owns: research/, writeups/
  │     Reads: everything
  │     Delegates via: task management system
  │
  ├── Librarian (mid-tier model + API tools)
  │     Owns: literature/
  │     Writes to: research/CLAIMS_REGISTRY.md
  │
  ├── Red Team (different provider's frontier model)
  │     Owns: adversarial/
  │     Reads: artifacts under review only (NOT COO's reasoning)
  │
  ├── Lab Tech (code-optimized model)
  │     Owns: code/
  │     Reads: experiment design specs
  │
  ├── Liaison (mid-tier model, audience-modeling focus)
  │     Owns: liaison/
  │     Reads: research/STRUCTURAL_MAPPING.md, all outbound drafts
  │
  ├── Scout (cheap model, OpenClaw, constrained autonomy)
  │     Owns: scouting/
  │     Reads: COO-drafted, Liaison-reviewed outbound posts
  │
  ├── Scribe (Haiku-class, event-driven)
  │     Writes to: research/DECISION_LOG.md, research/STATE_FILE.md
  │     Monitors: git commits for consistency, updates State File and Decision Log
  │
  └── Project Manager (cheap model, periodic cron)
        Owns: _meta/
        Reads: everything
        Audits: file tree, process compliance, provenance
        Reports to: COO
```

### Role Principles

1. **The COO is the only agent that makes research decisions.** All other agents execute within defined scopes. Sub-agents do not interpret, prioritize, or redirect research — they execute tasks and report results.

2. **The Red Team receives artifacts, not reasoning.** When the COO sends work to the Red Team for adversarial review, it sends the artifact (hypothesis document, experiment design, results) WITHOUT the COO's justification or interpretation. The Red Team attacks the work on its own terms. This prevents the COO's framing from softening the critique.

3. **The Scout never drafts its own content.** All outbound posts are drafted by the COO, reviewed by the Liaison, approved by the COO, then handed to the Scout for posting. The Scout executes, monitors, and collects — it does not create. Follow-up posts go back through the COO → Liaison → COO approval loop before posting.

4. **The Scribe is the provenance layer.** When any agent completes significant work, it sends a structured notification to the Scribe. The Scribe updates the Decision Log and State File. This removes the burden of documentation discipline from working agents and centralizes it in an agent whose only job is record-keeping.

5. **The PM audits, never directs.** The PM checks that files are in the right places, that documentation is current, that process steps are being followed. It reports problems to the COO. It does not reassign tasks, modify process documents, or make research judgments.

6. **The Liaison owns cross-disciplinary communication precision.** It maintains the Audience Framing Guide, reviews all outbound communications, and assists the COO with ensuring terminology is used correctly for each target audience. It operates from the reader's perspective, which is structurally different from the COO's researcher perspective.

### Model Tier Recommendations

| Role | Model Tier | Rationale |
|---|---|---|
| COO | Frontier (e.g., Claude Opus, GPT latest) | Integrative reasoning, synthesis, complex judgment |
| Red Team | Frontier, **different provider** | Adversarial quality needs strong reasoning; different provider reduces correlated blind spots |
| Librarian | Mid-tier + API access | Retrieval and verification, not deep reasoning |
| Lab Tech | Code-optimized | Implementation quality; may be same provider as COO if that provider's code model is strong |
| Liaison | Mid-tier | Audience modeling and terminology precision; doesn't need frontier reasoning |
| Scout | Cheap + OpenClaw | Mechanical posting and collection; minimal reasoning needed |
| Scribe | Cheapest available (Haiku-class) | Structured record-keeping; pattern-following, not reasoning |
| PM | Cheap | Structural auditing; pattern-matching against expected file states |

Models are swappable. As frontier models improve, today's frontier becomes tomorrow's mid-tier. The role definitions and trust boundaries persist regardless of which specific model fills each role.

---

## PART 2: INFRASTRUCTURE

### Project File Tree

When a new project is initialized, the following directory structure is created in a git repository:

```
project-root/                       ← git repo
│
├── _meta/                          ← PM-owned: system health
│   ├── SYSTEM_LOG.md               ← PM's log of failures, improvements, patterns
│   ├── AUDIT_REPORTS/              ← PM's periodic audit outputs
│   └── AGENT_REGISTRY.md           ← Current agent assignments, models, prompt versions
│
├── research/                       ← COO-owned: core research artifacts
│   ├── STATE_FILE.md               ← Machine-readable project state (Scribe-maintained)
│   ├── SCOPE_DOCUMENT.md           ← Project boundaries and kill criteria
│   ├── STRUCTURAL_MAPPING.md       ← Cross-field claims and validity tracking
│   ├── DECISION_LOG.md             ← Running decision record (Scribe-maintained)
│   ├── CLAIMS_REGISTRY.md          ← Empirical claims with provenance and verification
│   ├── HYPOTHESES.md               ← Hypotheses with test specifications
│   ├── EXPERIMENT_DESIGN.md        ← Experiment designs and architecture docs
│   └── PHASE_REPORTS/              ← Structured summaries per phase gate
│
├── literature/                     ← Librarian-owned
│   ├── _INDEX.md                   ← Librarian's working state and search history
│   ├── papers/                     ← Organized by domain subdirectories
│   ├── searches/                   ← Search query logs and raw results
│   └── verification/               ← Citation verification records
│
├── adversarial/                    ← Red Team-owned
│   ├── _INDEX.md                   ← Red Team's working state
│   └── reviews/                    ← One file per review, named by phase and date
│
├── code/                           ← Lab Tech-owned
│   ├── _INDEX.md                   ← Lab Tech's working state
│   ├── src/                        ← Experiment implementation
│   ├── tests/                      ← Verification, baselines, parameter sweeps
│   ├── results/                    ← Raw output data
│   └── logs/                       ← Run logs with parameters and seeds
│
├── liaison/                        ← Liaison-owned
│   ├── _INDEX.md                   ← Liaison's working state
│   ├── audience_framing_guide.md   ← Maps project terms to audience interpretations
│   └── reviews/                    ← Outbound communication reviews
│
├── scouting/                       ← Scout-owned
│   ├── _INDEX.md                   ← Scout's working state
│   ├── outbound/                   ← Posts: COO-drafted, Liaison-reviewed, COO-approved
│   ├── responses/                  ← Raw collected community responses
│   └── summaries/                  ← Scout's organized response summaries
│
└── writeups/                       ← COO-owned
    ├── abstracts/                  ← Five-way writeup exercise outputs
    └── final/                      ← Final synthesis documents
```

### Directory Ownership Rules

1. Each agent writes only to its owned directory and to specific shared documents in `research/` as defined in its identity document.
2. No agent modifies another agent's directory.
3. The COO and PM have read access to everything.
4. All other agents read `research/` and their own directory.
5. The Red Team reads ONLY the specific artifact sent for review — it does not browse the project tree to gather context. The COO controls what the Red Team sees.

### Git Workflow

**Why git:** Three problems solved by one tool — provenance tracking (who changed what, when), conflict detection (two agents editing the same file), and rollback (undoing agent mistakes).

**Workflow:**

1. All agents commit directly to main. (Per-agent branches are available as an escalation if concurrent write conflicts become a recurring problem, but start without them.)
2. Every commit has a structured message: `[agent-role]: [action summary] — [files affected]`
   - Example: `librarian: verified 5 ALife citations, 4 passed, 1 failed — CLAIMS_REGISTRY.md, literature/verification/alife_batch_001.md`
   - Example: `coo: approved hypothesis H1 and H3, killed H2 — research/HYPOTHESES.md, research/DECISION_LOG.md`
3. The Scribe monitors commits and ensures the State File and Decision Log reflect them.
4. The PM periodically audits the git log:
   - Has every agent committed recently (vs. working in memory without saving)?
   - Has any agent committed to a directory it doesn't own?
   - Are commit messages structured correctly?
   - Are there files modified after being marked `verified` without the status being reset?

**Provenance via git:**

All "who did this and when" provenance lives in git history, not in manually-maintained document metadata. This eliminates the drift problem where agents edit documents and forget to update provenance fields.

**Simplified YAML frontmatter** (semantic metadata only — things git doesn't capture):

```yaml
---
verification_status: unverified | verified | disputed
verified_by: [agent role that verified]
phase: [phase number when created/last substantively updated]
tags: [domain tags for searchability]
---
```

The PM audits by cross-referencing frontmatter against git log: if a file was modified after being marked `verified`, the `verification_status` should have been reset to `unverified`. If it wasn't, the PM flags this to the COO.

### Task Orchestration

The framework requires a task management system — any tool that lets you create tasks, assign them to agents, track status, and record completion. The specific tool doesn't matter; the separation of concerns does.

**What goes in the task system:**
- Task assignment (who, what, priority, deadline)
- Task status (pending, in progress, complete, blocked)
- Completion notifications with file pointers ("task complete, results at `literature/verification/alife_batch_001.md`")

**What does NOT go in the task system:**
- Research content, analysis, data, or findings
- Anything that needs to persist as institutional knowledge

**The rule:** If an agent completes a task and the only record of what it did is in the task system's completion message, something went wrong. All work products must be written to the file tree. Task completions contain file pointers to the work, not the work itself.

### Handoff Protocol

Every inter-agent delegation follows this pattern:

1. **COO creates a task in the task system** with:
   - Clear objective (what to do)
   - Input file paths (what to read)
   - Expected output file paths (where to write results)
   - Shared documents to update as side effects (e.g., "update CLAIMS_REGISTRY.md")
   - Scope constraints (what NOT to do)

2. **Sub-agent executes:**
   - Reads inputs from specified file paths
   - Does the work
   - Writes outputs to specified file paths
   - Updates shared documents as specified
   - Commits to git with structured message
   - Sends structured notification to Scribe
   - Marks task complete with output file pointers

3. **Scribe records:**
   - Updates Decision Log with the action
   - Updates State File if the action advances the project state

4. **COO reviews:**
   - Reads the output files
   - Validates quality
   - Integrates into the research process

### Outbound Communication Pipeline

For community engagement (forum posts, etc.), the flow is:

```
COO drafts the question (specifying target community and objective)
  → Liaison reviews for audience-appropriate framing
  → COO approves Liaison's revisions
  → Scout posts to community, monitors for responses
  → Scout collects responses into scouting/responses/
  → Liaison summarizes responses with terminology mapping
  → COO synthesizes into research process
```

Follow-up posts loop back through COO → Liaison → COO before the Scout posts them.

The Scout has a hard constraint: **never disclose the full hypothesis or experiment design.** It asks focused methodological questions without revealing the larger research program.

For direct researcher emails: PI-handled. This is relationship capital, not a delegatable task.

---

## PART 3: PI CHECKPOINT PROTOCOL

Throughout the process, certain steps are marked with `★ PI CHECKPOINT ★`. At these points, the COO MUST:

1. **Stop work.** Do not proceed to the next step.
2. **Present a summary** of the work completed and the decision needed.
3. **Present Red Team critiques verbatim.** If adversarial review has occurred since the last checkpoint, the COO must include the Red Team's unedited critique alongside its own response to that critique. The PI judges whether the COO adequately addressed the critique or swept something under the rug. **The COO must not pre-filter, summarize, or soften Red Team output at PI Checkpoints.**
4. **Wait for explicit PI approval** before continuing.
5. **Record the PI's decision** (including any modifications) in `DECISION_LOG.md` via the Scribe.

PI Checkpoints exist because certain decisions require human judgment that cannot be delegated to AI, even with good process. The COO is the staff. The PI is the decision-maker.

**An AI agent must NEVER pass a PI Checkpoint on its own, even if it believes the correct decision is obvious.**

---

## PART 4: CORE PRINCIPLES

### 1. Process Substitutes for Expertise

In a traditional lab, quality comes from experienced researchers recognizing problems through intuition. This lab has no such intuition. Every quality check must be **explicit, procedural, and verifiable**. If it can't be written as a checklist item with a pass/fail criterion, it isn't a real check.

### 2. LLMs Are Brilliant but Tasteless

AI team members can synthesize literature, write code, critique arguments, and generate hypotheses. They cannot: recognize when something "feels off," identify problems outside their training distribution, resist confirmation bias without structural prompting, or distinguish a genuine insight from a plausible-sounding just-so story. The multi-agent architecture mitigates this by assigning adversarial review to a structurally separate agent, but does not eliminate it.

### 3. File-as-Memory / Stateless Operation

No agent should need to remember anything from a previous session. All state lives in files under git version control. Every consequential action must be committed before the step is considered complete. The rule: **if it's not committed, it didn't happen.**

### 4. TDD for Research

Borrowing from test-driven development:

- **Write the test first**: Before running any experiment, define what the null result looks like, what would constitute a meaningful result, and what would falsify the hypothesis. Write these down. This is your "test."
- **Red state**: The experiment hasn't been run. The hypothesis is unconfirmed.
- **Green state**: The experiment produced results that pass the pre-registered criteria AND survived adversarial review AND are robust to parameter variation.
- **Refactor**: Iterate on the experiment design, not just the code. Simplify. Remove confounds. Strengthen baselines.

### 5. Kill Criteria Are Not Optional

Every phase has explicit conditions under which the project should be stopped or pivoted. These are defined in advance and evaluated honestly.

**When a kill criterion is triggered, the COO MUST stop and present it to the PI as a `★ PI CHECKPOINT ★`.** The COO does not make the kill/pivot/override decision — the PI does. The COO presents: which criterion was triggered, the evidence, and options (kill, pivot, or override with explicit justification). The PI's decision is recorded in `DECISION_LOG.md`.

### 6. External Checkpoints Are Non-Negotiable

At two specific points (after experiment design, after first major result), the process requires input from at least one human domain expert outside the PI-LLM loop. This cannot be satisfied by additional LLM consultation, regardless of how many models are used. The Scout can facilitate community-level feedback; direct researcher contact is PI-handled. See `templates/EXPERT_ENGAGEMENT.md` for the protocol.

---

## PART 5: THREE-TIER OPERATING MODEL

Not every idea deserves the full process. Most ideas should die fast and cheap. The framework operates at three tiers of investment, and ideas graduate (or die) at each level.

### Tier 1: Spike (1-2 weeks)

**Purpose:** Kill bad ideas before any infrastructure exists.

**Who's active:** COO + Red Team only. No other agents. No file tree. No git. No task tracking.

**What happens:**
1. PI describes the idea to the COO in any format.
2. COO does a quick literature scan (not the full Phase 1 — just enough to check for obvious prior art and obvious killers).
3. COO drafts a one-page Spike Assessment using `templates/SPIKE.md`.
4. Red Team attacks the core analogy / intersection: "Is this superficial? Is this already done? Is there an obvious reason this won't work?"
5. COO presents the Spike Assessment to the PI with the Red Team's critique verbatim.
6. **★ PI CHECKPOINT ★** PI decides: kill, park, or escalate to Proof of Concept.

**Kill criteria (any one kills the spike):**
- The intersection has been thoroughly explored by an existing group
- The core analogy is rated "false friend" or "suggestive parallel" by both COO and Red Team
- There is no computationally testable hypothesis visible
- The PI loses interest after seeing the assessment (this is a legitimate kill — motivation matters for independent research)

**What it produces:** A single Spike Assessment file. If killed, this file is the only artifact. If escalated, it becomes input to Phase 0.

**Cost:** Minimal. Two frontier model sessions, a few hours of PI time. This is where 60-70% of ideas should die.

### Tier 2: Proof of Concept (4-8 weeks)

**Purpose:** Test whether the idea produces interesting dynamics before committing to full rigor.

**Who's active:** COO, Librarian, Red Team, Lab Tech. Liaison and Scout may be activated if early external feedback would help. Scribe and PM are active but light-touch.

**What happens:**
1. Initialize the project: git repo, file tree, templates. But run a COMPRESSED process:
   - Combined Phase 0-1: Scope + literature review in one pass. Reduced depth — 10 papers per domain (not 15), 3 citation spot-checks per domain (not 5), no serendipity sweep.
   - Combined Phase 2-3: Structural mapping + ONE hypothesis. Adversarial review on the core mapping and the hypothesis only.
   - Compressed Phase 4-5: Design and implement a TOY experiment — not the full-scale version. Simplified baselines (null model + one control). No parameter sweeps yet. The question is: "do the dynamics I expect actually appear, and are they distinguishable from the boring explanation?"
2. At each combined phase, run the mandatory checks from `01_PHASE_CHECKLISTS.md` but at reduced depth: 3-4 mandatory checks (not all), no randomized deep-dive pools.
3. External expert check is OPTIONAL at PoC tier (but recommended if you have easy access).

**Kill criteria:**
- The toy experiment doesn't show the expected dynamics
- The dynamics appear but are indistinguishable from the null model
- The structural mapping doesn't survive Red Team review
- The literature review reveals the idea has been done (with results)

**Transition gate to Full Protocol — ★ PI CHECKPOINT ★:**
The COO presents:
- Spike Assessment (from Tier 1)
- Structural Mapping with at least the core pair classified
- Toy experiment results vs. null model
- Red Team critique of the mapping and the toy results (verbatim)
- Recommendation: proceed to Full Protocol, pivot, or kill

The PI decides. If proceeding, the PoC artifacts become the starting point for Phases 1-3 of the Full Protocol (they get deepened, not redone from scratch).

**Cost:** Moderate. Full agent team at reduced intensity, ~$200-500 in API costs depending on model pricing and experiment complexity.

### Tier 3: Full Protocol (8-16 weeks)

**Purpose:** Produce defensible, publication-ready results.

**Who's active:** All agents at full capacity.

**What happens:** The complete phase process (Phases 0-8) as described in Part 6 below. All checklists at full depth. All adversarial review. External expert checks mandatory. Parameter sweeps. Full reproducibility checks. Five-way writeup.

**Entry requirement:** Must have passed the Tier 2 transition gate.

**Why this tier exists separately:** Full Protocol is expensive in time, compute, and PI attention. By requiring Tier 1 and Tier 2 to pass first, the system ensures that Full Protocol effort is only spent on ideas that have already survived two rounds of pressure-testing. This prevents the most common failure mode of solo research: spending months on a beautifully documented dead end.

### Tier Transitions

```
Spike ──── kill (most ideas)
  │
  └── ★ PI: escalate to PoC
        │
        PoC ──── kill (some ideas)
          │
          └── ★ PI: escalate to Full Protocol
                │
                Full Protocol ──── kill (rare, but possible)
                  │
                  └── Publication-ready results
```

Every transition is a PI Checkpoint. The COO recommends. The PI decides. No automatic escalation.

---

## PART 6: RESEARCH PROCESS — PHASES

**Note:** The phases below describe the **Full Protocol** (Tier 3). At PoC tier (Tier 2), phases are compressed as described above. At Spike tier (Tier 1), phases do not apply — use the Spike template instead.

A research project in Full Protocol moves through nine phases (including Intake). Each phase has a **gate** — conditions that must be met before proceeding. Gates are evaluated using `01_PHASE_CHECKLISTS.md`.

The `★` markers indicate PI Checkpoints where the COO must stop and wait for PI approval.

```
Intake: Seed Idea → Structured Scope
  │ ★ PI CHECKPOINT: Review and approve draft scope
  ▼
Phase 0: Project Inception & Scoping
  │ GATE 0: Scope complete, kill criteria defined, agents initialized
  │ ★ PI CHECKPOINT: Approve scope and kill criteria
  ▼
Phase 1: Domain Reconnaissance
  │ GATE 1: Literature landscape mapped, domain risks identified
  │ Primary agent work: Librarian (heavy), COO (synthesis), Red Team (review)
  ▼
Phase 2: Structural Mapping & Synthesis
  │ GATE 2: Cross-field mappings explicit, validity conditions stated
  │ ★ PI CHECKPOINT: Approve mappings before hypothesis work
  │ Primary agent work: COO (heavy), Red Team (heavy), Liaison (initial framing guide)
  ▼
Phase 3: Hypothesis Formulation
  │ GATE 3: Hypotheses stated, null models defined, tests pre-registered
  │ ★ PI CHECKPOINT: Approve hypotheses and test specifications
  │ Primary agent work: COO (heavy), Red Team (heavy), Librarian (novelty checks)
  ▼
Phase 4: Experiment Design
  │ GATE 4: Design reviewed, baselines specified, code architecture planned
  │ ★ PI CHECKPOINT: Approve experiment design
  │ ★ MANDATORY EXTERNAL EXPERT CHECK (Scout + PI)
  │ Primary agent work: COO (heavy), Red Team (heavy), Lab Tech (architecture review)
  ▼
Phase 5: Implementation & Execution
  │ ★ PI CHECKPOINT: Approve full experiment run (compute commitment)
  │ GATE 5: Code reviewed, baselines run, parameter sweeps complete
  │ Primary agent work: Lab Tech (heavy), Red Team (code review), COO (oversight)
  ▼
Phase 6: Analysis & Interpretation
  │ Step 1 is PI-only: PI writes initial interpretation before LLM consultation
  │ GATE 6: Results robust, adversarial interpretations addressed
  │ ★ CONDITIONAL EXTERNAL EXPERT CHECK (if surprising/too-clean results)
  │ Primary agent work: COO (heavy), Red Team (heavy), Librarian (verification)
  ▼
Phase 7: Communication & Documentation
  │ ★ PI CHECKPOINT: Approve final writeup
  │ GATE 7: Five-way writeup complete, claims registry finalized
  │ Primary agent work: COO (heavy), Liaison (heavy), Red Team (review), Scout (community)
  ▼
Phase 8: Retrospective
  │ Primary agent work: COO, PM (audit findings feed in)

ADDITIONAL PI CHECKPOINTS (event-triggered):
  ★ Any kill criterion triggered → PI decides kill/pivot/override
  ★ Any scope change proposed → PI approves or rejects
  ★ Any surprising or anomalous result → PI reviews before narrative is built
```

---

### INTAKE: SEED IDEA → STRUCTURED SCOPE

**Purpose:** Transform the PI's initial idea — in whatever form — into a structured draft Scope Document for PI review.

**This phase is collaborative between PI and COO.** No other agents are active yet.

**Steps:**

1. **PI provides the seed idea.** Any format: a description, a question, a table of domains, a paragraph, a reference to prior conversations. There is no required format.

2. **COO structures the seed into a draft Scope Document.** Using the seed, fill in as much of `templates/SCOPE_DOCUMENT.md` as possible: core question, domains, expected contribution, initial out-of-scope list, preliminary kill criteria, rough time estimate. Flag sections that couldn't be filled and list questions for the PI.

3. **COO performs a quick prior art check.** Before presenting the draft, search for whether this exact intersection has been explored. Summarize findings in 2-3 sentences. Use web search and academic APIs where available.

4. **★ PI CHECKPOINT ★** Present the draft Scope Document and prior art findings. The PI reviews, modifies, and approves or redirects. Do NOT proceed until approved.

5. **Record the approved seed and any PI modifications** in `DECISION_LOG.md` as the first entry.

6. **Update STATE_FILE.md** to reflect Intake complete, Phase 0 can begin.

**CHECKPOINT: COMMIT DRAFT SCOPE AND DECISION LOG TO GIT.**

---

### PHASE 0: PROJECT INCEPTION & SCOPING

**Purpose:** Formalize the approved draft scope into a complete Scope Document. Initialize the project infrastructure.

**Steps:**

1. **Initialize project infrastructure:**
   a. Create the full project file tree as specified in Part 2.
   b. Initialize git repo (if not already done).
   c. Copy all templates from `templates/` into `research/`.
   d. Create `_INDEX.md` files in each agent-owned directory.
   e. Set up agent assignments and record in `_meta/AGENT_REGISTRY.md`.

2. **Complete the Scope Document.** Finalize all sections: core question, expected contribution, out-of-scope list (minimum 5 items), success criteria, kill criteria (minimum 3, specific and falsifiable), and time/effort budget.

3. **Generate or load Domain Failure Modes.** If `03_PROJECT_DOMAIN_RISKS.md` exists for this intersection, copy it to the project. If not, generate one using `02_PROMPT_LIBRARY.md` → Phase 0 → "Domain Risk Discovery."

4. **Initialize the Liaison's Audience Framing Guide.** Delegate to Liaison: create an initial `liaison/audience_framing_guide.md` with preliminary entries for each domain's audience based on the Scope Document and domain list.

5. **Run Phase 0 checklist** from `01_PHASE_CHECKLISTS.md`.

6. **★ PI CHECKPOINT ★** Present the completed Scope Document and Domain Failure Modes to the PI. The PI approves scope, kill criteria, and time budget.

**CHECKPOINT: COMMIT ALL INITIALIZED FILES TO GIT.**

**Gate 0 Criteria:**
- [ ] Full project file tree created and committed
- [ ] Scope document complete with all sections filled
- [ ] Kill criteria specific and falsifiable (minimum 3)
- [ ] Time/effort budget stated
- [ ] Domain failure modes document exists
- [ ] Agent assignments recorded in Agent Registry
- [ ] PI has approved scope

**Kill Criteria for Phase 0:**
- The intersection has already been thoroughly explored
- The research question cannot be made computationally tractable
- The domains do not actually intersect substantively (the analogy is surface-level)

---

### PHASE 1: DOMAIN RECONNAISSANCE

**Purpose:** Map the literature landscape in each domain. This is the most Librarian-intensive phase.

**Agent Allocation:**
- **Librarian:** Heavy — literature search, citation verification, Claims Registry population
- **COO:** Medium — synthesis, gap analysis, adversarial review coordination
- **Red Team:** Medium — adversarial review of the intersection's viability

**Steps:**

1. **COO delegates literature mapping to Librarian.** For each domain, create a task with:
   - Input: Domain name and description from Scope Document
   - Objective: Find 15+ foundational papers, 10+ recent key papers, 5+ active research groups, open questions, and methodological norms
   - Output: Structured report in `literature/papers/[domain]/`, verification records in `literature/verification/`
   - Side effect: Update `research/CLAIMS_REGISTRY.md` with citation spot-checks (minimum 5 per domain)
   - Reference: Use prompts from `02_PROMPT_LIBRARY.md` → Phase 1 → "Literature Landscape Mapping"

2. **Librarian executes and reports.** Librarian searches using LLM knowledge AND Semantic Scholar / OpenAlex APIs. Cross-checks that cited papers exist and say what claimed. Updates its `_INDEX.md` with search history and completion status. Commits all outputs. Notifies Scribe.

3. **COO reviews Librarian output and synthesizes.** Reads the literature reports. Builds the terminology crosswalk in `research/STRUCTURAL_MAPPING.md`. Identifies cross-domain gaps.

4. **COO delegates adversarial review to Red Team.** Send the intersection description and literature findings to Red Team with the task: "Identify researchers who would consider this intersection trivial, already-explored, or misguided."

5. **Serendipity sweep.** COO delegates to Librarian: retrieve 5 recent papers (last 6 months) from a key journal in each field, NOT selected for relevance. COO reviews abstracts for unexpected connections.

6. **Run Phase 1 checklist** from `01_PHASE_CHECKLISTS.md`.

**CHECKPOINT: ALL AGENTS COMMIT. SCRIBE UPDATES STATE FILE.**

**Gate 1 Criteria:**
- [ ] At least 15 foundational papers per domain identified and verified
- [ ] At least 5 citation spot-checks per domain in Claims Registry
- [ ] Terminology crosswalk completed in Structural Mapping
- [ ] Cross-domain gap analysis completed
- [ ] Red Team adversarial review of intersection completed
- [ ] Serendipity sweep completed
- [ ] No kill criteria triggered

**Kill Criteria for Phase 1:**
- Intersection substantially explored by existing group (>5 papers directly on topic)
- Fundamental conceptual barrier identified making the intersection incoherent
- Literature reveals the analogy has been tried and shown to be unproductive

---

### PHASE 2: STRUCTURAL MAPPING & SYNTHESIS

**Purpose:** Make explicit claims about what maps between fields, under what conditions, and what would break the mapping.

**Agent Allocation:**
- **COO:** Heavy — this is core intellectual work
- **Red Team:** Heavy — false isomorphism detection
- **Liaison:** Light — begins building the audience framing guide based on mappings

**Steps:**

1. **COO completes the Structural Mapping.** For each domain pair, fill in `research/STRUCTURAL_MAPPING.md`: claimed relationship, formal mapping attempt, validity conditions, falsification conditions, known limitations, key structural differences.

2. **COO delegates false isomorphism review to Red Team.** Send the Structural Mapping document. Task: "Destroy each mapping. Find every reason it's superficial or misleading." Red Team must be a different provider than the COO's model.

3. **COO classifies each mapping:** Strong isomorphism, productive analogy, suggestive parallel, or false friend. Records justification.

4. **COO delegates to Liaison:** Review the Structural Mapping and update `liaison/audience_framing_guide.md` with: for each mapping, how would each field's audience interpret it? Where will they misread the claim?

5. **Run Phase 2 checklist** from `01_PHASE_CHECKLISTS.md`.

6. **★ PI CHECKPOINT ★** Present the Structural Mapping to the PI. PI approves mapping classifications before hypothesis work begins. PI should scrutinize any mapping rated "productive analogy" or weaker.

**CHECKPOINT: ALL AGENTS COMMIT. SCRIBE UPDATES.**

**Gate 2 Criteria:**
- [ ] Every domain pair has a structural mapping entry
- [ ] Every mapping has validity and falsification conditions
- [ ] Red Team false isomorphism review completed (different provider)
- [ ] No "false friend" remains as a core pillar
- [ ] Liaison's initial audience framing guide updated
- [ ] PI has approved mappings

**Kill Criteria for Phase 2:**
- Core claimed connection doesn't survive adversarial review
- All mappings are "suggestive parallel" or weaker

---

### PHASE 3: HYPOTHESIS FORMULATION

**Purpose:** State specific, testable hypotheses with pre-registered test criteria.

**Agent Allocation:**
- **COO:** Heavy — hypothesis generation and refinement
- **Red Team:** Heavy — hypothesis attack
- **Librarian:** Light — novelty verification

**Steps:**

1. **COO formulates hypotheses** using `02_PROMPT_LIBRARY.md` → Phase 3 → "Hypothesis Generation." Each must include: precise statement, mapping dependencies, null model, PASS/FAIL/INCONCLUSIVE criteria (written BEFORE experiment design), boring alternative explanation.

2. **COO delegates novelty check to Librarian.** For each hypothesis, search Semantic Scholar / OpenAlex for existing work that tests or resolves it.

3. **COO delegates adversarial review to Red Team.** Send hypotheses (without COO's reasoning about why they're good). Task: attack each one for triviality, prior resolution, untestability, and weak mapping dependency.

4. **COO integrates adversarial findings.** Modifies, retains, or discards hypotheses based on Librarian and Red Team reports. Records all in `research/HYPOTHESES.md`.

5. **Run Phase 3 checklist** from `01_PHASE_CHECKLISTS.md`.

6. **★ PI CHECKPOINT ★** Present hypotheses, test specifications, and adversarial findings. PI decides which to pursue, modify, or discard.

**CHECKPOINT: ALL AGENTS COMMIT. SCRIBE UPDATES.**

**Gate 3 Criteria:**
- [ ] At least one hypothesis with complete test specification
- [ ] Null model explicitly defined for each
- [ ] Red Team adversarial review completed (different provider)
- [ ] No hypothesis trivially true or already resolved
- [ ] Novelty check by Librarian completed
- [ ] PI has approved hypotheses

**Kill Criteria for Phase 3:**
- All hypotheses trivially true or already resolved
- Hypotheses cannot be distinguished from null models computationally
- Hypotheses depend on a "false friend" mapping

---

### PHASE 4: EXPERIMENT DESIGN

**Purpose:** Design computational experiments. Highest-risk phase for a non-expert PI.

**Agent Allocation:**
- **COO:** Heavy — design leadership
- **Red Team:** Heavy — design attack
- **Lab Tech:** Light — architecture feasibility review
- **Scout + Liaison:** Medium — external expert engagement

**Steps:**

1. **COO designs experiments** using `02_PROMPT_LIBRARY.md` → Phase 4. Must specify: environment, agents, communication channels, selection mechanism, baselines (minimum 3: null, random, ablation), parameters with sweep ranges, metrics, replicates, statistical tests, data logging, compute estimate.

2. **COO runs "boring explanation" and "design contains conclusion" checks.**

3. **COO delegates architecture review to Lab Tech.** Task: "Is this design implementable? What are the technical risks? Where will implementation be hardest?"

4. **COO delegates adversarial review to Red Team.** Send the experiment design without the COO's justification. One Red Team prompt uses a domain-expert persona.

5. **★ MANDATORY EXTERNAL EXPERT CHECK ★**
   Follow the protocol in `templates/EXPERT_ENGAGEMENT.md`. Key points:
   - **Community engagement (via Scout):** COO drafts focused methodological questions. Liaison reviews for appropriate framing. COO approves. Scout posts to relevant communities. Scout collects responses. Liaison summarizes with terminology mapping. COO synthesizes.
   - **Direct researcher contact (PI-handled):** PI emails or speaks with a domain expert. Records feedback in `research/DECISION_LOG.md`.
   - This step cannot be satisfied by additional LLM review.
   - Document all expert feedback using the engagement record format in the template.

6. **★ PI CHECKPOINT ★** Present the final design (incorporating all feedback) to the PI. PI approves before implementation.

7. **Run Phase 4 checklist** from `01_PHASE_CHECKLISTS.md`.

**CHECKPOINT: ALL AGENTS COMMIT. SCRIBE UPDATES.**

**Gate 4 Criteria:**
- [ ] Experiment design complete for each hypothesis
- [ ] Baselines specified (null, random, ablation)
- [ ] Parameter sweep ranges defined
- [ ] "Boring explanation" check passed
- [ ] "Design contains conclusion" check passed
- [ ] Lab Tech architecture review completed
- [ ] Red Team adversarial review completed (different provider)
- [ ] External expert feedback received and recorded
- [ ] PI has approved design

**Kill Criteria for Phase 4:**
- External expert identifies unfixable fundamental flaw
- "Boring explanation" cannot be ruled out by any feasible design
- Computational resources exceed budget
- Design inevitably contains its conclusion

---

### PHASE 5: IMPLEMENTATION & EXECUTION

**Purpose:** Write code, run experiments, collect data. Lab Tech-intensive phase.

**Agent Allocation:**
- **Lab Tech:** Heavy — implementation, testing, execution
- **Red Team:** Medium — code review (specifically looking for bugs that would produce expected results as artifacts)
- **COO:** Light — oversight and PI interface

**Steps:**

1. **COO delegates implementation to Lab Tech.** Provide: experiment design doc, code architecture doc, hypothesis statement. Lab Tech implements in `code/src/`, writes tests in `code/tests/`, logs everything in `code/logs/`.

2. **COO delegates code review to Red Team.** Send the code AND the expected result. Task: "Find bugs that would produce this result as an artifact." Red Team must be a different model than Lab Tech.

3. **Lab Tech runs small-case verification.** Trivially small case where dynamics can be verified by hand. Documents results.

4. **Lab Tech runs all baselines.** Verifies they produce expected (boring) results. If unexpected: STOP and report to COO.

5. **★ PI CHECKPOINT ★** COO presents baseline results and small-case verification. PI approves committing compute to the full run.

6. **Lab Tech runs full experiment:** minimum 30 replicates per condition, full parameter sweeps, complete data logging, random seeds logged.

7. **Lab Tech runs reproducibility check.** Re-runs one striking result with different random seeds.

8. **Run Phase 5 checklist** from `01_PHASE_CHECKLISTS.md`.

**CHECKPOINT: ALL CODE AND DATA COMMITTED AND TAGGED IN GIT. SCRIBE UPDATES.**

**Gate 5 Criteria:**
- [ ] Code reviewed by different model than writer
- [ ] Small case verification completed and documented
- [ ] All baselines producing expected results
- [ ] Full experiment completed with specified replicates
- [ ] Parameter sweeps completed
- [ ] Reproducibility check completed
- [ ] All code/data versioned in git
- [ ] PI approved the full run

**Kill Criteria for Phase 5:**
- Baselines produce same results as experimental conditions
- Results only appear in a narrow parameter regime
- Reproducibility check fails

---

### PHASE 6: ANALYSIS & INTERPRETATION

**Purpose:** Analyze results, test robustness, interpret findings.

**Agent Allocation:**
- **COO:** Heavy — interpretation and synthesis
- **Red Team:** Heavy — result attack
- **Librarian:** Light — verification of any new empirical claims

**Steps:**

1. **PI writes initial interpretation FIRST** — before any LLM sees results. Records in Phase Report as "PI Initial Interpretation." This prevents anchoring on LLM narratives.

2. **COO performs statistical analysis.** Effect sizes, not just p-values. Confidence intervals. Multiple comparison corrections if relevant.

3. **COO delegates adversarial interpretation to Red Team.** Send results and PI's interpretation. Task: "Generate the most damaging critique and the most compelling alternative interpretation."

4. **COO evaluates parameter sensitivity.** Are qualitative conclusions robust across sweeps?

5. **COO updates Structural Mapping** based on results. Delegates any new claims to Librarian for verification.

6. **★ CONDITIONAL EXTERNAL EXPERT CHECK ★** If results are surprising OR suspiciously clean, trigger external feedback via Scout pipeline or PI direct contact.

7. **COO updates Claims Registry** with all new empirical claims from interpretation.

8. **Run Phase 6 checklist** from `01_PHASE_CHECKLISTS.md`.

**CHECKPOINT: ALL ANALYSIS COMMITTED. SCRIBE UPDATES.**

**Gate 6 Criteria:**
- [ ] PI initial interpretation recorded before LLM consultation
- [ ] Statistical analysis complete with effect sizes
- [ ] Red Team adversarial interpretation completed (different provider)
- [ ] Parameter sensitivity documented
- [ ] Structural Mapping updated
- [ ] External check completed (if triggered)
- [ ] Claims Registry updated

**Kill Criteria for Phase 6:**
- Boring explanation is more parsimonious than proposed interpretation
- Results not robust across parameter sweep
- Results are implementation artifacts

---

### PHASE 7: COMMUNICATION & DOCUMENTATION

**Purpose:** Write up findings for each relevant audience. Liaison-intensive phase.

**Agent Allocation:**
- **COO:** Heavy — writeup leadership
- **Liaison:** Heavy — audience framing review, all outbound review
- **Red Team:** Heavy — writeup attack
- **Scout:** Medium — community engagement for feedback

**Steps:**

1. **Five-way writeup exercise.** COO drafts a 2-page extended abstract for each domain's venue. Liaison reviews each for audience-appropriate framing. The differences between versions reveal where synthesis is strong and weak.

2. **COO prepares full writeup.** Synthesizes across fields in PI's own framing.

3. **Final Claims Registry review.** Every claim in writeup must appear in `research/CLAIMS_REGISTRY.md` as verified. Delegate verification of any gaps to Librarian.

4. **COO delegates adversarial review to Red Team.** One hostile reviewer prompt, one friendly-but-rigorous prompt.

5. **Liaison does final outbound review.** Checks the full writeup for terminology precision and audience misread risks.

6. **★ PI CHECKPOINT ★** Present final writeup, five-way exercise observations, adversarial findings, and Liaison's review. PI approves before any external sharing.

7. **Run Phase 7 checklist** from `01_PHASE_CHECKLISTS.md`.

**CHECKPOINT: ALL WRITEUPS COMMITTED. SCRIBE UPDATES.**

**Gate 7 Criteria:**
- [ ] Five-way writeup completed
- [ ] Liaison review of all versions completed
- [ ] Full writeup complete
- [ ] All claims verified in Claims Registry
- [ ] Red Team adversarial review completed
- [ ] All code, data, and documents archived in git
- [ ] PI has approved final writeup

---

### PHASE 8: RETROSPECTIVE

**Purpose:** Evaluate the process itself. PM findings feed in here.

**Steps:**

1. **Process evaluation:** What did checklists catch? What slipped through? What to change?

2. **LLM and agent performance evaluation:** Which models helped most? Where did they mislead? Which agent role was most/least valuable? What prompts need revision?

3. **PM contributes audit findings.** PM's `_meta/SYSTEM_LOG.md` provides data on: file tree violations, documentation lapses, process compliance patterns, recurring failure modes.

4. **Update process documents** based on findings: checklists, prompts, agent identity docs, domain risks.

5. **Log scope drift.** Compare actual trajectory against Scope Document.

6. **Record in `RETROSPECTIVE.md`** in the project root.

**CHECKPOINT: COMMIT RETROSPECTIVE AND ALL UPDATED PROCESS DOCS.**

---

## PART 7: MULTI-MODEL STRATEGY

### When to Use Multiple Models

| Situation | Strategy |
|---|---|
| Literature review and synthesis | Librarian (single mid-tier model). Cross-check via Semantic Scholar / OpenAlex, not other LLMs. |
| Adversarial review at any phase | **Red Team (mandatory different provider from COO).** Independent review — Red Team does not see COO's reasoning. |
| Hypothesis generation | COO (single frontier model) in collaboration with PI. Red Team for adversarial review. |
| Experiment design | COO for design. Lab Tech for architecture feasibility. Red Team for adversarial review. |
| Code generation | Lab Tech (code-optimized model). Red Team (different model) for code review. |
| Result interpretation | PI writes first. COO interprets. Red Team attacks. Compare all three. |
| Outbound communication | COO drafts. Liaison reviews. Scout posts. Three agents, potentially three different models. |

### Key Principles

- **Red Team MUST be a different provider than COO.** This is the primary mechanism for reducing correlated blind spots.
- **When models agree, that is LESS informative than when they disagree.** Agreement may reflect shared training data.
- **Models are swappable.** The role definitions and trust boundaries persist regardless of which specific model fills each role.
- **Document which models fill each role** in `_meta/AGENT_REGISTRY.md`.

---

## PART 8: SERENDIPITY AND ANTI-HABITUATION

### Serendipity Mechanisms

1. **Monthly random paper sweep:** COO delegates to Librarian — 5 recent papers per domain from key journals, NOT selected for relevance. COO reviews abstracts.
2. **Journal TOC subscriptions:** 3-4 key journals across domains.
3. **Monthly virtual seminar:** PI attends one talk in a non-primary domain.
4. **Quarterly wildcard search:** COO prompts for unexpected connections between domains.

### Anti-Habituation

1. **Randomized checklist questions:** 15+ questions per phase pool, 5-7 selected randomly each time.
2. **Rotating adversarial personas:** Red Team uses different reviewer personas each time.
3. **Quarterly process audit:** PM produces comprehensive audit. COO and PI review.

---

## PART 9: SCOPE MANAGEMENT

**Scope creep is the specific vulnerability of self-funded interdisciplinary projects with tireless AI teams.**

1. Every new direction is evaluated against `research/SCOPE_DOCUMENT.md`.
2. In scope: proceed.
3. Out of scope but interesting: log in `research/SCOPE_DOCUMENT.md` → Future Investigations Log. Do not pursue.
4. Requires scope change: **★ PI CHECKPOINT ★** — COO presents the proposed change with justification explaining why the original scope was wrong. Record in Decision Log.
5. Any scope expansion resets the time/effort budget and requires re-evaluation of kill criteria.

---

## PART 10: PROJECT INITIALIZATION — QUICK REFERENCE

To start a new project:

**Option A: You have a hunch (start at Spike)**
1. Describe your idea to the COO.
2. COO runs a Spike using `templates/SPIKE.md` — quick lit scan + Red Team attack on the core analogy.
3. COO presents Spike Assessment. You decide: kill, park, or escalate to PoC.

**Option B: Spike passed, escalating to Proof of Concept**
1. Create a new directory and initialize a git repo.
2. Copy this framework's process docs (`00_*`, `01_*`, `02_*`, `agents/`, `templates/`) into the repo.
3. If a `03_PROJECT_DOMAIN_RISKS.md` exists for your research intersection, include it.
4. Set up agent assignments using the identity documents in `agents/`.
5. Run the compressed PoC process (see Part 5, Tier 2). COO drives.
6. At the PoC transition gate, you decide: kill, pivot, or escalate to Full Protocol.

**Option C: PoC passed, escalating to Full Protocol**
1. Deepen the PoC artifacts into full Phase 1-3 outputs.
2. Follow the full phase process (Part 6) sequentially. Do not skip phases, gates, or PI Checkpoints.
3. Commit to git after every step.
4. When in doubt, this document is the authoritative source.
