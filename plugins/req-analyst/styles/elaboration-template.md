# Elaborated Requirement Template

This template defines the structure for the compiled elaboration. The orchestrator agent must follow this format exactly when compiling findings from sub-agents.

The plugin is a **thinking partner**, not a gatekeeper. Frame everything as observations and prompts the team can react to in the next refinement — not as work that must be done before development can start.

**Skip any section with no findings — never write "None identified."**

---

## Elaborated Requirement

**Issue:** #[number] — [title]
**Type:** Story | Task | Bug | Spike
**Readiness signal (hint):** `GROOMED` | `NEEDS CLARIFICATION` | `NEEDS DECOMPOSITION`

---

### Summary

[3–5 sentences: what this is, the underlying intent (problem being solved), how success is defined, and the most useful thing this elaboration surfaced.]

| Dimension | Detail |
|---|---|
| **Stated need** | [What they asked for] |
| **Underlying intent** | [What problem this solves; what disappears if done] |
| **Success definition** | [How they'll judge it; "this is a win" criteria] |
| **Current workaround** | [What exists today; pain being replaced] |

---

### Fit with Existing Requirements

> Reasoning at the **product / requirements level** about how this item fits the context already documented in the repo (PRDs, specs, RFCs, ADRs, feature briefs, user stories). **Not a code-level analysis.**

- **Overlaps:** [Existing documents that already cover part of this — file path + what they cover]
- **Dependencies:** [Things this assumes are already specified elsewhere]
- **Contradictions:** [Where this conflicts with a previously-agreed requirement, ADR, or feature brief]
- **Gaps:** [What this exposes that the existing requirements don't say]

*(Skip entirely if the repo has no requirement documents. If documents exist but the new ask sits cleanly alongside them, just say so in one line.)*

---

### Intent & User Context

- **Who & when:** [Primary user; situational context — calm planning vs high-stress operation]
- **Constraints:** [Time, device, connectivity, regulation — only if relevant]
- **Workflow:** [Before → this step → after; happy path; key edge flows]
- **Decision points:** [Where users think; what can be automated vs must stay human]

---

### User Journey

> Where this requirement fits in the end-to-end user journey, with usability touchpoints and friction risks. Skip if the requirement is too narrow for meaningful journey context.

| # | Stage | User Goal | Touchpoint | Emotion | Issues |
|---|-------|-----------|------------|---------|--------|
| 1 | [Stage] | [Goal] | [Where] | [State] | #[refs] |
| **2** | **[This requirement]** | **[Goal]** | **[Where]** | **[State]** | **#[this]** |
| 3 | [Stage] | [Goal] | [Where] | [State] | #[refs] |

- **Upstream trigger / downstream consequence:** [What flows in / out]
- **Usability touchpoints:** [Accessibility, discoverability, error states, empty states, "what happens when…"]
- **Friction risks:** [Where the user is most likely to get stuck or frustrated]
- **Journey gaps:** [Steps with no corresponding issue or feature]
- **Moments that matter:** [High-stakes, trust-building, or delight opportunities]

---

### Personas & Adoption

> Distinct user types affected, where their goals diverge, and what adoption looks like for each. Skip persona table if a single persona is clearly the only audience; skip adoption table if the requirement is trivial to adopt.

| Persona | Role | Frequency | Primary Goal |
|---------|------|-----------|--------------|
| [Label] | [Who] | [How often] | [Goal] |

- **Conflicts:** [Where personas' needs diverge; suggested resolution]
- **Underserved:** [User types not mentioned but likely affected]

| Persona | Onboarding | Migration from today | Documentation / change-management | Success signal |
|---|---|---|---|---|
| [Label] | [What they need first time] | [Path from current workflow] | [What would smooth the rollout] | [How we'd know they're using it] |

---

### Domain & Competitive Context

> Domain knowledge, terminology, regulations, business rules, and how comparable products solve this — only include what's relevant.

- **Concepts & terminology:** [What terms/data mean to users — semantic, not structural]
- **Regulations / compliance:** [Only if genuinely relevant]
- **Business rules:** [Standard behavior; exceptions ("except when…"); overrides]
- **User expectations:** [Fast enough, trustworthy, simple]
- **Comparable products / competitors:** [How they approach this; patterns; differentiation opportunities; common pitfalls]

*(Skip the competitive section if web search yields nothing relevant.)*

---

### Open Questions & Gaps

> Framed as **prompts for the next refinement**, not as blockers. The team decides what to do with them.

| # | Question / Assumption | Severity | Suggested prompt for the team |
|---|---|---|---|
| 1 | [What's ambiguous or missing] | `CRITICAL` / `WARNING` / `INFO` | [Precise, answerable question] — @[person] |

*(Skip if no genuine gaps were found.)*

---

### Risks, Dependencies & Assumptions

- **Value & priority:** [Primary value driver; possible MVP vs nice-to-have; time sensitivity]
- **Risks:** [Specific to this item — with mitigation idea]
- **Dependencies:** [Upstream / downstream / external]
- **Assumptions to validate:** [Conditions assumed true — worth confirming with the product owner]

*(Skip subsections with no findings.)*
