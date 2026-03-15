---
verification_status: unverified
verified_by: null
phase: 2
tags: [mapping, synthesis, cross-domain]
---

# Structural Mapping

## PURPOSE

The intellectual spine of the project. Tracks every claimed connection between domains: what maps to what, under what conditions, and what would break it. This is a LIVING DOCUMENT updated at Phase 2 (initial mapping), Phase 4 (design reveals weaknesses), and Phase 6 (results confirm or weaken).

**OWNED BY:** COO. **REVIEWED BY:** Red Team (false isomorphism detection), Liaison (audience framing implications), PI (approval at Phase 2 gate).

**UPDATE RULE:** Update immediately when a mapping is proposed, reclassified, or evidence is found for/against. Reset `verification_status` to `unverified` on any substantive change.

---

## Project Identity

- **Project Name:** [FROM SCOPE]
- **Project ID:** [FROM SCOPE]

---

## Terminology Crosswalk

| Our canonical term | Domain 1 term | Domain 2 term | Domain 3 term | ... | Critical differences |
|---|---|---|---|---|---|
| | | | | | |

---

## Pairwise Domain Mappings

*Complete one section per domain pair.*

### Mapping: [Domain A] ↔ [Domain B]

**Claimed relationship:** [ONE SENTENCE]

**Classification:**
- [ ] Strong isomorphism — formal structural equivalence
- [ ] Productive analogy — not equivalent but generates testable hypotheses
- [ ] Suggestive parallel — motivating but not load-bearing
- [ ] False friend — surface similarity, deep structural difference

**Classification justification:** [WHY]

**Direction:** [A→B / B→A / bidirectional — explain]

**Formal mapping attempt:**

```
Element in Domain A          →    Element in Domain B
[concept/mechanism]          →    [concept/mechanism]
```

*If you cannot formalize this mapping, state that explicitly. It signals the mapping may be weaker than it appears.*

**Validity conditions:** [What must be true for this to hold]

1. [CONDITION]
2. [CONDITION]

**Falsification conditions:** [What observation would prove it false]

1. [OBSERVATION]
2. [OBSERVATION]

**Known limitations:** [Where the mapping explicitly doesn't work]

1. [LIMITATION]
2. [LIMITATION]

**Key structural differences:**

1. [DIFFERENCE AND IMPLICATIONS]
2. [DIFFERENCE AND IMPLICATIONS]

**Dependent hypotheses:** [From HYPOTHESES.md — what falls if this mapping breaks]

**Evidence log:**

| Date | Evidence | Supports/Weakens | Source | Impact | Noted By |
|---|---|---|---|---|---|
| | | | | | |

---

*[REPEAT FOR EVERY DOMAIN PAIR]*

---

## Overall Assessment

- **Strongest mapping:** [WHICH AND WHY]
- **Weakest mapping:** [WHICH AND WHY]
- **Load-bearing mappings:** [WHICH ONES — IF THEY FALL, DOES THE PROJECT WORK?]
- **Internal coherence:** [DO PAIRWISE MAPPINGS FIT TOGETHER?]
