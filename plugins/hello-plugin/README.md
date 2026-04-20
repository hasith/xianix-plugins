# hello-plugin (template)

A **minimal Xianix plugin template** you can copy and customize. It does one small thing end-to-end so you can see how every piece of a plugin fits together:

> `/hello [name]` — greets the user and writes a one-paragraph summary of the current repository, plus a suggested next step.

Use this as the starting point for your own plugin — copy the folder, rename it, and replace the command/agent/skill/hook with your own.

---

## What's in here

```
hello-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest — name, version, what to load
├── commands/
│   └── hello.md             # Slash command: /hello [name]
├── agents/
│   └── greeter.md           # Sub-agent that does the actual work
├── skills/
│   └── greet-user/
│       └── SKILL.md         # Skill exposing the same flow to the agent
├── hooks/
│   ├── hooks.json           # Hook registration
│   └── welcome.sh           # SessionStart hook — prints a load hint
└── README.md                # You are here
```

Every folder is **optional** except `.claude-plugin/plugin.json`. Delete the ones you don't need.

---

## How it works

When the user runs `/hello Alice`:

1. The slash command in `commands/hello.md` is invoked with `$ARGUMENTS = "Alice"`.
2. The command delegates to the **greeter** agent (`agents/greeter.md`).
3. The greeter reads `README.md` and the top-level folder list, then writes a short greeting + one-paragraph summary + suggested next step to the chat.
4. Nothing on disk is modified.

The same flow is also available as the **greet-user** skill, so the agent can invoke it without the user typing the slash command.

The **SessionStart** hook in `hooks/welcome.sh` prints a one-line hint when a session starts so the user knows the plugin is loaded.

---

## Try it locally

From the marketplace root:

```bash
claude plugin marketplace add ./
/plugin install hello-plugin@xianix-plugins-official
/hello Alice
```

You should see something like:

```
Hi Alice! This repository is the official Xianix plugins marketplace —
a small Node-free directory of Markdown + JSON plugin definitions, with
two production plugins (pr-reviewer, req-analyst) and this template.

Suggested next step: open `README.md` to see how to add the marketplace.
```

---

## Customizing this template for your own plugin

1. **Rename the folder** — `hello-plugin` → `your-plugin-name` (use kebab-case).
2. **Update `.claude-plugin/plugin.json`** — change `name`, `version`, `description`, `author`, `repository`, `keywords`.
3. **Replace the command** — edit `commands/hello.md` (or rename the file). The frontmatter `name` becomes the slash command (`/hello` → `/your-command`).
4. **Replace the agent** — edit `agents/greeter.md`. Keep `tools:` minimal — only list what the agent actually needs.
5. **Replace the skill** — edit `skills/greet-user/SKILL.md` (or rename the folder). Skills let the main agent invoke your flow without an explicit slash command.
6. **Decide on hooks** — keep `hooks/` if you need lifecycle automation (SessionStart, PreToolUse, PostToolUse, etc.); delete it otherwise. Remember to also remove the `hooks` field from `plugin.json`.
7. **Register in the marketplace** — add an entry for your plugin in `.claude-plugin/marketplace.json` at the repo root.

---

## Conventions used in this marketplace

- **Markdown for human-readable definitions** (commands, agents, skills) with YAML frontmatter for metadata.
- **JSON for machine-readable manifests** (`plugin.json`, `hooks.json`).
- **Bash scripts for hooks**, invoked via `${CLAUDE_PLUGIN_ROOT}` so they resolve correctly regardless of install location.
- **Agents declare `tools:` explicitly** — least privilege.
- **Agents are autonomous** — they don't pause to ask the user mid-flow; they fail loudly if something is wrong.

---

## License

MIT — same as the rest of this marketplace. Replace with your own license when you fork.
