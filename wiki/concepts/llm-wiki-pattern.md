---
title: "LLM Wiki Pattern"
type: concept
sources:
  - raw/articles/llm-wiki.md
  - raw/articles/how-to-build-llm-wiki.md
related:
  - "[[llm-wiki]]"
  - "[[rag-vs-llm-wiki]]"
created: 2026-07-29
updated: 2026-07-29
confidence: high
---

A pattern for building personal knowledge bases using LLMs, popularized by Andrej Karpathy. Instead of RAG-style retrieval at query time, the LLM incrementally builds and maintains a persistent wiki of interlinked markdown files.

## Architecture

Three layers:
- **Raw sources** (`raw/`) — immutable source documents. The LLM reads but never modifies.
- **The wiki** (`wiki/`) — LLM-generated markdown pages with YAML frontmatter, cross-referenced via [[wikilinks]].
- **The schema** (`AGENTS.md` / `CLAUDE.md`) — conventions and workflows that turn an LLM into a disciplined wiki maintainer.

## Operations

- **Ingest** — add a new source; LLM creates summaries, updates concepts/entities, maintains index and log.
- **Query** — ask questions; LLM navigates via index, reads relevant pages, synthesizes answers with citations.
- **Lint** — health check for contradictions, orphan pages, missing concepts, stale claims.

## Key Insight

The wiki is a persistent, compounding artifact. Knowledge is compiled once and kept current, not re-derived on every query. The LLM handles the bookkeeping that causes human-maintained wikis to collapse.
