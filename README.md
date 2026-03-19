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
- **Risk scoring** — Numeric 0-100 risk assessment before execution
- **Ship pipeline** — One command: review → test → version → changelog → PR
- **Visual QA** — Headless browser health checks with diff-aware page testing
- **Session retrospective** — Quantitative metrics on atoms, gates, and hotspots

### Option 2: Lite Package
Copy governance files into any project. Works with your existing AI tools: **Cursor, Claude Code, Windsurf, Amp, Copilot, Gemini**, and more.

[Download Lite Packages →](https://archondev.io/download)

**What you get:**
- .archon/active/architecture.md template with best practices
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

### Local Governance SQLite (Dev Only)

Governance data for this repo lives in `.archon/governance.db` and is local-only. It is never synced to Supabase.  
To initialize or refresh it:

```bash
pnpm exec tsx scripts/init-governance-db.ts
```

---

## Commands

| Command | Description |
|---------|-------------|
| `archon` | Interactive mode — just run and follow prompts |
| `archon init` | Initialize in your project |
| `archon login` | Authenticate with ArchonDev |
| `archon config ai` | Switch from Free mode to BYOK and configure provider keys |
| `archon status` | Show login status and current mode |
| `archon plan <description>` | Create a work item with AI planning (extracts and confirms multi-item requests) |
| `archon execute <atom-id>` | Execute with quality gates |
| `archon list` | List all work items |
| `archon show <atom-id>` | Show details |
| `archon watch` | Live TUI dashboard with status |
| `archon bug report <title>` | Bug report with root cause analysis |
| `archon review init` | Initialize AI-powered code review |
| `archon review analyze` | Scan project and populate review tasks |
| `archon review run` | Run AI review on pending tasks |
| `archon usage` | Usage by period and model |
| `archon keys add <provider>` | Add your own API key — BYOK (Bring Your Own Key) |
| `archon keys list` | Show configured API keys by provider |
| `archon preferences` | Interactive settings menu (models, keys, usage) |
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
| `archon governance status` | Show governance status (AGD) |
| `archon governance architecture update` | Update architecture with change reason |
| `archon governance task update` | Update governance tasks |
| `archon governance handoff` | Log handoff + current context |
| `archon governance migrate` | Migrate legacy governance files |
| `archon governance sqlite-init` | Initialize or refresh local governance SQLite DB |
| `archon github connect` | Link GitHub account for cloud execution |
| `archon github status` | Check GitHub connection status |
| `archon session save [name]` | Save current session to cloud |
| `archon session resume [id]` | Resume session on another device |
| `archon execute ATOM --cloud` | Execute in cloud (creates PR when done) |
| `archon cloud status` | List cloud executions |
| `archon parallel cloud ATOM-001 ATOM-002` | Legacy command (disabled in free/BYOK mode) |
| `archon index init [--local\|--cloud]` | Initialize semantic indexing |
| `archon index update [--cloud]` | Index changed files |
| `archon index search "query" [--cloud]` | Semantic code search |
| `archon parallel status` | Show parallel execution status |
| `archon ship` | Ship pipeline: review → test → version → changelog → PR |
| `archon ship --dry-run` | Run all ship checks without committing |
| `archon qa` | Visual QA with headless browser health checks |
| `archon qa --url <url>` | Test specific URL |
| `archon retro` | Session retrospective with quantitative metrics |
| `archon deploy` | One-click deploy (auto-detect platform) |
| `archon cleanup check` | Analyze workspace for bloat |
| `archon cleanup run` | Execute cleanup tasks |
| `archon cleanup auto [enable\|disable]` | Enable/disable auto cleanup on start |

**Notes:**  
- Content-only requests (stories, outlines, lessons, visuals) use lightweight planning to avoid blocking.
- BYOK shows per‑model usage and cost by today/week/month/year in `archon preferences` → “View usage details.”  
- You can paste multi‑line requests into interactive prompts; Archon captures them as a single response.
- Proposal approvals like `approve plan` now bind to the pending proposal context in chat mode.
- Governance boundary/path checks in execute now steer with actionable guidance and set atoms to `BLOCKED` rather than hard failing.
- Analysis-first requests now return recommendations first and accept natural confirmations (`yes`, `go ahead`, `create`) to create governed tasks.
- Chat continuation supports natural directives (`continue`, `move forward`), and path-scope governance blocks now attempt automatic re-plan + retry recovery.
- Chat now preserves your high-signal original request better across exploratory turns (for example: `check folders`), and avoids duplicate plan/execution prompts.
- After explicit approvals in chat (`yes`, `approve plan`), execution continues directly without extra confirmation prompts.

**Tip:** Use `archon plan --edit` to adjust title and acceptance criteria before planning.
**Web Checks:** If Archon detects a web project, it prompts to run A11y/SEO/GEO checks and stores your preference in `.archon/config.yaml`.

## Pricing

| Mode | Cost | What You Get |
|------|------|--------------|
| **Free (Download / Governance)** | $0 | Governance/workflow layer with no built-in AI calls |
| **BYOK (CLI + AI)** | $0 to ArchonDev | Use your own provider keys; provider bills tokens directly |

No paid tiers, no credit purchases, and no Archon token markup.

### BYOK Key Security

- Your API keys are stored locally in `~/.archon/keys.json` (never uploaded to ArchonDev servers).
- Keys are encrypted at rest with AES-256-GCM and the file is set to owner-only permissions (`0600`).
- Archon uses your keys only to call your chosen providers on your behalf.
- If your device is compromised, an attacker could access local files. Treat keys as sensitive secrets.

## How It Works

1. **Login & Choose Mode** — Create account, choose Free or BYOK
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
Mode: Free (download-only governance)

FREE mode: no built-in AI calls.
→ Run 'archon config ai' to enable BYOK for CLI AI features

→ What kind of project are you building?
  [AI asks natural follow-up questions based on your answers]
  (Type "config ai" or "help" anytime)

✓ Project initialized!
```

### In-Session Commands

Type these anytime during interactive prompts:

| Command | Description |
|---------|-------------|
| `config ai` | Open BYOK key setup |
| `status` | Show login and mode info |
| `keys` | List configured API keys |
| `help` | Show available commands |
| `quit` | Exit ArchonDev |

## Cloud Execution (Legacy)

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

# 3b. Queue multiple atoms in parallel (legacy command; disabled in free/BYOK mode)
archon parallel cloud ATOM-001 ATOM-002

# 4. Check progress
archon cloud status         # List all cloud executions
archon cloud logs <id>      # View execution logs
```

The cloud worker clones your repo, runs the Executor agent, creates a feature branch, and opens a PR. You can close your terminal after queuing.
Cloud execution is currently disabled in the free/BYOK model. Use local execution with BYOK keys.

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

## Website Deploy (Bunny.net)

From this repo root:

```bash
./scripts/deploy-website.sh
```

Or from `website/`:

```bash
npm run deploy
```

Required env vars: `BUNNY_FTP_PASSWORD` (or `BUNNY_STORAGE_PASSWORD` depending on script path), `BUNNY_API_KEY`, `BUNNY_PULLZONE_ID`.

## CLI Publish

Build CLI from repo root:

```bash
pnpm run build
```

Stable publish (from repo root):

```bash
npm publish
```

Pre-release publish (required when version contains `-rc.*`):

```bash
npm publish --tag rc
```

Publish commands are run from:

`/Users/davidlevine/Library/CloudStorage/Dropbox/WEB/ArchonDev`

---

*ArchonDev by Jumping Ahead Corp.*
