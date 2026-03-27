# Contributing Guide

## Repository Structure

```
Claude-skills-marketing/
├── README.md              # Skill index — must be updated when adding/removing skills
├── CONTRIBUTING.md        # This file
└── skills/
    └── <skill-name>/     # One folder per skill
        ├── skill.md      # Required — the skill definition
        └── references/   # Optional — supporting docs, examples, templates
```

## How to Add a New Skill

### 1. Create the skill folder

```
skills/<skill-name>/skill.md
```

- Folder name = skill name, use lowercase kebab-case (e.g., `blog-publish`, `social-post`)
- Each skill lives in its own folder under `skills/`
- Do NOT put skill files anywhere else

### 2. Write `skill.md` with frontmatter

Every `skill.md` must start with this frontmatter:

```yaml
---
name: <skill-name>
description: <One-line description of what this skill does>
user_invocable: true
---
```

Then include:
- **What it does** — brief summary
- **When to use** — trigger conditions
- **Execution steps** — numbered steps the agent should follow
- **Common patterns** — examples of typical usage

### 3. Add references (optional)

If the skill needs supporting files (style guides, templates, example configs), put them in:

```
skills/<skill-name>/references/
```

### 4. Update README.md

Add your skill to the table in `README.md` under the appropriate category. If no category fits, create a new one.

```markdown
| [skill-name](skills/skill-name/) | Description | `/skill-name` |
```

### 5. Submit a PR

- Branch from `main`
- Branch name: `add-skill/<skill-name>`
- PR title: `Add skill: <skill-name>`
- PR must include: skill.md + README.md update
- One skill per PR

## Skill Categories

Organize skills under these categories in README.md. Add new categories as needed.

| Category | Examples |
|----------|---------|
| Website Content Management | website-update, blog-publish |
| Content Creation | content-rewrite, social-post |
| SEO & Analytics | seo-audit, traffic-report |
| Design & Media | screenshot-compression, video-to-gif |

## Rules

1. **One folder per skill** — never put multiple skills in the same folder
2. **No loose files** — everything goes inside `skills/<skill-name>/`
3. **Keep skill.md self-contained** — it should work without external dependencies when possible
4. **No secrets or credentials** — never hardcode tokens, passwords, or API keys
5. **Use relative paths for references** — reference files as `references/xxx.md`, not absolute paths
