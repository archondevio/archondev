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
- **Risk scoring** — 0-100 risk assessment before every execution
- **Ship pipeline** — `archon ship`: review → test → version → changelog → PR
- **Visual QA** — `archon qa`: headless browser health checks with diff-aware page testing
- **Session retrospective** — `archon retro`: quantitative metrics on your session

### Option 2: Lite Package
Context-aware intelligence for your existing AI tools: **Cursor, Claude Code, Windsurf, Amp, Copilot, Gemini**, and more. Your AI detects what you're doing and proactively offers the right help — no commands to memorize.

[Download Lite Packages →](https://archondev.io/download)

**Context-Aware Intelligence (NEW):**
- **Fix-First Code Review** — Auto-fixes mechanical issues, only asks about ambiguous ones
- **AI Slop Detection** — 10-item blacklist catches generic AI design patterns, scored A-F
- **Systematic Debugging** — Root cause first, 3-strike hypothesis testing, regression prevention
- **Ship Readiness Dashboard** — Pre-deploy checklist tracks all quality gates across your session
- **Scope Management** — 4 modes (expand/selective/hold/reduce) when scope creep detected
- **Self-Regulation Guardrails** — Blast radius checks, file limits, automatic checkpoints
- **Design Governance** — DESIGN.md as design source of truth with visual audit
- **Completion Status** — Clear DONE/CONCERNS/BLOCKED/NEEDS_CONTEXT reporting
- **Progress Reflection** — Solo retro at natural milestones
- **Expert Review Spec** — Generate a consultant-ready technical spec (gap analysis, approach review, UX enhancement) at any milestone
- **Features Dashboard** — Live HTML page tracking which capabilities you've used, what's available, and what's recommended next

**Governance Foundation:**
- .archon/active/architecture.md template with best practices
- **Quality Level / Posture** — prototype/production/enterprise-grade behavior
- **DEPENDENCIES.md** — File-level dependency tracking to prevent regressions
- IDE-specific rule files (.cursorrules, CLAUDE.md, GEMINI.md, etc.)
- **24 on-demand AI skills** — Design review, debugging, ship readiness, scope review, accessibility, SEO/GEO, color scheme picker, expert review, features dashboard, and more — loaded only when triggered, keeping context lean
- **Skills-based architecture** — 80% smaller context footprint (8.6 KB core vs 42 KB monolithic). Skills load on-demand with progressive disclosure
- **Claude Code: 16 native slash commands** — `/debug`, `/design-review`, `/ship-readiness`, `/code-review`, `/scope-check`, `/expert-review`, `/geo-optimize`, `/seo-check`, `/accessibility`, `/reflect`, `/handoff`, `/plan-tasks`, `/color-scheme`, `/rollback`, `/dashboard`, `/constitution`
- **GEO Optimization** — 7-phase protocol for AI search citation: identity phrases, atomic claims, JSON-LD schemas, and audit ([free tools](https://archondev.io/geo))
- **Task Extraction** — AI confirms all items before starting, nothing gets forgotten
- **Context Handoff** — Memory management for long sessions
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
| `archon` | Chat-first interactive mode — just run and start talking |
| `archon init` | Initialize in your project |
| `archon mode` | Choose local governance mode or BYOK AI mode |
| `archon config ai` | Guided BYOK provider-key setup |
| `archon status` | Show local mode, auth, and project status |
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
| `archon index init` | Initialize local semantic indexing |
| `archon index update` | Index changed files |
| `archon index search "query"` | Semantic code search |
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
- BYOK shows per-model usage and cost by today/week/month/year in `archon preferences` → “View usage details.”  
- You can paste multi-line requests into interactive prompts; Archon captures them as a single response.
- Proposal approvals like `approve plan` now bind to the pending proposal context in chat mode.
- Governance boundary/path checks in execute now steer with actionable guidance and set atoms to `BLOCKED` rather than hard failing.
- Analysis-first requests now return recommendations first and accept natural confirmations (`yes`, `go ahead`, `create`) to create governed tasks.
- Chat continuation supports natural directives (`continue`, `move forward`), and path-scope governance blocks now attempt automatic re-plan + retry recovery.
- Chat now preserves your high-signal original request better across exploratory turns (for example: `check folders`), and avoids duplicate plan/execution prompts.
- After explicit approvals in chat (`yes`, `approve plan`), execution continues directly without extra confirmation prompts.

**Tip:** Use `archon plan --edit` to adjust title and acceptance criteria before planning.
**Web Checks:** If Archon detects a web project, it prompts to run A11y/SEO/GEO checks and stores your preference in `.archon/config.yaml`.

## Pricing

**ArchonDev is Free.** There are no paid tiers, no subscriptions, and no credit card required.

| Mode | Cost to ArchonDev | What You Get |
|------|-------------------|--------------|
| **Download / Governance** | $0 | Governance/workflow layer with no built-in AI calls |
| **CLI + AI (BYOK)** | $0 | Full CLI with AI — bring your own API keys; your provider bills tokens directly at cost |

No Archon token markup. You pay your LLM provider directly at their published rates.

### BYOK Key Security

- Your API keys are stored locally in `~/.archon/keys.json` (never uploaded to ArchonDev servers).
- Keys are encrypted at rest with AES-256-GCM and the file is set to owner-only permissions (`0600`).
- Archon uses your keys only to call your chosen providers on your behalf.
- If your device is compromised, an attacker could access local files. Treat keys as sensitive secrets.

## How It Works

1. **Run `archon`** — Archon inspects the current folder and governance state
2. **Add keys only if needed** — BYOK setup is local-only and optional until you want AI actions
3. **Start in chat** — Ask naturally; Archon decides when to stay conversational vs create atoms
4. **Governance loads first** — Architecture, dependencies, and progress are respected automatically
5. **Changes are validated** — Quality gates and approval policy stay active
6. **Continuity persists** — Handoffs, pending work, and learnings stay local across sessions

## First Run Experience

```bash
$ archon

ArchonDev - AI-Powered Development Governance
────────────────────────────────────────────────

AI mode: Local governance only

No provider keys configured yet.
→ Run 'archon config ai' to enable BYOK for CLI AI features

→ What kind of project are you building?
  [AI asks natural follow-up questions based on your answers]
  (Type "mode" or "help" anytime)

✓ Project initialized!
```

### In-Session Commands

Type these anytime during interactive prompts:

| Command | Description |
|---------|-------------|
| `config ai` | Open BYOK key setup |
| `status` | Show local mode and optional auth info |
| `keys` | List configured API keys |
| `help` | Show available commands |
| `quit` | Exit ArchonDev |

## Cloud Execution (Legacy)

These commands are preserved only for backward compatibility and are hidden from the normal CLI surface.
They are not part of the current local-first product path.

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

- [archondev.io](https://archondev.io) — Main website
- [archondev.io/geo](https://archondev.io/geo) — Free GEO optimization tools (Claude skill + prompt generator)
- [archondev.io/color-schemes](https://archondev.io/color-schemes) — Color Scheme Picker (26 curated schemes)
- [AI Coding Problems Research](docs/ai-coding-problems-research.md) — Market research on AI coding assistant issues
