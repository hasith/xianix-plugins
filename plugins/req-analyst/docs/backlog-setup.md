# Backlog Setup

The `req-analyst` plugin works with **GitHub Issues**, **Azure DevOps Work Items**, and **plain text input**. This guide explains how to structure your backlog items and how the plugin is triggered.

The plugin is a **thinking partner**, not a gatekeeper. It surrounds the item with the context a senior analyst would bring to refinement — it does not block work.

---

## Item Structure

The agent works with any format, but produces a richer elaboration when the original item includes more context.

### Minimum (title only)

The agent can elaborate from just a title, but will surface many open questions:

```
Title: Add user profile page
Body: (empty)
```

### Recommended (title + description)

Include a brief description of the intent and any known constraints:

```
Title: Add user profile page
Body:
Users should be able to view and edit their profile information
including name, email, and avatar. This is part of the
user management epic.
```

### Ideal (title + description + context)

Include any existing acceptance criteria, references, or constraints:

```
Title: Add user profile page
Body:
Users should be able to view and edit their profile information.

## Context
- Part of epic #15 (User Management)
- Design mockup: [link]
- API endpoint already exists: GET /api/users/:id

## Initial Acceptance Criteria
- User can view their profile
- User can update their name and email
- Avatar upload supports JPG and PNG
```

The plugin also reads the surrounding repository for **PRDs, specs, RFCs, ADRs, feature briefs, and user stories** — anything in `docs/`, `specs/`, `requirements/`, `adr/`, etc. The richer that context is, the stronger the *Fit with Existing Requirements* analysis becomes.

---

## Triggering the Plugin

### Manual

Run the command directly in Claude Code:

```
/requirement-analysis 42
```

### Tag-driven (recommended for teams)

The plugin is designed to be **tag-driven** when run through the Xianix Agent. It runs when the `ai-dlc/issue/analyze` label (GitHub) or tag (Azure DevOps) is present on an item and one of the following happens:

| Scenario | What it covers |
|---|---|
| Tag newly applied | A human (or another rule) adds `ai-dlc/issue/analyze` to an existing issue or work item |
| Item created with the tag already present | The item is opened with the tag included from the start |

The label / tag is the single source of truth for "elaborate this backlog item." There is no assignee-based trigger.

See the README *Rule Examples* section for the full webhook rule blocks.

---

## Readiness Signal Labels (Triage Hint)

The plugin applies one of these labels/tags after the elaboration. They are **hints for triage**, not gates — the team decides what to do next.

| Signal | GitHub label | Azure DevOps tag | Meaning |
|---|---|---|---|
| Looks good for sprint planning | `groomed` | `groomed` | Intent clear, no critical open questions |
| Worth a short conversation first | `needs-clarification` | `needs-clarification` | Open questions posted as prompts |
| Likely too large | `needs-decomposition` | `needs-decomposition` | The elaboration suggests how it might split |

**GitHub:** You may want to create these labels (and `ai-dlc/issue/analyze`) in your repository beforehand. The agent will create them if they don't exist (requires repo admin permissions).

**Azure DevOps:** Tags are created automatically — no setup needed.

---

## Item Types

The agent auto-detects the item type from labels/tags or content and tunes the depth of analysis:

| Type | GitHub detection | Azure DevOps detection | Lenses emphasized |
|---|---|---|---|
| **Story** | Label `story` or `feature` | Work item type `User Story` | Personas & adoption, journey, usability, fit-with-existing |
| **Task** | Label `task` or `chore` | Work item type `Task` | Dependencies, fit-with-existing, scope clarity |
| **Bug** | Label `bug` | Work item type `Bug` | Reproduction context, expected vs actual, edge cases |
| **Spike** | Label `spike` or `research` | Work item type `Task` + tag `spike` | Open questions, success criteria, time-box |

A bug fix should not produce a 500-line elaboration — the orchestrator scales the output to the item.

---

## Workflow

### GitHub

1. Create a GitHub issue with at least a title
2. Either add the `ai-dlc/issue/analyze` label (if rules are configured) or run `/requirement-analysis <issue-number>` manually
3. The agent posts each lens as a separate comment on the issue
4. Product owner / team review:
   - If `groomed` — move to sprint planning
   - If `needs-clarification` — react to the posted prompts in the next refinement, then re-run if useful
   - If `needs-decomposition` — split into smaller issues and elaborate each

### Azure DevOps

1. Create a work item (User Story, Bug, or Task) with at least a title
2. Either add the `ai-dlc/issue/analyze` tag (if rules are configured) or run `/requirement-analysis <work-item-id>` manually
3. The agent posts each lens as a separate comment on the work item
4. Same review flow as above

---

## Platform Support

| Platform | Fetch items | Post results | Find related items |
|---|---|---|---|
| **GitHub** | `gh` CLI (`gh issue view`) | Comments via `gh` CLI | By milestone / labels |
| **Azure DevOps** | REST API (`curl`) | Comments via REST | By iteration path (WIQL) |
| **Generic / plain text** | User-provided | Written to file | Manual |
