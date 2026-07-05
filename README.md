# cc-skills

Scaffold for a Claude Code skill plugin that auto-updates from GitHub. Holds any number of skills: **one folder = one skill**. Start with one, add more whenever.

## How the auto-update works

Claude Code runs `git pull` on this repo's **default branch (`main`)** at session start when it is installed as a marketplace plugin. Push to `main`, the next session pulls it. There is no release/tag step: GitHub Releases are **not** used and would not auto-apply.

## Layout

```
cc-skills/
├── .claude-plugin/
│   ├── marketplace.json   # marketplace manifest (lists this plugin)
│   └── plugin.json        # plugin manifest
└── skills/
    └── example-skill/     # one folder = one skill
        └── SKILL.md
```

Everything under `skills/` is a skill. One skill is one folder with a `SKILL.md`. Two skills is two folders, and so on. They all ship inside this one plugin and install together.

A skill folder can also hold optional subfolders that load only when needed:

```
skills/your-skill/
├── SKILL.md          # required: frontmatter + instructions
├── scripts/          # optional: runnable code
├── references/       # optional: docs loaded on demand
└── assets/           # optional: templates, images, data
```

### SKILL.md rules

- `name` (required): 1-64 chars, lowercase `a-z 0-9 -`, no leading/trailing/consecutive hyphen, and **must match the folder name**.
- `description` (required): 1-1024 chars. Say what it does AND when to use it, with keywords the user would type.
- Optional: `license`, `compatibility`, `metadata`, `allowed-tools`.
- Keep the body under ~500 lines; move long material into `references/`. The full body loads only when the skill activates; subfolder files load only when referenced.

Full field rules live in the example `SKILL.md`. Spec: https://agentskills.io/specification

## Install

```
/plugin marketplace add hlebtkachenko/cc-skills
/plugin install cc-skills@cc-skills
```

Restart the session so the skills load.

## Add a skill

1. Copy `skills/example-skill/` to a new folder under `skills/`, named with your skill's slug.
2. In its `SKILL.md`, set `name:` to that same slug (it must match the folder) and write `description:` with real trigger words.
3. Replace the body with your instructions. Delete the "Authoring reference" section.
4. Delete `skills/example-skill/` once you have your own.
5. Validate: `skills-ref validate ./skills/your-skill`.
6. Commit and push to `main`.

## Add hooks / commands / agents (optional)

Extend `.claude-plugin/plugin.json` with a `hooks` block, or add `commands/` and `agents/` dirs. See the Claude Code plugin docs.
