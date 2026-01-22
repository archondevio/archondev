<p align="center">
  <img src="https://archondev.io/images/archon-robot.png" alt="ArchonDev" width="120" />
</p>

<h1 align="center">ArchonDev</h1>

<p align="center">
  <strong>AI Development Governance</strong><br>
  Stop babysitting your AI. Start shipping.
</p>

<p align="center">
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
| Cursor | [cursor-package.zip](https://github.com/archondevio/archondev/releases/latest/download/cursor-package.zip) |
| Claude Code / Amp | [claude-amp-package.zip](https://github.com/archondevio/archondev/releases/latest/download/claude-amp-package.zip) |
| Windsurf / Codeium | [windsurf-package.zip](https://github.com/archondevio/archondev/releases/latest/download/windsurf-package.zip) |
| VS Code + Copilot | [vscode-copilot-package.zip](https://github.com/archondevio/archondev/releases/latest/download/vscode-copilot-package.zip) |
| OpenAI Codex | [codex-package.zip](https://github.com/archondevio/archondev/releases/latest/download/codex-package.zip) |
| Generic (any AI) | [generic-package.zip](https://github.com/archondevio/archondev/releases/latest/download/generic-package.zip) |

**What's in the package:**

| File | Purpose |
|------|---------|
| `ARCHITECTURE.md` | Governance constitution — components, invariants, protected paths |
| `AGENTS.md` | AI instructions — code review, local SQLite, memory management |
| `DEPENDENCIES.md` | Regression prevention — tracks what breaks when you change files |
| `progress.txt` | Learning log — persists knowledge across sessions |
| `.archon/config.yaml` | Configuration file |
| `examples/` | Sample workflows and patterns |
| IDE-specific rules | `.cursorrules`, `CLAUDE.md`, etc. |

**Usage:**
1. Download the package for your IDE
2. Unzip to your project root
3. Tell your AI: `"read ARCHITECTURE.md"`

---

## Features

- **📐 Architectural Governance** — Define components, boundaries, and invariants your AI must respect
- **🔗 Dependency Tracking** — Know what breaks before you change it
- **🧠 Learning Persistence** — AI remembers patterns across sessions via `progress.txt`
- **🔍 Code Review Mode** — AI reviews code without modifying it
- **📦 Local Database** — Optional SQLite for tracking atoms and learnings
- **🛡️ Quality Gates** — Every change must pass before commit

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
