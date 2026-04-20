---
name: greet-user
description: Greet the user and give a one-paragraph summary of the current repository, plus an obvious next step. Use when the user says hi, asks "what is this repo?", or runs the /hello command. Usage: /greet-user [name]
argument-hint: [name]
---

Greet the user (use the name "$ARGUMENTS" if provided, otherwise just "there") and orient them in the current repository.

Use the **greeter** agent to do the work. The greeter will:

1. Detect the project type from top-level files (`README.md`, `package.json`, `pyproject.toml`, `.claude-plugin/plugin.json`, etc.)
2. Read the README (if present) just enough to summarize the project in one paragraph
3. Output a short, friendly greeting + a one-paragraph summary + one suggested next step

If no name is provided, greet them as "there". Do not ask follow-up questions.
