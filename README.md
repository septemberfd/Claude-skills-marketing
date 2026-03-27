# Claude Skills - Marketing

A collection of reusable [Claude Code](https://claude.com/claude-code) skills for marketing and content operations.

## Skills

### Website Content Management
| Skill | Description | Usage |
|-------|-------------|-------|
| [website-update](skills/website-update/) | Update content on milvus.io or zilliz.com — copy, images, CTAs, cards, nav, footer — then auto-create a PR | `/website-update` |

### Content Creation
| Skill | Description | Usage |
|-------|-------------|-------|
| [techblog-review](skills/techblog-review/) | Review and rewrite translated tech blog posts for the Zilliz developer blog — extract images, rewrite prose, add SEO/GEO metadata | `/techblog-review` |

## How to Install

Copy the skill folder into your Claude Code skills directory:

```bash
cp -r skills/<skill-name> ~/.claude/skills/<skill-name>
```

Then restart Claude Code. The skill will be available as a slash command.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add new skills.
