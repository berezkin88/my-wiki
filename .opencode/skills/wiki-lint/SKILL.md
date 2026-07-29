---
name: wiki-lint
description: Health-check the wiki for contradictions, orphan pages, missing concepts, and stale low-confidence pages
---

Scan the entire `wiki/` directory. Check for:

- Contradictions between pages
- Orphan pages (no incoming [[wikilinks]])
- Missing concepts (referenced but no page exists)
- Low-confidence pages that haven't been updated recently
  Save results to `outputs/lint-[today's date].md`
