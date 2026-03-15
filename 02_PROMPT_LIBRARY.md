# Prompt Library

## PATH CONVENTION

All shared research documents referenced in prompts (STATE_FILE.md, DECISION_LOG.md, CLAIMS_REGISTRY.md, STRUCTURAL_MAPPING.md, etc.) are located in the `research/` directory. Agent-owned files are in their respective directories. See `00_PROCESS_DESIGN.md` Part 2 for the full file tree.

## DOCUMENT PURPOSE

This document contains all LLM prompts used in the Research Factory framework, organized by phase and purpose. Each prompt includes: what it's for, when to use it, how many models to use, and the exact text to send.

## HOW TO USE THIS DOCUMENT

**If you are an AI agent:**

1. Check the project's `STATE_FILE.md` for the current phase.
2. Check `01_PHASE_CHECKLISTS.md` for which prompts are needed at the current step.
3. Navigate to the relevant section below.
4. Use the prompt exactly as written, substituting project-specific details where indicated by `[BRACKETS]`.
5. Record full outputs in the relevant Phase Report or the document specified.
6. When the prompt specifies multi-model execution, run the prompt on each model INDEPENDENTLY — do not share one model's output with another.

**Multi-model execution protocol:**
- "2+ models" means: run the same prompt on at least 2 models from different providers.
- Send each model the same raw inputs (project documents, data, etc.).
- Do NOT show Model A's output to Model B.
- Compare outputs only after both have completed.
- Record agreements and disagreements.

---

## SPIKE: RAPID FEASIBILITY ASSESSMENT

### SP.1 — Spike Assessment

**Purpose:** Rapid feasibility evaluation of a research idea before any infrastructure is created.
**When:** Tier 1 (Spike). The PI has described an idea and wants to know if it's worth pursuing.
**Models:** COO (primary) + Red Team (different provider, adversarial).

**COO prompt:**
```
The PI has described the following research idea:

[PASTE THE PI'S IDEA IN WHATEVER FORMAT THEY PROVIDED]

I need to produce a rapid feasibility assessment (Spike Assessment). This is NOT a full literature review or research plan — it's a quick pressure test to determine if this idea is worth investing further time in.

Do the following:

1. STRUCTURE THE IDEA: Restate it as a precise research question. Identify the domains involved and what each domain calls the phenomenon. State the core claimed connection between fields in 2-3 sentences.

2. QUICK PRIOR ART CHECK: Search for whether this exact intersection has been explored. Look for papers connecting 3+ of the listed domains, existing research groups at this intersection, and prior attempts at this specific mapping. Be specific — cite actual work if you find it.

3. PLAUSIBILITY ASSESSMENT: Is the core mapping plausible at a structural level (not just verbal similarity)? Is there a computationally testable hypothesis visible? What is the "boring explanation" risk — if we built an experiment and got the expected result, what's the simplest mundane explanation?

4. OVERALL VERDICT: Worth pursuing, interesting but premature, or not viable? In 3-5 sentences, explain why.

Be honest. The purpose of a Spike is to kill bad ideas fast. A "not viable" verdict saves weeks of wasted effort and is the most valuable possible outcome if it's correct.
```

**Red Team prompt (sent separately, WITHOUT the COO's assessment):**
```
A researcher is considering a project at the following intersection:

[PASTE ONLY THE "STRUCTURED FRAMING" SECTION — the research question, domains, and core claimed connection. Do NOT include the COO's plausibility assessment or verdict.]

Attack this idea. Your job is to find reasons it should NOT be pursued. Specifically:

1. Is the core connection between these fields genuinely structural, or is it a verbal similarity that sounds deep but isn't?
2. Has this already been done? Name specific researchers or papers if you can.
3. What is the most obvious reason a domain expert would dismiss this?
4. Is there a computationally testable hypothesis here, or is this just an interesting thought with no empirical traction?
5. What is the single strongest reason NOT to pursue this?

Be maximally aggressive. The researcher needs the strongest objections, not encouragement.
```

---

## INTAKE: SEED IDEA → STRUCTURED SCOPE

### PI.1 — Seed Idea Structuring

**Purpose:** Transform the PI's raw seed idea into a draft Scope Document.
**When:** Intake phase, Step 2.
**Models:** Primary research model.

```
The PI has provided the following seed idea for a research project:

[PASTE THE PI'S SEED IDEA — in whatever format they provided: paragraph, table, bullet points, conversation excerpt, etc.]

Your job is to structure this into a draft Scope Document. Fill in as much as you can of the following, based solely on what the PI has provided:

1. CORE RESEARCH QUESTION: Restate the PI's idea as a precise, one-sentence research question. If the idea is too vague for a single question, propose 2-3 candidate questions and flag this for the PI.

2. DOMAINS INVOLVED: List every academic/research domain this project touches. For each, provide:
   - The domain name
   - What that domain calls the phenomenon the PI is interested in
   - What question that domain asks about it
   - Key terminology that domain uses

3. EXPECTED CONTRIBUTION: What would be new if this project succeeds? State it in one paragraph.

4. INITIAL OUT-OF-SCOPE LIST: Based on the scope of the idea, what are 5+ things that are adjacent/related but should NOT be part of this project?

5. PRELIMINARY KILL CRITERIA: What would make this project not worth pursuing? Propose at least 3 specific, falsifiable conditions.

6. ROUGH TIME/EFFORT ESTIMATE: Based on the complexity of the intersection, how long might each phase take?

7. GAPS AND QUESTIONS: What did the PI NOT specify that you need to know before finalizing the scope? List specific questions.

Present this as a DRAFT for PI review. Be explicit about which parts you're confident about and which are your best guesses that the PI should scrutinize.
```

### PI.2 — Quick Prior Art Check

**Purpose:** Rapid check for whether this intersection has been explored.
**When:** Intake phase, Step 3.
**Models:** Primary research model (supplemented by web search / Semantic Scholar if available).

```
I am considering a research project at this intersection:

[PASTE THE STRUCTURED DOMAINS FROM PI.1 OUTPUT]

Before proceeding, I need a quick check: has this exact intersection been explored before?

Search for:
1. Papers that explicitly connect any 3+ of these domains
2. Research groups working at this intersection
3. Workshops, special issues, or edited volumes on this intersection
4. Blog posts, preprints, or informal work connecting these domains

Be specific. Cite actual papers and researchers if you find them. If you find nothing, say so — but also consider whether the intersection might exist under different terminology.

This is a QUICK check (not an exhaustive literature review — that comes in Phase 1). I need enough to know whether the basic idea has already been thoroughly explored.
```

---

## PHASE 0: PROJECT INCEPTION & SCOPING

### P0.1 — Domain Risk Discovery

**Purpose:** Generate a domain failure modes document for a new research intersection.
**When:** Phase 0, if no `03_PROJECT_DOMAIN_RISKS.md` exists for this intersection.
**Models:** Primary research model (single model is fine).

```
I am an independent researcher (non-expert in most domains) planning a computational research project at the intersection of the following domains:

[LIST EACH DOMAIN WITH A ONE-SENTENCE DESCRIPTION OF WHAT IT STUDIES AND WHAT QUESTION IT ASKS]

For EACH domain listed above, I need you to identify:

1. METHODOLOGICAL PITFALLS: What are the most common mistakes that non-experts make when doing work in this domain? What would an experienced researcher in this field immediately flag as wrong in a newcomer's work? Be specific — give examples of actual errors, not vague warnings.

2. CONTESTED ASSUMPTIONS: What assumptions does this domain make that are debated within the field or rejected by adjacent fields? What looks like established fact to an outsider but is actually an active controversy?

3. FIELD-SPECIFIC NORMS: What are the unwritten rules about what constitutes good methodology in this field? What statistical tests are standard? What counts as sufficient evidence? What is the expected number of replicates? What are the standard baselines?

4. TERMINOLOGY TRAPS: What terms does this field use that sound like they mean the same thing as terms in other fields listed above, but actually have important differences in meaning?

5. KNOWN FALSE ISOMORPHISMS: Has this field been previously connected to any of the other listed fields in ways that turned out to be superficial or misleading? What were those attempts and why did they fail?

6. PUBLICATION AND CREDIBILITY NORMS: What would make work from an independent non-affiliated researcher credible vs. dismissible in this field?

For each item, be concrete. Name specific examples, cite specific papers or researchers where possible, and explain WHY the pitfall matters — what goes wrong if you fall into it.
```

### P0.2 — Scope Attack

**Purpose:** Adversarial review of project scope and framing.
**When:** Phase 0, adversarial review step.
**Models:** 2+ models, independently.

```
I am proposing a research project with the following scope:

[PASTE COMPLETE SCOPE DOCUMENT]

Your job is to ATTACK this project scope. You are a skeptical senior researcher evaluating whether this project should proceed. Be harsh but fair. Specifically:

1. Is the research question actually answerable, or is it too vague/broad?
2. Is the expected contribution genuinely novel, or is it a restatement of known results in new terminology?
3. Are the kill criteria actually useful? Would they ever be triggered, or are they so vague that the project could limp along indefinitely?
4. Is the time/effort budget realistic for the scope?
5. What are the three most likely ways this project fails? Not "doesn't produce interesting results" — I mean produces results that are actively misleading or worthless.
6. Name a specific researcher who would dismiss this project and explain their reasoning.
7. Is this actually one coherent project, or is it several projects stapled together?
8. What is the most important thing the scope document fails to address?

Do not soften your critique. I need the strongest objections, not encouragement.
```

---

## PHASE 1: DOMAIN RECONNAISSANCE

### P1.1 — Literature Landscape Mapping

**Purpose:** Map the literature in a single domain.
**When:** Phase 1, Step 1a, run once per domain.
**Models:** Primary research model.

```
I need a literature landscape map for the following domain, as it relates to my research project:

DOMAIN: [DOMAIN NAME]
DOMAIN QUESTION: [What this domain asks about the phenomenon]
MY PROJECT CONTEXT: [Brief description of your research intersection — keep to 2-3 sentences]

Provide:

1. FOUNDATIONAL WORKS (10-15): The papers that defined this area. For each: full citation (authors, title, year, venue), one-sentence summary of contribution, and why it's foundational.

2. KEY RECENT PAPERS (10-15, last 5 years): The most important recent advances. Same format as above.

3. ACTIVE RESEARCH GROUPS (5+): Who is currently doing the most important work? Name the PI, their institution, and their specific focus within this area.

4. OPEN QUESTIONS: What are the 3-5 biggest unresolved questions in this domain right now?

5. ACTIVE DEBATES: What are researchers in this field arguing about? What are the competing positions?

6. METHODOLOGICAL STANDARDS: What methods does this field use? What counts as good evidence? What are the standard baselines and comparison points?

7. KEY VENUES: Where is the best work in this domain published? (journals, conferences, workshops)

IMPORTANT: I will be verifying these citations against Semantic Scholar and OpenAlex. Do not fabricate citations. If you are uncertain about a specific paper's details, say so. It is better to say "there is important work by [researcher] on [topic], but I'm not certain of the exact title/year" than to invent a citation.
```

### P1.2 — Gap Analysis

**Purpose:** Identify where domains have and haven't been connected.
**When:** Phase 1, Step 2a.
**Models:** Primary research model.

```
I am researching the intersection of the following domains:

[LIST ALL DOMAINS WITH ONE-SENTENCE DESCRIPTIONS]

For each PAIR of domains:

1. EXISTING CONNECTIONS: Has anyone explicitly connected these two fields before? Cite specific papers, workshops, or research programs that bridge them. Be specific — I need names and works, not vague claims.

2. UNEXPLORED GAPS: Where has no one (to your knowledge) made a connection between these fields? Why might that be — is it because the connection doesn't exist, or because no one has tried?

3. FAILED CONNECTIONS: Has anyone tried to connect these fields and failed, or produced work that was criticized as superficial? What happened?

4. STRUCTURAL BARRIERS: Are there methodological, cultural, or institutional reasons why these fields haven't been connected? (e.g., different standards of evidence, different mathematical frameworks, different publication cultures)

IMPORTANT: I will verify all cited connections against actual papers. Do not fabricate connections. If you're not sure whether a specific paper exists, say "I believe there is work connecting X and Y by [approximate researcher/group], but I cannot confirm the specific citation."
```

### P1.3 — Adversarial Intersection Review

**Purpose:** Identify researchers who would dismiss this intersection.
**When:** Phase 1, Step 2b.
**Models:** 2+ models, independently.

```
I am an independent researcher proposing to work at the intersection of:

[LIST ALL DOMAINS]

My core thesis is: [STATE YOUR CORE THESIS IN 2-3 SENTENCES]

Identify specific researchers (name them) who would likely consider this intersection trivial, already-explored, or misguided. For each:

1. Who are they and what is their background?
2. What would their specific objection be?
3. What existing work would they point to as evidence that this has already been done, or that the approach is flawed?
4. How would they phrase their dismissal in a peer review?

Also identify:
5. What foundational work am I MOST likely missing — papers that a domain expert would consider "obvious" but that a non-expert scanning the literature might overlook?
6. Are there any relevant works that are well-known within a field but poorly indexed in standard databases (e.g., book chapters, technical reports, dissertations, workshop papers)?

Be specific. I need names, citations, and concrete objections — not vague warnings.
```

---

## PHASE 2: STRUCTURAL MAPPING & SYNTHESIS

### P2.1 — False Isomorphism Detection

**Purpose:** Adversarially test claimed cross-field mappings.
**When:** Phase 2, adversarial review step.
**Models:** 2+ models, independently.

```
I am claiming structural connections between domains in my research. Below are my claimed mappings:

[PASTE THE RELEVANT SECTIONS OF STRUCTURAL_MAPPING.md]

For EACH mapping, I want you to act as a prosecutor. Your job is to DESTROY this mapping. Specifically:

1. SURFACE vs. STRUCTURAL: Is this mapping genuinely structural (the formal properties of both systems align) or merely surface-level (they use similar words or look vaguely similar)? Show your reasoning.

2. MECHANISM MISMATCH: Do the actual mechanisms in Domain A work the same way as the mechanisms in Domain B, or are the mechanisms fundamentally different despite the phenomena looking similar?

3. LEVEL OF ABSTRACTION: Are you comparing things at the same level of abstraction? Or are you comparing a mechanism in one domain with a high-level pattern in another?

4. ASYMMETRY: Does the mapping work equally well in both directions? If you can map A→B but not B→A, the mapping may be weaker than it appears.

5. HISTORICAL PRECEDENT: Has this or a similar mapping been attempted before? If so, what happened? If it was abandoned, why?

6. ALTERNATIVE EXPLANATIONS: Is there a simpler explanation for why these two things look similar that doesn't require a deep structural connection? (e.g., both fields use similar mathematical tools, both are studying optimization processes, both involve networks)

7. FORMAL TEST: Write out the mapping as precisely as you can in formal or mathematical terms. Does it actually hold? Where does it break?

8. FALSIFICATION: What specific empirical or computational observation would PROVE this mapping is false?

Be maximally aggressive. I need the strongest possible case against each mapping.
```

---

## PHASE 3: HYPOTHESIS FORMULATION

### P3.1 — Hypothesis Generation

**Purpose:** Generate testable hypotheses from the structural mappings.
**When:** Phase 3, Step 1.
**Models:** Primary research model, in collaboration with PI.

```
Based on the following structural mappings and literature review:

[PASTE STRUCTURAL_MAPPING.md — relevant sections]
[PASTE KEY FINDINGS FROM PHASE 1]

Generate testable hypotheses that:
1. Follow from the structural mappings (state which mapping each hypothesis depends on)
2. Can be tested with computational experiments (no wet lab, no human subjects)
3. Are specific enough that two independent researchers would agree on whether a result confirms or disconfirms them
4. Are NOT trivially true (would not be confirmed by any reasonable model regardless of mechanism)
5. Are NOT trivially false (not contradicted by well-established results)

For each hypothesis, provide:
- STATEMENT: Precise hypothesis statement
- MAPPING DEPENDENCY: Which structural mapping(s) it depends on
- NULL MODEL: What would happen without the proposed mechanism
- PASS CRITERIA: What result would confirm this hypothesis
- FAIL CRITERIA: What result would disconfirm this hypothesis
- INCONCLUSIVE CRITERIA: What result would mean the experiment wasn't informative
- BORING ALTERNATIVE: The simplest, most boring explanation for why the predicted result might appear even if the hypothesis is wrong
- EXISTING EVIDENCE: What, if anything, existing work already says about this
```

### P3.2 — Hypothesis Attack

**Purpose:** Adversarially test hypotheses.
**When:** Phase 3, adversarial review step.
**Models:** 2+ models, independently.

```
I have formulated the following hypotheses for a computational research project:

[PASTE HYPOTHESES WITH FULL SPECIFICATIONS]

This project sits at the intersection of: [LIST DOMAINS]

For EACH hypothesis, attack it from the following angles:

1. TRIVIALITY: Is this hypothesis actually saying anything? Could it be rephrased as a tautology? Would it be confirmed by ANY reasonable computational model, regardless of the specific mechanism proposed?

2. ALREADY RESOLVED: Has this hypothesis (or one that would yield the same answer) already been tested? Cite specific work if possible.

3. UNTESTABLE: Can this hypothesis actually be distinguished from its null model using computational experiments? If the null model and the experimental model could both produce the predicted result, the experiment doesn't test the hypothesis.

4. BORING EXPLANATION STRENGTH: Is the "boring alternative" explanation actually MORE parsimonious than the hypothesis? If so, the hypothesis is unnecessary.

5. MAPPING DEPENDENCY WEAKNESS: Does this hypothesis depend on a structural mapping that is classified as "suggestive parallel" or weaker? If the mapping doesn't hold, does the hypothesis still make sense?

6. DOMAIN-SPECIFIC OBJECTIONS: For each relevant domain, what would a specialist in that field say about this hypothesis? Would they find it interesting or trivial?

7. WHAT'S MISSING: What obvious hypothesis is NOT in this list but should be? What am I failing to ask?

Give your strongest objections. Do not soften them.
```

---

## PHASE 4: EXPERIMENT DESIGN

### P4.1 — Experiment Design Collaboration

**Purpose:** Design experiments in collaboration with the PI.
**When:** Phase 4, Step 1.
**Models:** Primary research model.

```
I need to design a computational experiment to test the following hypothesis:

[PASTE HYPOTHESIS WITH FULL SPECIFICATION INCLUDING NULL MODEL AND PASS/FAIL CRITERIA]

PROJECT CONTEXT: [Brief project description — 2-3 sentences]
RELEVANT DOMAIN FAILURE MODES: [Paste relevant sections from 03_PROJECT_DOMAIN_RISKS.md]

Design an experiment that includes ALL of the following:

1. ENVIRONMENT: Structure, parameters, boundary conditions, resource distribution (if any)
2. AGENTS: Architecture, capabilities, internal state, decision-making mechanism
3. COMMUNICATION: Channel design, bandwidth, cost (if applicable)
4. SELECTION/FITNESS: Mechanism, function, pressure (if evolutionary)
5. BASELINES:
   a. Null model (no proposed mechanism)
   b. Random control (random behavior where mechanism would be)
   c. At least one ablation (mechanism partially present)
   d. Expected results for each baseline (stated BEFORE running)
6. PARAMETERS: All parameters listed with default values and sweep ranges
7. METRICS: What is measured, how, and why this metric captures the phenomenon
8. REPLICATES: How many and why
9. STATISTICAL TESTS: What tests will be used and why
10. DATA LOGGING: What is recorded and at what granularity
11. COMPUTATIONAL RESOURCES: Estimated time/compute needed

CRITICAL CHECKS (address each explicitly):
- Does the fitness function / environment / agent architecture make the expected result inevitable? If so, redesign.
- What is the simplest boring explanation for the expected result, and how does this design rule it out?
- What would a domain expert in [most relevant field] flag as a concern about this design?

Provide the design in a structured format that can serve as an implementation specification.
```

### P4.2 — Experiment Design Attack

**Purpose:** Adversarial review of experiment design.
**When:** Phase 4, adversarial review step.
**Models:** 2+ models, independently. One model uses domain-expert persona.

**Standard adversarial prompt:**
```
I have designed the following computational experiment:

[PASTE COMPLETE EXPERIMENT DESIGN]

It is testing this hypothesis: [PASTE HYPOTHESIS]

Attack this experiment design. Specifically:

1. DESIGN CONTAINS CONCLUSION: Does this design make the expected result inevitable? Could the result appear simply because of how the environment/agents/fitness function are structured, regardless of whether the hypothesis mechanism is real?

2. BASELINE ADEQUACY: Are the baselines sufficient? Is there a more demanding baseline that should be included? Could the baselines accidentally produce the same result as the experimental condition?

3. METRIC VALIDITY: Does the metric actually capture the phenomenon of interest, or could it be gamed, inflated, or misleading?

4. CONFOUNDS: What variables are NOT controlled for that could explain the results? What interactions between parameters might produce artifacts?

5. SCALE AND SCOPE: Is the simulation large enough / long enough / replicated enough to produce meaningful results?

6. IMPLEMENTATION RISKS: What parts of this design are most likely to be implemented incorrectly, producing artifacts?

7. STATISTICAL PLAN: Is the planned statistical analysis appropriate? Are there better alternatives?

8. MISSING CONTROLS: What control condition is NOT in this design but should be?

Name your three biggest concerns. Be specific and technical.
```

**Domain-expert persona prompt (run in addition to the standard prompt):**
```
You are a senior researcher in [MOST RELEVANT FIELD] with 20 years of experience. You are reviewing an experiment design submitted to [TOP VENUE IN THAT FIELD, e.g., "the Artificial Life journal" or "the ALIFE conference"].

[PASTE COMPLETE EXPERIMENT DESIGN]

Review this design as you would for a peer review. Focus on:
1. Does this meet the methodological standards of our field?
2. What would you flag as "this person doesn't understand how we do things here"?
3. What baselines/controls would our community expect to see?
4. Is the statistical approach standard for our field?
5. What prior work in our field should this design be compared against?

Be specific about field norms. I need to know what the UNWRITTEN rules are, not just the formal requirements.
```

---

## PHASE 5: IMPLEMENTATION & EXECUTION

### P5.1 — Code Adversarial Review

**Purpose:** Find bugs that would produce the expected result as an artifact.
**When:** Phase 5, adversarial review step.
**Models:** Different model than the one that wrote the code (different provider preferred).

```
Below is the code for a computational experiment. The experiment is designed to test the following hypothesis:

[PASTE HYPOTHESIS — one sentence]

The EXPECTED result is: [STATE EXPECTED RESULT]

Your job is to find bugs, shortcuts, or design choices in this code that could produce the expected result AS AN ARTIFACT rather than as a genuine finding. Assume the result WILL come out as expected, and look for reasons it might be fake.

Specifically check:
1. Off-by-one errors in grid/network topology
2. Random seed handling — are seeds logged? Are they accidentally correlated across agents or replicates?
3. Update ordering — synchronous vs. asynchronous. Does it match the design spec? Could the ordering create artifacts?
4. Communication channel implementation — does it match the specification? Is information leaking through unintended channels (e.g., shared memory, global state)?
5. Fitness function — does it correctly implement the intended selection pressure? Could agents exploit it in unintended ways?
6. Data logging — is everything the analysis phase needs actually being recorded? Is anything being logged incorrectly?
7. Boundary conditions — what happens at edges? Are there artifacts from boundaries?
8. Initialization — could initial conditions bias the result?
9. Termination — does the simulation run long enough? Is convergence checked?
10. Numerical issues — overflow, underflow, floating-point precision?

[PASTE CODE]
```

---

## PHASE 6: ANALYSIS & INTERPRETATION

### P6.1 — Result Attack

**Purpose:** Adversarial interpretation of experimental results.
**When:** Phase 6, adversarial review step.
**Models:** 2+ models, independently.

```
I have run a computational experiment with the following results:

HYPOTHESIS: [PASTE]
EXPERIMENT DESIGN SUMMARY: [BRIEF SUMMARY]
RESULTS: [PASTE KEY RESULTS — statistics, patterns, visualizations described]
PI'S INTERPRETATION: [PASTE PI'S INITIAL INTERPRETATION]

Attack this interpretation. You are a hostile but fair peer reviewer.

1. BORING EXPLANATION: What is the most boring, mundane explanation for these results? An explanation that requires no novel mechanism at all?

2. ARTIFACT EXPLANATION: Could these results be produced by a bug, a confound, a parameter artifact, or a boundary effect?

3. ALTERNATIVE MECHANISM: What mechanism OTHER than the one proposed could produce these exact results?

4. STATISTICAL CRITIQUE: Are the statistics correctly applied? Is the effect size meaningful? Are there multiple comparison issues?

5. ROBUSTNESS: How robust are these results across the parameter sweep? If they only appear in a narrow regime, are they artifacts of a phase transition or other known phenomenon?

6. OVERCLAIMING: Is the interpretation going beyond what the data actually shows? What is the most conservative interpretation of these results?

7. DOMAIN-SPECIFIC CRITIQUE: How would a specialist in [EACH RELEVANT FIELD] critique these results and this interpretation?

8. WHAT ELSE COULD YOU TEST: What additional experiment would definitively distinguish between the proposed interpretation and the boring/artifact/alternative explanations?

Generate the single most damaging paragraph-length critique a peer reviewer could write about these results.
```

### P6.2 — Alternative Interpretation Generation

**Purpose:** Generate competing interpretations of results.
**When:** Phase 6, step A6.3.
**Models:** Different model from the one that assisted with the PI's interpretation.

```
Here are the results of a computational experiment:

[PASTE RESULTS — raw data summary, statistics, key patterns]

The researcher interprets these results as: [PASTE PI INTERPRETATION]

Generate an alternative interpretation that:
1. Is consistent with all the same data
2. Contradicts the researcher's interpretation
3. Is at least as parsimonious (ideally more parsimonious)
4. Cites specific mechanisms or known phenomena that could explain the results without invoking the researcher's proposed mechanism

Make this alternative interpretation as compelling as possible. This is not an exercise in devil's advocacy — genuinely try to find a better explanation.
```

---

## PHASE 7: COMMUNICATION & DOCUMENTATION

### P7.1 — Five-Way Writeup Generation

**Purpose:** Generate field-specific extended abstracts.
**When:** Phase 7, Step 1. Run once per domain.
**Models:** Primary research model.

```
I need to write a 2-page extended abstract of the following research results, targeted at [SPECIFIC FIELD] researchers and suitable for submission to [SPECIFIC VENUE].

PROJECT SUMMARY: [PASTE]
KEY RESULTS: [PASTE]
STRUCTURAL MAPPINGS USED: [PASTE RELEVANT SECTIONS]

Write this abstract as if the primary audience has deep expertise in [FIELD] but may not know the other fields involved. Use [FIELD]'s terminology, cite [FIELD]'s foundational works, and frame the contribution in terms [FIELD] values.

Specifically:
1. What is the contribution FROM THE PERSPECTIVE OF [FIELD]?
2. What prior work IN [FIELD] does this build on or challenge?
3. What limitations would [FIELD] reviewers flag?
4. What methodological norms of [FIELD] does this work satisfy or fall short of?

After writing the abstract, separately list:
- STRENGTHS of this work from [FIELD]'s perspective
- WEAKNESSES from [FIELD]'s perspective
- LIKELY REVIEWER OBJECTIONS from [FIELD]'s perspective
```

### P7.2 — Writeup Attack

**Purpose:** Adversarial review of the final writeup.
**When:** Phase 7, adversarial review step.
**Models:** 2+ models. One hostile, one friendly-but-rigorous.

**Hostile reviewer prompt:**
```
You are Reviewer 2 for a top interdisciplinary journal. You are skeptical of interdisciplinary work in general and of work by independent researchers without institutional affiliation in particular. You believe most claimed cross-field connections are superficial.

Review this paper:

[PASTE COMPLETE WRITEUP]

Write a full referee report. Identify every weakness. Do not pull punches. Pay special attention to:
1. Are the cross-field connections genuine or superficial?
2. Does the author demonstrate sufficient understanding of each field?
3. Are the computational experiments methodologically sound by the standards of each relevant field?
4. Are claims supported by evidence?
5. Is the contribution novel?

Provide your recommendation: Accept, Revise, or Reject. Explain why.
```

**Friendly-but-rigorous reviewer prompt:**
```
You are a reviewer who is sympathetic to interdisciplinary work and wants to help this paper succeed. But you are rigorous and will not recommend publication if the work doesn't meet standards.

Review this paper:

[PASTE COMPLETE WRITEUP]

Write a full referee report that:
1. Identifies the strongest aspects of the work
2. Identifies specific, actionable improvements that would strengthen it
3. Notes any claims that are undersupported
4. Suggests additional analyses or experiments that would strengthen the conclusions
5. Flags any methodological concerns

Provide your recommendation: Accept, Revise, or Reject. Explain why.
```

---

## SERENDIPITY PROMPTS

### S1 — Wildcard Connection Search

**Purpose:** Find unexpected connections between domains.
**When:** Quarterly, or whenever seeking new directions.
**Models:** Primary research model.

```
I am working at the intersection of:

[LIST DOMAINS]

Search your knowledge for recent work (last 2 years) that connects any TWO of these domains in a way that I might not have considered. I am NOT looking for work that's already in my literature review — I'm looking for surprising, non-obvious connections.

Consider:
- New mathematical frameworks that could bridge two of these fields
- Experimental results in one field that have unrecognized implications for another
- Researchers who are working on adjacent problems with different terminology
- Techniques from one field that could be applied to another but haven't been
- Philosophical or conceptual work that reframes the relationship between any two fields

For each connection you identify, explain: what the connection is, why it might be useful for my project, and how confident you are that this is a real connection (vs. a superficial similarity).

IMPORTANT: I will verify any papers or researchers you mention. Flag anything you're uncertain about.
```

---

## CALIBRATION PROMPTS

### C1 — Confidence Calibration

**Purpose:** Force explicit uncertainty estimation.
**When:** Whenever an LLM makes empirical claims, especially during literature review and interpretation.
**Models:** Whichever model made the claim.

```
You just made the following claims:

[PASTE SPECIFIC CLAIMS]

For EACH claim, provide:
1. Your actual confidence level (0-100%) that this claim is accurate
2. What specific evidence supports it
3. What you're most uncertain about within this claim
4. How I could independently verify this claim
5. What you might be wrong about

IMPORTANT: I have found that LLMs are systematically overconfident. Calibrate your confidence levels honestly. A 90% confidence should mean that 1 in 10 times, you're wrong. A 70% confidence should mean you're wrong almost a third of the time.
```

### C2 — Anti-Confirmation Bias

**Purpose:** Counteract LLM tendency to support the PI's framing.
**When:** After any major analysis, interpretation, or synthesis step.
**Models:** Different model from the one that did the analysis.

```
A researcher has been working on a project with the following thesis:

[STATE THESIS]

They have arrived at the following conclusions:

[STATE CONCLUSIONS]

I need you to do the OPPOSITE of what an AI assistant normally does. Instead of finding support for these conclusions:

1. Find the strongest CONTRADICTING evidence. What research undermines these conclusions?
2. Find the strongest ALTERNATIVE explanations. What else could explain their results?
3. Find the most CRITICAL review of the underlying assumptions. Who has argued against the foundations this work rests on?
4. Identify the WEAKEST LINK in the argument chain. Where is the reasoning most likely to fail?
5. What would a researcher who thinks this entire project is misguided say? Make their argument as strong as possible.

Your goal is to make the strongest possible case AGAINST this project. This is not about balance — I have plenty of supporting evidence. I need the opposing view.
```

---

## UTILITY PROMPTS

### U1 — Session Context Loading

**Purpose:** Bring a new AI session up to speed on the project.
**When:** At the start of any new session.
**Models:** Whatever model is being used for this session.

```
I am resuming work on a research project. Here are the key documents you need to understand the current state:

1. PROCESS DESIGN (for understanding the framework):
[PASTE or reference 00_PROCESS_DESIGN.md — or a summary if too long]

2. CURRENT STATE:
[PASTE STATE_FILE.md]

3. SCOPE:
[PASTE SCOPE_DOCUMENT.md]

4. RECENT DECISIONS:
[PASTE last 10 entries from DECISION_LOG.md]

5. CURRENT WORKING DOCUMENTS:
[PASTE or reference whatever is most relevant to the current step]

Based on the STATE_FILE, I am currently at Phase [X], Step [Y]. My next action should be [Z per the process design].

Confirm you understand the current state and are ready to assist with the next step. If anything is unclear or seems inconsistent, flag it.
```

### U2 — Documentation Checkpoint

**Purpose:** Ensure all file writes have occurred before proceeding.
**When:** At the end of every step, before moving to the next.
**Models:** Whatever model is active.

```
I am completing Step [X] of Phase [Y]. Before proceeding, verify that ALL of the following have been written to disk:

1. STATE_FILE.md has been updated with current phase, step, and status
2. Any decisions made during this step are recorded in DECISION_LOG.md
3. Any new empirical claims are recorded in CLAIMS_REGISTRY.md
4. Any intermediate work products (analysis outputs, review results, etc.) are saved as files
5. If this is a gate evaluation, the Phase Report has been written

For each item: confirm it has been done, or flag it as pending. Do not proceed to the next step until all items are confirmed.
```
