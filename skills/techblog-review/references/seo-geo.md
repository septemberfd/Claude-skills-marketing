# SEO & GEO Checklist

## SEO (Search Engine Optimization)

### Metadata
- **Meta title** (`meta_title`): 50-60 chars. Primary keyword within the first 3-4 words. Don't stuff.
- **Meta description** (`desc`): 150-160 chars. Start with a hook or pain point. Include primary + one secondary keyword naturally.
- **Keywords** (`meta_keywords`): Max 5. Pick terms people actually search for. Mix branded (Milvus) with generic (RAG retrieval, hybrid retrieval).
- **URL slug** (`id`): Short, keyword-rich, lowercase, hyphens. Must end with `.md`.

### On-Page
- **H1**: One per article (the title). Should contain the primary keyword.
- **H2/H3**: Include relevant keywords naturally. Question-style headings ("What Is X?") match search intent well.
- **Internal links**: Link key terms to Zilliz/Milvus doc pages. 5-10 per article.
- **Image alt text**: Descriptive, includes relevant terms. Not keyword-stuffed.
- **First 100 words**: Should contain the primary keyword and clearly state what the article covers.

## GEO (Generative Engine Optimization)

GEO optimizes for AI models (ChatGPT, Claude, Gemini) that cite web content in their responses. The goal: make your content **extractable and citable** at the sentence/paragraph level.

### What AI Models Look For

1. **Self-contained definitions** — A paragraph that defines a concept completely, without needing surrounding context. AI models quote these directly.
   - Good: "Corrective Retrieval-Augmented Generation (CRAG) is a method that adds an evaluation and correction step between retrieval and generation in a RAG pipeline. It was introduced in the paper *Corrective Retrieval Augmented Generation* (Yan et al., 2024)."
   - Bad: "CRAG is meant to solve this problem. It changes the usual RAG flow."

2. **Question-style headings** — H2/H3 that match common queries. When someone asks ChatGPT "what is CRAG?", it looks for content under a heading like "What Is CRAG?"

3. **Structured comparisons** — Tables comparing approaches, with specific numbers. AI models love structured data.

4. **Academic citations** — Author names and years for papers/research. Makes content more authoritative.

5. **Specific numbers and benchmarks** — "3-5x higher QPS", "6ms latency", "92% accuracy". Concrete data gets cited over vague claims.

6. **Natural Q&A pairs** — Visible Q&A content at the end of the article. Conversational tone, not formal FAQ-speak. Each answer must be self-contained (makes sense without reading the rest of the article).

### What NOT to Do

- No hidden JSON-LD structured data — all GEO content must be visible
- No labeled "Key takeaways" or "TL;DR" boxes — feels artificial, weave summaries into the intro naturally
- No labeled "FAQ" section header — use a natural lead-in instead
- Don't repeat the same definition in multiple places hoping AI will pick it up — one clear definition is better than three weak ones

### How GEO and SEO Work Together

| Element | SEO Value | GEO Value |
|---------|-----------|-----------|
| Question-style headings | Match search intent, featured snippets | Match AI query patterns |
| Comparison tables | Scannable content, time-on-page | Structured data AI can extract |
| Internal links | PageRank, crawl paths | Authority signals |
| Specific benchmarks | Credibility, click-through | AI prefers concrete data |
| Self-contained definitions | Featured snippet eligibility | Direct citation material |
| Q&A pairs | Long-tail keyword coverage | AI Q&A extraction |
