# External Expert Engagement Protocol

## PURPOSE

Defines how to seek, document, and act on feedback from human domain experts outside the PI-LLM loop. This protocol applies at two mandatory points: after experiment design (Phase 4) and conditionally after surprising or suspiciously clean results (Phase 6).

The goal is to get genuine diagnostic feedback — not just a box to check.

---

## WHO COUNTS AS AN EXPERT

An external expert must meet at least ONE of these criteria:

1. **Active researcher** in one of the project's domains, with publications in the last 5 years
2. **PhD holder** whose dissertation is directly relevant to one of the project's domains
3. **Industry practitioner** with 5+ years of hands-on experience in a relevant technical area (e.g., a senior ML engineer for model merging questions, a computational biologist for ALife questions)
4. **Graduate student** (PhD level) actively working on a directly relevant topic — less experienced but often more available and more current on recent work

An external expert must NOT be:

- An AI language model, regardless of persona or prompting
- The PI themselves
- Someone with no verifiable expertise in any of the project's domains
- Someone with a personal or financial stake in the project's success

---

## WHAT TO SHOW THEM

### Phase 4 (Experiment Design) — show:

1. **The experiment design document** — full specification including baselines, parameters, metrics
2. **The hypothesis being tested** — stated precisely, with null model
3. **The structural mapping it depends on** — what cross-field connection you're claiming
4. **Specific questions** — not "what do you think?" but focused questions like:
   - "Is this baseline appropriate for testing X in your field?"
   - "Would the [specific field] community accept this methodology?"
   - "What am I missing about how [specific mechanism] actually works?"
   - "Is there prior work I should know about that tests something similar?"

### Phase 6 (Surprising/Clean Results) — show:

1. **The results** — key findings with statistics and visualizations
2. **Your interpretation** (the PI's initial interpretation, not the COO's)
3. **The boring alternative explanation** — "this could also be explained by..."
4. **Specific questions:**
   - "Does this result seem real or does it look like an artifact to you?"
   - "What would you check first if you saw this in your own lab?"
   - "Is the effect size meaningful by your field's standards?"

### What NOT to show:

- The full research program (keep the scope narrow to get focused feedback)
- Your excitement level (it anchors the expert toward agreement)
- The COO's interpretation (get the expert's independent read first)

---

## ENGAGEMENT CHANNELS (ranked by diagnostic value)

| Channel | Diagnostic Value | Effort | When to Use |
|---|---|---|---|
| **1:1 with a domain researcher** (video, email, coffee) | Highest | High | When you can identify a specific expert whose work is relevant. PI-handled — this is relationship building. |
| **Paid consultation** (Clarity.fm, expert network, freelance academic) | High | Medium | When you need specific expertise and don't have a personal connection. |
| **Targeted forum post** (Alignment Forum, specific subreddit, field-specific community) | Medium-High | Low | When the question is focused and the community is technically sophisticated. Scout-handled via standard pipeline. |
| **Conference/workshop interaction** (poster session, Q&A, hallway conversation) | Medium-High | Medium | When timing aligns. Especially good for getting candid feedback. PI-handled. |
| **Broad community post** (general subreddit, Twitter/X, general mailing list) | Low-Medium | Low | Last resort. Responses are variable quality and hard to calibrate. |

**Anonymous community feedback (forum posts via Scout) can satisfy the requirement ONLY if:**
- At least 2 responses come from users with demonstrable domain knowledge (post history, credentials, technical depth of response)
- The responses address the specific methodological questions asked, not just general opinions
- The COO explicitly assesses whether the forum responses are diagnostically equivalent to expert feedback, and presents this assessment to the PI

**If community responses are shallow, generic, or non-expert, the requirement is NOT satisfied.** Escalate to a higher-value channel.

---

## HOW TO DOCUMENT THE ENGAGEMENT

For each external expert interaction, record:

```markdown
## Expert Engagement Record

- **Date:** [DATE]
- **Phase:** [4 or 6]
- **Expert:** [NAME or "anonymous forum user [username]"]
- **Credentials:** [Why this person qualifies as an expert per criteria above]
- **Channel:** [1:1 / paid consultation / forum / conference]
- **What was shown:** [List of documents/information shared]
- **Questions asked:** [Exact questions]

### Expert's Response
[Full response — verbatim if written, detailed notes if verbal]

### Key Feedback Points
1. [POINT — and whether it's an endorsement, concern, or suggestion]
2. [POINT]
3. [POINT]

### Disagreements with Project's Approach
[Any points where the expert disagrees with the project's framing, methodology, or interpretation. These are the most valuable data points.]

### Action Taken
| Feedback Point | Action | Rationale |
|---|---|---|
| [POINT] | INCORPORATED / ACKNOWLEDGED / DISMISSED | [WHY] |

### Impact on Project
- Design modifications made: [LIST or NONE]
- Kill criteria triggered: [YES / NO]
- Confidence level change: [INCREASED / UNCHANGED / DECREASED]
```

Save engagement records in `research/PHASE_REPORTS/` as part of the relevant Phase Report.

---

## WHEN EXPERT FEEDBACK BLOCKS PROGRESS

If an expert identifies a fundamental flaw:

1. Record it fully.
2. COO assesses: is this fixable? Is this a misunderstanding? Is this a genuine killer?
3. **★ PI CHECKPOINT ★** — present the expert's feedback, the COO's assessment, and options (fix, pivot, kill).
4. If the PI overrides expert concern: record the override with explicit justification in `DECISION_LOG.md`. This is a defensibility risk — the writeup should disclose that an expert flagged this concern and explain why the project proceeded despite it.

If multiple experts raise the same concern: treat this as strong evidence of a real problem. The bar for overriding multiple independent expert objections should be very high.

---

## TIPS FOR GETTING USEFUL FEEDBACK

1. **Ask specific questions, not "what do you think?"** Experts are busy. Focused questions get focused answers.
2. **Show the work, not just the idea.** An experiment design document is more useful to review than a verbal description of your concept.
3. **Make it easy to say "this is wrong."** Frame your request as "I'm looking for problems" not "I'm looking for validation."
4. **Acknowledge your non-expert status honestly.** Most domain experts are generous with genuine newcomers and harsh with people who pretend expertise they don't have.
5. **Follow up.** If an expert gives feedback and you change the design, let them know. This builds the relationship for future consultations.
