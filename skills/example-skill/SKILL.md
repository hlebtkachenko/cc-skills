---
name: example-skill
description: >
  Replace this. State WHAT the skill does and WHEN to use it, with concrete
  keywords the user is likely to say. This is the only text loaded at startup to
  decide relevance, so make it specific. Max 1024 characters.
  Trigger words: example, placeholder, scaffold test.
---

# Example Skill

Placeholder body. Replace everything below with your own instructions. This file
is loaded in full once the skill activates, so keep it focused. Recommended:
under 500 lines. Move long material into `references/`.

## Instructions

1. Step-by-step actions the model should take when this skill triggers.
2. Any conventions, output format, or constraints.
3. Reference bundled files with relative paths one level deep, e.g.
   `references/guide.md` or `scripts/run.py`.

## Examples

Show a concrete input and the expected output. Add common edge cases.

---

# Authoring reference

Delete this whole section once you understand it. It documents the format so you
do not have to leave the file to write a valid skill.

## Frontmatter fields

| Field           | Required | Rule                                                                                         |
| --------------- | -------- | -------------------------------------------------------------------------------------------- |
| `name`          | yes      | 1-64 chars, lowercase `a-z 0-9 -` only, no leading/trailing/consecutive hyphen. MUST equal the folder name. |
| `description`   | yes      | 1-1024 chars. What it does + when to use it + keywords the user would say.                    |
| `license`       | no       | License name or a bundled license file reference.                                            |
| `compatibility` | no       | Max 500 chars. Environment needs (product, packages, network). Most skills omit this.        |
| `metadata`      | no       | Map of string keys to string values (e.g. `author`, `version`).                              |
| `allowed-tools` | no       | Space-separated pre-approved tools, e.g. `Bash(git:*) Read`. Experimental.                    |

## Folder layout (one skill = one folder)

```
your-skill/
├── SKILL.md          # required: frontmatter + instructions
├── scripts/          # optional: runnable code (self-contained, clear errors)
├── references/       # optional: docs loaded on demand (keep files small + focused)
└── assets/           # optional: templates, images, data files
```

## Progressive disclosure

- `name` + `description` (~100 tokens) load at startup for every skill.
- The full `SKILL.md` body loads only when the skill activates. Keep it under
  ~5000 tokens / 500 lines.
- Files in `scripts/`, `references/`, `assets/` load only when referenced. Push
  heavy detail there so it costs no context until needed.

## Validate before shipping

```
skills-ref validate ./skills/your-skill
```

Spec: https://agentskills.io/specification
