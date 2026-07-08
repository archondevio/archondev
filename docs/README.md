# ArchonDev Documentation

## Overview

This folder contains internal documentation for ArchonDev development and marketing.

## Current Status (2026-07-08)

- Source/package version is `3.3.0` for the UX/UI Expert Review Lite package release.
- Current npm latest is `archondev@3.1.0` as of 2026-07-08; the v3.3.0 UX/UI Expert Review work is being shipped as Lite packages, website/downloads, GitHub release assets, and source docs, not as an npm publish.
- **UX/UI Expert Review (2026-07-08):** Lite packages now ship `ux-ui-review.md` for opt-in expert usability, interaction, information architecture, desktop-app, and Flutter desktop audits with severity-rated fixes and validation recommendations. Claude Code adds `/ux-review`.
- **Document Ingestion (2026-07-01):** Lite packages now ship a MarkItDown MCP skill for opt-in conversion of PDFs, Office files, web pages, and other sources into Markdown for AI review, RAG prep, and local semantic indexing. The skill keeps setup optional and includes local-trust security guidance plus a CLI fallback for large documents.
- Product direction is now local-first CLI + BYOK AI with no required platform login on the primary path.
- **Two-Audience Marketing Framework (2026-05-24):** CLI and Lite packages now support truth-layer governance, agent clarity audits, atomic claims, AI-washing risk registers, and human memory maps. Lite packages now ship 29 on-demand skill files. Claude Code variant now includes 21 native slash commands (`.claude/commands/`), including `/memory-map`, `/washing-audit`, `/truth-layer`, `/ux-review`, and `/markitdown`.
- **Skills-Based Architecture (2026-04-14):** Lite packages refactored from monolithic 42 KB AGENTS.md to slim 8.6 KB governance core + on-demand skill files with YAML frontmatter. **80% reduction in always-on context.** Skills load only when their trigger condition matches (progressive disclosure).
- **v3.0.1: Local-First CLI vNext** — Runtime features inspired by [gstack](https://github.com/garrytan/gstack) now ship inside a fully local-first CLI contract:
  - **Risk Scoring** — 0-100 risk assessment before atom execution. Scores protected paths, stable components, dependency fan-out. HIGH/CRITICAL triggers confirmation based on approval policy.
  - **Fix-First Code Review** — `archon review` auto-fixes mechanical issues, batches ambiguous decisions, detects scope drift and doc staleness. Auto-detects review mode (engineering/design/scope).
  - **Ship Pipeline** — `archon ship`: merge base → tests → review → risk → version → changelog → PR. Say "ship it" in chat.
  - **Post-Ship Doc Staleness** — After PR creation, scans for docs referencing changed code. Offers to create update tasks.
  - **Headless Browser QA** — `archon qa`: Playwright health checks with diff-aware page testing (Astro, Next.js, Remix).
  - **Session Retrospective** — `archon retro`: duration, atoms completed/failed, gate pass rate, risk averages, file hotspots.
  - **Ship Intent Detection** — Chat directives "ship it", "deploy", "create pr", "go live", "publish", "release" route to ship pipeline.
- **Lite packages enhanced with Context-Aware Intelligence** — AI proactively detects user context and offers relevant capabilities instead of requiring slash commands.
- **Lite capabilities (inspired by gstack evaluation):**
  - **Design Governance Chain** — DESIGN.md as design source of truth, contextual design review on frontend changes, design system generation.
  - **AI Slop Detection** — 10-item blacklist of recognizable AI-generated design anti-patterns, scored A-F.
  - **Fix-First Code Review** — Auto-fixes mechanical issues, only asks about genuinely ambiguous ones.
  - **Self-Regulation Protocol** — Blast radius checks, file count limits, 3-strike rule, change checkpoints.
  - **Systematic Debugging** — Root cause investigation first, 3-strike hypothesis testing, mandatory regression tests.
  - **Completion Status Protocol** — DONE / DONE_WITH_CONCERNS / BLOCKED / NEEDS_CONTEXT reporting.
  - **Ship Readiness Dashboard** — Pre-ship checklist tracking all quality gates across the session.
  - **Project Strategy Questions** — Forcing questions for new projects (demand reality, narrowest wedge, etc.).
  - **Scope Review** — 4 modes (expand/selective/hold/reduce) when scope creep detected mid-feature.
  - **Progress Reflection** — Solo retro at natural milestones (what worked, what didn't, carry forward).
  - **Expert Review Spec** — Generate consultant-ready technical spec (gap analysis, approach review, UX enhancement) at any milestone. Output: `docs/expert-review-[DATE].md` with reviewer response template.
  - **Features Dashboard** — Live HTML page (`.archon/dashboard.html`) tracking which capabilities the user has used, which are available, and what's recommended next. Updated automatically each session. Includes dashboard HTML template.
- **Dark Mode Contrast Fix (2026-04-11):** Updated red text across the website to use high-contrast `dark:text-red-400` (#f87171) in dark mode. Fixed in: index.astro, BeforeAfter.astro, AdversarialProcess.astro, docs.astro, AIProblemsStory.astro, ProblemSolution.astro, terms.astro.
- **Color Scheme Picker** — New page at [archondev.io/color-schemes](https://archondev.io/color-schemes):
  - 26 curated color schemes (5 dark + 21 light) with live interactive preview
  - Click any scheme to see it applied to the page in real-time
  - Export in 4 formats: CSS Variables, Tailwind Config, JSON, HTML Usage snippet
  - Download all 26 schemes as a single `design-tokens.css` file
  - Includes ArchonDev brand scheme as the default
  - Full SEO/GEO optimization with JSON-LD structured data (WebApplication + HowTo schemas)
  - Added as a skill (`color-scheme-picker.md`) in all 7 Lite packages so AI assistants can help users pick and implement color schemes
- **GEO Optimization Tools (2026-03-30):**
  - **Claude Code Skill** — Downloadable `geo-optimization` skill with SKILL.md (YAML frontmatter format). 7-phase workflow: context gathering, identity generation (7-word phrase + 50-word description), user selection, schema generation (Organization + Service + FAQPage JSON-LD), atomic claims (18 tokens or fewer), implementation, and audit.
  - **GEO Prompt Generator** — New page at [archondev.io/geo](https://archondev.io/geo) with JavaScript tool: user enters URL, gets a comprehensive GEO prompt to copy-paste into Claude, ChatGPT, or any AI assistant.
  - **Enhanced GEO Scenario** — Updated `geo-optimization.md` across all 7 Lite package variants with latest techniques from AEO research: atomic phrases, banned word list, 7-phase protocol, audit checklist, and link to archondev.io/geo.
  - **Website GEO Optimization** — Applied GEO best practices to archondev.io itself: @graph JSON-LD with Organization + SoftwareApplication + Service schemas, FAQPage schema with 6 Q&As using atomic phrases, updated meta descriptions on all pages, consistent identity language ("Govern AI-Generated Code to Production-Ready Standards").
  - **GEO Skill Download** — Available at [archondev.io/downloads/geo-optimization-skill.zip](https://archondev.io/downloads/geo-optimization-skill.zip) and on the GitHub release.
  - Public docs, website messaging, and package metadata now align on the shipped local-first contract.
- Lite packages deployed to Bunny + GitHub release with updated workflow guidance (design approval gate, root-cause debugging gate, two-stage review checklist).
- CLI journey is conversational-first with lower-friction continuation and approval handling.
- Pricing model is now only: Local governance mode (no built-in AI calls) and BYOK CLI mode (user-provider billed tokens). No paid tier, no credits, no subscription gate.

## Documents

| Document | Description |
|----------|-------------|
| [ai-coding-problems-research.md](ai-coding-problems-research.md) | Market research on AI coding assistant problems. Compiled findings from METR, Stack Overflow, Apiiro, and other sources. |
| [lite-features-prd.md](lite-features-prd.md) | Product requirements for Lite package enhancements. |
| [lite-user-journey-evaluation-2026-02-15.md](lite-user-journey-evaluation-2026-02-15.md) | Canonical Lite user-journey map (as-is, ideal flow, implementation, and future evaluation criteria). |
| [cli-user-journey-evaluation-2026-02-15.md](cli-user-journey-evaluation-2026-02-15.md) | Historical CLI journey baseline from pre-free/BYOK consolidation (kept for implementation traceability). |
| [kilo-inspired-features-prd.md](kilo-inspired-features-prd.md) | Feature analysis inspired by Kilo AI. |
| [superpowers-integration-evaluation-2026-02-15.md](superpowers-integration-evaluation-2026-02-15.md) | Evaluation of `superpowers-main` features for Lite vs CLI adoption, exclusions, and rollout/deploy protocol. |
| [video-script.md](video-script.md) | Script for ArchonDev promotional video. |

## Core Features

| Feature | File | Purpose |
|---------|------|---------|
| **Architectural Governance** | .archon/active/architecture.md | Define components, boundaries, invariants |
| **Dependency Tracking** | DEPENDENCIES.md | Track file-level dependencies, prevent regressions |
| **Learning Persistence** | progress.txt | Append-only log of patterns and insights |
| **AI Instructions** | AGENTS.md (8.6 KB core) | Governance rules + skills registry (29 on-demand skills) |
| **Context-Aware Triggers** | AGENTS.md skills registry | Proactive detection of user context → loads relevant skill on-demand |
| **Design Governance** | DESIGN.md + archondev-skills/design-review.md | Design system source of truth, visual audit, AI slop detection (A-F) |
| **UX/UI Expert Review** | archondev-skills/ux-ui-review.md | Expert usability, interaction, information architecture, desktop-app, and Flutter desktop audit |
| **Fix-First Code Review** | archondev-skills/code-review.md | Auto-fix mechanical issues, ask about ambiguous ones |
| **Self-Regulation** | AGENTS.md core + archondev-skills/self-regulation.md | Hard limits always-on; full blast radius protocol loads on-demand |
| **Systematic Debugging** | archondev-skills/systematic-debugging.md | Root cause first, hypothesis testing, regression prevention |
| **Ship Readiness Dashboard** | archondev-skills/ship-readiness.md | Pre-ship checklist across all quality gates |
| **Scope Review** | archondev-skills/scope-review.md | Expand/selective/hold/reduce when scope creep detected |
| **Progress Reflection** | archondev-skills/progress-reflection.md | Solo retro at milestones — what worked, what didn't |
| **Risk Scoring (CLI)** | src/core/risk/ | 0-100 pre-execution risk assessment, policy-aware confirmation |
| **Ship Pipeline (CLI)** | src/core/ship/ + src/cli/ship.ts | Merge → test → review → risk → version → changelog → PR |
| **Browser QA (CLI)** | src/core/browser/ + src/cli/qa.ts | Playwright health checks, diff-aware page testing |
| **Session Metrics (CLI)** | src/core/metrics/ + src/cli/retro.ts | Duration, atoms, gate pass rate, file hotspots |
| **Scope Drift Detection (CLI)** | src/core/code-review/scope-drift.ts | Detects files modified outside planned scope |
| **Doc Staleness Detection (CLI)** | src/core/code-review/doc-staleness.ts | Flags docs referencing changed code |
| **Color Scheme Picker** | website/src/pages/color-schemes.astro + archondev-skills/color-scheme-picker.md | 26 curated schemes with live preview, multi-format export (CSS/Tailwind/JSON/HTML) |
| **GEO Optimization** | archondev-skills/geo-optimization.md + website/src/pages/geo.astro | Two-audience GEO protocol: identity phrases, atomic claims, JSON-LD schemas, surface audit |
| **Truth Layer** | archondev-skills/truth-layer.md + src/cli/truth-layer.ts | Living claims-and-evidence artifact used by content-touching commands |
| **AI-Washing Audit** | archondev-skills/ai-washing-audit.md + src/cli/geo.ts | Risk register for unsupported AI claims and defensible rewrites |
| **Human Memory Map** | archondev-skills/human-memory-map.md + src/cli/brand.ts | Six-surface diagnostic for what humans remember versus intended positioning |
| **MarkItDown MCP Document Ingestion** | archondev-skills/markitdown-mcp.md | Optional local MCP workflow for converting PDFs, Office files, URLs, and other sources into Markdown for AI review and indexing |
| **GEO Claude Skill** | website/public/downloads/geo-optimization-skill/SKILL.md | Downloadable Claude Code skill for automated GEO optimization workflow |
| **GEO Prompt Generator** | website/src/pages/geo.astro (client-side JS) | URL input → comprehensive GEO prompt for any AI assistant |
| **Task Extraction** | .archon/active/tasks.json | Track multi-item requests, prevent lost requirements |
| **Handoff Context** | .archon/current_context.md | Current context for session handoff |
| **Accessibility Check** | archondev-skills/accessibility-audit.md | WCAG 2.2 AA compliance before going live |
| **Expert Review Spec** | archondev-skills/expert-review.md | Consultant-ready technical spec: gap analysis, approach review, UX enhancement |
| **Features Dashboard** | archondev-skills/features-dashboard.md + .archon/dashboard-template.html | Live HTML page tracking feature usage, availability, and recommendations |
| **Governance Store (SQLite)** | .archon/governance.db | Local-only searchable governance DB (architecture, tasks, handoffs, decisions) |
| **Lite Journey Reference** | docs/lite-user-journey-evaluation-2026-02-15.md | Required baseline for evaluating Lite UX changes before implementation |
| **CLI Journey Reference** | docs/cli-user-journey-evaluation-2026-02-15.md | Required baseline for evaluating CLI UX changes before implementation |

## Key Features by Version

### v3.3.0 (Current)

- **UX/UI Expert Review** — Lite packages include `archondev-skills/ux-ui-review.md`, an opt-in skill for deeper usability, interaction, information architecture, desktop-app, and Flutter desktop audits.
- **Severity-rated fixes** — The skill produces prioritized findings with concrete fixes, validation guidance, and source anchors for Nielsen Norman Group heuristics, WCAG 2.2, Apple HIG, Microsoft Windows design guidance, and GNOME HIG.
- **Claude Code command** — Claude Code adds `/ux-review`.
- **Lite packages** — all seven variants ship 29 skills; Claude Code ships 21 native slash commands.

### v3.2.0

- **MarkItDown MCP Document Ingestion** — Lite packages include `archondev-skills/markitdown-mcp.md`, an optional local skill for converting PDFs, Office files, URLs, and other documents into Markdown.
- **Security-first setup guidance** — The skill documents STDIO, localhost HTTP, and Docker sandbox options, plus warnings about file/network access permissions.
- **Large document fallback** — The skill recommends the plain MarkItDown CLI `-o` output path when MCP responses are too large for assistant context.
- **Lite packages** — all seven variants ship 28 skills; Claude Code ships 20 native slash commands, including `/markitdown`.

### v3.1.0

- **Truth Layer** — `archon truth-layer init/audit` creates and audits `.archon/truth-layer.md` for claims, evidence, customer language, proof, constraints, pricing logic, objections, and category beliefs.
- **Agent Clarity + AI-Washing Audits** — `archon geo audit`, `archon geo claims`, and `archon geo washing-audit` now produce multi-surface, evidence-aware artifacts.
- **Human Memory Map** — `archon brand memory-map` pressure-tests what buyers remember across six surfaces.
- **Lite packages** — all seven variants ship 27 skills; Claude Code ships 19 native slash commands.
- **Website** — `/agent-readiness/` explains the two-audience framework.

### v3.0.1

- **Packaging verification correction** — the published npm package and installed CLI now reflect the same hidden-command local-first surface validated in the repo.
- **Version detection hardening** — update checks now prefer the running package context before falling back to global npm metadata.

### v3.0.0
- **G-Stack CLI Integration** — Runtime features inspired by [gstack](https://github.com/garrytan/gstack):
  - `archon ship` — Executable ship pipeline (merge base → tests → review → risk → version → changelog → PR)
  - `archon qa` — Headless browser QA with diff-aware page testing
  - `archon retro` — Session retrospective with quantitative metrics
  - Pre-execute risk scoring (0-100) with policy-aware confirmation
  - Fix-first code review with scope drift detection and doc staleness checks
  - Ship intent detection in chat ("ship it", "deploy", "create pr", etc.)
- **Free/BYOK model enforced** — no paid tier, no credits, no subscription gate for core product usage.
- **Native SQLite runtime** — local SQLite now uses Node built-in `node:sqlite` (Node 22+) and no longer depends on `better-sqlite3`.

### v2.19.56-rc.21 (Current RC)
- **Original-Task Recovery Hardening** — Chat keeps high-signal original requests across exploratory follow-ups, so `do my original task` maps back correctly.
- **Lower-Friction Approval Flow** — `yes`/`approve plan` now executes approved work directly in chat without an extra execution confirmation prompt.
- **Noise Reduction Guards** — Duplicate rapid plan prompt output and accidental concurrent continue-runs are suppressed.

### v2.19.38
- **Staged Path-Scope Auto-Recovery** — Chat execution now auto-replans/retries path-scope governance blocks, then escalates to a forced-base-path retry if needed.
- **Natural Continuation Commands** — `continue`/`move forward` execute continuation flow instead of creating accidental atoms.
- **Analysis Approval Auto-Continue** — `yes`/`go ahead` after analysis-first planning now creates and begins implementation in one flow.
- **Scope-Constrained Planning Input** — Chat planning injects allowed-path constraints before atom creation to reduce out-of-scope execute proposals.

### v2.19.30
- **Analysis-First by Default** — Approval for analysis requests now returns evaluated recommendations first, without creating atoms.
- **Explicit Task Conversion** — Users can create governed work from analysis with explicit `create atom`.
- **Explicit Execution Control** — Chat execution requires explicit execute wording, preventing accidental starts from conversational `continue`.

### v2.19.29
- **Governance Steering Mode** — Architecture/path violations now pause execution with corrective guidance instead of hard `FAILED` outcomes.
- **Proposal Approval Context** — `approve plan` now maps to pending proposal context reliably across chat loops.
- **Fluid Recovery Path** — Off-course work is surfaced as actionable guidance with blocked-state recovery, not crash-like failure.

### v2.19.25
- **Chat-First Stability** — Read-only file/folder requests now stay in exploratory conversation flow.
- **Execute Failure Safety** — Failed execution no longer hard-crashes the interactive session from invalid atom transition handling.
- **Apple Terminal Hardening** — Additional safe-mode prompt/input reductions for dictation-heavy usage.
- **Model Defaults Refresh** — Gemini 3.1 Pro, GPT-5.3 Codex, Sonnet/Opus 4.6 defaults and aliases aligned.

### v2.19.10
- **BYOK Startup Usage Panel** — Interactive startup now shows BYOK usage/cost context immediately.
- **Zero-State Usage Visibility** — BYOK startup model usage section now shows explicit zero usage (`No usage yet ... $0.0000`) instead of appearing blank.

### v2.19.4
- **Design Approval Gate** — Plan flow now requires explicit design approval before adversarial planning.
- **Plan Structure Enforcement** — Plans are normalized with verification and acceptance-check steps.
- **Root-Cause Bug Intake** — Bug workflow now captures evidence, reproducibility, and root-cause hypothesis.
- **Two-Stage AI Review** — Spec-compliance review runs before code-quality review.

### v2.19.0
- **Governance Store CLI** — Manage governance via `archon governance` (status, tasks, handoffs, migration)
- **AGD Migration** — Legacy `ARCHITECTURE.md` and `.archon/current-tasks.md` migrate into AGD layout
- **Governance SQLite/FTS** — Searchable architecture, tasks, handoffs, and decisions
- **Lite Packages Updated** — New `.archon/active|history|archive` layout with handoff templates

### v2.4.0
- **Dependency Graph Scheduler** — Wave-based parallel execution
- **Eject Command** — Clean removal of ArchonDev from projects
- **Atomic Rollback** — Revert individual atom commits via git

### v2.3.0
- **5-Phase Interview System** — Discovery → Features → Technical → Branding → Review
- **Project Constitution** — Immutable specification with SHA-256 hash
- **Challenge Mode** — AI pushback on scope creep
- **Atom Generator** — Transform Constitution into prd.json

### v2.0.0 - v2.2.0
- **Cloud Agents** — Execute in cloud, get PR when done
- **GitHub Integration** — Connect GitHub for automatic PRs
- **Semantic Indexing** — AI-powered codebase search (local/cloud)
- **Cross-Device Sessions** — Save and resume sessions

### v1.7.0 - v1.9.0
- **Quality Level / Posture** — prototype/production/enterprise modes
- **SEO Optimization** — Automated meta tags, Open Graph
- **GEO for AI Search** — Optimize for ChatGPT/Perplexity citations
- **Pre-Deploy Accessibility** — WCAG 2.2 AA compliance

## Key Statistics (from Research)

- **62%** of AI-generated code contains security vulnerabilities
- **66%** of developers say "almost right but not quite" code is their top frustration
- **19% slower** — Developers using AI were slower but *believed* they were 20% faster
- **4,600+** ADA web accessibility lawsuits filed in US (2023)

## CLI Commands (3.x source; npm latest 3.1.0)

| Command | Description |
|---------|-------------|
| `archon` | Chat-first interactive mode (local governance + BYOK aware) |
| `archon mode` | Choose local governance mode or BYOK AI mode |
| `archon plan <description>` | Create governed work item |
| `archon execute <atom-id>` | Execute with risk scoring and quality gates |
| `archon ship` | Ship pipeline: merge → test → review → risk → version → changelog → PR |
| `archon ship --dry-run` | Run all ship checks without committing or pushing |
| `archon qa` | Visual QA with headless browser health checks (Playwright) |
| `archon qa --url <url>` | Test specific URL with health scoring |
| `archon retro` | Session retrospective with quantitative metrics |
| `archon interview` | 5-phase project interview |
| `archon generate` | Generate prd.json from Constitution |
| `archon parallel schedule` | Analyze dependencies for parallel execution |
| `archon revert <atom-id>` | Revert atom commits |
| `archon eject` | Remove ArchonDev from project |
| `archon a11y check` | Run WCAG 2.2 AA accessibility audit |
| `archon deps list` | View dependency rules |
| `archon review init` | Initialize code review |
| `archon governance status` | Show governance status (AGD) |
| `archon governance architecture update` | Update architecture with change reason |
| `archon governance task update` | Update governance tasks |
| `archon governance handoff` | Log handoff + current context |
| `archon governance migrate` | Migrate legacy governance files |
| `archon governance sqlite-init` | Initialize or refresh local governance SQLite DB |
| `archon config ai` | Guided BYOK setup |
| `archon usage` | Usage by period and model (BYOK) |

**Notes:**  
- `archon plan --edit` lets you adjust title and acceptance criteria before planning.  
- Parallel execution uses the current CLI entrypoint and respects `--skip-gates`.
- Quality-gate rollback is scoped to atom-touched files (no full working tree reset).
- Legacy remote commands are hidden from normal help; the primary UX is local-first.
- BYOK mode now also shows startup usage and estimated provider spend, including explicit zero-state model usage when no usage exists.
- BYOK shows per-model usage and cost by today/week/month/year in `archon preferences` → “View usage details.”
- Interactive journey prompts are conversational-first; numbered menu selections remain optional shortcuts.
- You can paste multi-line requests into interactive prompts; Archon captures them as a single response.
- Content-only requests (stories, outlines, lessons, visuals) use lightweight planning to avoid blocking.
- Governance boundary violations in execute now pause with guidance (`BLOCKED`) instead of hard execution failure.
- Analysis-first requests support natural confirmations (`yes`, `go ahead`, `create`) to create governed tasks.
- Chat continuation supports natural directives (`continue`, `move forward`) and path-scope blocks can auto-recover via replan + retry.

## BYOK Key Security

- BYOK keys are stored locally in `~/.archon/keys.json` and are never uploaded to ArchonDev servers.
- Keys are encrypted at rest with AES-256-GCM and the file is set to owner-only permissions (`0600`).
- BYOK runs locally; legacy remote commands are retired and should not call Supabase, Fly, Stripe, or Archon-managed telemetry.
- If your device is compromised, an attacker could access local files. Treat keys as sensitive secrets.

## Retired Infrastructure

The current product does not need Supabase auth/database, Fly payment API, Fly cloud worker, Stripe checkout, server-side usage tracking, daily user-count emails, or Supabase model-registry sync. Treat those as historical references unless a new architecture decision explicitly reintroduces paid remote services.

Shutdown status as of 2026-04-26:
- Supabase project `yjdkcepktrbabmzhcmrt` was deleted.
- Fly apps `archondev-api` and `archondev-worker` were destroyed.
- CLI compatibility commands for remote/auth/cloud/session paths now print retirement guidance instead of calling Archon-managed infrastructure.

## Local Governance SQLite (Dev Only)

Governance data is stored locally in `.archon/governance.db`. This is a development-only database and is never synced to Supabase.

Workflow:
1. Ensure governance files exist under `.archon/active`, `.archon/history`, `.archon/archive`, plus `progress.txt`.
2. Initialize or refresh the DB by running:

```bash
pnpm exec tsx scripts/init-governance-db.ts
```

This script loads architecture, tasks, handoffs, decisions, and completed tasks into SQLite for fast local search.

## Related

- [Main README](../README.md) — Project overview and CLI commands
- [ARCHITECTURE.md](../ARCHITECTURE.md) — Governance constitution
- [CHANGELOG.md](../CHANGELOG.md) — Version history
- [archondev.io](https://archondev.io) — Website
- [archondev.io/docs](https://archondev.io/docs) — Full documentation
- [archondev.io/color-schemes](https://archondev.io/color-schemes) — Color Scheme Picker (26 curated schemes, live preview, multi-format export)
- [archondev.io/geo](https://archondev.io/geo) — GEO Optimization tools (Claude skill download + prompt generator)

---

*ArchonDev by Jumping Ahead Corp.*
