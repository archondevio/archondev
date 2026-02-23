# ArchonDev Documentation

## Overview

This folder contains internal documentation for ArchonDev development and marketing.

## Documents

| Document | Description |
|----------|-------------|
| [ai-coding-problems-research.md](ai-coding-problems-research.md) | Market research on AI coding assistant problems. Compiled findings from METR, Stack Overflow, Apiiro, and other sources. |
| [lite-features-prd.md](lite-features-prd.md) | Product requirements for Lite package enhancements. |
| [kilo-inspired-features-prd.md](kilo-inspired-features-prd.md) | Feature analysis inspired by Kilo AI. |
| [video-script.md](video-script.md) | Script for ArchonDev promotional video. |

## Core Features

| Feature | File | Purpose |
|---------|------|---------|
| **Architectural Governance** | ARCHITECTURE.md | Define components, boundaries, invariants |
| **Dependency Tracking** | DEPENDENCIES.md | Track file-level dependencies, prevent regressions |
| **Learning Persistence** | progress.txt | Append-only log of patterns and insights |
| **AI Instructions** | AGENTS.md | Code review, database, memory management, accessibility |
| **Task Extraction** | .archon/current-tasks.md | Track multi-item requests, prevent lost requirements |
| **Accessibility Check** | archondev-scenarios/pre-deploy-accessibility.md | WCAG 2.2 AA compliance before going live |

## Key Features by Version

### v2.19.4 (Current)
- **Design Approval Gate** — Plan flow now requires explicit design approval before adversarial planning.
- **Plan Structure Enforcement** — Plans are normalized with verification and acceptance-check steps.
- **Root-Cause Bug Intake** — Bug workflow now captures evidence, reproducibility, and root-cause hypothesis.
- **Two-Stage AI Review** — Spec-compliance review runs before code-quality review.

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

## CLI Commands (v2.19.4)

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
| `archon pricing` | Switch pricing tier |

**Notes:**  
- `archon plan --edit` lets you adjust title and acceptance criteria before planning.  
- Parallel execution uses the current CLI entrypoint and respects `--skip-gates`.
- Quality-gate rollback is scoped to atom-touched files (no full working tree reset).
- Cloud execution is Credits-only. BYOK and Free tiers run locally.
- Content-only requests (stories, outlines, lessons, visuals) use lightweight planning to avoid blocking.

## BYOK Key Security

- BYOK keys are stored locally in `~/.archon/keys.json` and are never uploaded to ArchonDev servers.
- Keys are encrypted at rest and the file is set to owner-only permissions (`0600`).
- BYOK runs locally; cloud execution is Credits-only.
- If your device is compromised, an attacker could access local files. Treat keys as sensitive secrets.

## Related

- [Main README](../README.md) — Project overview and CLI commands
- [ARCHITECTURE.md](../ARCHITECTURE.md) — Governance constitution
- [CHANGELOG.md](../CHANGELOG.md) — Version history
- [archondev.io](https://archondev.io) — Website
- [archondev.io/docs](https://archondev.io/docs) — Full documentation

---

*ArchonDev by Jumping Ahead Corp.*
