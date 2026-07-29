---
title: "Spec-Driven Development (SDD): The Definitive 2026 Guide"
source: "https://thebcms.com/blog/spec-driven-development"
author:
  - "[[Momčilo Popov]]"
published: 2026-05-11
created: 2026-07-30
description: "Spec-driven development (SDD) is a 2026 software methodology where executable specifications, not code, are the source of truth. Learn how it works, the top tools (GitHub Spec Kit, Kiro, Claude Code), and how to use it with AI coding agents."
tags:
  - "clippings"
---
**Spec-driven development (SDD) is a software development methodology in which an executable, version-controlled specification - not the code - is the single source of truth.** The team (or an AI coding agent) first writes a detailed spec describing *what* the system should do, then derives an implementation plan, breaks it into atomic tasks, and only then generates the code. The spec stays alive: when requirements change, you edit the spec and regenerate the relevant code.

SDD emerged in 2025 as a direct response to the failure mode of "vibe coding" with large language models - agents that produce plausible code that drifts from intent, hallucinates APIs, and decays as projects scale. By 2026, every major AI coding tool - GitHub Spec Kit, AWS Kiro, Claude Code, Cursor, OpenSpec, BMAD, Tessl, Google Antigravity - has shipped its own flavor of SDD.

This guide is the definitive reference for spec-driven development in 2026: what it is, why it matters, how it compares to TDD and vibe coding, the EARS notation that makes specs AI-readable, and a head-to-head review of every major SDD tool with concrete workflows for Claude Code, GitHub Copilot, and Cursor.

## TL;DR - Spec-driven development in 60 seconds

- **What it is:** A methodology where the spec is the artifact and the code is the build output, similar to how `.c` files compile to binaries.
- **Why now:** AI coding agents are powerful but context-blind. A precise spec gives them the constraints they need to ship working code without drift.
- **The 4 phases:** Specify → Plan → Tasks → Implement, each with a human checkpoint.
- **The leading tools:** GitHub Spec Kit (open source, model-agnostic), AWS Kiro (agentic IDE), Claude Code skills, Cursor Plan Mode, OpenSpec, BMAD-METHOD, Tessl.
- **The notation:** EARS (Easy Approach to Requirements Syntax) - five patterns that turn fuzzy requirements into testable, AI-parseable statements.
- **The result:** ~3–10× higher first-pass success rate from AI agents on non-trivial tasks, according to early adopter reports from GitHub and AWS.

## What is spec-driven development?

Spec-driven development (SDD) is a methodology in which a written specification is treated as the primary, executable artifact of a software project, and code is a regenerable output produced from that spec by humans, AI agents, or both. The spec captures *intent, behavior, edge cases, and non-functional requirements* in a structured form that both people and language models can read and act on.  
This mirrors the same principle behind [structured content](https://thebcms.com/blog/structured-content-guide): Information becomes more reusable and reliable when it follows a clear model.

In a spec-driven workflow:

1. **The spec is versioned** alongside the code (often in a `specs/` or `.specify/` directory in the same repo).
2. **The spec is the source of truth.** When a bug or feature request comes in, the spec is updated first; the code is regenerated or modified to match.
3. **The spec is structured.** It uses a fixed schema - user stories, acceptance criteria in EARS notation, architectural constraints, a "constitution" of project-wide rules - not free-form prose.
4. **The spec is executable in the sense that an agent can drive it.** A coding agent can read it, generate a plan, break it into tasks, write the code, and verify the result against the original acceptance criteria.

This inverts the traditional flow. In conventional development, requirements are a Word doc that gets thrown over a wall, the code becomes the truth, and the spec rots within a sprint. In SDD, the spec lives in the repo, evolves with the project, and the code can be torn down and rebuilt from it.

### Spec-driven development definition (short version)

Spec-driven development is a software methodology where versioned, structured specifications - not code - are the source of truth, and code is generated or maintained against those specs by humans and AI coding agents.

## Why spec-driven development matters in 2026

The shift to SDD is not a fashion trend. It's a direct response to three failure modes that emerged once LLM-based coding agents went mainstream in 2024–2025:

1. **Intent drift.** A prompt like "add login" is wildly underspecified. The model picks reasonable defaults - and those defaults rarely match what the team actually wanted.
2. **Context decay.** As a codebase grows past the agent's effective context window, it forgets older decisions and silently contradicts them.
3. **Unverifiable output.** Without explicit acceptance criteria, there's no way to know whether the agent's code is "right." Code reviews become endless.

A precise spec fixes all three. It is the missing layer between human intent and machine execution. The phrase that keeps appearing in 2025–2026 GitHub and AWS posts is *"the spec is the prompt."*

### The data

- **GitHub** reports that teams using Spec Kit on internal projects ship features with roughly an order-of-magnitude fewer "regenerate from scratch" cycles than ad-hoc prompting.
- **AWS Kiro** documents real customer cases where 40-hour features were shipped in under 8 hours of human time when authored as specs first.
- **DeepLearning.AI** launched a dedicated "Spec-Driven Development with Coding Agents" short course in late 2025, taught by Sandeep Dinesh - a signal that the methodology has crossed from experimental to mainstream.

## Spec-driven development vs vibe coding

"Vibe coding" - a term popularized by Andrej Karpathy in early 2025 - describes the workflow of prompting an AI agent in natural language and accepting whatever it produces. It's fast for prototypes and miserable at scale.

|  | **Vibe coding** | **Spec-driven development** |
| --- | --- | --- |
| **Source of truth** | The generated code | The versioned spec |
| **Best for** | One-off scripts, prototypes, demos | Production code, multi-month projects, team work |
| **Failure mode** | Silent drift, hallucinated APIs, context loss | Over-specification, slow start, spec-rot if not maintained |
| **Reviewability** | Diff the code (human did not write it) | Diff the spec (human wrote it) |
| **AI agent autonomy** | High but brittle | High and bounded |
| **Onboarding new engineers** | Read the code, good luck | Read the spec, then the code |

Vibe coding is to SDD what "just type it into the terminal" is to shell scripts versus version-controlled deployment automation. They're not enemies - vibe coding is a great way to explore - but production systems need a spec layer.

This is also why teams are comparing [AI coding platforms with traditional page builders](https://thebcms.com/blog/ai-coding-platforms-vs-page-builders) when choosing tools for production-ready workflows.

## Spec-driven development vs TDD vs BDD

SDD is often confused with TDD (test-driven development) and BDD (behavior-driven development). They share DNA but differ in what they treat as the canonical artifact.

|  | **TDD** | **BDD** | **SDD (Spec-driven)** |
| --- | --- | --- | --- |
| **Canonical artifact** | Failing unit test | Gherkin scenario (Given/When/Then) | Versioned spec + EARS criteria |
| **Order of operations** | Test → Code → Refactor | Scenario → Step defs → Code | Spec → Plan → Tasks → Code (often by agent) |
| **Primary executor** | Developer | Developer + QA | Developer + agent |
| **Focus** | Code correctness at the unit level | Behavior and collaboration from the user perspective | Requirements clarity and traceability before coding |

TDD says *"write the test first"*. BDD says *"write the behavior first, in business language"*. SDD says *"write the whole spec first - behavior, architecture, edge cases, constraints - and let an agent produce the code, tests, and docs from it."*

SDD subsumes parts of BDD: EARS-style acceptance criteria are essentially Gherkin's more rigorous cousin. And a good SDD workflow still produces unit and integration tests - but they are generated *from* the spec, not the other way around.

---

![sdd-4-steps.png](https://cdn.thebcms.com/api/v3/instance/670e90c0cedcf9e4d34d1a23/media/6a020fe195fe56d352f6fb8e/bin2/sdd-4-steps.webp?webp=t&sizeT=1920x-1&apiKey=670e90c0cedcf9e4d34d24e7.a2132a1499ac4abf17c3c3183070d09975292fb5fe5c0f15d2d8c9288171554b.670e90c0cedcf9e4d34d1a23)

## How spec-driven development works: the 4 phases

Every major SDD framework - GitHub Spec Kit, Kiro, OpenSpec, BMAD - converges on the same four-phase loop. The names differ; the structure is identical.

### Phase 1 - Specify (the "what" and "why")

You (or the agent, in interview mode) author a spec document that includes:

- **User stories** - *"As a \[role\], I want \[capability\], so that \[outcome\]."*
- **Acceptance criteria in EARS notation** - testable, unambiguous statements (covered below).
- **Functional requirements** - what the system must do.
- **Non-functional requirements** - performance budgets, accessibility targets, security constraints, observability.
- **Out-of-scope notes** - what the system *won't* do, to bound the agent.

This is the slowest phase and the most important. Time spent here is repaid 10× downstream.

### Phase 2 - Plan (the "how")

The agent (or human + agent) translates the spec into a technical plan:

- Architecture choices and rationale.
- Data model and schemas.
- API contracts.
- Library and framework selections, with constraints from a project "constitution" (e.g., *"no new runtime dependencies without an ADR"*).
- Migration strategy if touching existing code.

The output is a `plan.md` (or equivalent) committed alongside the spec.

### Phase 3 - Tasks (the "in what order")

The plan is decomposed into atomic, independently-shippable tasks. Each task has:

- A single objective.
- Inputs (files to read, related specs).
- Outputs (files to create/modify, tests to write).
- An acceptance check.

A good task list looks like a checklist a junior engineer could execute. That's the point: an agent is, effectively, a fast junior engineer.

### Phase 4 - Implement (the "go")

The agent works through tasks. Each task ends with a verification step: did the produced code satisfy the acceptance criteria? If not, the agent iterates - *bounded by the spec*, not free-running.

Critically: humans review at every phase boundary. The spec is reviewed before the plan. The plan is reviewed before tasks. Tasks are reviewed before implementation. This is what makes SDD predictable.

## EARS notation: writing specs AI agents actually follow

EARS - *Easy Approach to Requirements Syntax* - was created by Alistair Mavin and colleagues at Rolls-Royce in 2009. It became the secret weapon of SDD because it produces requirements that are unambiguous enough for an LLM to act on.

EARS defines five patterns:

1. **Ubiquitous** - always true.
	*"The system shall log every authentication attempt."*
2. **Event-driven** - `WHEN [trigger] THE [system] SHALL [response]`.
	*"WHEN a user submits the login form THE system SHALL validate credentials against the auth provider."*
3. **State-driven** - `WHILE [state] THE [system] SHALL [behavior]`.
	*"WHILE a sync is in progress THE system SHALL display a non-dismissable progress indicator."*
4. **Unwanted behavior** - `IF [condition] THEN THE [system] SHALL [response]`.
	*"IF credential validation fails three times in 60 seconds THEN THE system SHALL lock the account for 15 minutes."*
5. **Optional features** - `WHERE [feature is included] THE [system] SHALL [behavior]`.
	*"WHERE multi-factor authentication is enabled THE system SHALL require a TOTP code after password validation."*

Why this matters for AI agents: each pattern collapses to a single, testable claim. There is no ambiguity about scope, trigger, or response. An agent can read an EARS requirement, generate the code, and write a test that verifies it - all without guessing.

The "constitution" file at the heart of GitHub Spec Kit and BMAD is essentially a list of ubiquitous EARS statements about the project itself: *"The system shall use TypeScript strict mode. The system shall reject PRs that lower test coverage. The system shall avoid runtime dependencies on unmaintained packages."*

## The top spec-driven development tools in 2026

The SDD tool landscape exploded between July 2025 (GitHub Spec Kit announcement) and early 2026. Here's the head-to-head.

### 1\. GitHub Spec Kit

The reference implementation, open-sourced by GitHub in September 2025.

- **What it is:** A CLI (`specify`) plus a set of prompts, templates, and slash commands that work with Claude Code, GitHub Copilot, Cursor, Codex CLI, Gemini CLI, opencode, Windsurf, and Qwen Code.
- **Model-agnostic:** Yes - that's the headline feature.
- **Slash commands:** `/constitution`, `/specify`, `/clarify`, `/plan`, `/tasks`, `/analyze`, `/implement`, `/checklist`.
- **Where it shines:** Teams that want a standard SDD workflow across multiple AI coding tools without vendor lock-in.
- **Repo:** `github/spec-kit` on GitHub.

### 2\. AWS Kiro

Amazon's agentic IDE, built from the ground up for SDD.

- **What it is:** A standalone IDE (VS Code fork) where spec, plan, tasks, and code live in one workspace, with deep AWS integration.
- **Killer feature:** "Hooks" - automated guardrails (test, lint, security scan) that run after every agent action.
- **Best for:** Teams already on AWS, especially those building serverless apps.
- **Caveat:** Less portable than Spec Kit; tied to the Kiro app.

### 3\. Claude Code with cc-sdd

Anthropic shipped first-class SDD support through the Claude Code "skills" system in late 2025.

- **What it is:** A set of skills (`/sdd:specify`, `/sdd:plan`, etc.) that turn Claude Code into an SDD workflow without leaving the terminal.
- **Best for:** Solo developers and small teams that already use Claude Code.
- **Pairs with:** GitHub Spec Kit (the Spec Kit prompts work natively with Claude Code).

### 4\. Cursor (Plan Mode + AGENTS.md)

Cursor took a slightly different tack: rather than ship dedicated slash commands, it leans on Plan Mode and the `AGENTS.md` convention.

### It takes a minute to start using BCMS

![Gradient](https://thebcms.com/assets/images/features/gradients/bottom-circles.svg)

- **Plan Mode:** A read-only mode where Cursor explores the codebase and produces a plan before any edits.
- **AGENTS.md:** A project-level constitution that every agent action respects.
- **MCP support:** Spec Kit and OpenSpec both work in Cursor via MCP servers.
- **Best for:** Teams that want SDD with maximum flexibility and an IDE-first workflow.

### 5\. OpenSpec

A lightweight, framework-agnostic SDD library that has gained traction in the indie developer community.

- **What it is:** A CLI plus a spec format (Markdown + YAML frontmatter) that any agent can read.
- **Best for:** Teams that want SDD without committing to a vendor toolchain.

### 6\. BMAD-METHOD

A community methodology that predates GitHub Spec Kit and influenced its design.

- **What is the** **[BMAD method](https://thebcms.com/blog/bmad-method-website-content)****:** A set of conventions and prompt packs for spec-first development.
- **Distinctive:** Heavy emphasis on the project "constitution" and on multi-agent role-play (Architect, PM, QA, Dev) within a single workflow.

### 7\. Tessl

A commercial SDD platform focused on enterprise compliance.

- **What it is:** A spec-driven dev environment with audit trails, regulated-industry templates, and CI integration.
- **Best for:** Fintech, healthtech, and other regulated domains.

### 8\. Google Antigravity

Google's late-2025 entrant - a desktop IDE built around an "agent first" model where every action originates from a spec.

- **Best for:** Teams exploring deeply autonomous agents under spec constraints.

### Choosing a tool: the 30-second rubric

- **Already in Claude Code?** → Spec Kit + cc-sdd skills.
- **In Cursor?** → Plan Mode + AGENTS.md + Spec Kit via MCP.
- **AWS shop?** → Kiro.
- **GitHub Copilot in VS Code?** → Spec Kit (it's literally Microsoft's reference path).
- **Need audit trail / compliance?** → Tessl.
- **No vendor lock-in?** → OpenSpec or Spec Kit.

![choosing-a-sdd-tool-in-30-seconds-ed25cbbdf95b97cf.png](https://cdn.thebcms.com/api/v3/instance/670e90c0cedcf9e4d34d1a23/media/6a02127d95fe56d352f6fb96/bin2/choosing-a-sdd-tool-in-30-seconds-ed25cbbdf95b97cf.webp?webp=t&sizeT=1920x-1&apiKey=670e90c0cedcf9e4d34d24e7.a2132a1499ac4abf17c3c3183070d09975292fb5fe5c0f15d2d8c9288171554b.670e90c0cedcf9e4d34d1a23)

## Spec-driven development with Claude Code (step-by-step)

Here's the canonical workflow with Claude Code and GitHub Spec Kit. This is the path with the lowest friction in early 2026.

### Step 1 - Initialize

```
uvx --from git+https://github.com/github/spec-kit.git specify init my-project --ai claude cd my-project
```

This scaffolds a `.specify/` directory with `memory/constitution.md`, `templates/`, and `scripts/`.

### Step 2 - Write the constitution

In Claude Code:

`/constitution`

Claude interviews you about project-wide rules (language, style, testing, dependencies) and writes them to `.specify/memory/constitution.md`. This becomes the immutable backdrop for every future agent action.

### Step 3 - Specify the feature

Claude produces `specs/001-magic-link-auth/spec.md` with user stories, EARS criteria, and out-of-scope notes. You review and edit in plain Markdown.

### Step 4 - Clarify

`/clarify`

Claude asks you targeted questions about ambiguity it found: *"Should magic links be single-use or reusable until expiry?"*, *"Should we rate-limit by email or IP?"* You answer; the spec is updated.

### Step 5 - Plan

`/plan`

Claude produces `plan.md` with the architecture, data model, and library choices. Review it. Edit it. Reject and re-run if needed - *cheap iterations on the plan beat expensive iterations on the code.*

### Step 6 - Tasks

`/tasks`

Claude breaks the plan into a numbered checklist. Each task is independently shippable.

### Step 7 - Implement

`/implement`

Claude executes each task, runs tests after each, and commits in logical chunks. You review the PR.

The whole loop, for a non-trivial feature, takes 2–6 hours of human time - most of it review and clarification, not typing.

## Spec-driven development with GitHub Copilot

GitHub Copilot's SDD path is essentially identical to the Claude Code path because Spec Kit is the canonical layer for both. The difference is the binding: instead of `--ai claude` you pass `--ai copilot`, and the slash commands are exposed inside VS Code's chat panel.

```
uvx --from git+https://github.com/github/spec-kit.git specify init my-project --ai copilot
```

Then in VS Code:

Spec Kit is, by design, the *least opinionated* SDD layer - which is why Microsoft, Anthropic, and Google have all converged on it as the interoperable standard.

## Spec-driven development in Cursor

Cursor takes a slightly different shape. There are three idiomatic paths:

1. **Plan Mode + AGENTS.md** - write `AGENTS.md` at the repo root (Cursor's name for the constitution), enter Plan Mode to produce a spec and plan, then exit Plan Mode to implement.
2. **Spec Kit via MCP** - install Spec Kit and expose its commands to Cursor via MCP. You get the same `/specify`, `/plan`, `/tasks`, `/implement` flow.
3. **OpenSpec** - point Cursor at an `openspec.yaml` file. Lightweight; great for small repos.

Cursor's edge: the inline diff UX makes reviewing agent-generated PRs against a spec much faster than in terminal-based tools.

## A real spec-driven development example

Let's walk through a compact, end-to-end example: adding a "Save for later" feature to an e-commerce site.

### The spec (excerpt)

### The plan (excerpt)

### The tasks

### The result

An agent executing this list in Claude Code or Cursor produces a single PR with ~8 commits, all green tests, and a diff a reviewer can read in 15 minutes - because the reviewer already saw the spec.

## Common pitfalls (and how to avoid them)

1. **Over-specification.** Don't spec implementation details ("use a Map instead of an Object"). Spec *behavior and constraints*. Let the plan phase handle implementation.
2. **Under-specification.** "It should work well" is not a requirement. EARS or it doesn't count.
3. **Skipping the constitution.** Without project-level rules, every spec re-litigates the same decisions.
4. **Treating the spec as immutable.** Specs evolve. When you change behavior, update the spec first, the code second.
5. **No human checkpoints.** Letting an agent go from prompt to merged PR with no human review is vibe coding wearing a Halloween costume.
6. **Specs in Notion, code in Git.** The spec has to live in the repo, versioned with the code, or it rots.

## Best practices for spec-driven development in 2026

1. **One feature = one spec directory** - `specs/NNN-feature-name/{spec.md, plan.md, tasks.md}`.
2. **Constitution first** - commit `AGENTS.md` (or `.specify/memory/constitution.md`) before writing your first spec.
3. **Use EARS for acceptance criteria** - every time.
4. **Review at phase boundaries** - never skip from spec to code.
5. **Keep specs short** - 1–3 pages. If a spec gets bigger, split it.
6. **Spec the negative space** - "out of scope" is as important as "in scope."
7. **Cite the spec in commits and PRs** - `feat(auth): magic link, refs specs/004-magic-link/spec.md`.
8. **Run a** `**/clarify**` **pass** - let the agent surface ambiguity before it guesses.
9. **Use checklists** - Spec Kit's `/checklist` command produces pre-flight checks (security, accessibility, observability) tailored to your spec.
10. **Treat specs as durable docs** - they outlive the code generated from them; future agents (and humans) will read them as the canonical reference.

## Is spec-driven development the future of software engineering?

The honest answer: **yes for some software, no for everything**.

For production code - anything destined for users, customers, or regulated environments - SDD will be the default within 24 months. The economics are too strong: an extra hour writing a spec saves three days of agent thrash and three weeks of code review.

For exploratory, throwaway, or one-off scripts, vibe coding remains faster and more fun. SDD doesn't replace that; it complements it. The mature engineer in 2027 will vibe-code prototypes and spec-drive everything that ships.

What's clear is that SDD is the bridge that turns AI coding agents from impressive demos into reliable teammates. As one GitHub engineer put it: *"You can't ship the spec we don't have."*

## Spec-driven development FAQ

### What is spec-driven development in AI?

Spec-driven development in AI is the practice of writing a structured, versioned specification before invoking an AI coding agent, so the agent has explicit goals, constraints, and acceptance criteria. It replaces ad-hoc prompting ("vibe coding") with a disciplined Spec → Plan → Tasks → Implement loop driven by tools like GitHub Spec Kit, AWS Kiro, or Claude Code skills.

### What is the difference between SDD and TDD?

TDD (test-driven development) treats a failing unit test as the primary artifact: write a test, write the code to pass it, refactor. SDD treats the spec itself as the primary artifact: tests, code, and docs are all generated from it. SDD is broader (it includes architecture, NFRs, constraints) and is designed to be executable by AI agents, while TDD is a tighter developer-only loop. Most SDD workflows still produce TDD-style tests as an output.

### Is spec-driven development the same as waterfall?

No. Waterfall locks the spec at the start of a multi-month phase and discourages change. SDD treats the spec as a living, version-controlled artifact that is edited continuously and regenerates code as it changes. The spec lives in the same repo as the code, in the same PRs.

### Who created spec-driven development?

There is no single inventor. The modern, AI-centric form of SDD coalesced in 2025 around GitHub's Spec Kit (open-sourced September 2025), AWS Kiro (launched July 2025), the BMAD-METHOD community framework, and earlier writing on intent-based programming. EARS notation - the requirement syntax most SDD frameworks use - was created by Alistair Mavin at Rolls-Royce in 2009. Martin Fowler's articles on "Exploring Gen AI" gave the field its modern vocabulary.

### What is EARS notation?

EARS (Easy Approach to Requirements Syntax) is a set of five sentence patterns - Ubiquitous, Event-driven, State-driven, Unwanted-behavior, and Optional-feature - that turn fuzzy requirements into unambiguous, testable statements. Every major SDD tool uses EARS (or a near-clone) for acceptance criteria because the structure is easy for both humans and large language models to parse and verify against.

### What is the "constitution" in spec-driven development?

The constitution is a project-level rules document that every spec, plan, and agent action must respect. It contains the durable decisions a team has made - language, framework, testing, accessibility, security, dependency policy - written as ubiquitous EARS statements. It's usually stored as `AGENTS.md` at the repo root or `.specify/memory/constitution.md` and committed to version control.

### Can I use spec-driven development on an existing project?

Yes. Start by writing a constitution that codifies the project's existing conventions (a one-hour exercise with an agent in interview mode). Then adopt SDD for new features, leaving existing code untouched. Over time, you can backfill specs for high-value areas of the codebase.

### What is the best tool for spec-driven development?

There is no single "best" - the right tool depends on your stack. GitHub Spec Kit is the most portable and model-agnostic option. AWS Kiro is the most integrated agentic IDE. Claude Code with cc-sdd skills is the lowest-friction terminal workflow. Cursor with Plan Mode and AGENTS.md is the best fit for IDE-first teams. For regulated industries, Tessl offers audit trails out of the box.

### Does spec-driven development replace vibe coding?

No - they're complementary. Use vibe coding for prototypes, throwaway scripts, and exploration. Use SDD for production code, multi-month projects, and anything multiple people will maintain. The pattern most teams converge on is: vibe-code a spike, distill the result into a spec, then spec-drive the production version.

---

## Where to go next

If you've made it this far, the highest-leverage next step is: pick one small feature you'd ship this week, spend 30 minutes writing it as a Spec Kit-style spec with EARS acceptance criteria, then run it through Claude Code or Cursor. The gap between that experience and the equivalent vibe-coded one will be all the argument you need.

For more on the tooling and content side, see our companion guides on [building modern AI workflows with MCP](https://thebcms.com/blog/bcms-mcp-and-chatgpt), [structuring content as data](https://thebcms.com/blog/content-hub-guide), and [optimizing Next.js for performance](https://thebcms.com/blog/optimize-nextjs-guide). And if you're managing specs alongside marketing pages, docs, and product content, [BCMS](https://thebcms.com/) gives your team a single content layer your AI tools can read from and write to.

### It takes a minute to start using BCMS

![Gradient](https://thebcms.com/assets/images/features/gradients/bottom-circles.svg)

## Join our Newsletter

Get all the latest BCMS updates, news and events.

By submitting this form you consent to us emailing you occasionally about our products and services. You can unsubscribe from emails at any time, and we will never pass your email to third parties.

![Gradient](https://thebcms.com/assets/images/features/gradients/bottom-circles.svg)

### Continue reading

There are many actionable insights in this blog post. Learn more:

![Server-Driven UI](https://cdn.thebcms.com/api/v3/instance/670e90c0cedcf9e4d34d1a23/media/670e90c0cedcf9e4d34d1dda/bin2/sdui-thumb.webp?webp=t&sizeT=900x-1&apiKey=670e90c0cedcf9e4d34d24e7.a2132a1499ac4abf17c3c3183070d09975292fb5fe5c0f15d2d8c9288171554b.670e90c0cedcf9e4d34d1a23)

Web Dev

### [Server-Driven UI framework on the Web: Examples, Benefits & Use Cases](https://thebcms.com/blog/server-driven-ui-on-the-web-examples)

29 Oct 2022

![Follow illustration](https://cdn.thebcms.com/api/v3/instance/670e90c0cedcf9e4d34d1a23/media/670e90c0cedcf9e4d34d1d64/bin2/3.webp?webp=t&sizeT=900x-1&apiKey=670e90c0cedcf9e4d34d24e7.a2132a1499ac4abf17c3c3183070d09975292fb5fe5c0f15d2d8c9288171554b.670e90c0cedcf9e4d34d1a23)

Web Dev

### [Why do these 15 devs still choose Gatsby.js over Next.js](https://thebcms.com/blog/15-gatsbyjs-developers-to-follow)

18 Aug 2022

![Webflow is becoming too expensive](https://cdn.thebcms.com/api/v3/instance/670e90c0cedcf9e4d34d1a23/media/670e90c0cedcf9e4d34d1d06/bin2/3dfdbe9c-7da0-4810-bffc-4c2ab3d3d32b-1.webp?webp=t&sizeT=900x-1&apiKey=670e90c0cedcf9e4d34d24e7.a2132a1499ac4abf17c3c3183070d09975292fb5fe5c0f15d2d8c9288171554b.670e90c0cedcf9e4d34d1a23)

Web Dev

### [Is Webflow Too Expensive? Real Pricing](https://thebcms.com/blog/is-webflow-too-expensive)

14 Mar 2022