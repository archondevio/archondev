<p align="center">
  <img src="https://archondev.io/images/archon-robot.png" alt="ArchonDev" width="120" />
</p>

<h1 align="center">ArchonDev</h1>

<p align="center">
  <strong>AI Development Governance</strong><br>
  Stop babysitting your AI. Start shipping.
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

### 🚀 Full CLI (Recommended)

The complete AI development system with adversarial planning, quality gates, and learning persistence.

```bash
npm install -g archondev
```

Then run:
```bash
archon
```

[📖 Full Documentation →](https://archondev.io/docs)

---

### 📦 Lite Package (Keep Your Tools)

Already using Cursor, Claude Code, Windsurf, or Copilot? Drop governance files into your project. Your AI follows the rules.

**Download for your IDE:**

| IDE | Download |
|-----|----------|
| Cursor | [cursor-package.zip](https://github.com/archondevio/archondev/releases/latest/download/cursor-package.zip) (~20KB) |
| Claude Code / Amp | [claude-amp-package.zip](https://github.com/archondevio/archondev/releases/latest/download/claude-amp-package.zip) (~20KB) |
| Google Gemini | [gemini-package.zip](https://github.com/archondevio/archondev/releases/latest/download/gemini-package.zip) (~20KB) |
| Windsurf / Codeium | [windsurf-package.zip](https://github.com/archondevio/archondev/releases/latest/download/windsurf-package.zip) (~20KB) |
| VS Code + Copilot | [vscode-copilot-package.zip](https://github.com/archondevio/archondev/releases/latest/download/vscode-copilot-package.zip) (~20KB) |
| OpenAI Codex | [codex-package.zip](https://github.com/archondevio/archondev/releases/latest/download/codex-package.zip) (~20KB) |
| Generic (any AI) | [generic-package.zip](https://github.com/archondevio/archondev/releases/latest/download/generic-package.zip) (~20KB) |

**What's in the package:**

| File | Purpose |
|------|---------|
| `ARCHITECTURE.md` | Governance constitution — components, invariants, protected paths, accessibility config |
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
3. Tell your AI: `"read ARCHITECTURE.md"`

---

## VS Code Extension

Real-time violations + **quick-fix suggestions**. Press Ctrl+. (Cmd+.) for lightbulb menu with auto-fixes.

[Download archondev-0.2.0.vsix](https://archondev.io/downloads/archondev-0.2.0.vsix)

---

## Features

### Core Governance
- **📐 Architectural Governance** — Define components, boundaries, and invariants your AI must respect
- **🔗 Dependency Tracking** — Know what breaks before you change it (`DEPENDENCIES.md`)
- **🧠 Learning Persistence** — AI remembers patterns across sessions via `progress.txt`
- **🛡️ Quality Gates** — Every change must pass before commit

### New in v1.8.0
- **🔍 SEO Optimization** — Automated meta tags, Open Graph, Twitter Cards
  - AI scans, identifies gaps, generates missing tags
  - User approves before changes are applied
  - Trigger: `seo check`, `seo fix`, `add open graph`
- **🤖 GEO for AI Search** — Optimize for ChatGPT, Perplexity, Claude citations
  - AI generates 3 candidate 7-word brand phrases
  - AI generates 3 candidate 50-word descriptions
  - User selects preferred identity
  - JSON-LD schemas for AI comprehension
  - Trigger: `geo identity`, `geo schema`

### New in v1.7.0
- **♿ Pre-Deploy Accessibility Check** — WCAG 2.2 AA compliance before going live
  - Legal liability warnings (ADA, EAA, Section 508)
  - Auto-fix for common issues (contrast, alt text, focus)
  - WCAG 2.2 AA badge for compliant sites
  - CLI: `archon a11y check`, `archon a11y fix`, `archon a11y badge`

### New in v1.6.x
- **📋 Task Extraction Protocol** — AI confirms all items in multi-item requests before starting
  - Prevents lost requirements (AI often forgets items 3+ in a list)
  - Trigger phrases: `plan these tasks`, `task status`, `what's on my list`
- **🚀 Smart Onboarding** — Detects new project, existing project, or continuing session
- **🔍 Code Review Mode** — AI reviews code without modifying it

### Tools & Extensions
- **📦 Local Database** — Optional SQLite for tracking atoms and learnings
- **💡 VS Code Extension** — Real-time diagnostics with quick-fix suggestions

---

## CLI Commands

| Command | Description |
|---------|-------------|
| `archon` | Interactive mode |
| `archon plan <description>` | Create governed work item |
| `archon execute <atom-id>` | Execute with quality gates |
| `archon review init` | Initialize code review |
| `archon a11y check` | Run WCAG 2.2 AA audit |
| `archon a11y fix` | Auto-fix accessibility issues |
| `archon deps list` | View dependency rules |
| `archon watch` | Live TUI dashboard |
| `archon seo check` | Run SEO meta tag audit |
| `archon seo fix` | Apply recommended SEO fixes |
| `archon geo identity` | Generate brand identity phrases |
| `archon geo schema` | Generate JSON-LD schemas |

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
