---
name: hello
description: Greet the user and give a one-paragraph summary of the current repository. Optionally accepts a name. Usage: /hello [name]
argument-hint: [name]
---

Greet the user (use the name "$ARGUMENTS" if provided, otherwise just "there") and give them a quick orientation to the current repository.

## What This Does

This command invokes the **greeter** agent. The greeter will:

1. Read the repository's `README.md` (or top-level docs) if present
2. Glance at the top-level folder structure to understand what kind of project this is
3. Produce a short, friendly greeting followed by a **one-paragraph summary** of the repo (what it is, the main pieces, and an obvious next step the user could take)

The output is written to the chat — nothing is modified on disk.

## How to Use

```
/hello                # Greet the current user
/hello Alice          # Greet Alice
```

## Output Shape

```
Hi <name>! This repository is <one-paragraph summary>.
Suggested next step: <one concrete thing to look at>.
```

---

Starting greeting now...
