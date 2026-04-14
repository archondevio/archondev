# ArchonDev Documentation

## Overview

This folder contains the public documentation snapshot for the current ArchonDev release.

## Current Status (2026-04-14)

- Published stable `archondev@3.0.0` to npm (`latest` tag).
- Product direction is now local-first CLI + BYOK AI with no required platform login on the primary path.
- Lite packages remain free downloads for Cursor, Claude Code, Windsurf, VS Code, Gemini, Codex, and generic assistants.
- Legacy remote/cloud/session commands still exist for backward compatibility, but they are hidden from the normal CLI surface and are not part of the primary product story.

## Release Highlights

### v3.0.0: Local-First CLI vNext

- Chat-first startup with governance loaded automatically from the current folder.
- No required platform login for the main path.
- BYOK is the only AI-enabled mode in the primary flow.
- Local-only usage ledger for privacy.
- Filesystem-based skills with contextual suggestions.
- Automatic continuity handoff before context exhaustion.
- Safe parallel continuation for independent ready atoms.
- Hidden legacy remote/cloud/session/GitHub commands so help text matches the real product.

### Lite Package Capabilities

- Context-aware triggers
- Fix-first code review
- AI slop detection
- Systematic debugging
- Ship readiness dashboard
- Scope review
- Self-regulation guardrails
- Progress reflection
- Expert review spec
- Features dashboard

## CLI Commands (v3.0.0)

| Command | Description |
|---------|-------------|
| `archon` | Chat-first interactive mode (local governance + BYOK aware) |
| `archon mode` | Choose local governance mode or BYOK AI mode |
| `archon config ai` | Guided BYOK setup |
| `archon status` | Show local mode and project status |
| `archon plan <description>` | Create governed work item |
| `archon execute <atom-id>` | Execute with risk scoring and quality gates |
| `archon ship` | Ship pipeline: merge → test → review → risk → version → changelog → PR |
| `archon qa` | Visual QA with headless browser health checks |
| `archon retro` | Session retrospective with quantitative metrics |
| `archon deps list` | View dependency rules |
| `archon review init` | Initialize code review |
| `archon governance status` | Show governance status |
| `archon usage` | Usage by period and model |

## Pricing

**ArchonDev is Free.** There are no paid tiers, no subscriptions, and no credit card required.

| Mode | Cost to ArchonDev | What You Get |
|------|-------------------|--------------|
| **Download / Governance** | $0 | Governance/workflow layer with no built-in AI calls |
| **CLI + AI (BYOK)** | $0 | Full CLI with AI — bring your own API keys; your provider bills tokens directly at cost |

## Privacy

- BYOK keys are stored locally in `~/.archon/keys.json`.
- Usage tracking is local-only in the current primary product path.
- Governance SQLite lives locally in `.archon/governance.db` and is never synced to Supabase.

## Related

- [Main README](../README.md) — Project overview and CLI commands
- [CHANGELOG.md](../CHANGELOG.md) — Version history
- [archondev.io](https://archondev.io) — Website
- [archondev.io/docs](https://archondev.io/docs) — Full documentation
- [archondev.io/download](https://archondev.io/download) — Lite package downloads
