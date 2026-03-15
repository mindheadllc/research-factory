# Research Factory

**A defense-in-depth process framework for AI-assisted computational research across multiple disciplines.**

A project by [Raj Jha](https://rajjha.com) · [𝕏](https://x.com/rajjha) · [Projects](https://rajjha.com/projects/) · © Mindhead Holdings LLC licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Built for independent researchers who use AI language models as their research team — and who understand that LLMs are brilliant, prolific, and systematically untrustworthy.

---

## The Problem

AI models will enthusiastically help you build an elaborate argument on a foundation that a domain expert would dismiss in five minutes. They'll find evidence supporting your hypothesis while quietly ignoring contradicting evidence. When you use multiple models to "validate" your work, they'll agree with each other — because they share the same training data and the same blind spots, not because you've found independent confirmation.

Most AI research workflows treat models as reliable assistants. This framework treats them as **brilliant but tasteless team members who need structural oversight** — adversarial review, provenance tracking, mandatory human checkpoints, and kill criteria that are actually enforced.

## Who This Is For

- **Independent researchers** working at the intersection of multiple fields where you're not a deep expert in every domain
- **Retired professionals** pursuing serious intellectual projects — your "Life of the Mind" chapter
- **Graduate students and early-career researchers** who want process discipline for interdisciplinary side projects
- **Citizen scientists** working on computational problems and wanting defensible methodology
- **Anyone building AI-assisted research workflows** who wants to see a worked example of how to distrust your tools productively

This framework is purpose-built for the case where **you don't have a lab full of domain experts** checking each other's work. It substitutes explicit process for tacit expertise — turning the quality controls that normally live in experienced researchers' heads into repeatable, auditable procedures.

## What Makes This Different

Most "AI for research" tools help you go faster. This one helps you **go faster without producing garbage.** Here's what's structurally different:

### 1. Adversarial Review with Mandatory Provider Diversity

Every major work product gets attacked by a **Red Team agent that must be a different model from a different provider** than the one that produced the work. The Red Team receives only the artifact — not the reasoning behind it. This structurally reduces correlated blind spots rather than just prompting the same model to "be critical."

### 2. Structural Mapping Rigor

Cross-disciplinary research lives and dies on the quality of its analogies. The framework forces you to formally classify every claimed connection between fields as one of four levels — **strong isomorphism, productive analogy, suggestive parallel, or false friend** — with explicit validity conditions and falsification criteria for each. This is the difference between "these fields seem related" and "here's the formal mapping, here's what would break it, and here's the evidence."

### 3. Kill Criteria as First-Class Citizens

Every project starts by defining specific, falsifiable conditions under which it should be killed. These are checked at every phase gate. When triggered, the process stops and escalates to the human researcher — it doesn't rationalize continuing. Most research frameworks treat stopping as a failure. This one treats **failing to stop as the real failure.**

### 4. TDD for Research

Borrowed from test-driven development: write the test before the experiment. Define what the null model predicts, what would confirm the hypothesis, and what would disconfirm it — all before designing the experiment. Results are evaluated against these pre-registered criteria, not post-hoc narratives.

### 5. Multi-Agent Role Separation

Not "more agents = better" but **specific roles with specific trust boundaries:**

| Role | What It Does | Why It's Separate |
|---|---|---|
| **COO** | Research reasoning, synthesis, delegation | Needs full context; is also the primary source of confirmation bias |
| **Librarian** | Literature search, citation verification | Mechanical work that doesn't need frontier reasoning; frees the COO for thinking |
| **Red Team** | Adversarial review of all work products | Must be isolated from the COO's reasoning to be effective |
| **Lab Tech** | Code implementation and execution | Implements specs without knowing hypotheses; catches design-contains-conclusion problems |
| **Liaison** | Cross-disciplinary communication precision | Holds the audience perspective, which is structurally different from the researcher perspective |
| **Scout** | Community engagement and feedback collection | Constrained autonomy; never drafts its own content |
| **Scribe** | Decision log and state file maintenance | Removes documentation burden from working agents |
| **PM** | Process compliance auditing | Catches when agents skip steps or put files in wrong places |

### 6. Cold-Start / Stateless Design

Every session can be the first session. All project state lives in files under git version control. Any agent can pick up where another left off. **If it's not committed, it didn't happen.** This isn't just good practice — it's essential for long-duration projects where you'll have hundreds of LLM sessions that each need full context.

### 7. Mandatory Human Expert Checkpoints

The framework explicitly requires human domain expert feedback at two points (experiment design and surprising results) and **explicitly states that additional LLM consultation cannot satisfy this requirement.** Most AI research frameworks leave external validation optional. This one makes it non-negotiable because it's the circuit-breaker for the fundamental problem: AI reviewers share the same blind spots as AI creators.

## Three Operating Tiers

Not every idea deserves the full process. Most ideas should die fast and cheap.

| Tier | Duration | What It Is | When to Kill |
|---|---|---|---|
| **Spike** | 1-2 weeks | Quick feasibility check. COO + Red Team only. Minimal infrastructure. One-page assessment: is this worth pursuing? | Core analogy is superficial, intersection already explored, or obvious killer found. |
| **Proof of Concept** | 4-8 weeks | Lightweight project with compressed phases, one hypothesis, toy experiment. | Toy experiment doesn't show interesting dynamics, or mapping doesn't survive adversarial review. |
| **Full Protocol** | 8-16 weeks | Complete process with all checklists, adversarial review, external experts, parameter sweeps, and publication-ready output. | Standard kill criteria at every gate. |

Start at Spike. Most ideas never leave Spike. That's the point.

## What's in the Box

```
research-factory/
├── README.md                          ← You're reading it
├── LICENSE                            ← CC BY-SA 4.0
├── CONTRIBUTING.md                    ← How to contribute
│
├── 00_PROCESS_DESIGN.md               ← Master document: phases, gates, checkpoints,
│                                         file tree, git workflow, agent coordination
├── 01_PHASE_CHECKLISTS.md             ← Verification checklists per phase with
│                                         adversarial review and randomized deep-dives
├── 02_PROMPT_LIBRARY.md               ← Every prompt organized by phase and purpose
│
├── agents/                            ← Agent identity documents
│   ├── COO.md                            (cold-start protocols, handoff contracts)
│   ├── LIBRARIAN.md
│   ├── RED_TEAM.md
│   ├── LAB_TECH.md
│   ├── LIAISON.md
│   ├── SCOUT.md
│   ├── SCRIBE.md
│   └── PM.md
│
├── templates/                         ← Per-project document templates
│   ├── SPIKE.md
│   ├── SCOPE_DOCUMENT.md
│   ├── STRUCTURAL_MAPPING.md
│   ├── STATE_FILE.md
│   ├── DECISION_LOG.md
│   ├── CLAIMS_REGISTRY.md
│   ├── PHASE_REPORT.md
│   ├── AGENT_REGISTRY.md
│   └── EXPERT_ENGAGEMENT.md
│
└── examples/
    └── DOMAIN_RISKS_EXAMPLE.md        ← Worked example of domain failure modes
```

## Quick Start

1. **Clone this repo** into your project directory.
2. **Set up your agents.** Assign models to roles using the identity documents in `agents/`. The critical constraint: the Red Team must be a different provider than the COO.
3. **Got a hunch? Start with a Spike.** Describe your idea to the COO. It runs a feasibility assessment using `templates/SPIKE.md` and presents its findings with the Red Team's critique. You decide: kill or escalate.
4. **Spike survived? Run a Proof of Concept.** Initialize the project file tree, run compressed phases, build a toy experiment. See if the dynamics are real.
5. **PoC showed something? Go Full Protocol.** All checklists, all adversarial review, external expert checks, parameter sweeps. The works.
6. **At every phase gate,** the COO stops and presents its work — including Red Team critiques verbatim. You make the call.

For the full process, start with `00_PROCESS_DESIGN.md`.

## Infrastructure Requirements

The framework is **infrastructure-agnostic.** You need:

- **An AI model provider** (or multiple — the Red Team requires a different provider than the COO)
- **A file system** with git version control
- **A task management system** that supports delegation and status tracking (any tool that lets you assign tasks to agents and track completion works)

Everything else — which specific models, which orchestration platform, which publishing tools — is your choice. The framework specifies roles and protocols, not implementations.

## How to Generate Domain Failure Modes

The framework includes a worked example of domain-specific failure modes (`examples/DOMAIN_RISKS_EXAMPLE.md`) for a project at the intersection of artificial life, bioelectric signaling, AI alignment, model merging, and philosophy of mind.

For your own project, generate a domain failure modes document using the "Domain Risk Discovery" prompt in `02_PROMPT_LIBRARY.md` → Phase 0 → P0.1. This prompt asks a frontier model to identify, for each of your domains: methodological pitfalls non-experts commonly hit, contested assumptions, field-specific norms, terminology traps, and known false isomorphisms with adjacent fields.

Save the output as `03_PROJECT_DOMAIN_RISKS.md` in your project directory and reference it throughout the research process.

## FAQ

**How is this different from just using Claude/GPT for research?**
Using a single model as a research assistant gives you speed but no quality control. This framework adds structural adversarial review, multi-model diversity, mandatory human checkpoints, and kill criteria — the things that separate "I asked AI and it sounded right" from "I tested this systematically and here's what survived."

**Do I need all eight agents?**
No. At Spike tier, you need only the COO and Red Team. Other agents come online as you escalate. The Scribe and PM are quality-of-life additions for longer projects.

**What if I'm only working in one field?**
The framework's biggest value is at interdisciplinary intersections where cross-field analogies need rigorous testing. If you're working in a single domain, the Structural Mapping and Liaison components are less relevant, but the adversarial review, kill criteria, and TDD-for-research principles still apply.

**Can a lab use this?**
It was designed for independent researchers who lack a team of domain experts. A lab could adapt the adversarial review and kill criteria components, but the full agent architecture assumes you're compensating for missing human expertise with process.

## License

This work is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

© Mindhead Holdings LLC

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to contribute improvements, report what works and what doesn't, and share your experience using the framework.
