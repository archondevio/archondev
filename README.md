<p align="center">
  <img src="https://archondev.io/images/logo-watermark.png" alt="ArchonDev" width="180" />
</p>

<h1 align="center">ArchonDev</h1>

<p align="center">
  <strong>Govern AI Code Your Way</strong><br>
  CLI for total control. Drop-in for your existing tools.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/archondev"><img src="https://img.shields.io/npm/v/archondev.svg" alt="npm version"></a>
  <a href="https://archondev.io">Website</a> •
  <a href="https://archondev.io/docs">Documentation</a> •
  <a href="https://archondev.io/download">Download</a> •
  <a href="https://archondev.io/changelog">Changelog</a>
</p>

---

## What is ArchonDev?

ArchonDev is an AI-powered development governance system that prevents your AI coding assistant from making architectural mistakes, forgetting context, and introducing regressions.

**The Problem:** AI coding assistants are powerful but unreliable. They hallucinate, ignore your architecture, forget what they learned, and break things they just fixed.

**The Solution:** ArchonDev adds governance — architectural rules your AI must follow, quality gates before every change, and persistent learning across sessions.

---

## Two Ways to Use ArchonDev

### Full CLI — Replace Your Tools

AI terminal that governs itself. Total control with architecture enforcement, dependency tracking, and security sentinels.

```bash
npm install -g archondev
```

Then run:
```bash
archon
```

Content-only requests (stories, outlines, lessons, visuals) use lightweight planning to avoid blocking.

[Full Documentation →](https://archondev.io/docs)

---

## BYOK Key Security

When you use BYOK, your API keys stay on your machine and are never uploaded to ArchonDev servers. The CLI encrypts keys at rest and stores them with owner-only file permissions. BYOK runs locally; cloud execution is Credits-only.

### Lite Package — Enhance Your Tools

Governance files for any IDE or AI tool. Drop into Cursor, Claude Code, Windsurf, or any AI coding assistant.

**Download for your IDE:**

| IDE | Download |
|-----|----------|
| Cursor | [cursor-package.zip](https://github.com/archondevio/archondev/releases/latest/download/cursor-package.zip) (~50KB) |
| Claude Code / Amp | [claude-amp-package.zip](https://github.com/archondevio/archondev/releases/latest/download/claude-amp-package.zip) (~50KB) |
| Google Gemini | [gemini-package.zip](https://github.com/archondevio/archondev/releases/latest/download/gemini-package.zip) (~50KB) |
| Windsurf / Codeium | [windsurf-package.zip](https://github.com/archondevio/archondev/releases/latest/download/windsurf-package.zip) (~50KB) |
| VS Code + Copilot | [vscode-copilot-package.zip](https://github.com/archondevio/archondev/releases/latest/download/vscode-copilot-package.zip) (~50KB) |
| OpenAI Codex | [codex-package.zip](https://github.com/archondevio/archondev/releases/latest/download/codex-package.zip) (~50KB) |
| Generic (any AI) | [generic-package.zip](https://github.com/archondevio/archondev/releases/latest/download/generic-package.zip) (~50KB) |

**What's in the package:**

| File | Purpose |
|------|---------|
| `.archon/active/architecture.md` | Governance constitution — components, invariants, protected paths, accessibility config |
| `.archon/active/tasks.json` | Active task list for multi-item requests |
| `.archon/current_context.md` | Current context handoff file for long sessions |
| `AGENTS.md` | AI instructions — code review, task extraction, accessibility, SEO, GEO, memory management |
| `DEPENDENCIES.md` | Regression prevention — tracks what breaks when you change files |
| `progress.txt` | Learning log — persists knowledge across sessions |
| `.archon/config.yaml` | Configuration file |
| `archondev-scenarios/` | Smart onboarding for new/existing/continuing projects |
| `examples/` | Sample workflows and patterns |
| IDE-specific rules | `.cursorrules`, `CLAUDE.md`, `GEMINI.md`, etc. |

**Usage:**
1. Download the package for your IDE
2. Unzip to your project root
3. Tell your AI: `"read .archon/active/architecture.md"`

---

## VS Code Extension

Real-time violations + **quick-fix suggestions**. Press Ctrl+. (Cmd+.) for lightbulb menu with auto-fixes.

[Download archondev-0.2.0.vsix](https://archondev.io/downloads/archondev-0.2.0.vsix)

---

## Features

### Core Governance
- **Architectural Governance** — Define components, boundaries, and invariants your AI must respect
- **Quality Level / Posture** — Right-sized architecture (prototype/production/enterprise)
- **Dependency Tracking** — Know what breaks before you change it (`DEPENDENCIES.md`)
- **Learning Persistence** — AI remembers patterns across sessions via `progress.txt`
- **Quality Gates** — Every change must pass before commit

### New in v2.19.6
- **Conversational Flow Fixes** — Mixed requests like "analyze then help me do X" now continue smoothly into task handling.
- **Usage Transparency by Tier** — `archon usage` now reports practical model-level spend:
  - Credits: since-last-top-up context, base model cost, platform fee, and credits deducted.
  - BYOK: estimated provider spend by model for Today, Last 24 Hours, Last 7 Days, Last 30 Days, and Year to Date.
- **Usage History Reliability** — Fixed profile/user ID resolution in CLI usage commands to prevent false empty usage results.

### New in v2.19.4
- **Design Approval Gate** — Plan flow requires explicit design approval before plan generation.
- **Plan Structure Enforcement** — Plans include explicit verification and acceptance-check steps.
- **Root-Cause Bug Intake** — Bug reports now capture evidence, reproducibility, and root-cause hypothesis.
- **Two-Stage AI Review** — Spec compliance review runs before code quality review.

### New in v2.19.0
- **Governance Store CLI** — Status, task updates, handoffs, and legacy migration via `archon governance`
- **AGD Migration** — Move legacy governance files into `.archon/active|history|archive`
- **Governance SQLite/FTS** — Search architecture, tasks, handoffs, and decisions
- **Lite Packages Updated** — New AGD layout with task and handoff templates

### New in v2.18.0
- **Automated Model Registry Sync** — Daily pricing verification against provider docs
  - New models: Claude Opus 4.6, GPT-5, GPT-5 Mini
  - Confidence scoring prevents bad parses from corrupting billing
  - CLI: `archon models sync`, `archon models list`

### New in v2.17.0
- **CLI Hardening** — Security and governance fixes
  - Supabase SDK no longer imported directly in CLI (uses core helpers)
  - Git commit hardened against shell injection
  - Rollback scoped to atom-touched files only
  - API key entry masked, plan editing supported

### New in v2.16.0
- **Intent Detection** — Smart routing for codebase analysis vs implementation
  - New `explore` intent routes analysis requests to summary flow
  - Polite prefixes ("Please", "Can you") no longer break pattern matching
  - `runExploreFlow()` shows project summary without triggering planning

### New in v2.15.0
- **Credits Usage Dashboard** — Balance and model usage stats on startup
  - Color-coded balance display, top 3 model usage breakdown

### New in v2.14.0
- **Auth & Payment UX Fixes** — 5 critical fixes (timeout bug, BYOK flow, payment clarity)

### New in v2.12.0
- **Billing Audit & Reconciliation** — Immutable audit log, daily balance reconciliation, discrepancy alerts
  - CLI: `archon credits audit`

### New in v2.11.0
- **Atomic Billing Security** — Complete billing rewrite with server-side tier checks, atomic transactions, idempotency keys, race condition prevention

### New in v2.10.0
- **Multi-Provider Support** — OpenAI and Google AI alongside Anthropic
- **Database-Driven Model Registry** — Pricing stored in Supabase for instant updates

### New in v2.6.0
- **Smart Model Routing** — Automatic cost optimization for AI operations
  - Three model tiers: PLANNING ($$$), REASONING ($$), EXECUTION ($)
  - Operations automatically routed to optimal tier
  - Configure per-tier model preferences via `archon preferences`
  - 80-95% cost savings on routine tasks

### New in v2.5.0
- **Streamlined Onboarding** — Complete rewrite of first-run experience
  - Login required first — Creates user account before any other steps
  - Tier selection upfront — Choose FREE/BYOK/Credits before AI calls
  - Fixed double-init bug that confused new users
  - Clear, sequential output — no more jumbled messages
- **AI-Powered Conversational Interview** — Natural conversation replaces rigid menus
  - AI asks follow-up questions based on your answers
  - Infers project details from natural language
  - Uses Haiku model for cost-efficient onboarding
  - Falls back to simple prompts when no API key available
  - Say "skip" or "just start" anytime to use defaults
- **Update Notifications** — Automatic version checking on startup
  - Background check against npm registry (non-blocking)
  - Shows banner when new version available
  - Displays update command: `npm update -g archondev`

### New in v2.4.0
- **Dependency Graph Scheduler** — Analyze atom dependencies for parallel execution
  - Wave-based scheduling using topological sort
  - CLI: `archon parallel schedule`, `archon parallel run-waves`
- **Eject Command** — Clean removal of ArchonDev from any project
  - CLI: `archon eject --dry-run`
- **Atomic Rollback** — Revert individual atom commits via git
  - CLI: `archon revert <atom-id>`, `archon history`

### New in v2.3.0
- **5-Phase Interview System** — Conversational interview to define your project
  - Phases: Discovery → Features → Technical → Branding → Review
  - CLI: `archon interview`, `archon interview show`, `archon interview validate`
- **Project Constitution** — Immutable specification generated from interview
  - Formal contract between you and AI for what gets built
  - Complexity tier calculation (SIMPLE/MODERATE/COMPLEX/ENTERPRISE)
  - Build hours and cost estimation
  - SHA-256 hash for integrity verification
- **Challenge Mode** — AI pushback on scope creep during review
  - Detects too many features, high complexity, vague requirements
  - Suggests features to defer to post-MVP
  - Scope score (0-100) to identify risk
- **Atom Generator** — Transform Constitution into prd.json
  - CLI: `archon generate`, `archon generate --dry-run`
  - Auto-generates setup, database, auth atoms
  - Splits complex features into backend/frontend atoms

### New in v2.1.0
- **GitHub Integration** — Connect GitHub for cloud execution with automatic PR creation
  - Connect: `archon github connect`
  - Status: `archon github status`
  - Cloud agents clone repos, make changes, and submit PRs automatically
- **Cloud Semantic Indexing** — Semantic search stored in Supabase pgvector
  - Setup: `archon index init --cloud`
  - Index: `archon index update --cloud`
  - Search: `archon index search "query" --cloud`
  - Cost: ~$0.01-0.30/month storage, queries are free
- **Webhook-Triggered Worker** — Cloud worker with instant job pickup and auto-stop for cost savings

### New in v2.0.0
- **Cloud Agents** — Run agents in the cloud, close your laptop, check progress anywhere
  - Execute: `archon execute ATOM-001 --cloud`
  - Watch: `archon execute ATOM-001 --cloud --watch`
  - Status: `archon cloud status`
  - Requires: `archon github connect` first
- **Cross-Device Sessions** — Save session, continue on another machine
  - Save: `archon session save`
  - Resume: `archon session resume [id]`
- **Parallel Agents** — Run multiple agents simultaneously with git worktrees
  - Execute: `archon execute --parallel ATOM-001 ATOM-002`
  - Manage: `archon parallel status`, `archon parallel merge`
- **One-Click Deploy** — Auto-detect platform and deploy
  - Deploy: `archon deploy`
  - Preview: `archon deploy --preview`
- **Semantic Indexing** — AI-powered codebase search (local with Ollama or cloud with pgvector)
  - Local: `archon index init --local`
  - Cloud: `archon index init --cloud`
  - Search: `archon index search "query"`
- **Smart Orchestration** — System suggests optimal execution mode based on project size
  - Configure: `archon preferences execution-set parallel.mode always`

### New in v1.9.0
- **Quality Level / Posture** — Tell AI how rigorous to be
  - `prototype`: Fast iteration, minimal governance, skip complex patterns
  - `production`: Secure defaults, basic monitoring, modular design (default)
  - `enterprise`: Full governance with audit logging, RBAC, SLOs, compliance
  - Applies to architecture, code generation, AND code review
  - Prevents over-engineering for simple projects
- Trigger: Set `qualityLevel.posture` in `.archon/active/architecture.md`

### New in v1.8.0
- **SEO Optimization** — Automated meta tags, Open Graph, Twitter Cards
  - AI scans, identifies gaps, generates missing tags
  - User approves before changes are applied
  - Trigger: `seo check`, `seo fix`, `add open graph`
- **GEO for AI Search** — Optimize for ChatGPT, Perplexity, Claude citations
  - AI generates 3 candidate 7-word brand phrases
  - AI generates 3 candidate 50-word descriptions
  - User selects preferred identity
  - JSON-LD schemas for AI comprehension
  - Trigger: `geo identity`, `geo schema`

### New in v1.7.0
- **Pre-Deploy Accessibility Check** — WCAG 2.2 AA compliance before going live
  - Legal liability warnings (ADA, EAA, Section 508)
  - Auto-fix for common issues (contrast, alt text, focus)
  - WCAG 2.2 AA badge for compliant sites
  - CLI: `archon a11y check`, `archon a11y fix`, `archon a11y badge`

### New in v1.6.x
- **Task Extraction Protocol** — AI confirms all items in multi-item requests before starting
  - Prevents lost requirements (AI often forgets items 3+ in a list)
  - Trigger phrases: `plan these tasks`, `task status`, `what's on my list`
- **Smart Onboarding** — Detects new project, existing project, or continuing session
- **Code Review Mode** — AI reviews code without modifying it

### Tools & Extensions
- **Local Database** — Optional SQLite for tracking atoms and learnings
- **VS Code Extension** — Real-time diagnostics with quick-fix suggestions

---

## CLI Commands

| Command | Description |
|---------|-------------|
| `archon` | Interactive mode |
| `archon interview` | 5-phase project interview |
| `archon generate` | Generate prd.json from Constitution |
| `archon plan <description>` | Create governed work item |
| `archon execute <atom-id>` | Execute with quality gates |
| `archon execute --cloud` | Execute in cloud (creates PR) |
| `archon execute --parallel` | Execute multiple atoms in parallel |
| `archon github connect` | Link GitHub account for cloud execution |
| `archon github status` | Check GitHub connection status |
| `archon cloud status` | List cloud executions |
| `archon session save` | Save session for cross-device |
| `archon session resume` | Resume saved session |
| `archon parallel status` | Show parallel execution status |
| `archon deploy` | One-click deploy (auto-detect platform) |
| `archon index init [--local\|--cloud]` | Initialize semantic index |
| `archon index update [--cloud]` | Index changed files |
| `archon index search <query> [--cloud]` | Semantic codebase search |
| `archon review init` | Initialize code review |
| `archon a11y check` | Run WCAG 2.2 AA audit |
| `archon deps list` | View dependency rules |
| `archon watch` | Live TUI dashboard |
| `archon seo check` | Run SEO meta tag audit |
| `archon geo identity` | Generate brand identity phrases |

[Full CLI Reference →](https://archondev.io/docs#cli-reference)

---

## Pricing

| Tier | Cost | What You Get |
|------|------|--------------|
| **Free** | $0 | Ultra-cheap models (GPT-5-nano, Gemini Flash-Lite) |
| **Credits** | Pay as you go | All models, 10% service fee |
| **BYOK** | $0 | Use your own API keys |

No subscriptions. No commitments.

---

## Links

- **Website:** [archondev.io](https://archondev.io)
- **Documentation:** [archondev.io/docs](https://archondev.io/docs)
- **Changelog:** [archondev.io/changelog](https://archondev.io/changelog)
- **Download Lite Packages:** [archondev.io/download](https://archondev.io/download)

---

## License

MIT © [Jumping Ahead Corp.](https://archondev.io)

---

<p align="center">
  <sub>Built with the Ralph Protocol — fresh context, persistent learning.</sub>
</p>
