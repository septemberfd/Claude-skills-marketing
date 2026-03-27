---
name: techblog-review
description: Review and rewrite translated tech blog posts (especially tutorials) for the Zilliz developer blog. Extracts images, rewrites prose, adds SEO/GEO metadata, and outputs to an article folder for review.
---

# Tech Blog Review

Review and rewrite a translated English tech blog post so it reads naturally, flows logically, and is ready to publish — complete with SEO/GEO optimization, images, and metadata.

## When to Use

Use this skill when the user provides a `.docx` (or `.md`) blog post that has been translated from Chinese to English and needs to be polished for the Zilliz developer blog.

## Two Phases

This skill has two phases. **Phase 1 (Review)** runs when the skill is first invoked. **Phase 2 (Package)** runs later when the user says "打包" / "package" / "pack it up" after they've finished reviewing and editing.

---

## Phase 1: Review and Rewrite

Follow these steps **in order**. The ordering matters — audience analysis must happen first, then image extraction, then metadata, then rewriting.

### Step 0: Audience Analysis (MUST DO FIRST)

**Before touching a single word**, analyze who will actually read this article. This step shapes everything that follows — title, intro, headings, keyword choices, and structure. Do NOT skip this.

Ask yourself:

1. **Who is the target reader?** Not just "developers" — be specific. Is it a backend engineer building RAG? A marketing team doing GEO? An ML engineer evaluating vector databases? A data scientist exploring embeddings? The same topic can serve very different audiences.

2. **What pain points brought them here?** What problem are they trying to solve right now? What frustration would make them search for this topic? The intro must hit this pain immediately.

3. **What would they search for?** Think about actual search queries and AI prompts. A marketer searches "how to rank in AI search" not "Milvus GEO pipeline." A developer searches "fix RAG retrieval errors" not "corrective retrieval augmented generation." Keywords and title must match what the audience actually types.

4. **What questions would they ask ChatGPT/Perplexity about this topic?** These become your Q&A pairs and inform your heading structure.

Write down the answers before proceeding. They directly determine:
- **Title**: must hook the target reader's pain point, using words they'd search for
- **Intro**: must open with their specific problem, not a generic definition
- **Headings**: should match queries the audience would search or ask AI
- **Keywords**: must be terms this audience actually uses
- **Q&A pairs**: must address questions this audience would ask
- **Conclusion**: must speak to their next steps, not generic wrap-up

**Example:** An article about GEO content generation:
- ❌ Audience: "developers" → Title: "How to Build a GEO Pipeline with OpenClaw and Milvus"
- ✅ Audience: "marketing/growth teams losing traffic to AI search" → Title: "GEO Content at Scale: How to Rank in AI Search Without Poisoning Your Brand"

### Step 1: Locate the Source File

The user will provide a path to the `.docx` or `.md` file. **Do not move or copy the source file.** Read it in place from whatever path the user gives.

### Step 2: Create the Article Folder

Create a folder in the current working directory, named after the article slug:

```bash
mkdir -p <article-slug>
```

All output files (rewritten .md, images) go into this folder. This keeps each article self-contained and easy to find.

### Step 3: Extract Images from the Docx

A `.docx` is a zip file. Extract the images and figure out where they go.

```bash
mkdir -p /tmp/docx_extracted
unzip -o "/path/to/source.docx" -d /tmp/docx_extracted
ls /tmp/docx_extracted/word/media/
```

Then parse `/tmp/docx_extracted/word/document.xml` to find each image's position — match each `<w:drawing>` element to the surrounding paragraph text (3 paragraphs before and after). This tells you where to insert each image in the rewrite.

- **View each image** to understand what it depicts (needed for alt text).
- **Rename** from generic (`image1.png`) to descriptive (`crag-four-step-workflow.png`).
- **Copy** renamed images into the article folder.

If there are no images, note it and move on.

### Step 4: Extract Text Content

```bash
textutil -convert txt -stdout "/path/to/source.docx"
```

If `textutil` is unavailable, use `pandoc` or the raw XML.

### Step 5: Write SEO/GEO Metadata (informed by Step 0)

Do this **before** rewriting — it influences heading choices and keyword placement. All choices here must be driven by the audience analysis from Step 0.

- **Meta title** (`meta_title`): 50-60 chars, primary keyword front-loaded. Must use words the target audience would search for.
- **Meta description** (`desc`): 150-160 chars, hook with the audience's pain point, include key terms
- **Meta keywords** (`meta_keywords`): **max 5**, comma-separated. Must be terms the target audience actually searches, not technical jargon they wouldn't use.
- **Slug** (`id`): short, keyword-rich, lowercase, hyphens, **must end with `.md`**
- **Cover** (`cover`): carry over from original if provided

See `references/seo-geo.md` for the full SEO/GEO checklist.

### Step 6: Rewrite — Structure, Strategy, Then Prose

This is NOT just polishing sentences. You are reshaping the article for the target audience (Step 0) and for discoverability (SEO/GEO). Work in this order:

**6a. Restructure for the audience and for AI citability**

Before touching prose, evaluate and fix the article's structure:

- **Title**: must satisfy three conditions simultaneously:
  1. **Accurately reflect the article's content** — don't distort the topic for SEO
  2. **Target the right reader** — the target reader should immediately feel "this is for me"
  3. **Contain keywords the target audience actually searches** — traffic comes from AI search + Google search. If the title doesn't contain searchable terms, no one will find the article. Conceptual or poetic phrases (e.g., "Computation Over Search") belong in the body as insights, NOT in the title.
- **Intro (first 2-3 paragraphs)**: must open with the audience's specific pain, not a generic definition. The reader should feel "this is about my problem" within the first sentence.
- **Headings**: rewrite H2/H3 to match what the audience would search or ask AI. Use question-style where natural. Each heading should work as a standalone query. **Headings must read as complete thoughts** — a colon followed by a noun-phrase pileup is weak. After a colon, use a complete verb phrase or clause.
  - Weak: `Milvus V2: Segment-Oriented Storage with Parquet` (noun pileup)
  - Strong: `Milvus V2: How Segment-Level Parquet Cuts API Calls by 10x` (complete verb phrase)
- **Add structure for GEO citability**: look for opportunities to add comparison tables, summary tables, parameter tables — anywhere prose can be replaced with structured data that AI models extract more easily.
- **Conclusion**: must speak to the target audience's next steps, not generic wrap-up.
- **Never touch code blocks** — carry them over verbatim.

**6b. Apply GEO structural strategies**

Go beyond text quality — actively restructure content for AI discoverability:

- **Self-contained definitions**: ensure core concepts have a clean, quotable definition paragraph (one that AI can cite without surrounding context)
- **Comparison tables**: convert "A does this, B does that" prose into tables wherever possible
- **Parameter/config tables**: for tutorials, present options as tables rather than bullet lists
- **Structured headings**: H2s should map to broad queries ("What Is X?"), H3s to specific sub-queries ("How Does X Handle Y?")
- **Direct answers first**: each section should lead with the answer, then explain. Not build-up → reveal.
- **Academic citations**: include author names and year for papers/research

**6c. Polish the prose**

See `references/writing-style.md` for detailed guidelines:

- Tone should match the target audience (developer-to-developer, or marketer-friendly, etc.)
- **Rewrite, don't patch** — rethink sentence by sentence, don't just fix grammar
- Combine choppy translated sentences into flowing paragraphs
- Cut filler, hedging ("That is why...", "In real projects..."), and redundancy
- Make transitions natural, not mechanical

### Step 7: Place Images with Alt Text

Insert images at their original positions (identified in Step 3).

```markdown
![Descriptive alt text explaining what the image shows](descriptive-filename.png)
```

Alt text should describe the image content for accessibility and SEO — not just repeat the heading.

### Step 8: Add Internal Links

- **At least 20 internal links** per article to zilliz.com or milvus.io pages
- **Keywords must match the target URL correctly** — e.g., "vector database" → what-is-a-vector-database, "collection" → manage-collections docs, "scalar fields" → scalar_index docs. Don't link generic text like "click here" or mismatch terms to URLs.
- **Spread links across the entire article** — not just the CTA or conclusion. Every major section should have relevant links.
- Link papers/research with proper academic citation (author, year)

### Step 9: Add CTA Block

Three CTAs at the end, **above** the Q&A section. Natural tone — not a hard sell.

```markdown
If you're building RAG or agent systems and running into retrieval quality issues, we'd love to help:

- Join the [Milvus Slack community](https://slack.milvus.io/) to ask questions, share your architecture, and learn from other developers working on similar problems.
- [Book a free 20-minute Milvus Office Hours session](https://milvus.io/office-hours) to walk through your use case with the team—whether it's CRAG design, hybrid retrieval, or multi-tenant scaling.
- If you'd rather skip the infrastructure setup and jump straight to building, [Zilliz Cloud](https://cloud.zilliz.com/signup) (managed Milvus) offers a free tier to get started.
```

Adapt the wording to match the article's topic. The Zilliz Cloud line should always feel like a convenience option ("skip the setup"), not a pitch.

### Step 10: Add Q&A Pairs

After the CTA, add a `---` divider followed by 3-4 natural Q&A pairs related to the article's topic. These serve GEO (AI models can cite them) and reader value.

Rules:
- **Conversational tone** — write like a developer would actually ask, not formal FAQ-speak
- **Self-contained answers** — each answer should make sense without reading the rest of the article
- **No labeled "FAQ" heading** — use a natural lead-in like "A few questions that come up often when teams start implementing X:"
- **No hidden JSON-LD** — all GEO content must be visible

### Step 11: Format as YAML Frontmatter and Save

The output must use YAML frontmatter compatible with the [blog publisher tool](https://septemberfd.github.io/blog-publisher/):

```yaml
---
title: Article Title Here
id: article-slug-here.md
meta_title: Article Title Here
meta_keywords: keyword1, keyword2, keyword3
desc: "150-char meta description here."
cover: https://assets.zilliz.com/cover_image.png
---
```

**Critical field names** — the publisher expects exactly these:
- `desc` (not `description`)
- `id` (not `slug`, must end with `.md`)
- `meta_keywords` (not `keywords`)

Save the final markdown as `<article-slug>.md` inside the article folder. Use the slug from the `id` field (without the `.md` extension) as the filename. For example, if `id: milvus-cdc-standby-cluster.md`, save as `milvus-cdc-standby-cluster.md`. Do NOT use generic names like `<article-slug>.md`.

### Phase 1 Checklist

Before telling the user the review is done:

- [ ] Article folder created and named after the slug
- [ ] All images from the original are present in the folder with descriptive filenames and alt text
- [ ] Code blocks are untouched
- [ ] YAML frontmatter has all required fields with correct field names
- [ ] `id` ends with `.md`
- [ ] `meta_keywords` has 5 or fewer terms
- [ ] `desc` is under 160 chars
- [ ] CTA block is present (above Q&A)
- [ ] Q&A pairs are present (below CTA, natural tone)
- [ ] At least 20 internal links to zilliz.com / milvus.io, keywords matched correctly, spread across full article
- [ ] Title contains searchable keywords (not just conceptual phrases), reads as a complete thought
- [ ] H2/H3 headings read as complete thoughts (no noun-phrase pileups after colons)

**After Phase 1, tell the user:**
- The article folder path
- Open the folder so they can review
- Remind them to say "打包" / "package" when ready

**Do NOT create a zip at this stage.**

---

## Phase 2: Package

Triggered when the user says "打包", "package", "pack it up", or similar.

### What to Do

1. **Read the user's edited `<article-slug>.md`** from the article folder — do NOT use your original version. The user may have made changes.
2. **Generate two outputs:**

**Output A: Zip for blog publisher**
```bash
cd <article-folder>
zip -j <article-slug>.zip <article-slug>.md *.png *.jpg *.jpeg 2>/dev/null; true
```
Flat structure, no subdirectories. The user drops this into the blog publisher.

**Output B: Docx for Google Docs / Feishu sync**
```bash
cd <article-folder>
pandoc <article-slug>.md -o <article-slug>.docx
```
If pandoc is not installed, tell the user to install it (`brew install pandoc`) and retry.

3. **Both files go into the article folder.**

### Phase 2 Checklist

- [ ] Read the user's latest `<article-slug>.md` (not the original version)
- [ ] Zip contains the .md + all images (flat)
- [ ] Docx generated successfully
- [ ] Both files are in the article folder
- [ ] Open the article folder for the user

### Final Article Folder Structure

```
<article-slug>/
├── <article-slug>.md          # The rewritten article (user may have edited)
├── image1.png            # Extracted/renamed images (if any)
├── image2.png
├── <article-slug>.zip    # For blog publisher (Phase 2)
└── <article-slug>.docx        # For Google Docs / Feishu (Phase 2)
```
