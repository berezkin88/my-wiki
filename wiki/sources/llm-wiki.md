---
title: "LLM Wiki — Concept Overview"
type: source-summary
sources:
  - raw/articles/llm-wiki.md
related:
  - "[[llm-wiki-pattern]]"
  - "[[rag-vs-llm-wiki]]"
created: 2026-07-29
updated: 2026-07-29
confidence: high
---

Andrej Karpathy's core idea file describing the LLM Wiki pattern — an LLM-maintained personal knowledge base. Key insight: instead of RAG-style retrieval at query time, the LLM incrementally builds and maintains a persistent wiki of interlinked markdown files. Three-layer architecture: `raw/` (immutable sources), `wiki/` (LLM-generated pages), `schema/CLAUDE.md` (conventions). Three operations: ingest, query, lint. The human curates sources and asks questions; the LLM does all bookkeeping.
