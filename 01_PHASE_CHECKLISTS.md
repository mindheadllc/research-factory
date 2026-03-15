# Phase Checklists

## PATH CONVENTION

All shared research documents referenced in this file (STATE_FILE.md, DECISION_LOG.md, CLAIMS_REGISTRY.md, STRUCTURAL_MAPPING.md, SCOPE_DOCUMENT.md, HYPOTHESES.md) are located in the `research/` directory of the project tree. Agent-owned documents are in the respective agent directories. See `00_PROCESS_DESIGN.md` Part 2 for the full file tree.

## DOCUMENT PURPOSE

This document contains the step-by-step verification checklists for each phase of a research project conducted in the Research Factory framework. Each phase has:

1. **Mandatory checks** — must all pass for the gate to open.
2. **Embedded adversarial review steps** — specific points where LLMs are prompted to attack the work.
3. **Randomized deep-dive question pool** — a set of 15+ probing questions, from which 5-7 are randomly selected each time the checklist is run. This prevents habituation.

## HOW TO USE THIS DOCUMENT

**If you are an AI agent:**

1. Check the project's `STATE_FILE.md` to determine the current phase.
2. Navigate to that phase's section below.
3. Execute each mandatory check in order.
4. For randomized pools: select 5-7 questions at random (use actual randomization, not sequential selection). Answer each one. If any answer reveals a problem, flag it and record in `DECISION_LOG.md`.
5. For adversarial review steps: use the prompts specified (found in `02_PROMPT_LIBRARY.md`) and record results.
6. Evaluate the gate criteria. Record PASS or FAIL in `STATE_FILE.md`.
7. **WRITE ALL RESULTS TO DISK** in the relevant Phase Report before proceeding.

**If you are the PI:**

Review the completed checklist output produced by your AI team. Pay special attention to any items flagged as concerns. Make the final PASS/FAIL gate decision.

---

## PHASE 0: PROJECT INCEPTION & SCOPING — CHECKLIST

### Mandatory Checks

- [ ] **M0.1 — Research question clarity**: State the core research question in one sentence. Does it make a specific claim or ask a specific question (not vague)?
  - FAIL condition: The question uses only vague terms like "explore the relationship between" without specifying what about the relationship.

- [ ] **M0.2 — Domain enumeration**: List every domain this project touches. For each domain, state in one sentence: what that domain calls the phenomenon, and what question practitioners in that domain would ask about it.
  - FAIL condition: Any domain is listed without both a terminology mapping and a question.

- [ ] **M0.3 — Scope document completeness**: Verify that `SCOPE_DOCUMENT.md` has all sections filled: core question, expected contribution, out-of-scope list (minimum 5 items), success criteria, kill criteria (minimum 3), and time/effort budget.
  - FAIL condition: Any section is empty or contains placeholders.

- [ ] **M0.4 — Kill criteria quality**: Review each kill criterion. Is it specific and falsifiable? Could you determine whether it has been triggered based on observable evidence?
  - FAIL condition: Any kill criterion is vague (e.g., "if the project isn't going well").

- [ ] **M0.5 — Domain failure modes**: A `03_PROJECT_DOMAIN_RISKS.md` exists for this research intersection, OR one has been generated using the Phase 0 prompts in the Prompt Library.
  - FAIL condition: No domain failure modes document exists.

- [ ] **M0.6 — Document instantiation**: All template documents have been copied to the project directory and initialized.
  - FAIL condition: Any template is missing.

- [ ] **M0.7 — Prior art initial scan**: An initial search has been conducted to check whether this exact intersection has been explored. Summarize findings.
  - FAIL condition: No search conducted.

### Adversarial Review Step

Using the prompt `02_PROMPT_LIBRARY.md` → Phase 0 → "Scope Attack":

- [ ] **A0.1**: Run the Scope Attack prompt with 2 different LLMs. Record both outputs.
- [ ] **A0.2**: For each concern raised, either (a) modify the scope to address it, or (b) record explicit justification for why it's not a real concern, in `DECISION_LOG.md`.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. Is the expected contribution actually novel, or is it a restatement of known results in new terminology?
2. Who would be the harshest critic of this project? What would they say? Can you name a specific researcher?
3. Are you pursuing this intersection because it's genuinely productive, or because it's aesthetically appealing?
4. What is the simplest version of this project that would still be interesting? Are you overcomplicating it?
5. If you had to explain this project's value to a skeptical funding committee in 2 minutes, what would you say? Does that pitch hold up?
6. Are there adjacent intersections (involving slightly different domain combinations) that would be more productive?
7. Is this project actually one project, or is it 2-3 projects awkwardly combined?
8. What would have to be true about the world for this project to be completely uninteresting? How confident are you that condition doesn't hold?
9. Is the time/effort budget realistic given the scope? What would you cut if you had half the time?
10. Are any of your domains included because they're fashionable rather than because they're structurally necessary?
11. Does this project require any empirical data you don't have and can't generate computationally?
12. What is the weakest link in your domain chain? Which domain contributes least?
13. Could a competent researcher in any single one of these domains dismiss this project in one sentence? What would that sentence be?
14. Are you conflating "interesting to me" with "contributes to knowledge"? What's the distinction here?
15. What happens if your first experiment produces a null result? Is there a meaningful project left?

---

## PHASE 1: DOMAIN RECONNAISSANCE — CHECKLIST

### Mandatory Checks

- [ ] **M1.1 — Literature depth per domain**: For each domain, verify: at least 15 foundational/key papers identified, at least 3 active research groups named, at least 2 ongoing debates or open questions identified.
  - FAIL condition: Any domain falls below these minimums.

- [ ] **M1.2 — Citation verification**: For each domain, at least 5 specific claims about papers have been spot-checked against actual paper content (using Semantic Scholar, OpenAlex, or direct retrieval). Results recorded in `CLAIMS_REGISTRY.md`.
  - FAIL condition: Spot-checks not performed, or error rate exceeds 20%.

- [ ] **M1.3 — Terminology crosswalk**: The `STRUCTURAL_MAPPING.md` document contains a terminology crosswalk section listing, for every key concept, what each relevant domain calls it.
  - FAIL condition: Terminology crosswalk is absent or incomplete.

- [ ] **M1.4 — Cross-domain gap analysis**: An explicit analysis of where these domains have been connected before (with citations) and where they have NOT been connected.
  - FAIL condition: Gap analysis is missing or relies solely on LLM assertions without citation support.

- [ ] **M1.5 — Serendipity sweep**: For each domain, 5 recent papers (not selected for relevance) have been retrieved and abstracts reviewed. Any unexpected connections or challenges noted.
  - FAIL condition: Sweep not performed.

- [ ] **M1.6 — Temporal coverage**: Literature review includes foundational older work (not just recent publications). For each domain, at least 2 works from before 2010 are included.
  - FAIL condition: Literature review is skewed toward only recent work.

- [ ] **M1.7 — Non-English and non-prestigious venue check**: An explicit search has been conducted for relevant work in non-English-language publications and in less prominent venues (workshops, regional conferences, technical reports).
  - FAIL condition: Search not conducted. (It's fine if nothing is found, but the search must happen.)

### Adversarial Review Step

- [ ] **A1.1**: Using 2+ models, run the prompt: "What established researchers would consider this intersection trivial, already-explored, or misguided? Name them and explain their likely objections."
- [ ] **A1.2**: Using 2+ models, run the prompt: "What foundational work am I likely missing? What papers would a domain expert consider 'obvious' that a non-expert might overlook?"
- [ ] **A1.3**: Record all adversarial findings. For each, either incorporate the finding or record justification for dismissing it.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. Are you reading primary sources, or relying on other papers' characterizations of primary sources?
2. Is there a textbook in any of these domains that you should read (or at least skim the relevant chapters of) rather than relying on paper summaries?
3. Are the "foundational papers" you've identified actually foundational, or are they just the most-cited recent papers?
4. Have you identified any researchers who have worked at THIS intersection before (even partially)? Have you read their work?
5. Are there relevant dissertations or theses that might not appear in standard paper searches?
6. Is there relevant work in adjacent fields you haven't considered (e.g., systems biology, control theory, game theory, information theory)?
7. Are the "open questions" you've identified actually open, or have they been resolved in work you haven't found?
8. Do the domain experts you've identified actually agree with each other? Are there schools of thought within each domain?
9. Are you over-indexing on one domain's framing at the expense of others?
10. Is there relevant work in industry (not just academia) — technical reports, blog posts, open-source projects?
11. Have you checked preprint servers (arXiv, bioRxiv) for very recent unpublished work?
12. Are you aware of any retracted or significantly criticized papers in your literature review?
13. Do you understand the methodological norms of each field (how they do experiments, what statistics they use, what counts as evidence)?
14. Are there review articles or survey papers that would give you a faster, more reliable domain overview than cherry-picking individual papers?
15. Can you identify the "citation network" structure — which papers cite which, and are there distinct clusters that don't cite each other?

---

## PHASE 2: STRUCTURAL MAPPING & SYNTHESIS — CHECKLIST

### Mandatory Checks

- [ ] **M2.1 — Pairwise mapping completeness**: For every pair of domains in the project, the `STRUCTURAL_MAPPING.md` contains: claimed relationship (isomorphism, analogy, parallel, or false friend), formal requirements for the mapping to hold, falsification conditions, and known limitations.
  - FAIL condition: Any domain pair is missing or incomplete.

- [ ] **M2.2 — Classification rigor**: Each mapping is classified as one of: strong isomorphism, productive analogy, suggestive parallel, or false friend. Classification includes explicit justification.
  - FAIL condition: Any mapping is unclassified or classification lacks justification.

- [ ] **M2.3 — False isomorphism review**: The false isomorphism adversarial review has been run with 2+ models (see adversarial step below). All findings recorded.
  - FAIL condition: Review not run or run with only 1 model.

- [ ] **M2.4 — No "false friend" core pillars**: No mapping classified as "false friend" remains a core pillar of the research. If one was demoted, the decision and its implications are recorded in `DECISION_LOG.md`.
  - FAIL condition: A false friend is still treated as load-bearing.

- [ ] **M2.5 — Directional clarity**: For each mapping, it is clear which direction the analogy runs. Is Domain A's framework being applied to Domain B's phenomena, or vice versa? Or is the claim truly bidirectional?
  - FAIL condition: Direction is ambiguous.

### Adversarial Review Step

- [ ] **A2.1**: Using 2+ models independently (do NOT share one model's output with another), run: `02_PROMPT_LIBRARY.md` → Phase 2 → "False Isomorphism Detection."
- [ ] **A2.2**: For each mapping, compile a "prosecution case" — the strongest argument that this mapping is superficial or misleading. Record.
- [ ] **A2.3**: For each mapping, identify what empirical observation would definitively prove the mapping is false. Record in `STRUCTURAL_MAPPING.md`.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. Are you mapping concepts or mechanisms? (Concepts can look similar while mechanisms differ fundamentally.)
2. For your strongest claimed isomorphism: write out the formal mapping as precisely as you can. Does it actually work at the formal level, or only at the verbal level?
3. Could you explain each mapping to an expert in Domain A without them objecting? What about Domain B?
4. Are you finding connections because they're real, or because you're pattern-matching on shared vocabulary?
5. Is there a mathematical framework (category theory, information theory, dynamical systems theory) that could formalize your mappings? If not, why not?
6. Are the mappings symmetric? (If A maps to B, does B map back to A in the same way?)
7. What is the most important structural DIFFERENCE between the two things you're mapping? Are you giving that difference enough weight?
8. Has anyone else claimed this mapping before? If yes, was it productive? If no, is that because it's novel or because experts saw through it?
9. Are you confusing "both involve X" with "they involve X in the same way"?
10. If you removed your weakest mapping from the project, would the project still work?
11. Are any of your mappings circular? (A is like B because B is like A.)
12. Do the mathematical/formal properties of the systems actually match? (e.g., continuous vs. discrete, deterministic vs. stochastic, finite vs. infinite)
13. Are you mapping between phenomena at the same level of abstraction, or are you comparing a mechanism in one domain with a high-level pattern in another?
14. Would replacing your analogy with a literal statement make it obviously false?
15. Is there a simpler explanation for why these domains look similar that doesn't require a deep structural connection? (e.g., common mathematical tools, shared intellectual ancestry, humans liking certain patterns)

---

## PHASE 3: HYPOTHESIS FORMULATION — CHECKLIST

### Mandatory Checks

- [ ] **M3.1 — Hypothesis precision**: Each hypothesis is stated precisely enough that two independent researchers would agree on whether a given experimental result confirms or disconfirms it.
  - FAIL condition: Hypothesis is vague or admits multiple interpretations of what would count as confirmation.

- [ ] **M3.2 — Null model specification**: For each hypothesis, a null model is explicitly defined. The null model describes what would happen in the ABSENCE of the mechanism the hypothesis proposes.
  - FAIL condition: No null model, or null model is vaguely defined.

- [ ] **M3.3 — Test specification (TDD)**: For each hypothesis, PASS/FAIL/INCONCLUSIVE criteria are written BEFORE any experiment is designed. Criteria are specific and measurable.
  - FAIL condition: Criteria are absent, vague, or written after experiment design.

- [ ] **M3.4 — Structural mapping dependency**: Each hypothesis explicitly states which structural mapping(s) from `STRUCTURAL_MAPPING.md` it depends on. If that mapping were invalidated, the hypothesis would fall.
  - FAIL condition: Hypothesis doesn't reference its mapping dependencies.

- [ ] **M3.5 — Novelty check**: A search has been conducted to verify the hypothesis has not already been tested and resolved by existing work. Search strategy and results documented.
  - FAIL condition: No novelty search conducted.

- [ ] **M3.6 — Triviality check**: The hypothesis is not trivially true (i.e., true by construction in any reasonable model) and not trivially false (contradicted by well-established results).
  - FAIL condition: Hypothesis fails triviality check.

### Adversarial Review Step

- [ ] **A3.1**: Using 2+ models, run `02_PROMPT_LIBRARY.md` → Phase 3 → "Hypothesis Attack." Each model reviews independently.
- [ ] **A3.2**: Specifically probe: "What is the simplest, most boring explanation for why the predicted result would appear? Is the hypothesis even necessary to explain it?"
- [ ] **A3.3**: Specifically probe: "What existing work would a domain expert cite to say this hypothesis is already resolved?"
- [ ] **A3.4**: Record all findings. Modify hypotheses or record justification for retaining them unchanged.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. If your hypothesis is confirmed, so what? What does it actually tell us that we didn't know?
2. Is your hypothesis actually about the phenomenon, or about your model of the phenomenon? (These are different things.)
3. What would change in any field if your hypothesis is confirmed? Is the answer "nothing"?
4. Are your PASS criteria too lenient? Would a skeptic accept them?
5. Are your FAIL criteria too harsh? Could an informative result still be classified as FAIL?
6. Is there a stronger version of your hypothesis you could test instead?
7. Is there a weaker version that would be more defensible and still interesting?
8. Could your hypothesis be tested with a thought experiment rather than a simulation? If so, is the simulation adding anything?
9. Does your null model actually represent "no effect," or does it smuggle in assumptions that bias toward your expected result?
10. What would a Bayesian prior for this hypothesis look like? Is there strong prior evidence for or against it?
11. Are you testing a prediction or fitting an observation? (If you already know the answer and are designing an experiment to confirm it, that's fitting, not testing.)
12. Does the hypothesis make any predictions you DON'T expect to be true? If not, is it too flexible?
13. What would the hypothesis look like if it were wrong? Can you describe the "wrong" world concretely?
14. Is the hypothesis one claim or secretly several claims bundled together? Can you decompose it?
15. Would a domain expert say your null model is the right null model? Or would they insist on a different baseline?

---

## PHASE 4: EXPERIMENT DESIGN — CHECKLIST

### Mandatory Checks

- [ ] **M4.1 — Design completeness**: The experiment design document specifies: environment structure, agent architecture, communication channels (if any), selection mechanism (if evolutionary), ALL parameters with ranges, baseline conditions, number of replicates, statistical tests, data logging plan, and computational resource estimate.
  - FAIL condition: Any element is missing.

- [ ] **M4.2 — Baselines specified**: At minimum three baselines: (a) null model (no proposed mechanism), (b) random control (random behavior where the mechanism would be), (c) at least one ablation (mechanism partially present). Each baseline has expected results stated in advance.
  - FAIL condition: Fewer than three baselines, or expected baseline results not stated.

- [ ] **M4.3 — "Boring explanation" check completed**: For the expected result, the simplest non-mechanism explanation has been identified and the design explicitly addresses it.
  - FAIL condition: Check not performed or boring explanation not addressed in design.

- [ ] **M4.4 — "Design contains conclusion" check completed**: The fitness function, environment, and agent architecture have been reviewed for whether they make the expected result inevitable regardless of the hypothesis.
  - FAIL condition: Check not performed.

- [ ] **M4.5 — Parameter sensitivity plan**: Specific parameter sweep ranges are defined. The plan states which parameters will be swept and in what increments.
  - FAIL condition: No sweep plan, or only the "interesting" parameters are swept.

- [ ] **M4.6 — Code architecture document**: A high-level architecture document exists describing modules, data flow, and how design choices map to hypothesis components.
  - FAIL condition: No architecture document.

- [ ] **M4.7 — External expert review completed**: At least one human domain expert has reviewed the experiment design. Feedback is recorded in `DECISION_LOG.md`. Design modifications (or justification for not modifying) are recorded.
  - FAIL condition: No external review. This cannot be waived.

- [ ] **M4.8 — Reproducibility provisions**: The design specifies: random seed logging, version control for code, data format and storage plan.
  - FAIL condition: Any reproducibility provision missing.

### Adversarial Review Step

- [ ] **A4.1**: Using 2+ models (each independently), run `02_PROMPT_LIBRARY.md` → Phase 4 → "Experiment Design Attack."
- [ ] **A4.2**: One model is prompted with a domain-expert persona for the most relevant field (e.g., "You are a senior ALife researcher reviewing an experiment design submitted to the Artificial Life journal").
- [ ] **A4.3**: Specifically ask each model: "If you were reviewing this experiment design for a top venue in [field], what would your three biggest concerns be?"
- [ ] **A4.4**: Record all concerns. Address each one or justify dismissal.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. What would happen if you doubled your grid/population size? Halved it? Does the result still hold qualitatively?
2. Is your communication channel design realistic for the analogy you're drawing? Or is it too rich/too poor?
3. Are agents initialized identically or with variation? Does initialization matter? Have you tested this?
4. What is your update rule (synchronous/asynchronous)? Does it matter? Many results in CA/ALife are artifacts of update ordering.
5. Is your fitness function smooth or discontinuous? Does it have local optima? How does this affect evolutionary dynamics?
6. How long do you run the simulation? How do you know it's long enough? Have you checked for convergence?
7. Are you measuring the right thing? Is your metric actually capturing the phenomenon you care about, or a proxy for it?
8. Could your result be an artifact of finite population size? Would it disappear with larger populations?
9. Is there a spatial/topological structure in your simulation? Is it justified, or is it an unexamined default?
10. What happens at the boundaries of your simulation? Are boundary effects contaminating your results?
11. Is the resolution/granularity of your simulation appropriate? Are you discretizing something that should be continuous, or vice versa?
12. Have you considered whether your system has known phase transitions in the parameter space? Are you near one?
13. What is the effective dimensionality of your parameter space? Have you identified which parameters actually matter?
14. Could your expected result be produced by a much simpler model? Have you tried the simplest possible model first?
15. Would your experiment be accepted as methodologically sound if published in [the most relevant journal]? What would the methods reviewers flag?

---

## PHASE 5: IMPLEMENTATION & EXECUTION — CHECKLIST

### Mandatory Checks

- [ ] **M5.1 — Cross-model code review**: The code has been reviewed by a different model (different provider preferred) than the one that wrote it. Review specifically checked: off-by-one errors, random seed handling, update ordering, communication channel implementation, and data logging completeness.
  - FAIL condition: Code reviewed by same model that wrote it, or review didn't cover the specified items.

- [ ] **M5.2 — Small case verification**: The experiment has been run on a trivially small case where dynamics can be verified by hand. Results match expectations. Verification documented.
  - FAIL condition: Small case not run or not verified.

- [ ] **M5.3 — Baselines run**: ALL baseline conditions have been run. Results are consistent with expectations. If unexpected, investigation completed before proceeding.
  - FAIL condition: Baselines not run, or unexpected baseline results not investigated.

- [ ] **M5.4 — Replication count**: Minimum 30 replicates per condition completed (or justified alternative based on power analysis).
  - FAIL condition: Fewer than 30 replicates without justification.

- [ ] **M5.5 — Parameter sweeps complete**: All planned parameter sweeps have been executed.
  - FAIL condition: Sweeps not completed.

- [ ] **M5.6 — Reproducibility check**: At least one striking result has been re-run with different random seeds and qualitative pattern confirmed.
  - FAIL condition: No reproducibility check performed.

- [ ] **M5.7 — Code and data versioned**: All code is version-controlled. All data is saved with metadata (parameters, random seeds, timestamps). Code version and data are linked.
  - FAIL condition: Code or data not versioned.

- [ ] **M5.8 — Run log**: A log exists documenting every experimental run: condition, parameters, random seed, start time, end time, any anomalies.
  - FAIL condition: No run log.

### Adversarial Review Step

- [ ] **A5.1**: A different model reviews the code looking specifically for bugs that would produce the expected result as an artifact. Prompt: "This code is supposed to test [hypothesis]. Review it assuming the result WILL come out as expected. What bugs, shortcuts, or design choices could produce that result as an artifact rather than a genuine finding?"
- [ ] **A5.2**: Review the data logging to verify that ALL information needed for analysis is actually being captured.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. Did you verify that your random number generator is actually producing random numbers? (Some implementations have known issues with certain seed values.)
2. Is there any shared state between replicates that could introduce correlation?
3. Does your simulation handle edge cases (empty populations, zero communication, maximum values)?
4. Have you profiled the code for performance bottlenecks that might have led to shortcuts in implementation?
5. Are there any hardcoded values that should be parameters?
6. Is your data output format unambiguous? Could the analysis code misparse it?
7. Have you checked for numerical overflow/underflow in any calculations?
8. If the simulation uses floating-point arithmetic, are there precision issues that could matter?
9. Is memory management correct? Are there leaks that would affect long-running simulations?
10. Does the code actually implement the design document, or did implementation diverge? Check specifically.
11. Are there race conditions if any part of the simulation is parallelized?
12. Is the output deterministic given the same random seed? (Test this.)
13. Have you stress-tested with extreme parameter values to see if the simulation behaves gracefully?
14. Are there any deprecated library functions being used that might behave differently than expected?
15. Does the code include adequate comments/documentation for someone else (or a future AI agent) to understand it?

---

## PHASE 6: ANALYSIS & INTERPRETATION — CHECKLIST

### Mandatory Checks

- [ ] **M6.1 — PI first interpretation**: Before any LLM was consulted about results, the PI recorded their own initial interpretation. This is in the Phase Report as "PI Initial Interpretation."
  - FAIL condition: No PI interpretation recorded, or it was written after LLM consultation.

- [ ] **M6.2 — Statistical rigor**: Appropriate statistical tests applied. Effect sizes reported (not just p-values). Multiple comparison corrections applied if relevant. Confidence intervals reported.
  - FAIL condition: Statistical analysis missing or incomplete.

- [ ] **M6.3 — Boring explanation test**: For each finding, the most boring explanation has been explicitly stated and evaluated. If the boring explanation is sufficient, the finding is downgraded.
  - FAIL condition: Boring explanation test not performed.

- [ ] **M6.4 — Parameter robustness**: Qualitative conclusions are documented as robust/fragile across parameter sweeps. Fragile conclusions are flagged.
  - FAIL condition: Robustness not evaluated.

- [ ] **M6.5 — Structural mapping update**: `STRUCTURAL_MAPPING.md` has been updated based on results. Mappings that gained or lost support are noted.
  - FAIL condition: Mapping not updated.

- [ ] **M6.6 — Claims Registry update**: Every empirical claim in the interpretation has been added to `CLAIMS_REGISTRY.md` with source evidence and strength rating.
  - FAIL condition: Claims not registered.

- [ ] **M6.7 — Conditional external check**: IF results are surprising OR suspiciously clean, external expert feedback has been sought.
  - FAIL condition: Triggering condition met but no external check conducted.

### Adversarial Review Step

- [ ] **A6.1**: Using 2+ models, run `02_PROMPT_LIBRARY.md` → Phase 6 → "Result Attack."
- [ ] **A6.2**: Each model independently generates the most damaging critique of the results. Do not show one model's critique to another.
- [ ] **A6.3**: One model is prompted: "Generate an alternative interpretation of these results that contradicts the PI's interpretation. Make it as compelling as possible."
- [ ] **A6.4**: Record all critiques. For each, either modify the interpretation or record explicit rebuttal.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. Did you see what you expected to see, or what was actually there? How confident are you that you're not fitting a narrative to noise?
2. What would you do differently if the result were exactly opposite? Would you question the methodology? If so, you should question it now too.
3. Is the effect size large enough to matter, or just large enough to be statistically significant?
4. Are there any data points you're ignoring or treating as outliers? What happens if you include them?
5. Could the result be an artifact of how you're measuring/quantifying the phenomenon?
6. If you showed this data (without your interpretation) to someone in each relevant domain, would they reach the same conclusion?
7. Are you over-interpreting a marginal result because it supports your hypothesis?
8. What is the simplest model that would produce this pattern? Is your explanation simpler than that?
9. Does the result actually test the hypothesis, or does it test something adjacent?
10. Are your visualizations accurate? Would a different visualization of the same data suggest a different story?
11. Have you tried analyzing the data with different methods/metrics? Do they converge?
12. Is there a temporal artifact? (E.g., the effect appears only in early/late timesteps due to transient dynamics.)
13. How would this result look to a reviewer who is explicitly hostile to your interdisciplinary framing?
14. Are you conflating correlation with mechanism? Does the data actually support the causal story you're telling?
15. If you had to bet real money on this result replicating in a completely independent implementation, how much would you bet?

---

## PHASE 7: COMMUNICATION & DOCUMENTATION — CHECKLIST

### Mandatory Checks

- [ ] **M7.1 — Five-way writeup**: For each domain in the project, a 2-page extended abstract has been written targeting that field's venue. Each uses that field's terminology and cites that field's foundational works.
  - FAIL condition: Not all domains covered, or abstracts use generic rather than field-specific language.

- [ ] **M7.2 — Five-way observations**: Differences between the five versions have been analyzed and recorded. Weak points identified.
  - FAIL condition: No comparative analysis.

- [ ] **M7.3 — Full writeup complete**: A synthesis document exists that tells the full story in the PI's own framing.
  - FAIL condition: No synthesis document.

- [ ] **M7.4 — Claims verification**: Every empirical claim in the final writeup appears in `CLAIMS_REGISTRY.md` with a verified source.
  - FAIL condition: Any unregistered claim in the writeup.

- [ ] **M7.5 — Limitations section**: The writeup includes an explicit limitations section that addresses: the use of AI assistants in the research process, the PI's non-expert status in most domains, the computational (not empirical) nature of the experiments, and specific methodological limitations.
  - FAIL condition: Limitations section missing or doesn't address these items.

- [ ] **M7.6 — Reproducibility package**: Code, data, parameters, random seeds, and instructions sufficient for independent replication are packaged and available.
  - FAIL condition: Reproducibility package incomplete.

### Adversarial Review Step

- [ ] **A7.1**: Using 2+ models, run `02_PROMPT_LIBRARY.md` → Phase 7 → "Writeup Attack." Each model reviews the full writeup independently.
- [ ] **A7.2**: One model is prompted as a hostile peer reviewer. Another as a friendly but rigorous reviewer.
- [ ] **A7.3**: Record all criticisms. Address substantive ones in revision.

### Randomized Deep-Dive Pool (Select 5-7 at random)

1. Would a reader from Domain A understand and respect the claims about Domain B? Or would they cringe?
2. Are you overclaiming? State the weakest honest version of your contribution. Is it still interesting?
3. Are you underclaiming? Are you hedging so much that the contribution is obscured?
4. Does the abstract accurately reflect what you actually found (vs. what you hoped to find)?
5. Are your figures/diagrams clear to someone not already immersed in the project?
6. Is the related work section fair to competing approaches? Or does it set up strawmen?
7. Could someone replicate your work from the writeup alone? What information would they be missing?
8. Are you transparent about where AI tools were used in the research process?
9. Would you be comfortable defending every claim in the writeup in a live Q&A? Which claims make you nervous?
10. Is the narrative structure honest, or does it present a "just-so story" that makes the research path look more linear than it was?
11. Are there negative results or failed approaches that should be reported but aren't?
12. Is the writing accessible to researchers in adjacent fields, or does it require expertise in ALL fields to understand?
13. Do your citations actually support the claims they're attached to? Spot-check 5.
14. Is the contribution clear and distinct from "we combined ideas from different fields"? What is the SPECIFIC new insight?
15. If this were published, would you be proud of it in 5 years?

---

## PHASE 8: RETROSPECTIVE — CHECKLIST

### Mandatory Checks

- [ ] **M8.1 — Process evaluation completed**: Written assessment of what the process caught, what slipped through, what to change.
- [ ] **M8.2 — LLM performance evaluation completed**: Assessment of which models helped most, where they misled, which prompts worked.
- [ ] **M8.3 — Scope drift evaluation**: Comparison of actual project trajectory against original `SCOPE_DOCUMENT.md`.
- [ ] **M8.4 — Process documents updated**: Any changes to checklists, prompts, or process design have been made based on findings.
- [ ] **M8.5 — RETROSPECTIVE.md written and saved** in the project directory.

---

## CHECKLIST EXECUTION PROTOCOL

When running any phase checklist:

1. Open the relevant Phase Report template. This is where results are recorded.
2. Execute mandatory checks in order. Each check must have a PASS/FAIL result with brief evidence/justification.
3. For adversarial review steps, use the specified prompts from `02_PROMPT_LIBRARY.md`. Record full outputs.
4. For the randomized pool, use a genuine random selection method (e.g., `import random; random.sample(range(1,16), 7)`). Record which questions were selected and answers to each.
5. Evaluate gate criteria. All mandatory checks must PASS. Adversarial review must be completed. Randomized pool must be completed (individual questions may raise concerns but don't directly gate).
6. Write the completed Phase Report to disk.
7. Update `STATE_FILE.md` with gate result.
8. **If the gate FAILS**: Record which items failed. Determine corrective actions. Record in `DECISION_LOG.md`. Re-execute relevant steps. Re-run the gate.
9. **If a kill criterion is triggered**: Stop. Record the trigger in `DECISION_LOG.md`. Evaluate with the PI whether to kill the project, pivot, or override (with explicit justification).
