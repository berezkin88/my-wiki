---
name: wiki-ingest
description: Ingest new source documents into the wiki — create summaries, update concept/entity pages, and maintain index/log
---

Read all new files in `raw/` that aren't already in `wiki/sources/`. For each new file:

1. Create a summary in `wiki/sources/`
2. Update or create concept and entity pages as needed
3. Update `wiki/index.md` with new entries
4. Append to `wiki/log.md`
   Report what changed.
