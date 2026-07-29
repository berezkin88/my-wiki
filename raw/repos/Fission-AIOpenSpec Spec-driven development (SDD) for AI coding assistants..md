---
title: "Fission-AI/OpenSpec: Spec-driven development (SDD) for AI coding assistants."
source: "https://github.com/Fission-AI/OpenSpec"
author:
published:
created: 2026-07-30
description: "Spec-driven development (SDD) for AI coding assistants. - Fission-AI/OpenSpec"
tags:
  - "clippings"
---
[![OpenSpec logo](https://github.com/Fission-AI/OpenSpec/raw/main/assets/openspec_bg.png)](https://github.com/Fission-AI/OpenSpec)**The most loved spec framework.** Our philosophy:

```
→ fluid not rigid
→ iterative not waterfall
→ easy not complex
→ built for brownfield not just greenfield
→ scalable from personal projects to enterprises
```

> [!tip] Tip
> **New workflow now available!** We've rebuilt OpenSpec with a new artifact-guided workflow.
> 
> Run `/opsx:propose "your idea"` to get started. → [Learn more here](https://github.com/Fission-AI/OpenSpec/blob/main/docs/opsx.md)

Follow [@0xTab on X](https://x.com/0xTab) for updates · Join the [OpenSpec Discord](https://discord.gg/YctCnvvshC) for help and questions.

## See it in action

```
You: /opsx:explore
AI:  What would you like to explore?
You: I want dark mode but I'm not sure how to do it cleanly.
AI:  Let me look at your styling setup...
     Cleanest path here: CSS variables + a small theme context,
     with system-preference detection. No new dependencies. Scope it?
You: Yes, let's do it.

You: /opsx:propose add-dark-mode
AI:  Created openspec/changes/add-dark-mode/
     ✓ proposal.md — why we're doing this, what's changing
     ✓ specs/       — requirements and scenarios
     ✓ design.md    — technical approach
     ✓ tasks.md     — implementation checklist
     Ready for implementation!

You: /opsx:apply
AI:  Implementing tasks...
     ✓ 1.1 Add theme context provider
     ✓ 1.2 Create toggle component
     ✓ 2.1 Add CSS variables
     ✓ 2.2 Wire up localStorage
     All tasks complete!

You: /opsx:archive
AI:  Archived to openspec/changes/archive/2025-01-23-add-dark-mode/
     Specs updated. Ready for the next feature.
```

**What do the specs actually look like?**

Plain Markdown — requirements with concrete scenarios, no special syntax to learn. Here's what goes in the `specs/` folder created above:

```
## ADDED Requirements

### Requirement: Theme selection
The app SHALL let users switch between light and dark themes,
defaulting to the system preference.

#### Scenario: User toggles dark mode
- **WHEN** the user clicks the theme toggle
- **THEN** the app switches to dark mode and persists the choice
```

Your AI writes these; you review the plan before any code is written.

OpenSpec is built with OpenSpec — browse this repo's live [specs](https://github.com/Fission-AI/OpenSpec/blob/main/openspec/specs) and in-flight [changes](https://github.com/Fission-AI/OpenSpec/blob/main/openspec/changes) for real examples at scale.

**OpenSpec Dashboard**

[![OpenSpec dashboard preview](https://github.com/Fission-AI/OpenSpec/raw/main/assets/openspec_dashboard.png)](https://github.com/Fission-AI/OpenSpec/blob/main/assets/openspec_dashboard.png)

## Why teams adopt OpenSpec

Solo, OpenSpec keeps you and your AI honest on a single repo. On a team, the hard part moves: a feature spans the API server, the web app, and a shared library; requirements are owned by one team and consumed by others; planning starts before any code exists.

**[Stores](https://github.com/Fission-AI/OpenSpec/blob/main/docs/stores-beta/user-guide.md)** are the answer — planning in a repo of its own. The same `openspec/` shape you already know (specs and changes), shared by `git push` like anything else. One source of truth your whole team and every coding agent can read, across every repo.

- **Cross-repo features** — one change, one plan, even when the code lands in three repos.
- **Shared requirements** — a platform team owns the specs; product teams reference them read-only, right where their coding agent can read them. No drifting wiki.
- **Plan before code** — capture the plan in the store now; the code repos catch up later.

> Stores are in **beta**. Start with the [Stores User Guide](https://github.com/Fission-AI/OpenSpec/blob/main/docs/stores-beta/user-guide.md).

## Quick Start

**Requires Node.js 20.19.0 or higher.**

Install OpenSpec globally:

```
npm install -g @fission-ai/openspec@latest
```

Then navigate to your project directory and initialize:

```
cd your-project
openspec init
```

> **Want your AI to do it?** Paste the [setup prompt](https://github.com/Fission-AI/OpenSpec/blob/main/docs/installation.md#install-with-your-ai-assistant) into your coding assistant — it installs the CLI, runs `openspec init`, and verifies the result.

Now talk to your AI:

- **Not sure what to build yet?** Start with `/opsx:explore`, a no-stakes thinking partner that reads your code, weighs options, and shapes a plan before anything is written. ([Explore guide](https://github.com/Fission-AI/OpenSpec/blob/main/docs/explore.md))
- **Already know what you want?** Go straight to `/opsx:propose <what-you-want-to-build>`.

Both are in the default profile. If you want the expanded workflow (`/opsx:new`, `/opsx:continue`, `/opsx:ff`, `/opsx:verify`, `/opsx:bulk-archive`, `/opsx:onboard`), select it with `openspec config profile` and apply with `openspec update`.

`/opsx:propose` is the canonical name; your tool may spell it `/opsx-propose` (Cursor, GitHub Copilot), `@opsx-propose` (Amazon Q) or `$openspec-propose` (Codex). `openspec init` prints the right form for the tools you picked — see [How To Invoke](https://github.com/Fission-AI/OpenSpec/blob/main/docs/supported-tools.md#how-to-invoke).

> [!note] Note
> Not sure if your tool is supported? [View the full list](https://github.com/Fission-AI/OpenSpec/blob/main/docs/supported-tools.md) – we support 30+ tools and growing.
> 
> Also works with pnpm, yarn, bun, and nix. [See installation options](https://github.com/Fission-AI/OpenSpec/blob/main/docs/installation.md).

## Docs

**Start here:** the **[Documentation Home](https://github.com/Fission-AI/OpenSpec/blob/main/docs/README.md)** maps everything. New to OpenSpec? Read [Getting Started](https://github.com/Fission-AI/OpenSpec/blob/main/docs/getting-started.md), then [How Commands Work](https://github.com/Fission-AI/OpenSpec/blob/main/docs/how-commands-work.md) (where you actually type `/opsx:propose`).

→ **[Getting Started](https://github.com/Fission-AI/OpenSpec/blob/main/docs/getting-started.md)**: first steps  
→ **[Explore First](https://github.com/Fission-AI/OpenSpec/blob/main/docs/explore.md)**: think it through with `/opsx:explore` before you commit  
→ **[How Commands Work](https://github.com/Fission-AI/OpenSpec/blob/main/docs/how-commands-work.md)**: where slash commands run vs the CLI  
→ **[Core Concepts at a Glance](https://github.com/Fission-AI/OpenSpec/blob/main/docs/overview.md)**: the whole mental model, one page  
→ **[Examples & Recipes](https://github.com/Fission-AI/OpenSpec/blob/main/docs/examples.md)**: real changes, start to finish  
→ **[Workflows](https://github.com/Fission-AI/OpenSpec/blob/main/docs/workflows.md)**: combos and patterns  
→ **[Existing Projects](https://github.com/Fission-AI/OpenSpec/blob/main/docs/existing-projects.md)**: adopt OpenSpec on a brownfield codebase  
→ **[Editing a Change](https://github.com/Fission-AI/OpenSpec/blob/main/docs/editing-changes.md)**: update artifacts, go back, reconcile manual edits  
→ **[Commands](https://github.com/Fission-AI/OpenSpec/blob/main/docs/commands.md)**: slash commands & skills  
→ **[CLI](https://github.com/Fission-AI/OpenSpec/blob/main/docs/cli.md)**: terminal reference  
→ **[Stores](https://github.com/Fission-AI/OpenSpec/blob/main/docs/stores-beta/user-guide.md)**: plan in a separate repo, shared across your team (beta)  
→ **[Supported Tools](https://github.com/Fission-AI/OpenSpec/blob/main/docs/supported-tools.md)**: tool integrations & install paths  
→ **[Concepts](https://github.com/Fission-AI/OpenSpec/blob/main/docs/concepts.md)**: how it all fits  
→ **[Multi-Language](https://github.com/Fission-AI/OpenSpec/blob/main/docs/multi-language.md)**: multi-language support  
→ **[Customization](https://github.com/Fission-AI/OpenSpec/blob/main/docs/customization.md)**: make it yours  
→ **[FAQ](https://github.com/Fission-AI/OpenSpec/blob/main/docs/faq.md)** · **[Troubleshooting](https://github.com/Fission-AI/OpenSpec/blob/main/docs/troubleshooting.md)** · **[Glossary](https://github.com/Fission-AI/OpenSpec/blob/main/docs/glossary.md)**: quick help

## Community schemas

Third-party schema bundles distributed via standalone repositories — these provide opinionated workflows that integrate OpenSpec with other tools, similar to how [github/spec-kit's community extension catalog](https://github.com/github/spec-kit/tree/main/extensions) handles tool integrations.

→ **[Browse the catalog](https://github.com/Fission-AI/OpenSpec/blob/main/docs/customization.md#community-schemas)** in the customization docs.

## Why OpenSpec?

AI coding assistants are powerful but unpredictable when requirements live only in chat history. OpenSpec adds a lightweight spec layer so you agree on what to build before any code is written.

- **Agree before you build** — human and AI align on specs before code gets written
- **Stay organized** — each change gets its own folder with proposal, specs, design, and tasks
- **Work fluidly** — update any artifact anytime, no rigid phase gates
- **Use your tools** — works with 30+ AI assistants via slash commands

### How we compare

**vs. [Spec Kit](https://github.com/github/spec-kit)** (GitHub) — Thorough but heavyweight. Rigid phase gates, lots of Markdown, Python setup. OpenSpec is lighter and lets you iterate freely.

**vs. [Kiro](https://kiro.dev/)** (AWS) — Powerful but you're locked into their IDE and limited to Claude models. OpenSpec works with the tools you already use.

**vs. nothing** — AI coding without specs means vague prompts and unpredictable results. OpenSpec brings predictability without the ceremony.

## Updating OpenSpec

**Upgrade the package**

```
npm install -g @fission-ai/openspec@latest
```

**Refresh agent instructions**

Run this inside each project to regenerate AI guidance and ensure the latest slash commands are active:

```
openspec update
```

## Usage Notes

**Model selection**: OpenSpec works best with high-reasoning models. We recommend Codex 5.5 and Opus 4.7 for both planning and implementation.

**Context hygiene**: OpenSpec benefits from a clean context window. Clear your context before starting implementation and maintain good context hygiene throughout your session.

## Contributing

**Small fixes** — Bug fixes, typo corrections, and minor improvements can be submitted directly as PRs.

**Larger changes** — For new features, significant refactors, or architectural changes, please submit an OpenSpec change proposal first so we can align on intent and goals before implementation begins.

When writing proposals, keep the OpenSpec philosophy in mind: we serve a wide variety of users across different coding agents, models, and use cases. Changes should work well for everyone.

**AI-generated code is welcome** — as long as it's been tested and verified. PRs containing AI-generated code should mention the coding agent and model used (e.g., "Generated with Claude Code using claude-opus-4-5-20251101").

### Development

- Install dependencies: `pnpm install`
- Build: `pnpm run build`
- Test: `pnpm test`
- Develop CLI locally: `pnpm run dev` or `pnpm run dev:cli`
- Conventional commits (one-line): `type(scope): subject`

## Other

**Telemetry**

OpenSpec collects anonymous usage stats.

We collect only command names and version to understand usage patterns. No arguments, paths, content, or PII. Automatically disabled in CI.

**Opt-out:** `export OPENSPEC_TELEMETRY=0` or `export DO_NOT_TRACK=1`