# ArchonDev Documentation

## Overview

This folder contains internal documentation for ArchonDev development and marketing.

## Current Status (2026-03-08)

- Published `archondev@2.19.56-rc.16` to npm (`rc` tag).
- Lite packages deployed to Bunny + GitHub release with updated workflow guidance (design approval gate, root-cause debugging gate, two-stage review checklist).
- CLI now enforces design-approval metadata checks, stronger plan structure, root-cause bug intake context, and staged AI review order (spec then quality).
- CLI journey is conversational-first with lower-friction continuation and approval handling.
- BYOK startup now shows usage transparency on launch, including explicit zero-state model usage output when usage is empty.
- Chat-first flow now routes "read/analyze files" requests to explore mode and no longer crashes on failed execution state transitions.
- Chat approval flow now correctly binds `approve plan` to the pending proposal context (no accidental atoms titled `approve`).
- Analysis-first requests now stay analysis-first after approval and return recommendation output before any atom is created.
- Chat continuation now supports natural directives such as `continue`, `move forward`, and `go ahead`.
- Governance execution now steers with explicit guidance by moving boundary/path violations to `BLOCKED` rather than failing execution.
- Path-scope governance blocks now trigger automatic re-plan + retry recovery in chat mode, with a second stricter retry phase when needed.
- Pricing model is now only: Free download mode (no built-in AI) and BYOK CLI mode (user-provider billed tokens). No paid tier, no credits, no subscription gate.

## Documents

| Document | Description |
|----------|-------------|
| [ai-coding-problems-research.md](ai-coding-problems-research.md) | Market research on AI coding assistant problems. Compiled findings from METR, Stack Overflow, Apiiro, and other sources. |
| [lite-features-prd.md](lite-features-prd.md) | Product requirements for Lite package enhancements. |
| [lite-user-journey-evaluation-2026-02-15.md](lite-user-journey-evaluation-2026-02-15.md) | Canonical Lite user-journey map (as-is, ideal flow, implementation, and future evaluation criteria). |
| [cli-user-journey-evaluation-2026-02-15.md](cli-user-journey-evaluation-2026-02-15.md) | Canonical CLI user-journey map including tiering, model selection, payment/top-up, and insufficient-funds recovery. |
| [kilo-inspired-features-prd.md](kilo-inspired-features-prd.md) | Feature analysis inspired by Kilo AI. |
| [superpowers-integration-evaluation-2026-02-15.md](superpowers-integration-evaluation-2026-02-15.md) | Evaluation of `superpowers-main` features for Lite vs CLI adoption, exclusions, and rollout/deploy protocol. |
| [video-script.md](video-script.md) | Script for ArchonDev promotional video. |

## Core Features

| Feature | File | Purpose |
|---------|------|---------|
| **Architectural Governance** | .archon/active/architecture.md | Define components, boundaries, invariants |
| **Dependency Tracking** | DEPENDENCIES.md | Track file-level dependencies, prevent regressions |
| **Learning Persistence** | progress.txt | Append-only log of patterns and insights |
| **AI Instructions** | AGENTS.md | Code review, database, memory management, accessibility |
| **Task Extraction** | .archon/active/tasks.json | Track multi-item requests, prevent lost requirements |
| **Handoff Context** | .archon/current_context.md | Current context for session handoff |
| **Accessibility Check** | archondev-scenarios/pre-deploy-accessibility.md | WCAG 2.2 AA compliance before going live |
| **Governance Store (SQLite)** | .archon/governance.db | Local-only searchable governance DB (architecture, tasks, handoffs, decisions) |
| **Lite Journey Reference** | docs/lite-user-journey-evaluation-2026-02-15.md | Required baseline for evaluating Lite UX changes before implementation |
| **CLI Journey Reference** | docs/cli-user-journey-evaluation-2026-02-15.md | Required baseline for evaluating CLI UX changes before implementation |

## Key Features by Version

### v2.19.56-rc.16 (Current RC)
- **Original-Task Recovery Hardening** — Chat keeps high-signal original requests across exploratory follow-ups, so `do my original task` maps back correctly.
- **Lower-Friction Approval Flow** — `yes`/`approve plan` now executes approved work directly in chat without an extra execution confirmation prompt.
- **Noise Reduction Guards** — Duplicate rapid plan prompt output and accidental concurrent continue-runs are suppressed.

### v2.19.38 (Current)
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

## CLI Commands (v2.19.38)

| Command | Description |
|---------|-------------|
| `archon` | Interactive mode (login, tier, interview) |
| `archon plan <description>` | Create governed work item |
| `archon execute <atom-id>` | Execute with quality gates |
| `archon execute --cloud` | Execute in cloud (creates PR) |
| `archon interview` | 5-phase project interview |
| `archon generate` | Generate prd.json from Constitution |
| `archon parallel schedule` | Analyze dependencies for parallel execution |
| `archon parallel cloud <atom-ids...>` | Queue multiple atoms for cloud execution (Credits tier) |
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
- BYOK tier now also shows startup usage and estimated provider spend, including explicit zero-state model usage when no usage exists.
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
- BYOK runs locally; cloud execution is Credits-only.
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
