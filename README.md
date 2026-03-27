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

### Partner Operations
| Skill | Description | Usage |
|-------|-------------|-------|
| [aws-smartsheet](skills/aws-smartsheet/) | Generate AWS Partner AI Customer Success Smartsheet form markdown from a Zilliz customer case study URL | `/aws-smartsheet <customer-url>` |

## How to Install

1. Download the skill file from the skill folder (e.g. `skills/aws-smartsheet/aws-smartsheet.md`)

2. Copy it into your Claude Code commands directory:
   ```bash
   mkdir -p ~/.claude/commands
   cp aws-smartsheet.md ~/.claude/commands/
   ```

3. Restart Claude Code. The skill will be available as a slash command:
   ```
   /aws-smartsheet https://zilliz.com/customers/filevine
   ```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add new skills.
