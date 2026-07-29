# my-wiki

An LLM-maintained personal research wiki following [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f).

**Three layers:**
- `raw/` — immutable source documents (articles, papers, etc.)
- `wiki/` — LLM-generated markdown pages with cross-references
- `AGENTS.md` — schema config that turns an LLM into a disciplined wiki maintainer

**Workflows:** ingest (process new sources), query (ask questions against the wiki), lint (health checks for contradictions, orphans, stale claims).

The LLM does the bookkeeping; I curate the sources and ask the questions.
