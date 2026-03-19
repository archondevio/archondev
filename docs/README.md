# ArchonDev Documentation

## Overview

This folder contains internal documentation for ArchonDev development and marketing.

## Current Status (2026-03-19)

- Published stable `archondev@2.19.57` to npm (`latest` tag).
- Published test channel `archondev@2.19.56-rc.21` to npm (`rc` tag).
- **v2.19.57: G-Stack CLI Integration** — Runtime features inspired by [gstack](https://github.com/garrytan/gstack) now ship as executable CLI infrastructure:
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
- Lite packages deployed to Bunny + GitHub release with updated workflow guidance (design approval gate, root-cause debugging gate, two-stage review checklist).
- CLI journey is conversational-first with lower-friction continuation and approval handling.
- Pricing model is now only: Free download mode (no built-in AI) and BYOK CLI mode (user-provider billed tokens). No paid tier, no credits, no subscription gate.

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
| **AI Instructions** | AGENTS.md | Code review, context-aware intelligence, governance |
| **Context-Aware Triggers** | AGENTS.md | Proactive detection of user context → relevant capability offers |
| **Design Governance** | DESIGN.md + archondev-scenarios/design-review.md | Design system source of truth, visual audit, interaction states |
| **AI Slop Detection** | AGENTS.md | 10-item blacklist of AI design anti-patterns, scored A-F |
| **Fix-First Code Review** | AGENTS.md | Auto-fix mechanical issues, ask about ambiguous ones |
| **Self-Regulation** | AGENTS.md | Blast radius checks, file limits, 3-strike rule, checkpoints |
| **Systematic Debugging** | archondev-scenarios/systematic-debugging.md | Root cause first, hypothesis testing, regression prevention |
| **Completion Status** | AGENTS.md | DONE / DONE_WITH_CONCERNS / BLOCKED / NEEDS_CONTEXT |
| **Ship Readiness Dashboard** | archondev-scenarios/ship-readiness.md | Pre-ship checklist across all quality gates |
| **Scope Review** | archondev-scenarios/scope-review.md | Expand/selective/hold/reduce when scope creep detected |
| **Progress Reflection** | AGENTS.md | Solo retro at milestones — what worked, what didn't |
| **Risk Scoring (CLI)** | src/core/risk/ | 0-100 pre-execution risk assessment, policy-aware confirmation |
| **Ship Pipeline (CLI)** | src/core/ship/ + src/cli/ship.ts | Merge → test → review → risk → version → changelog → PR |
| **Browser QA (CLI)** | src/core/browser/ + src/cli/qa.ts | Playwright health checks, diff-aware page testing |
| **Session Metrics (CLI)** | src/core/metrics/ + src/cli/retro.ts | Duration, atoms, gate pass rate, file hotspots |
| **Scope Drift Detection (CLI)** | src/core/code-review/scope-drift.ts | Detects files modified outside planned scope |
| **Doc Staleness Detection (CLI)** | src/core/code-review/doc-staleness.ts | Flags docs referencing changed code |
| **Task Extraction** | .archon/active/tasks.json | Track multi-item requests, prevent lost requirements |
| **Handoff Context** | .archon/current_context.md | Current context for session handoff |
| **Accessibility Check** | archondev-scenarios/pre-deploy-accessibility.md | WCAG 2.2 AA compliance before going live |
| **Governance Store (SQLite)** | .archon/governance.db | Local-only searchable governance DB (architecture, tasks, handoffs, decisions) |
| **Lite Journey Reference** | docs/lite-user-journey-evaluation-2026-02-15.md | Required baseline for evaluating Lite UX changes before implementation |
| **CLI Journey Reference** | docs/cli-user-journey-evaluation-2026-02-15.md | Required baseline for evaluating CLI UX changes before implementation |

## Key Features by Version

### v2.19.57 (Current Stable)
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

## CLI Commands (v2.19.57)

| Command | Description |
|---------|-------------|
| `archon` | Interactive mode (login, mode selection, interview) |
| `archon plan <description>` | Create governed work item |
| `archon execute <atom-id>` | Execute with risk scoring and quality gates |
| `archon ship` | Ship pipeline: merge → test → review → risk → version → changelog → PR |
| `archon ship --dry-run` | Run all ship checks without committing or pushing |
| `archon qa` | Visual QA with headless browser health checks (Playwright) |
| `archon qa --url <url>` | Test specific URL with health scoring |
| `archon retro` | Session retrospective with quantitative metrics |
| `archon execute --cloud` | Execute in cloud (creates PR) |
| `archon interview` | 5-phase project interview |
| `archon generate` | Generate prd.json from Constitution |
| `archon parallel schedule` | Analyze dependencies for parallel execution |
| `archon parallel cloud <atom-ids...>` | Legacy command (disabled in free/BYOK mode) |
| `archon revert <atom-id>` | Revert atom commits |
| `archon eject` | Remove ArchonDev from project |
| `archon github connect` | Link GitHub for cloud execution |
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
- Cloud execution is disabled in the current free/BYOK model.
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
- BYOK runs locally; cloud execution is currently disabled in the free/BYOK model.
- If your device is compromised, an attacker could access local files. Treat keys as sensitive secrets.

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

---

*ArchonDev by Jumping Ahead Corp.*
