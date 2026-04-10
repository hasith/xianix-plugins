---
name: review-code
description: Run a focused code quality review on the current branch. Checks readability, naming, duplication, error handling, and design patterns. Usage: /review-code [branch-name]
argument-hint: [branch-name]
disable-model-invocation: true
---

Run a focused code quality review of the current branch changes.

## Steps

1. Gather the diff against the base branch:
   ```bash
   BASE=$(git symbolic-ref refs/remotes/origin/HEAD 2>/dev/null | sed 's|refs/remotes/origin/||' || echo "main")
   git diff origin/${BASE}...HEAD
   git diff --name-only origin/${BASE}...HEAD
   ```

2. Use the **code-reviewer** agent, passing it the diff and changed file list.

3. Output the code review findings directly. Do not post to any platform — this is a local-only review.

If a branch name is provided, compare that branch against `main`. Otherwise, review the current branch.
