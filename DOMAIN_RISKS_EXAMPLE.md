# EXAMPLE: Project Domain Failure Modes

> **This is a worked example.** It shows what a completed domain failure modes document looks like for a specific project at the intersection of bioelectric signaling, artificial life, AI alignment, model merging, and philosophy of mind. Use it as a reference for structure and depth when generating your own domain risks document using the "Domain Risk Discovery" prompt in `02_PROMPT_LIBRARY.md` → Phase 0 → P0.1.

---

# Project Domain Failure Modes: Bioelectric Signaling × Artificial Life × AI Alignment × Model Merging × Philosophy of Mind

## DOCUMENT PURPOSE

This document captures known domain-specific risks, pitfalls, and failure modes for a research project at the intersection of the five domains listed above. It is specific to THIS research intersection and should be consulted at every phase to ensure domain-specific risks are being managed.

This document was generated based on extended analysis of the specific risks that arise when a non-expert PI conducts computational research at this intersection using AI language models as a research team.

## HOW TO USE THIS DOCUMENT

**If you are an AI agent:**

1. Read this document at the start of any session involving this project.
2. When working on any phase, check the relevant domain sections below for risks that apply to the current task.
3. When running adversarial reviews, use the domain-specific risks here to inform your critique — these are KNOWN pitfalls, not speculative ones.
4. Flag any time the project appears to be falling into one of these pitfalls.

**If you are the PI:**

This is your "what to watch out for" reference. Skim the relevant sections before each phase gate review.

---

## DOMAIN 1: ARTIFICIAL LIFE (ALife) — EVOLVED DIGITAL ORGANISMS WITH COMMUNICATION

### Risk 1.1: Designing Fitness Landscapes That Contain Your Conclusion

**Severity: CRITICAL — This is the single most common failure mode in computational evolution experiments.**

When you want to show that digital organisms evolve coordinated communication, the choices you make about environment structure, resource distribution, communication channel bandwidth, and fitness function all constrain what CAN evolve. If you give organisms a shared resource that can only be exploited through coordination, and you give them a communication channel, and coordination evolves — you may have demonstrated nothing more than "optimization finds the solution I made available."

**How to detect it:** Before running any experiment, ask: "Could a competent optimization algorithm find the coordination solution I'm looking for without any of the interesting dynamics I'm hoping to observe? If yes, the experiment isn't testing what I think it's testing."

**Mitigation:** Run a "dumb baseline" — a simple optimization algorithm (e.g., hill climbing, random search) in the same environment. If it finds the same coordination pattern, your evolutionary dynamics aren't doing interesting work. The interesting experiments are ones where coordination emerges DESPITE not being the obvious path, or where the FORM of coordination is surprising.

### Risk 1.2: Parameter Sensitivity / Narrow Regime Results

**Severity: HIGH**

You will find striking results that only exist in a narrow parameter regime. If your evolved communication only appears when mutation rate is between 0.003 and 0.007, it's probably an artifact of that specific parameter regime rather than a robust phenomenon.

**How to detect it:** Systematic parameter sweeps over ALL parameters, not just the ones you think matter.

**Mitigation:** Build parameter sweeps into the experiment design from day one. Report results across the full parameter space. Results that only appear in a narrow regime should be flagged and investigated — they may reflect phase transitions (which are interesting) or artifacts (which are not).

### Risk 1.3: Update Ordering Artifacts

**Severity: MEDIUM-HIGH**

Whether agents update synchronously (all at once) or asynchronously (one at a time) can qualitatively change the dynamics. Many published ALife results are sensitive to update ordering, and this is rarely reported. An experienced ALife researcher will immediately ask about this; a non-expert often treats it as an implementation detail.

**How to detect it:** Run the same experiment with synchronous and asynchronous updates. If results differ qualitatively, the update ordering is doing real work and must be justified.

**Mitigation:** Choose update ordering deliberately based on what the biological/theoretical analogy calls for. Document and justify the choice. Test sensitivity.

### Risk 1.4: Reporting Norms

**Severity: MEDIUM**

ALife research has specific expectations about how stochastic simulation results are reported: number of replicates (typically 30+), statistical comparisons between conditions (not just within), visualization of distributions (not just means), and discussion of what evolutionary dynamics are observed over time (not just final outcomes).

**How to detect it:** Read the methods sections of 10 recent papers in the Artificial Life journal and ALIFE conference proceedings. Note their reporting standards.

**Mitigation:** Match or exceed these standards in your own work.

---

## DOMAIN 2: BIOELECTRIC SIGNALING VIA GAP JUNCTIONS

### Risk 2.1: The Computational Metaphor vs. Biophysical Reality

**Severity: HIGH**

There is a meaningful difference between:
- "Cells exchange ions through gap junctions and this influences neighbor behavior" (well-established biophysics)
- "Cells perform distributed computation over bioelectric networks to solve morphogenetic problems" (a particular interpretive framework, primarily associated with Levin's group)

Your simulations will almost certainly model the latter, which means you're testing Levin's computational framework, not raw biology. This is fine, but if you don't state it explicitly, a reviewer from mainstream developmental biology will reject your framing before reading your results.

**How to detect it:** Ask: "Am I claiming my simulation models what cells actually do, or what Levin's framework says cells do?" If the answer is the former, you're overclaiming.

**Mitigation:** In all writeups and design documents, always distinguish between the biophysical substrate (what gap junctions do physically) and the computational abstraction you're working with. Be explicit that your digital organisms are testing whether the COMPUTATIONAL MODEL of bioelectric coordination produces interesting dynamics — not claiming to simulate actual cells.

### Risk 2.2: Contested Framework

**Severity: MEDIUM-HIGH**

Levin's framework is compelling but not universally accepted within developmental biology. Some researchers think the computational language he uses is a productive metaphor being treated as a literal mechanism. Your project inherits this debate whether you intend to or not.

**How to detect it:** Read critiques of Levin's framework (they exist but are less visible than the supportive work). Understand what the objections are.

**Mitigation:** Acknowledge this debate in your framing. Present your work as exploring the implications of the computational model, not as proving the computational model is correct. This also protects you: if Levin's framework is later refined or rejected, your work on the computational model still has value as a study of that type of computational architecture.

### Risk 2.3: Overfitting to Levin's Terminology

**Severity: MEDIUM**

Levin uses terms like "cognitive light cone," "goal-directed behavior in cells," and "competent agents at every scale." These are evocative and influential but also contested. If your project adopts this terminology uncritically, you inherit its assumptions and its critics.

**How to detect it:** For every Levin-specific term you use, ask: "Can I replace this with a more neutral term without losing precision? If not, am I aware that this term is contested?"

**Mitigation:** Define your own terms where possible. Use Levin's terms when referencing his framework specifically, but use more neutral language when describing your own computational experiments.

---

## DOMAIN 3: AI ALIGNMENT — INNER-OBJECTIVE DIVERGENCE

### Risk 3.1: The False Isomorphism with Evolutionary Dynamics

**Severity: CRITICAL — This is the most likely point of intellectual failure for this project.**

Inner alignment as described by Hubinger et al. has very specific technical preconditions: a mesa-optimizer arises within a base optimizer, develops an internal objective that differs from the base objective, and is coherent enough to pursue that objective strategically. This happens within a SINGLE optimization process (a learned model within a training process).

Evolved digital organisms that develop divergent sub-goals are doing something that LOOKS analogous but may differ in formal structure. In evolutionary systems, "goal divergence" usually means individual-level selection diverging from group-level selection — this is classical multilevel selection theory, with a century of literature behind it. The alignment community's framing is about learned objectives diverging from specified objectives within a single optimization process.

If you conflate these:
- An alignment researcher will say: "That's just multilevel selection, we already know about that, it's not the same problem."
- A biologist will say: "You're importing AI terminology onto standard evolutionary dynamics."

**How to detect it:** Write out the precise formal structure of inner alignment. Then write out the precise formal structure of what's happening in your evolutionary simulation. Compare them element by element. Where do they match formally, not just verbally?

**Mitigation:** The Structural Mapping document MUST address this mapping in detail. The mapping may turn out to be genuinely productive, but it requires heavy formal lifting to establish — it cannot be asserted by verbal analogy. If the mapping doesn't survive formal scrutiny, demote it from a core pillar to a "suggestive parallel."

### Risk 3.2: Alignment-Specific Terminology Misuse

**Severity: MEDIUM-HIGH**

Terms like "mesa-optimizer," "inner alignment," "deceptive alignment," and "goal misgeneralization" have precise technical definitions in the alignment literature. Using them loosely (e.g., applying "mesa-optimizer" to any sub-agent that develops its own behavior) will immediately flag your work as amateur to alignment researchers.

**How to detect it:** For each alignment term you use, find its original definition (usually in Hubinger et al. 2019 "Risks from Learned Optimization") and verify you're using it correctly.

**Mitigation:** Either use the terms precisely as defined, or use your own terms and explain how they relate to alignment terminology.

### Risk 3.3: The AI Safety Community's Standards

**Severity: MEDIUM**

The alignment community values formal/mathematical argumentation more than empirical demonstration. Computational experiments are valued mainly when they illustrate a theoretical point or provide counterexamples. An alignment researcher is more likely to be convinced by a formal proof that your evolutionary dynamics have property X than by 10,000 simulation runs showing property X empirically.

**How to detect it:** Read work published on the Alignment Forum and in ML safety venues. Note the style of argument that is valued.

**Mitigation:** If you want your work to be taken seriously by the alignment community, complement your computational experiments with as much formal analysis as possible. Even informal mathematical arguments are better than pure empirical demonstration.

---

## DOMAIN 4: MODEL MERGING AND FEDERATED LEARNING

### Risk 4.1: Weakest Analogy in the Project

**Severity: HIGH — This is flagged as the domain most at risk of not carrying its weight.**

The analogy between federated learning / model merging and biological coordination through gap junctions is suggestive but structurally thin. The mechanisms are very different:
- Neural network parameter averaging operates in a continuous high-dimensional space with particular geometric properties (loss landscape structure, linear mode connectivity).
- Biological coordination operates through discrete signaling events that modify cell state.
- Evolutionary merging of behavioral strategies (if that's the ALife angle) operates through recombination and selection.

These are three very different mathematical regimes. Claiming deep structural similarity requires heavy formal lifting that may not be justified.

**How to detect it:** Ask: "Can I write down a formal mapping between parameter averaging in a neural network and signaling through a gap junction? If not, is this actually a structural connection or just a verbal similarity?"

**Mitigation:** Either invest in making this connection rigorous (engaging seriously with the mathematics of both model merging geometry and bioelectric network dynamics) OR demote it from a core pillar to a "suggestive parallel" that motivates future work. Do not let a weak pillar undermine the four stronger ones.

### Risk 4.2: Rapidly Moving Field

**Severity: MEDIUM**

Model merging and federated learning are very active ML research areas. Results and understanding are changing quickly. What was considered surprising a year ago may now be well-understood. An LLM's knowledge may be 6-18 months behind current understanding.

**How to detect it:** Use Semantic Scholar / arXiv to check for very recent (last 6 months) papers on model merging.

**Mitigation:** Keep the literature review for this domain especially fresh. Don't rely solely on LLM knowledge — do targeted database searches for the latest work.

---

## DOMAIN 5: THE COMPUTATIONAL BOUNDARY OF SELF — PHILOSOPHY OF MIND

### Risk 5.1: Definitional Quicksand

**Severity: HIGH**

Clark and Chalmers' extended mind thesis, Levin's "self" at multiple scales, and the alignment community's concept of agent boundaries are three different philosophical projects with overlapping vocabulary:
- Clark/Chalmers: epistemological question about where cognition extends
- Levin: biological question about what constitutes an agent
- Alignment: engineering question about where one optimization process ends and another begins

When you write "the computational boundary of self," each community interprets that differently and evaluates your work against their own standards.

**How to detect it:** Show your definition of "self" or "agent boundary" to a philosopher, a biologist, and an alignment researcher (or simulate this with LLMs in persona mode). Do they all agree you mean the same thing?

**Mitigation:** Define YOUR terms formally at the start, in your own framework. Explicitly state how your definitions relate to AND differ from each field's usage. Don't let vocabulary do argumentative work — if you say "self," state exactly what you mean computationally.

### Risk 5.2: Armchair Philosophy Risk

**Severity: MEDIUM-HIGH**

Philosophers of mind will expect engagement with the PHILOSOPHICAL literature on personal identity, constitution, and emergence — not just the popular science versions. If you cite Clark and Chalmers but not the extensive critical literature responding to the extended mind thesis, your philosophical contribution will look shallow.

**How to detect it:** Check whether your citations in this domain include critics as well as proponents. If you only cite people who agree with the framing you're using, you're doing advocacy, not scholarship.

**Mitigation:** Read (or have LLMs help you understand) the main critiques of the extended mind thesis (Adams and Aizawa's "The Bounds of Cognition" is the classic critique). Engage with them in your framing, even if briefly.

### Risk 5.3: Empirical vs. Conceptual Contribution

**Severity: MEDIUM**

Philosophers will want to know: does your computational work actually advance the philosophical question, or does it just illustrate a position that was already argued on philosophical grounds? If the answer is the latter, the computational work adds little from a philosophy perspective.

**How to detect it:** Ask: "Does my simulation tell a philosopher anything they couldn't have figured out by thinking carefully? Does it rule out possibilities they couldn't have ruled out through argument alone?"

**Mitigation:** Focus your philosophical contribution on cases where the computational results genuinely CONSTRAIN or INFORM the philosophical debate — e.g., by showing that a certain boundary condition is necessary for agent coherence, or that a certain type of merging inevitably produces a certain type of identity disruption. These are things argument alone cannot establish.

---

## CROSS-DOMAIN RISKS

### Cross-Risk 1: The LLM Circular Validation Problem

**Severity: CRITICAL**

When LLMs are used both to produce work and to review it, the review can only catch errors within the LLM's knowledge space. The most dangerous errors — the ones a domain expert would catch in five minutes — are precisely the ones that fall OUTSIDE what any model knows to flag.

**Mitigation:** External expert checkpoints are mandatory at Phase 4 (experiment design) and conditionally at Phase 6 (surprising or suspiciously clean results). Additional LLM models cannot substitute for this.

### Cross-Risk 2: Confirmation Bias Amplification

**Severity: CRITICAL**

LLMs are trained to be helpful and responsive to the user's framing. When you describe your hypothesis and ask "is this supported by existing research," the model is predisposed to find supporting evidence. Your AI team will almost never spontaneously say "this whole approach is wrong." You must STRUCTURALLY force adversarial review through explicit prompting.

**Mitigation:** All adversarial review prompts in the Prompt Library are designed to counteract this. Use them faithfully. Run the Anti-Confirmation Bias prompt (C2 in the Prompt Library) after every major synthesis step.

### Cross-Risk 3: Correlated Blind Spots Across Models

**Severity: HIGH**

When you use multiple LLMs to validate novelty or completeness, all models share substantially overlapping training corpora. If a result is known but published in an obscure venue under different terminology, all models may miss it.

**Mitigation:** Use Semantic Scholar and OpenAlex citation graph traversal (not just keyword search) as an independent check. Follow citation chains from papers the models DO surface. This provides a different information-retrieval pathway than LLM recall.

### Cross-Risk 4: Temporal and Prestige Bias in Literature Coverage

**Severity: MEDIUM-HIGH**

LLMs oversample recent, highly-cited, English-language work from prestigious institutions. This project may be affected by:
- Relevant European computational biology work (published in less prominent venues)
- Japanese ALife research (strong tradition, sometimes published in Japanese)
- Older cybernetics and systems biology literature from the 1960s-70s (foundational but not in modern training distributions)
- Dissertation work that bridges these fields but was never published as journal papers

**Mitigation:** Explicitly search for work in these categories during Phase 1. Use the Non-English and Non-Prestigious Venue check in the Phase 1 checklist.

### Cross-Risk 5: The Terminology Translation Problem

**Severity: HIGH**

"Goal divergence" in alignment, "defection" in evolutionary dynamics, "loss of coherence" in bioelectricity — these may or may not be the same thing depending on formal details. LLMs will pattern-match across these terms aggressively and tell you connections exist that may be looser than they appear.

**Mitigation:** The Structural Mapping document is the primary defense. Maintain it rigorously. For every claimed connection between terms from different fields, write out the formal mapping. If it can't be written formally, it's weaker than it appears.
