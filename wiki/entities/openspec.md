---
title: "OpenSpec"
type: entity
sources:
  - raw/repos/Fission-AIOpenSpec Spec-driven development (SDD) for AI coding assistants..md
  - raw/articles/OpenCode & OpenSpec_ SDD in practice.md
related:
  - "[[spec-driven-development]]"
created: 2026-07-30
updated: 2026-07-30
confidence: high
---

A lightweight, framework-agnostic SDD library by Fission AI. Philosophy: fluid not rigid, iterative not waterfall. Works with 30+ AI coding assistants.

## Workflow

- `/opsx:explore` — thinking partner, explores codebase and options
- `/opsx:propose` — creates a change folder (proposal, specs, design, tasks)
- `/opsx:apply` — implements tasks
- `/opsx:archive` — merges delta spec into main spec

## Key Features

- **Delta spec model** — specs with ADDED/MODIFIED/REMOVED sections merge into the main spec
- **Stores** — cross-repo planning via shared spec repos
- **Slash commands** — integrates with OpenCode, Cursor, Copilot, Claude Code, etc.
