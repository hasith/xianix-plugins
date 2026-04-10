---
name: review-tests
description: Run a focused test coverage review on the current branch. Identifies missing tests, coverage gaps, and test quality issues. Usage: /review-tests [branch-name]
argument-hint: [branch-name]
disable-model-invocation: true
---

Run a focused test coverage review of the current branch changes.

## Steps

1. Gather the diff against the base branch:
   ```bash
   BASE=$(git symbolic-ref refs/remotes/origin/HEAD 2>/dev/null | sed 's|refs/remotes/origin/||' || echo "main")
   git diff origin/${BASE}...HEAD
   git diff --name-only origin/${BASE}...HEAD
   ```

2. Use the **test-reviewer** agent, passing it the diff and changed file list.

3. Output the test review findings directly. Do not post to any platform — this is a local-only review.

If a branch name is provided, compare that branch against `main`. Otherwise, review the current branch.
