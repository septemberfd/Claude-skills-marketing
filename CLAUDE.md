# CLAUDE.md

This repo stores reusable Claude Code skills for marketing and content operations.

## For AI Agents Contributing to This Repo

When adding or updating skills, follow these rules strictly:

### Structure
- Each skill goes in `skills/<skill-name>/skill.md`
- Supporting files go in `skills/<skill-name>/references/`
- Do NOT create files outside of `skills/` (except README.md, CONTRIBUTING.md, CLAUDE.md)

### PR Rules
- Branch from `main`, name it `add-skill/<skill-name>` or `update-skill/<skill-name>`
- One skill per PR
- Always update `README.md` to include the new/updated skill in the index table
- PR title format: `Add skill: <name>` or `Update skill: <name>`

### Skill File Format
Every `skill.md` must have YAML frontmatter with `name`, `description`, and `user_invocable: true`, followed by clear execution steps.

### What NOT to Do
- Do not put files in the repo root — only README.md, CONTRIBUTING.md, and CLAUDE.md belong there
- Do not commit secrets, tokens, or credentials
- Do not create empty placeholder folders
- Do not duplicate skills that already exist — update the existing one instead

Read `CONTRIBUTING.md` for the full guide.
