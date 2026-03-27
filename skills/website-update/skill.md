---
name: website-update
description: Update content on milvus.io or zilliz.com websites — change copy, images, CTAs, cards, nav, footer, add/remove sections — then create a PR.
user_invocable: true
---

# Website Update

Quickly update website content (copy, images, CTAs, cards, navigation, footer, pages) on milvus.io or zilliz.com and create a PR.

## Repos & Branches

| Site | Repo | Local Path | PR Target Branch |
|------|------|------------|-----------------|
| Milvus blog & small sections | `milvus-io/community` | `~/Documents/agent-work/community` | `master` |
| milvus.io website | `milvus-io/milvus.io` | `~/Documents/agent-work/milvus.io` | `preview` |
| zilliz.com | `zilliztech/zilliz.com` | `~/Documents/agent-work/zilliz.com` | `dev` |

**IMPORTANT:** All repos are already cloned locally. NEVER re-clone. If a repo directory doesn't exist, ask the user for the correct path.

## Execution Steps

Follow these steps strictly. Prioritize SPEED — use direct grep/glob, parallelize where possible, no unnecessary exploration.

### Step 1: Identify target
From the user's request, determine:
- Which repo to work in
- What page/section to modify
- What content to change (copy, image, URL, etc.)

### Step 2: Prepare repo
```bash
cd <repo-path>
git checkout <target-branch>  # master / preview / dev
git pull origin <target-branch>
```

### Step 3: Gather new content
If the user provides a blog URL or content source:
- For milvus.io blogs: fetch frontmatter via `gh api repos/milvus-io/community/contents/blog/en/<filename> --jq '.content' | base64 -d | head -20`
- For other sources: use WebFetch or ask the user
- Extract: title, description, cover image URL, link URL

### Step 4: Find files to edit
Use **direct grep** with keywords from the current content. Do NOT use Agent/Explore for simple searches.
```
# Example: find where a card title lives
grep -r "Current Card Title" <repo-path>/packages/ or <repo-path>/src/
```
Parallelize multiple greps if searching for different strings.

### Step 5: Make changes
- Edit files directly with the Edit tool
- If new images are needed, download with curl to the appropriate public/images/ directory
- Parallelize independent edits (multiple files, image download + text edits)

### Step 6: Create PR
Do all of these as fast as possible:
```bash
# Create branch from target branch
git checkout -b update/<descriptive-name>

# Stage, commit, push
git add <specific-files>
git commit -m "<descriptive message>

Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>"

git push -u origin update/<descriptive-name>

# Create PR to the correct target branch
gh pr create --base <target-branch> --title "<title>" --body "<body>"
```

**PR target branch rules:**
- `community` repo → base: `master`
- `milvus.io` repo → base: `preview`
- `zilliz.com` repo → base: `dev`

### Step 7: Return result
Return the PR URL to the user. Done.

## Speed Rules
1. NEVER clone repos — they're already local
2. NEVER use Agent/Explore subagents for simple file searches — use grep/glob directly
3. Parallelize: download images + edit text files + read source content simultaneously
4. Skip unnecessary verification steps — trust the grep results
5. Total time target: under 2 minutes for simple content swaps

## Common Patterns

### Replace a featured card / blog card
1. Grep the current title text to find i18n JSON + component file
2. Edit JSON (title, desc) + component (image src, href) in parallel
3. Download new cover image if needed
4. Commit & PR

### Update CTA text/link
1. Grep the current CTA text
2. Edit the i18n file or component directly
3. Commit & PR

### Update navigation / footer
1. Grep nav/footer keywords in config or layout files
2. Edit accordingly
3. Commit & PR

### Add new content section
1. Find the page component
2. Add the new section JSX/content
3. Add i18n strings if needed
4. Commit & PR
