---
name: review-performance
description: Run a focused performance review on the current branch. Identifies bottlenecks, N+1 queries, algorithmic inefficiencies, and resource waste. Usage: /review-performance [branch-name]
argument-hint: [branch-name]
disable-model-invocation: true
---

Run a focused performance review of the current branch changes.

## Steps

1. Gather the diff against the base branch:
   ```bash
   BASE=$(git symbolic-ref refs/remotes/origin/HEAD 2>/dev/null | sed 's|refs/remotes/origin/||' || echo "main")
   git diff origin/${BASE}...HEAD
   git diff --name-only origin/${BASE}...HEAD
   ```

2. Use the **performance-reviewer** agent, passing it the diff and changed file list.

3. Output the performance review findings directly. Do not post to any platform — this is a local-only review.

If a branch name is provided, compare that branch against `main`. Otherwise, review the current branch.
