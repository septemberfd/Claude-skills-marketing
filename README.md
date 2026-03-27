# Claude Skills - Marketing

面向市场营销和内容运营的 [Claude Code](https://claude.com/claude-code) 可复用 Skill 合集。

## Skills 列表

### 网站内容管理
| Skill | 描述 | 用法 |
|-------|------|------|
| [website-update](skills/website-update/) | 更新 milvus.io 或 zilliz.com 上的内容（文案、图片、CTA、卡片、导航栏、页脚等），并自动创建 PR | `/website-update` |

### 内容创作
| Skill | 描述 | 用法 |
|-------|------|------|
| [techblog-review](skills/techblog-review/) | 审校和改写 Zilliz 开发者博客的翻译技术文章 — 提取图片、改写正文、添加 SEO/GEO 元数据 | `/techblog-review` |

### 合作伙伴运营
| Skill | 描述 | 用法 |
|-------|------|------|
| [aws-smartsheet](skills/aws-smartsheet/) | 根据 Zilliz 客户案例网页链接，自动生成 AWS Partner AI Customer Success Smartsheet 表单的 markdown 文档 | `/aws-smartsheet <客户案例链接>` |

## 安装方法

1. 从对应的 skill 文件夹中下载 skill 文件（例如 `skills/aws-smartsheet/aws-smartsheet.md`）

2. 将文件复制到 Claude Code 的 commands 目录：
   ```bash
   mkdir -p ~/.claude/commands
   cp aws-smartsheet.md ~/.claude/commands/
   ```

3. 重启 Claude Code，即可通过斜杠命令使用：
   ```
   /aws-smartsheet https://zilliz.com/customers/filevine
   ```

## 贡献指南

请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解如何添加新的 skill。
