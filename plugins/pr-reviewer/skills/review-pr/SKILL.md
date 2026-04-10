---
name: review-pr
description: Trigger a comprehensive PR review. Runs code quality, security, test coverage, and performance analysis. Usage: /review-pr [PR number or branch name]
argument-hint: [pr-number or branch-name]
disable-model-invocation: true
---

Perform a comprehensive review of the pull request $ARGUMENTS.

Use the **orchestrator** agent to run a full PR review. The orchestrator will:

1. Index the codebase structure
2. Detect the hosting platform from `git remote get-url origin`
3. Gather PR context using git (diffs, commits, changed files)
4. Launch four specialized sub-agent reviews in parallel:
   - **code-reviewer** — Code quality, readability, naming, duplication, error handling
   - **security-reviewer** — OWASP vulnerabilities, secrets, injection, auth issues
   - **test-reviewer** — Test coverage, edge cases, test quality
   - **performance-reviewer** — N+1 queries, algorithmic complexity, memory issues
5. Compile all findings into a structured report (see `styles/report-template.md`)
6. Post the review to the detected platform automatically

If invoked with `--fix`: apply fixes to CRITICAL and WARNING issues, commit, and push before posting.

If a branch name is provided (e.g., `/review-pr feature/my-feature`), compare that branch against `main`.

If no argument is given, review the **current branch** against `main`.
