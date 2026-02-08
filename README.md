# ArchonDev

**AI Development Governance — Stop Babysitting Your AI Agent**

## Two Ways to Use ArchonDev

### Option 1: Full CLI (Recommended)
The complete AI development system. It manages your entire development process so you can focus on the big picture — not constantly correcting your AI.

```bash
# macOS/Linux:
npm install -g archondev && archon

# Windows PowerShell:
npm install -g archondev; archon
```

**What you get:**
- AI that reads and respects your architecture before writing code
- **Quality Level / Posture** — Right-sized architecture (prototype/production/enterprise)
- Adversarial planning (Architect proposes, Sentinel critiques)
- Automatic quality gates before changes are applied
- Learning persistence — mistakes are remembered and avoided
- **Dependency tracking** — prevent regressions with "what-breaks-what" map
- Bug reporting with root cause analysis
- AI-powered code review for any codebase
- Multi-provider key support with adversarial features

### Option 2: Lite Package
Copy governance files into any project. Works with your existing AI tools: **Cursor, Claude Code, Windsurf, Amp, Copilot, Gemini**, and more.

[Download Lite Packages →](https://archondev.io/download)

**What you get:**
- ARCHITECTURE.md template with best practices
- **Quality Level / Posture** — Tell AI if it's prototype, production, or enterprise-grade
- IDE-specific rule files (.cursorrules, CLAUDE.md, GEMINI.md, etc.)
- Progress tracking templates
- **DEPENDENCIES.md** — Track file-level dependencies to prevent regressions
- **First-Run Walkthrough** — Guided onboarding when AI detects your governance files
- **Code Review Mode** — Structured code review without changing your code
- **Local Database** — Track atoms and learnings in SQLite (no CLI required)
- **Memory Management** — Context handoff protocol for long sessions
- **Task Extraction Protocol** — AI confirms all items before starting, nothing gets forgotten
- **Pre-Deploy Accessibility** — WCAG 2.2 AA check before going live, legal liability warnings
- Works with any AI coding assistant

---

## Commands

| Command | Description |
|---------|-------------|
| `archon` | Interactive mode — just run and follow prompts |
| `archon init` | Initialize in your project |
| `archon login` | Authenticate with ArchonDev (tier selection on first login) |
| `archon upgrade` | Upgrade to BYOK (free unlimited) or Managed plan |
| `archon status` | Show login status and current tier |
| `archon plan <description>` | Create a work item with AI planning (extracts and confirms multi-item requests) |
| `archon execute <atom-id>` | Execute with quality gates |
| `archon list` | List all work items |
| `archon show <atom-id>` | Show details |
| `archon watch` | Live TUI dashboard with status and credits |
| `archon bug report <title>` | Bug report with root cause analysis |
| `archon review init` | Initialize AI-powered code review |
| `archon review analyze` | Scan project and populate review tasks |
| `archon review run` | Run AI review on pending tasks |
| `archon credits` | View credit balance |
| `archon credits add` | Purchase credits |
| `archon credits budget` | Set monthly budget and alerts |
| `archon keys add <provider>` | Add your own API key — BYOK (Bring Your Own Key) |
| `archon keys list` | Show configured API keys by provider |
| `archon preferences` | Interactive settings menu (billing, models, keys, usage) |
| `archon models` | List available AI models |
| `archon deps list` | View file dependency rules |
| `archon deps add` | Add a new dependency rule |
| `archon deps check --files <list>` | Check for downstream impacts |
| `archon deps graph` | Generate Mermaid dependency diagram |
| `archon a11y check` | Run WCAG 2.2 AA accessibility audit |
| `archon a11y fix` | Auto-fix common accessibility issues |
| `archon a11y badge` | Add accessibility compliance badge |
| `archon a11y pre-deploy` | Interactive pre-deployment check |
| `archon seo check` | Run SEO meta tag audit |
| `archon seo fix` | Apply recommended SEO fixes |
| `archon geo identity` | Generate brand identity phrases for AI citation |
| `archon geo schema` | Generate JSON-LD schemas |
| `archon github connect` | Link GitHub account for cloud execution |
| `archon github status` | Check GitHub connection status |
| `archon session save [name]` | Save current session to cloud |
| `archon session resume [id]` | Resume session on another device |
| `archon execute ATOM --cloud` | Execute in cloud (creates PR when done) |
| `archon cloud status` | List cloud executions |
| `archon parallel cloud ATOM-001 ATOM-002` | Queue multiple atoms for cloud execution (Credits tier) |
| `archon index init [--local\|--cloud]` | Initialize semantic indexing |
| `archon index update [--cloud]` | Index changed files |
| `archon index search "query" [--cloud]` | Semantic code search |
| `archon parallel status` | Show parallel execution status |
| `archon deploy` | One-click deploy (auto-detect platform) |
| `archon cleanup check` | Analyze workspace for bloat |
| `archon cleanup run` | Execute cleanup tasks |
| `archon cleanup auto [enable\|disable]` | Enable/disable auto cleanup on start |

**Tip:** Use `archon plan --edit` to adjust title and acceptance criteria before planning.
**Web Checks:** If Archon detects a web project, it prompts to run A11y/SEO/GEO checks and stores your preference in `.archon/config.yaml`.

## Pricing

| Tier | Cost | What You Get |
|------|------|--------------|
| **Free** | $0 | Ultra-cheap models (GPT-5-nano, GPT-4.1-nano, Gemini 2.5 Flash-Lite) — limited usage |
| **BYOK** (Bring Your Own Key) | **$0** | Use your own API keys, **unlimited usage**, all models |
| **Managed Plan** | 10% fee | All models, we handle billing, no API key setup |
| **Claude Subscription** *(coming soon)* | Your existing sub | Use Claude Pro/Max subscription instead of API keys |

No subscriptions. No commitments. Start free, upgrade anytime with `archon upgrade`.

### Claude Pro/Max Subscription Support (Coming Soon)

If you have an existing Claude subscription, you'll soon be able to use it with ArchonDev instead of API keys:

- **Claude Pro** ($20/mo) — Use your Pro subscription
- **Claude Max 5x** ($100/mo) — Higher limits for power users  
- **Claude Max 20x** ($200/mo) — Maximum throughput

This works similarly to how Claude Code allows subscription-based access. We're currently waiting on Anthropic to provide a public OAuth API for third-party applications. **For now, use BYOK (bring your own API key)** — we'll notify you when subscription support is available.

## How It Works

1. **Login & Choose Tier** — Create account, pick FREE/BYOK/Credits
2. **AI Interview** — Natural conversation about your project (or skip to defaults)
3. **Define Your Rules** — ARCHITECTURE.md with boundaries and invariants
4. **AI Reads Rules First** — Every session starts by understanding your architecture
5. **Changes Are Validated** — Quality gates check code before it's applied
6. **Learnings Persist** — Insights saved for future sessions

## First Run Experience

```bash
$ archon

ArchonDev - AI-Powered Development Governance
────────────────────────────────────────────────

Logged in as: you@example.com
Tier: Free (basic models)

⚠️  FREE TIER: Limited usage. Upgrade options:
  • BYOK (FREE) - Unlimited usage with your own API keys
  • Managed Plan - Just 10% fee on AI costs, zero setup
→ Run 'archon upgrade' to unlock unlimited access

→ What kind of project are you building?
  [AI asks natural follow-up questions based on your answers]
  (Type "upgrade" or "help" anytime)

✓ Project initialized!
```

### In-Session Commands

Type these anytime during interactive prompts:

| Command | Description |
|---------|-------------|
| `upgrade` | Open tier upgrade menu |
| `status` | Show login and tier info |
| `keys` | List configured API keys |
| `help` | Show available commands |
| `quit` | Exit ArchonDev |

## Cloud Execution

Run AI agents in the cloud — close your laptop and get a PR when it's done.

```bash
# 1. Authenticate
archon login

# 2. Connect GitHub (one-time setup)
archon github connect       # Opens browser for authorization
archon github status        # Verify connection

# 3. Plan locally, execute in cloud
archon plan "add user settings page"
archon execute ATOM-001 --cloud

# 3b. Queue multiple atoms in parallel (Credits tier)
archon parallel cloud ATOM-001 ATOM-002

# 4. Check progress
archon cloud status         # List all cloud executions
archon cloud logs <id>      # View execution logs
```

The cloud worker clones your repo, runs the Executor agent, creates a feature branch, and opens a PR. You can close your terminal after queuing.
Cloud execution is Credits-only. BYOK and Free tiers run locally.

## Working with Existing Projects

Have a project created by another AI agent? ArchonDev can review it first, then govern future changes.

```bash
# Step 1: Review existing code
cd your-existing-project
archon review init        # Create local review database
archon review analyze     # Scan project structure
archon review run --all   # AI reviews all features
archon review export > review-report.md

# Step 2: Set up governance
archon init --analyze     # Creates ARCHITECTURE.md

# Step 3: Fix issues with governed workflow
archon plan "fix critical issues from review"
archon execute <atom-id>
```

The CLI detects existing projects and suggests this workflow automatically.

## Documentation

- [archondev.io](https://archondev.io) — Main website with animated AI problems story
- [AI Coding Problems Research](docs/ai-coding-problems-research.md) — Market research on AI coding assistant issues

---

*ArchonDev by Jumping Ahead Corp.*
