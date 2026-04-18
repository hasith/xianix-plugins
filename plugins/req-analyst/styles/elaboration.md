# Requirement Elaboration Output Style Guide

Formatting and tone conventions for all `req-analyst` plugin output.

---

## Plugin Stance: Thinking Partner, Not Gatekeeper

The plugin's job is to **expand the team's thinking** — not to judge whether an item is "ready." Frame everything as observations and prompts the team can react to in the next refinement, not as work that must be done before development can start.

A lightweight readiness signal (`GROOMED` / `NEEDS CLARIFICATION` / `NEEDS DECOMPOSITION`) is also applied as a label/tag, but it is a **triage hint** — the real value is in the elaboration itself.

---

## Core Lenses

Push every requirement through these lenses:

| Lens | Question |
|---|---|
| **Fit with existing requirements** | How does this fit (or conflict with) what is already specified in the repo? |
| **Intent** | Why does this exist? What problem disappears if solved? |
| **Domain & competitive** | What domain knowledge, regulations, and competitor approaches apply? |
| **User journey** | Where does this sit in the broader workflow? Usability touchpoints? Friction risks? |
| **Personas & adoption** | Who is affected? How will they get from today to actually using this? |
| **Open questions** | What assumptions are worth validating? Which ACs are worth tightening? |

---

## General Principles

- **Thinking partner first** — observations and prompts, never blockers
- Be **specific and grounded** — every observation, gap, or risk must reference the actual issue content or an existing requirement document
- Be **actionable** — every question must be answerable with a yes/no or concrete decision
- Be **proportionate** — a bug fix should not produce a 500-line elaboration
- Be **concise** — each section must be scannable in under 30 seconds; **skip sections with no findings**
- Bring **domain knowledge and competitive context** — enrich, don't just restate
- Avoid filler: "Great requirement!", "This is interesting", "As an AI…"

---

## Severity Levels (Triage Hints)

| Label | When to use |
|---|---|
| `CRITICAL` | Without a decision here, two people would build two different things — worth a focused conversation before pickup |
| `WARNING` | Worth a quick conversation in refinement; developers will guess otherwise |
| `INFO` | Improves quality; safe to defer |

These are hints — the team decides what blocks them.

---

## Readiness Signal

| Signal | Meaning |
|---|---|
| `GROOMED` | Intent clear; no critical open questions; user context and workflow defined |
| `NEEDS CLARIFICATION` | Critical or warning open questions remain; intent ambiguous |
| `NEEDS DECOMPOSITION` | Likely too large — spans multiple domains or too many open dimensions; the elaboration suggests how it might split |

---

## Open-Question Format

```
| # | Question / Assumption | Severity | Suggested prompt for the team |
|---|---|---|---|
| 1 | [What's ambiguous — reference specific issue content] | CRITICAL | [Precise question] — @[person] |
```

- Questions must be answerable — avoid open-ended "tell me more"
- Tag the appropriate person when posting

---

## Section Order

1. Header (issue number, title, type, readiness signal)
2. Summary (with intent decomposition table)
3. **Fit with Existing Requirements** *(skip if repo has no requirement docs)*
4. Intent & User Context
5. User Journey *(if cross-issue context, usability, or friction add insight)*
6. Personas & Adoption *(if multiple user types or adoption is non-trivial)*
7. Domain & Competitive Context
8. Open Questions & Gaps
9. Risks, Dependencies & Assumptions

**Skip sections with no findings** rather than writing "None identified."

---

## Risk Rating

| Level | Meaning |
|---|---|
| Low | Unlikely or minor |
| Medium | Possible and noticeable |
| High | Likely or significant |

---

## Tone

- **Neutral, collaborative** — refinement input, not a review
- Gaps are observations: "Error handling is not specified" not "You forgot error handling"
- Concise — bullet points over paragraphs
- Questions must be precise: "Should the system prevent duplicate entries or allow them?" not "What about duplicates?"
- Frame value/priority as observations for the team, not decisions
