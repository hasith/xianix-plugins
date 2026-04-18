---
name: analyze-requirement
description: Run the full requirement elaboration on a backlog item (GitHub Issue, Azure DevOps Work Item, or plain text). Acts as a thinking partner — surrounds the item with fit-with-existing-requirements, intent, domain & competitive context, user journey, persona & adoption, and open questions. Usage: /analyze-requirement [issue-number or work-item-id]
argument-hint: [issue-number | work-item-id]
---

Elaborate item $ARGUMENTS as a thinking partner for the team — not as a gatekeeper.

Use the **orchestrator** agent to run the full elaboration. The orchestrator will:

1. Detect the hosting platform from `git remote get-url origin` (or read `PLATFORM` / `REPO_URL` / `ISSUE_NUMBER` env vars in CI)
2. Fetch item context (`gh` CLI for GitHub, `curl` REST API for Azure DevOps, prompt or local file for plain text)
3. Index repo documentation — README, `docs/`, `specs/`, `requirements/`, `adr/`, `rfcs/`, PRDs, feature briefs, user stories — and reason about how this item **fits the existing requirements** (overlaps, dependencies, contradictions, gaps) at the **product level, not the code level**
4. Classify the item (story, task, bug, spike) — used to tune the depth of analysis
5. Run four analysts in parallel (each receives the item content, related items, **and** the documentation summary + Fit note):

   **Phase 1 — Context lenses (parallel):**
   - **intent-analyst** — the "why" behind the ask, success definition, current workaround, decision points
   - **domain-analyst** — domain knowledge, terminology, regulations, comparable products / competitors
   - **journey-mapper** — upstream triggers, downstream consequences, **usability touchpoints, friction risks**
   - **persona-analyst** — affected personas, persona conflicts, **adoption considerations** (onboarding, migration, change management, success signals)

   **Phase 2 — Gap & Risk:**
   - **gap-risk-analyst** — open questions, assumptions to validate, ACs to tighten, dependencies — **framed as prompts for the team, not blockers**

6. Compile into the structured elaboration (see `styles/elaboration-template.md`)
7. Post each lens as a **separate comment** on the issue/work item — the original body is never modified — and apply a lightweight readiness signal label/tag as a triage hint

If an issue/work item number is provided (e.g., `/analyze-requirement 42`), fetch the item details first.

If no argument is given, prompt the user for an item number or paste the requirement text.
