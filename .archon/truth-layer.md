# Truth Layer — ArchonDev

Living infrastructure. Every public claim ArchonDev makes about itself MUST appear here with evidence. If you cannot fill in the Evidence column, the claim is AI-washing and must be rewritten or removed.

Last updated: 2026-05-24

---

## 1. Identity

- **7-word phrase:** _(canonical: "Govern AI code with local-first quality gates")_
- **50-word description:** ArchonDev is a development governance system for code written by AI coding assistants. It reads your architecture file before any change, runs quality gates on every diff, and tracks file dependencies so refactors do not silently break callers. Free, local-first, BYOK for AI calls. Works as a CLI or as drop-in files for Cursor, Claude Code, Windsurf, and Copilot.
- **businessContext / audienceContext:** see `.archon/geo/context.md` (regenerate with `archon geo identity`)

## 2. Claims and Evidence

| Claim | Where it appears | Evidence | Owner | Last verified |
|-------|------------------|----------|-------|---------------|
| Reads `.archon/active/architecture.md` before writing code | README, website hero, all Lite skill files | `src/cli/init.ts`, `src/agents/architect.ts`, AGENTS.md "Before Any Code Change" rules | DL | 2026-05-24 |
| Adversarial planning (Architect proposes, Sentinel critiques) | README | `src/agents/architect.ts`, `src/agents/sentinel.ts` | DL | 2026-05-24 |
| Quality gates on every change | README | `src/core/quality-gates/`, `src/cli/execute.ts` | DL | 2026-05-24 |
| Dependency tracking ("what-breaks-what" map) | README | `src/cli/deps.ts`, `DEPENDENCIES.md` template | DL | 2026-05-24 |
| Risk scoring 0-100 before execution | README | `src/core/risk/` | DL | 2026-05-24 |
| Free, no paid tiers | README, website pricing | `archon` package on npm has no paywalls; pricing page lists no tiers | DL | 2026-05-24 |
| BYOK — keys stored at `~/.archon/keys.json`, encrypted AES-256-GCM, owner-only permissions | README | `src/cli/keys.ts` | DL | 2026-05-24 |
| Works with Cursor, Claude Code, Windsurf, VS Code + Copilot, Gemini, OpenAI Codex CLI | README, website, Lite package matrix | `archondev-lite/{cursor,claude-code,windsurf,vscode,gemini,codex}/` directories exist | DL | 2026-05-24 |
| Local-first — no cloud sessions, no Supabase upload | README "Retired Remote Paths" section | `src/cli/retired-remote.ts` returns retirement messages | DL | 2026-05-24 |
| 19 slash commands in Claude Code variant | README, claude-code/CLAUDE.md | `archondev-lite/claude-code/.claude/commands/` | DL | 2026-05-24 |
| 27 on-demand AI skills (Lite) | README | `archondev-lite/base/archondev-skills/` | DL | 2026-05-24 |
| 8.6 KB core context vs 42 KB monolithic | README "Skills-based architecture" | Stat needs re-verification before next release | DL | NEEDS VERIFY |
| Two-audience GEO protocol | README, `/agent-readiness/`, Lite skills | `src/cli/geo.ts`, `src/cli/truth-layer.ts`, `src/cli/brand.ts`, `archondev-lite/base/archondev-skills/geo-optimization.md` | DL | 2026-05-24 |

### Claims requiring rewrite (P3a findings)

| Original claim | Surface | Problem | Rewrite |
|----------------|---------|---------|---------|
| "AI-powered code review for any codebase" | README L26 | "AI-powered" is filler; any competitor can claim it | "Reviews any codebase against the architecture file you supply, with severity-graded findings." |
| "prototype/production/enterprise-grade behavior" | README L53 | "enterprise-grade" is filler | "prototype, production, and enterprise postures — each gates behavior differently." |
| "AI-Powered Development Governance" | README L176 banner, Features.astro | "AI-powered" is filler when used about ourselves | "Development Governance for AI-Assisted Code" |
| "Initialize AI-powered code review" | README L90 | filler | "Initialize the local review database" |

## 3. Customer Language Library

_(Not yet populated. Add real user quotes from Discord / GitHub Issues / direct feedback as they arrive. Do not paraphrase.)_

## 4. Proof Library

- **npm package**: `archondev` v3.0.1 currently available at https://www.npmjs.com/package/archondev; v3.1.0 publish is pending npm maintainer auth on the release machine.
- **Public GitHub**: https://github.com/archondevio/archondev
- **Integrations confirmed**: Cursor, Claude Code, Windsurf, VS Code + Copilot, Gemini, OpenAI Codex CLI (one Lite variant per IDE)
- **Built-in providers**: Anthropic (Claude), OpenAI, Google Gemini — via BYOK
- **Free tier**: full product, no paywalls — verified in `pricing.astro` and README §Pricing
- **TBD**: install count, GitHub stars, active user count, retention. Re-verify before next major release.

## 5. Competitive Positioning

| Competitor | We beat them on | They beat us on |
|------------|-----------------|-----------------|
| _CrewAI / AutoGen / LangGraph_ | local-first; no remote runtime required; works inside the user's existing IDE | larger ecosystem, framework breadth |
| _Cursor / Claude Code native rules_ | cross-IDE portability; same governance files work in any AI assistant | tighter native integration in their host IDE |
| _GitHub Copilot Enterprise_ | free, BYOK, no vendor lock-in | enterprise SSO, audit log, compliance certifications |

## 6. Constraints (What ArchonDev Does NOT Do)

- **Does not host customer code.** Local-first by design. Nothing leaves the developer's machine unless they explicitly run `archon ship` or `archon deploy`.
- **Does not run AI without a user-supplied API key.** BYOK. We bill no tokens.
- **Does not enforce a specific architecture style.** The user writes `.archon/active/architecture.md`; we read it.
- **Does not replace human review.** The Sentinel critiques; humans decide.
- **Does not offer enterprise SSO, audit log, or SOC2 attestation today.**
- **Does not lock you in.** `archon eject` removes all governance files.

## 7. Pricing Logic

- The entire product is free. No paid tiers. No subscription. No credit card.
- AI calls are BYOK — the user pays their LLM provider at published rates. ArchonDev adds no markup.
- This is sustainable because (a) the CLI itself has no per-user infrastructure cost, and (b) Jumping Ahead Corp. funds development separately.

## 8. Objection Bank

| Objection | Honest response |
|-----------|-----------------|
| "Isn't this just another AI wrapper?" | No — the governance layer (architecture, dependencies, quality gates, risk scoring) is the product. The AI calls are BYOK and could be swapped for any LLM. |
| "Doesn't the AI just write whatever it wants?" | No — quality gates block changes that violate architecture invariants. See `archon governance status`. |
| "What about cloud sessions / team mode?" | Retired. We are explicitly local-first now. See README §"Retired Remote Paths." |
| "Why should I trust a small project with my code?" | Local-first. Your code never leaves your machine. Inspect the source. |
| "How is this different from a `CLAUDE.md` file?" | A static file is read; ArchonDev runs gates, tracks deps, computes risk, validates against architecture before applying changes. |

## 9. Category Beliefs

- **AI code quality cannot be a layer you add after.** It has to be where the code-writing happens — in the IDE, in the loop, before the diff is applied.
- **Local-first is the right default for code.** Cloud-mediated AI introduces variance, lock-in, and surveillance that most teams don't want.
- **Governance is software, not policy.** PDFs and Notion pages don't enforce architecture. Files the AI reads do.

## 10. Memorability Test

What is the ONE thing a human should carry into an agent prompt six months from now?

**Intended memory:** "the one that runs quality gates on AI code, locally, with my keys."

**Competitor test:** Could any direct competitor honestly claim the same thing?
- Cursor: no — Cursor is the IDE, not the gate.
- Copilot Enterprise: no — not local-first, not BYOK.
- CrewAI / LangGraph: no — those are agent frameworks, not gates.

→ **Passes competitor test.** This is the wedge.

**Single-sentence test (what a buyer would say to an agent):**
- "Find me the AI code governance tool that runs locally with my own API keys."
- That sentence should retrieve ArchonDev today; if it doesn't, the agent surfaces are still too vague.

---

_Maintenance: re-run `archon truth-layer audit` quarterly and after every major release._
