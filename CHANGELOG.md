# Changelog

All notable changes to ArchonDev are documented here.

---

## [2.19.31] - 2026-02-23

### One-Step Analysis Output for Plan-First Requests

- Plan-first analysis requests now return recommendation + implementation plan + sample draft immediately, without requiring an intermediate `approve plan` round-trip.
- Day-1 content detection was tightened to avoid accidentally pulling day-10/day-11 files into day-1 analysis.
- Added smoother handoff language: users can continue with `save this`/`create atom` only when they want governed implementation.

## [2.19.30] - 2026-02-23

### Analysis-First Planning Flow

- Requests that ask to review/analyze files and provide a plan first now stay in analysis mode after approval, instead of immediately creating atoms.
- Added explicit `create atom` chat directive to convert approved analysis into a governed task only when user confirms.
- Tightened chat execution control: implementation now requires explicit execute wording (`execute atom`, `run atom`, etc.) instead of generic `continue`.
- Added lightweight markdown file analysis summary for analysis-first flows to provide concrete recommendation context before task creation.

## [2.19.29] - 2026-02-23

### Governance Steering Instead of Hard Failure

- Execution now treats architecture boundary/path violations as guided pauses instead of hard failure outcomes.
- Governance violations move atoms to `BLOCKED` with clear corrective guidance, rather than `FAILED` retry semantics.
- Added explicit violation parsing in execute flow so users see actionable path-level guidance.

## [2.19.28] - 2026-02-23

### Proposal Approval Context Fix

- Fixed chat flow where `approve`/`approve plan` could be interpreted as a new task description.
- Added pending proposal context handling so approval directives apply to the previously proposed request.
- Unified approval handling across agent loop and follow-up conversation loop for consistent behavior.

## [2.19.6] - 2026-02-16

### Conversational UX + Usage Transparency

- Fixed interactive chat flow so mixed requests (analyze first, then proceed with a task) no longer stall in analysis-only mode.
- Improved freeform continuity in startup flows to avoid unintended session exits.
- Added tier-aware usage visibility in `archon usage`:
  - `CREDITS`: since-last-top-up context, base cost, platform fee, credits deducted, and per-model spend share.
  - `BYOK`: model usage and estimated provider spend for Today, Last 24 Hours, Last 7 Days, Last 30 Days, and Year to Date.
- Fixed usage/profile resolution in CLI reporting paths and corrected `archon credits history` filtering.

## [2.19.4] - 2026-02-15

### Superpowers-Informed Workflow Hardening

- Added required design-approval gate before plan generation in CLI planning flow.
- Strengthened generated plans with explicit verification and acceptance-check steps.
- Added root-cause investigation capture to bug intake (evidence, reproducibility, hypothesis).
- Enforced two-stage AI review order: spec compliance first, then code quality.
- Updated Lite package AGENTS/scenario guidance with design gate, root-cause gate, and two-stage review checklist.

## [2.19.3] - 2026-02-09

### Content Task Planning Recovery

- Improved detection for content-only tasks (stories, lessons, outlines, visuals).
- Automatically falls back to lightweight planning when adversarial planning fails on content tasks.
- Allows user correction during planning to reclassify content requests without blocking.

## [2.18.3] - 2026-02-08

### Parallel Cloud + Web Checks UI

- Added parallel cloud execution command: `archon parallel cloud <atom-ids...>` (Credits tier only)
- Interactive start flow now offers parallel local/cloud execution selection
- Web project detection surfaces SEO/GEO/A11y menu with last-run status and prompt modes
- Web checks now persist last-run results in `.archon/config.yaml`
- Cloud execution blocked for BYOK and FREE tiers with upgrade guidance
 - Hardened cloud execution gating with server-side tier check and Credits-only RLS policy
 - Web checks prompt no longer defaults to auto-run on Enter

## [2.18.0] - 2026-02-07

### Automated Model Registry Sync

**Pricing is now automatically verified daily against provider documentation.**

#### New Features

- **Automated sync Edge Function** (`model-registry-sync`): Runs daily at 6 AM EST, checks Anthropic, OpenAI, and Google pricing pages, diffs against DB, auto-updates when confidence is high, emails admin with changes or errors.
- **CLI command** `archon models sync`: Manually trigger model registry sync against provider pricing pages.
- **CLI command** `archon models list`: Display all active models with current pricing.
- **Sync audit table** (`model_registry_sync_runs`): Full audit trail of every sync run with diff summaries and confidence scores.

#### Pricing Corrections (Verified 2026-02-07)

| Model | Old (per 1M) | New (per 1M) | Source |
|-------|-------------|-------------|--------|
| gpt-5.2 | $3.00/$12.00 | $1.75/$14.00 | OpenAI Standard tier |
| gpt-5-nano | $0.025/$0.20 | $0.05/$0.40 | OpenAI Standard tier |
| gpt-4.1-nano | $0.05/$0.20 | $0.10/$0.40 | OpenAI Standard tier |
| gemini-2.5-flash-lite | $0.075/$0.30 | $0.10/$0.40 | Google paid tier |

#### New Models Added

- **Claude Opus 4.6** (`claude-opus-4-6`): $5/$25 per 1M tokens — Anthropic's latest, replaces Opus 4.5 as PLANNING tier default
- **GPT-5** (`gpt-5`): $1.25/$10.00 per 1M tokens
- **GPT-5 Mini** (`gpt-5-mini`): $0.25/$2.00 per 1M tokens

#### Safety Guardrails

- Confidence scoring (≥80% required for auto-update) prevents bad parses from corrupting billing
- Email alerts on every change AND on every error
- Model ID renames never automatic — only aliases added
- Deprecation requires 3+ consecutive "missing" runs

#### Files Changed

- `supabase/functions/model-registry-sync/index.ts` — Edge Function
- `supabase/migrations/021_model_registry_sync.sql` — Audit table
- `supabase/migrations/022_model_sync_cron.sql` — Cron schedule
- `src/cli/models-sync.ts` — CLI commands
- `src/core/models/registry.json` — Corrected pricing + new models
- `scripts/update-model-pricing.ts` — Updated KNOWN_PRICING
- `docs/MODEL-MANAGEMENT.md` — Updated documentation

## [2.17.0] - 2026-02-05

### CLI Hardening & Governance Fixes

- CLI no longer imports Supabase SDK directly; uses core client helpers instead.
- Authenticated Supabase clients now used for cloud and billing contexts.
- Quality-gate rollback is scoped to atom-touched files (no full working tree reset).
- Git commit invocation hardened to avoid shell injection.
- API key entry is now masked in `archon keys add`.
- `archon plan --edit` now supports editing title and acceptance criteria.
- Parallel execution uses the current CLI entrypoint and respects `--skip-gates`.
- Added tests for rollback and initialization/plan parsing.

## [2.16.0] - 2026-02-05

### Intent Detection & Explore Flow Fixes

**Fixed critical UX issues with codebase analysis requests and scenario detection.**

#### Problem Identified

Users saying "Please analyze the files in this folder" were incorrectly routed to the Architect/Sentinel planning flow, which:
1. Created atoms for analysis requests (wrong - analysis isn't implementation)
2. Sentinel blocked with many "BLOCKER" errors because analysis ≠ feature implementation
3. "Please" prefix broke regex pattern matching (anchored patterns didn't match)
4. Projects with ARCHITECTURE.md were shown "Starting a new project?" message

#### Fixes

| Issue | Fix |
|-------|-----|
| **Polite prefix breaking patterns** | Added `normalizeForIntent()` to strip "Please", "Can you", "Would you", etc. before pattern matching |
| **Analysis routed to plan()** | Added new `explore` intent type that routes to `runExploreFlow()` instead of creating atoms |
| **Wrong scenario detection** | `hasArchitecture` now triggers `ADAPT_EXISTING`, never `NEW_PROJECT` |
| **No exploration flow** | Created `runExploreFlow()` that scans project and shows summary without Architect/Sentinel |

#### New Intent Type: `explore`

Detected when user says things like:
- "analyze the codebase"
- "review the project"
- "let me know when you are ready"
- "what does this project do"
- "Please analyze the files in this folder"

#### New `runExploreFlow()` Function

Shows project summary:
- Project name, language, framework, package manager
- Source directories and file counts
- Governance status (ARCHITECTURE.md, invariants, protected paths)
- "✓ Analysis complete! I'm ready to work on this project"
- Menu for next actions (plan task, code review, set up governance)

#### Updated `handleAdaptExisting()`

Now accepts natural language input first:
- Detects intent from user's response
- Routes to explore/ad_hoc/app_builder based on confidence
- Falls back to menu only when intent is unclear
- Shows different message when ARCHITECTURE.md already exists

---

## [2.15.0] - 2026-02-05

### Credits Usage Dashboard

**Shows balance and model usage stats on startup for CREDITS tier users.**

- Color-coded balance display (green >$5, yellow $1-5, red <$1)
- Shows total spent in current period
- Top 3 model usage breakdown with costs
- Clear prompts for adding credits or switching tiers

---

## [2.14.0] - 2026-02-04

### Auth & Payment UX Fixes

**Fixed 5 critical issues in the auth/payment flow.**

| Issue | Fix |
|-------|-----|
| Auth timeout bug | Fixed setTimeout never being cleared after OAuth success |
| BYOK without keys | Blocking prompt with 3 options when no keys configured |
| Payment amount unclear | Interactive prompt for amount (default $10, min $5) |
| 404 on payment success | Created success.astro and cancel.astro redirect pages |
| Manage keys menu | Added "k" option in upgrade menu for BYOK users |

---

## [2.12.0] - 2026-02-04

### Billing Audit & Reconciliation System

**Added immutable audit logging and automated reconciliation for billing integrity.**

#### New Features

| Feature | Description |
|---------|-------------|
| **Audit Logging** | Immutable record of all billing events (purchases, deductions, refunds) |
| **Daily Reconciliation** | Automated job verifies expected vs actual balances |
| **Discrepancy Alerts** | Email alerts for balance discrepancies > $1.00 |
| **CLI History** | `archon credits audit` shows complete billing history |

#### New Database Tables (015_billing_audit.sql)

```sql
-- Immutable audit log (insert-only via RLS)
billing_audit_log (
  user_id, event_type, amount_cents,
  balance_before_cents, balance_after_cents,
  metadata, idempotency_key, created_at
)

-- Daily reconciliation records
billing_reconciliation (
  user_id, reconciliation_date,
  starting_balance_cents, purchases_cents, usage_cents,
  expected_balance_cents, actual_balance_cents,
  discrepancy_cents, status, notes
)
```

#### New RPC Functions

```sql
-- Log billing events
log_billing_event(p_user_id, p_event_type, ...) RETURNS UUID

-- Get user billing history
get_billing_history(p_user_id, p_limit, p_offset) RETURNS TABLE
```

#### New Supabase Edge Function

- `billing-reconciliation` - Daily job at 2:00 AM UTC
  - Compares purchases vs usage vs balance for CREDITS users
  - Flags discrepancies > $0.01
  - Emails admin for discrepancies > $1.00

#### CLI Commands

```bash
# View billing audit history
archon credits audit
archon credits audit --limit 50
```

#### Updated RPC (014_atomic_billing.sql)

- `record_usage_and_deduct()` now logs to `billing_audit_log` after successful deductions
- Stripe webhook logs `CREDITS_PURCHASED` events

---

## [2.11.0] - 2026-02-04

### Critical Security Update: Atomic Billing System

**Complete rewrite of the billing system to ensure payment security.**

#### Security Fixes

| Issue Fixed | Description |
|-------------|-------------|
| **Tier Trust Bypass** | Tier now determined server-side by Postgres RPC, not client |
| **Non-Atomic Billing** | Usage recording + credit deduction now atomic in single transaction |
| **Race Conditions** | Row-level locking prevents concurrent overspend |
| **Double Charging** | Idempotency keys prevent duplicate charges on retry |
| **RLS Too Permissive** | Users can no longer directly modify billing fields |
| **Input Validation** | Token counts validated (non-negative, max 10M, integer) |
| **Error Leakage** | Raw DB errors no longer exposed to users |

#### New Database Migration (014_atomic_billing.sql)

```sql
-- New atomic billing RPC function
record_usage_and_deduct(
  p_user_id, p_model, p_provider, p_operation,
  p_input_tokens, p_output_tokens,
  p_atom_id, p_execution_id, p_idempotency_key
) RETURNS JSONB

-- New balance check RPC
check_user_balance(p_user_id, p_estimated_cost_cents) RETURNS JSONB
```

#### Key Security Features

1. **Server-side tier determination** - Client cannot bypass billing by faking tier
2. **Atomic transactions** - FOR UPDATE row locks prevent race conditions
3. **Idempotency** - Unique constraint on `(user_id, idempotency_key)` prevents double-charging
4. **Exact decimal arithmetic** - Postgres NUMERIC prevents float rounding errors
5. **Conservative rounding** - CEIL used consistently to prevent underbilling
6. **Input validation** - Both client-side and database CHECK constraints

#### API Changes (Breaking)

- `UsageRecorder.recordAndDeduct()` no longer accepts `tier` parameter
- `UsageRecorder.estimateCost()` no longer accepts `tier` parameter
- `BillingContext` interface no longer has `tier` field
- `TrackedClientConfig` no longer has `tier` field

#### Migration Required

```bash
# Apply the security migration
npx supabase db push
```

#### Tests
- 675 tests passing (11 new for atomic billing)

---

## [2.10.0] - 2026-02-04

### Multi-Provider AI Client Support

Added full support for OpenAI and Google AI providers alongside Anthropic.

### Database-Driven Model Registry (IMPORTANT)

**Model definitions and pricing are now stored in Supabase for instant updates.**

#### New Database Tables
- `model_registry` - AI model definitions with pricing and tier info
- `model_defaults` - Default models for each category

#### How It Works
1. CLI checks Supabase `model_registry` first (5-minute cache)
2. Falls back to bundled `registry.json` if Supabase unavailable
3. Admin changes to database propagate instantly to all users

#### Key Fields
| Field | Purpose |
|-------|---------|
| `is_free_tier` | If TRUE, available on FREE tier |
| `is_active` | If FALSE, model is hidden |
| `cost_per_1k_input` | Pricing per 1k input tokens |
| `cost_per_1k_output` | Pricing per 1k output tokens |

#### Migration Required
```bash
# Apply the new migration
npx supabase db push
# Or run manually:
# supabase/migrations/013_model_registry.sql
```

#### New AI Clients
- **OpenAIClient** (`src/agents/clients/openai.ts`) - GPT-5, GPT-4.1, o3, o4 models
- **GoogleClient** (`src/agents/clients/google.ts`) - Gemini 2.5, Gemini 3 models
- **Client Factory** (`src/agents/clients/factory.ts`) - Provider-agnostic client creation

#### Provider Support Matrix
| Provider | Models | Free Tier |
|----------|--------|-----------|
| Anthropic | Claude Haiku/Sonnet/Opus | No |
| OpenAI | GPT-5-nano, GPT-4.1-nano, o3, o4 | gpt-5-nano, gpt-4.1-nano |
| Google | Gemini 2.5/3 Flash, Pro | gemini-2.5-flash-lite |

#### TrackedAIClient Updates
- Now supports all providers via factory pattern
- Uses `apiKeys` object instead of single `apiKey` parameter
- Provider auto-detection from model registry

#### New Tooling
- **Pricing Update Script** (`scripts/update-model-pricing.ts`) - Verify and update model pricing
  ```bash
  npx tsx scripts/update-model-pricing.ts --check
  npx tsx scripts/update-model-pricing.ts
  ```

#### Documentation
- **Model Management Guide** (`docs/MODEL-MANAGEMENT.md`) - Comprehensive guide for:
  - Adding new models
  - Updating pricing
  - Model evaluation criteria
  - Provider setup

#### Dependencies Added
- `openai@6.17.0` - OpenAI SDK
- `@google/generative-ai@0.24.1` - Google Generative AI SDK

#### Tests
- 664 tests passing
- New tests for factory utilities

---

## [2.9.0] - 2026-02-04

### CREDITS Tier Usage Tracking (Critical Fix)

The CREDITS tier is now fully functional with proper usage tracking and credit deduction.

### Pricing Architecture Fix (CRITICAL)

**FIXED: 1000x pricing calculation bug and eliminated duplicate pricing sources.**

#### The Problem
- Pricing was duplicated in 3 places: `registry.json`, `tracker.ts`, `anthropic.ts`
- `registry.json` uses per-1k token pricing, but `tracker.ts` assumed per-1M (1000x difference!)
- Model IDs didn't match between files (e.g., `claude-sonnet-4-20250514` vs `claude-sonnet-4-5-20250929`)

#### The Fix
- **Single source of truth**: All pricing now comes from `registry.json` via `getModelCostWithFallback()`
- **Alias support**: Models can have aliases for backward compatibility (e.g., `claude-sonnet` → `claude-sonnet-4-5-20250929`)
- **Conservative fallback**: Unknown models use highest pricing to prevent underbilling
- **Removed duplicates**: Deleted `MODEL_PRICING` from `tracker.ts` and `anthropic.ts`

#### Registry Format (per 1,000 tokens)
| Model | Input $/1k | Output $/1k |
|-------|------------|-------------|
| claude-sonnet-4-5 | $0.003 | $0.015 |
| claude-opus-4-5 | $0.005 | $0.025 |
| claude-haiku-4-5 | $0.001 | $0.005 |
| gpt-5-nano | $0.000025 | $0.0002 |

#### New Tests
- 657 tests passing (12 new for pricing validation)
- Exact pricing assertions to catch regressions
- Alias resolution tests
- Fallback strategy tests

#### What Was Broken
- Users could purchase credits via Stripe (worked)
- Balance was stored in `user_profiles.credit_balance_cents` (worked)
- **But usage was never persisted to `token_usage` table**
- **Credits were never deducted after AI calls**
- **Users were never blocked when balance was insufficient**

#### What's Fixed
- **UsageRecorder service** (`src/core/billing/recorder.ts`) - Persists usage to database and deducts credits atomically
- **TrackedAIClient wrapper** (`src/agents/tracked-client.ts`) - Records usage after every AI call
- **TrackedAdversarialPlanner** - Planning with usage tracking and credit deduction
- **TrackedExecutorAgent** - Execution with usage tracking and credit deduction
- **Pre-flight balance checks** - Blocks operations if credits insufficient
- **CLI integration** - `archon plan` and `archon execute` now track usage for authenticated users
- **Billing display** - Shows credits used and remaining balance after operations

#### Tier Behavior
- **CREDITS**: Usage tracked, 10% markup applied, credits deducted
- **BYOK**: Usage tracked (for analytics), no deduction (user pays provider directly)
- **FREE**: Usage tracked (for quota enforcement), no deduction

#### New Files
- `src/core/billing/recorder.ts` - UsageRecorder service
- `src/core/billing/recorder.test.ts` - 11 tests for recorder
- `src/agents/tracked-client.ts` - TrackedAIClient wrapper
- `src/agents/tracked-planner.ts` - TrackedAdversarialPlanner
- `src/agents/tracked-executor.ts` - TrackedExecutorAgent
- `src/cli/billing-context.ts` - Billing context helper for CLI

### Previous Session Fixes (Included in 2.8.x but not released)

#### Server Deployment Fixes
- Added missing Supabase credentials on Fly.io (SUPABASE_URL, SUPABASE_ANON_KEY, SUPABASE_SERVICE_KEY)
- Added missing Stripe credentials on Fly.io
- Fixed webhook handler to process `checkout.session.completed` events

#### CLI UX Improvements  
- Fixed BYOK flow asking users to run terminal commands while still in interactive prompt
- Now prompts for API key inline during tier selection
- Created checkout success/cancel pages at `website/public/checkout/`

### Tests
- 645 tests passing (11 new for recorder)

---

## [2.5.1] - 2026-02-02

### Website Improvements

#### Compare Page Expansion
- Expanded from 6 features to **25 features** across 5 categories
- Categories: Core Governance, Learning & Memory, Code Quality, Execution & Workflow, Compatibility & Pricing
- Added category header rows with left border accent for visual hierarchy
- Fixed category header visibility in light mode
- Added 4 more differentiators in "Why developers choose ArchonDev" section
- Added feature count summary at bottom of table

---

## [2.5.0] - 2026-02-02

### Major Improvements

#### Streamlined Onboarding Flow
Complete rewrite of the first-run experience:

- **Login required first** — Creates user account before any other steps
- **Tier selection upfront** — Choose FREE/BYOK/Credits before AI calls
- **Single init** — Fixed double-init bug that confused new users
- **Clear output** — No more jumbled messages during setup

#### AI-Powered Conversational Interview
Natural conversation replaces rigid numbered menus:

- AI asks follow-up questions based on your answers
- Infers project details from natural language
- Uses Haiku model for cost-efficient onboarding
- Falls back to simple text prompts when no API key available
- Say "skip" or "just start" anytime to use defaults

#### Update Notifications
Automatic version checking on startup:

- Background check against npm registry (non-blocking)
- Shows banner when new version available
- Displays update command: `npm update -g archondev`

### Technical Changes

- Added `InterviewerAgent` for AI-driven project interviews
- Added `update-check.ts` for version monitoring
- Added `tierConfirmed` flag to config schema
- Removed `displayGovernanceBanner` (caused double-init)
- Simplified interview fallback (text prompts vs numbered menus)

### Tests

- 634 tests passing (was 627)
- Added tests for update checker and interviewer agent

---

## [2.4.0] - 2026-01-29

### New Features

#### Dependency Graph Scheduler (`archon parallel schedule`)
Analyzes atom dependencies to optimize parallel execution:

- Wave-based scheduling using topological sort
- File pattern prediction for conflict detection
- Critical path identification
- Mermaid diagram output for visualization
- Options: `--mermaid`, `--only-ready`, `--max-parallelism`

#### Wave Execution (`archon parallel run-waves`)
Execute atoms in dependency-ordered waves:

- Runs independent atoms in parallel within each wave
- Respects explicit dependencies and file conflicts
- `--dry-run` option to preview execution plan

#### Eject Command (`archon eject`)
Clean removal of ArchonDev from any project:

- Removes `.archon/`, `prd.json`, `progress.txt`, `prompt.md`
- Cleans `package.json` (removes archondev key and archon scripts)
- Cleans `README.md` (removes ArchonDev sections)
- Keeps `ARCHITECTURE.md` by default (useful standalone)
- Options: `--dry-run`, `--force`, `--keep-architecture`, `--keep-readme`
- Works for lite package users

#### Atomic Rollback (`archon revert`)
Revert individual atom commits via git:

- Detects atom commits by patterns: `[ATOM-XXX]`, `[US-XXX]`
- Updates atom status to REVERTED after rollback
- Handles merge conflicts gracefully
- Options: `--force`, `--no-commit`

### New Commands

- `archon parallel schedule` — Analyze dependencies and show execution waves
- `archon parallel run-waves` — Execute atoms in dependency order
- `archon eject` — Remove ArchonDev metadata from project
- `archon history` — Show atom execution history from git
- `archon revert <atom-id>` — Revert specific atom execution
- `archon revertable` — List atoms that can be reverted

### Tests

- 45 new tests (627 total passing)

---

## [2.3.0] - 2026-01-29

### New Features

#### 5-Phase Interview System (`archon interview`)
A structured conversational interview that guides users through defining their project:

- **Phase 1: Discovery** — Elevator pitch, target user, pain points, core problem
- **Phase 2: Features** — MVP features, user stories, post-MVP wishlist
- **Phase 3: Technical** — Framework, database, hosting, authentication
- **Phase 4: Branding** — Project name, tagline, domain, colors
- **Phase 5: Review** — Validate, summarize, freeze for build

#### Project Constitution
Immutable specification document generated from the interview:

- Formal contract between user and AI for what gets built
- Validation ensures all required fields are complete
- Freezing generates SHA-256 hash for integrity verification
- Complexity tier calculation: SIMPLE, MODERATE, COMPLEX, ENTERPRISE
- Build hours and cost estimation based on features/routes/integrations

#### Challenge Mode (Scope Creep Detection)
AI pushback during Phase 5 Review to keep MVPs lean:

- Detects too many MVP features, high complexity, vague features
- Calculates scope score (0-100) to identify scope creep risk
- Suggests features to defer to post-MVP based on complexity/dependencies
- Detects missing critical components (auth, database)
- Generates conversational challenge prompts for user discussion

#### Constitution → Atoms Generator (`archon generate`)
Transforms frozen Constitution into executable prd.json:

- Auto-generates setup, database, auth atoms based on tech stack
- Splits complex features into backend/frontend atoms
- Calculates dependencies between atoms
- Estimates hours per atom and total build time
- Outputs prd.json with US-XXX IDs ready for `archon execute`

### New Commands

- `archon interview` — Start or resume 5-phase interview
- `archon interview show` — Display current Constitution
- `archon interview validate` — Check Constitution for completeness
- `archon interview export [file]` — Export Constitution to JSON
- `archon generate` — Generate prd.json from frozen Constitution
  - `--include-post-mvp` — Include POST_MVP priority features
  - `--dry-run` — Preview without writing file
  - `--output <file>` — Custom output path

### Improvements

- Dynamic interview flow skips questions it can infer from initial message
- Escape hatches: "just start", "skip", "later", "quick start"
- Intent detection classifies app_builder vs ad_hoc requests
- Tech stack hints extracted from natural language

### Tests

- 60+ new tests for interview module
- 582 total tests passing

---

## [2.2.0] - 2026-01-29

### New Features

#### First-Time Tier Selection
When a user logs in for the first time, they now get a clear pricing tier selection:
- **Free** — Ultra-cheap models (GPT-5-nano, Gemini Flash-Lite), $0 cost
- **BYOK (Bring Your Own Key)** — Your own API keys, all models available
- **Credits** — Pay-as-you-go with 10% service fee, all models available

Users can skip the selection (defaults to Free) and switch anytime.

#### New Command: `archon pricing`
Easy tier switching at any time. Shows current tier and allows switching between Free, BYOK, and Credits.

#### FREE Tier Abuse Prevention
Configurable cost limits for FREE tier users to prevent abuse:
- Daily limit: $1.00 (100 cents) — resets at midnight UTC
- Monthly limit: $5.00 (500 cents) — resets on 1st of month
- Limits are easily configurable in `src/core/tiers/restrictions.ts`

#### Silent Session Refresh
Sessions now automatically refresh when nearing expiration (within 5 minutes). Users stay logged in seamlessly across CLI restarts.

### Improvements

#### Credits Minimum Reduced
- Default credits purchase reduced from $10 to $5

#### Database Migration
- Added `daily_spend_cents`, `free_tier_monthly_cost_cents` columns for FREE tier tracking
- Added cron jobs for daily/monthly reset of FREE tier usage

---

## [2.1.2] - 2026-01-27

### Improvements

#### Configurable Cleanup Thresholds
All cleanup thresholds are now configurable in `archon.config.yaml`:
- `progressMaxLines` — Warn when progress.txt exceeds this (default: 500)
- `progressMaxKb` — Warn when progress.txt exceeds this size (default: 100KB)
- `progressArchiveDays` — Archive entries older than this (default: 30 days)
- `cacheRetentionDays` — Delete cache files older than this (default: 7 days)
- `cloudLogRetentionDays` — Delete cloud logs older than this (default: 30 days)
- `archonDirMaxMb` — Warn when .archon/ exceeds this size (default: 10MB)

Config now reads from both project-root `archon.config.yaml` and `.archon/config.yaml` (local overrides project).

#### Documentation
- Added "Cloud Execution" quick-start guide to README

---

## [2.1.1] - 2026-01-27

### New Features

#### Workspace Cleanup Commands
Keep your workspace lean for optimal AI performance.
- `archon cleanup check` — Analyze workspace for bloat (progress.txt, .archon/, cache)
- `archon cleanup run` — Execute cleanup tasks (archive old entries, clear stale cache)
- `archon cleanup auto [enable|disable]` — Enable auto cleanup check on `archon start`
- Auto-archives progress.txt entries older than 30 days to `docs/archive/`
- All 7 lite packages updated with File Cleanup & Maintenance section

### Improvements

#### Terms of Service
- Added arbitration hearing limits: briefs ≤10 pages, hearing ≤2 days

#### Progress Log Archiving
- Old progress.txt entries (v1.0-v1.9) archived to `docs/archive/progress-v1.0-to-v1.9.md`
- Current progress.txt trimmed to v2.0.0+ entries only

---

## [2.1.0] - 2026-01-27

### New Features

#### GitHub Integration
Connect your GitHub account for seamless cloud execution with automatic PR creation.
- `archon github connect` — Link your GitHub account via OAuth
- `archon github status` — Check connection status
- `archon github disconnect` — Unlink your account
- Cloud agents now clone repos, make changes, and create PRs automatically

#### Cloud Semantic Indexing (pgvector)
Semantic search across your codebase stored in Supabase.
- `archon index init --cloud` — Initialize cloud index with OpenAI embeddings
- `archon index update --cloud` — Index files to Supabase pgvector
- `archon index search "query" --cloud` — Semantic search across cloud index
- `archon index status --cloud` — Show cloud index statistics
- `archon index clear --cloud` — Clear cloud index
- **Cost**: Storage ~$0.01-0.30/month, embeddings ~$0.10-0.15/M tokens, queries free

#### Webhook-Triggered Cloud Worker
Cloud worker now uses webhooks for instant job pickup with auto-stop for cost savings.
- Worker starts automatically when jobs are queued
- Auto-stops when idle (no polling costs)
- Supabase Edge Function triggers worker on new executions

### Improvements

#### Daily Admin Stats Email
- Now scheduled via pg_cron at 8:00 AM EST daily
- Shows: user counts by tier, revenue, token usage by model, atoms, executions
- Sent even when there are no customers (shows zeros)

#### Documentation
- Docs page redesigned with wiki-style layout
- Fixed left navigation with section headings
- Tighter vertical spacing throughout
- New sections: GitHub Integration, Cloud Indexing
- Mobile-friendly collapsible table of contents

#### README
- Added 13 new CLI commands to command reference
- GitHub, session, cloud, index, parallel, and deploy commands documented

### Infrastructure

#### Database Migrations
- Migration 008: GitHub OAuth fields on user_profiles, repo fields on cloud_executions
- Migration 009: pgvector extension, code_embeddings table, indexing_jobs table
- Migration 010: Daily stats cron job setup

#### Deployments
- API server redeployed with GitHub OAuth endpoints
- Cloud worker redeployed with HTTP webhook endpoint
- Edge Functions: daily-stats (with cron), trigger-worker

---

## [2.0.0] - 2026-01-27

### Major Features

#### Cloud Agents
Run AI agents in the cloud so you can close your laptop while work continues.
- `archon execute ATOM-001 --cloud` — Queue execution in cloud
- `archon execute ATOM-001 --cloud --watch` — Execute and stream progress
- `archon cloud status` — List cloud executions with status
- `archon cloud cancel [id]` — Cancel running execution
- `archon cloud logs [id]` — View execution logs
- **Billing**: BYOK users pay $0.02/min compute only; Credits users pay tokens + 10% + compute
- **Requires**: GitHub connected via `archon github connect`

#### Cross-Device Sessions
Save your session and continue on another device.
- `archon session save [name]` — Save current session to cloud
- `archon session list` — List saved sessions
- `archon session resume [id]` — Download and restore session
- `archon session sync` — Sync session state after each atom
- Sessions include: pending atoms, progress.txt, ARCHITECTURE.md snapshots

#### Parallel Agents
Run multiple agents simultaneously using git worktrees.
- `archon execute --parallel ATOM-001 ATOM-002 ATOM-003` — Execute in parallel
- `archon parallel status` — Show status of parallel executions
- `archon parallel merge [atomId]` — Merge completed worktrees
- `archon parallel clean` — Remove all worktrees
- Results reviewable as separate PRs or merged sequentially

#### One-Click Deploy
Auto-detect platform and deploy with a single command.
- `archon deploy` — Auto-detect and deploy
- `archon deploy --platform fly` — Specify platform
- `archon deploy --preview` — Deploy to staging
- `archon deploy --dry-run` — Show what would happen
- Supported: Fly.io, Vercel, Netlify, Railway, Render

#### Semantic Indexing
AI-powered codebase search using local Ollama or cloud embeddings.
- `archon index init --local` — Initialize with local Ollama
- `archon index update` — Reindex changed files
- `archon index search "query"` — Semantic search
- `archon index status` — Show index statistics
- Local indexing is free using open-source models (nomic-embed-text)

#### Smart Orchestration
System analyzes project and suggests optimal execution mode.
- `archon preferences execution` — Show execution preferences
- `archon preferences execution-set parallel.mode always` — Set preference
- Modes: `always`, `ask`, `never` for both parallel and cloud
- When mode is `ask`, shows project analysis and prompts user

### Improvements

#### Governance Status Display
- CLI now displays governance status banner on startup
- Shows: posture, invariant count, protected paths, dependency rules, pending atoms
- Lite packages updated with Session Start Protocol (AI announces status)

#### Context Management
- New `ContextManager` class monitors token usage
- Warning at 60% context, mandatory handoff at 80%
- Prevents auto-compact by seamless handoffs
- Pending atoms saved to `.archon/pending-atoms.json` for continuation

#### Learning Verification
- Execute command now verifies progress.txt and AGENTS.md updates
- Logs warnings if learning capture was skipped
- `--no-verify-learning` flag to disable verification

### Lite Package Updates
- All 7 packages updated with Session Start Protocol
- All 7 packages updated with stricter Context Management instructions
- Handoff protocol now mandatory at 80% context

### Website & Documentation
- Homepage: New "Enterprise Features" section with Cloud, Sessions, Parallel, Deploy
- Docs: New sections for Cloud Agents, Sessions, Parallel, Deploy, Indexing
- GitHub README: Updated with v2.0.0 features, removed emojis for professional appearance

### Database
- New `sessions` table for cross-device session persistence
- New `cloud_executions` table for cloud agent tracking
- RLS policies for multi-tenant isolation

---

## [1.9.1] - 2026-01-26

### Website
- **Homepage updates**
  - Added explicit IDE tool references throughout (Cursor, Claude Code, Windsurf, Amp, Copilot, Gemini)
  - Hero subheadline now says "Drop-in for Cursor, Claude Code, Windsurf & more"
  - Added tool logos/badges row in "Choose Your Path" section
  - Changed hero tagline from "Production-ready code" to "Enterprise-ready code"
  - Top CTA button now links to /download instead of /docs
- **Download page updates**
  - Removed background section from instructions banner
  - Moved 3-step instructions directly under hero heading
  - Moved VS Code Extension card up (before GitHub Releases link)
  - Updated file sizes from ~20KB to ~40KB (reflects actual package sizes)
  - Added line break after "Tell your AI:" for better readability

### Documentation
- Updated README with full list of supported IDE tools

---

## [1.9.0] - 2026-01-25

### Added
- **Quality Level / Posture System** — Right-sized architecture that prevents over-engineering
  - New `qualityLevel` section in ARCHITECTURE.md with `posture` field
  - Three posture levels: `prototype`, `production`, `enterprise`
  - AI adjusts recommendations based on posture:
    - **Prototype**: Fast iteration, skip complex patterns, minimal governance
    - **Production**: Secure defaults, basic monitoring, modular design (default)
    - **Enterprise**: Full governance, audit logging, RBAC, incident response, SLOs, compliance
  - Enterprise requirements section for regulated/mission-critical projects
  - Prevents AI from suggesting microservices, event sourcing, multi-region HA for simple projects
  - New project interview includes posture question
- **Architecture Parser Updates**
  - New types: `QualityLevel`, `EnterpriseRequirements`, `Posture`, `DataSensitivity`
  - Parser extracts and validates all quality level fields
- **Architect Agent Improvements**
  - System prompt includes posture guidance
  - Context includes posture, data sensitivity, and compliance requirements
  - Key principle: "Enterprise-grade where required, otherwise minimal"
- **Executor Agent Improvements**
  - Posture-based implementation style in system prompt
  - Prototype: minimal code, fail-fast error handling
  - Production: user-safe errors, structured logging, timeouts
  - Enterprise: bounded retries, correlation IDs, audit logging, idempotency
- **Sentinel Agent Improvements**
  - Posture-based critique rubric
  - Prototype: lenient, only obvious security holes
  - Production: require error handling, basic tests, timeouts
  - Enterprise: BLOCKER if missing reliability story, security boundaries, audit logging
  - New issue types: `OPERATIONAL`, `COMPLIANCE`
- All 7 lite packages updated with:
  - `qualityLevel` section in ARCHITECTURE.md templates
  - Posture interpretation instructions in AGENTS.md
  - Posture-based code generation guidelines
  - Posture-based code review guidelines
  - Updated new-project-interview.md with scope question

### CLI
- `archon init` now accepts `--posture` flag (`prototype`, `production`, `enterprise`)
- Generated ARCHITECTURE.md includes appropriate defaults for chosen posture

---

## [1.8.0] - 2026-01-24

### Added
- **SEO Optimization** — Automated meta tag audit and generation for public websites
  - AI scans existing meta tags, identifies gaps, generates missing/improved tags
  - Covers: title, meta description, Open Graph, Twitter Cards, canonical URL, robots, JSON-LD
  - User approves changes before applying
  - New scenario file: `archondev-scenarios/seo-optimization.md`
  - Trigger phrases: `seo check`, `seo fix`, `add open graph`, `add twitter cards`
- **GEO for AI Search** — Optimize for ChatGPT, Perplexity, Claude citations
  - AI generates 3 candidate 7-word brand phrases with rationales
  - AI generates 3 candidate 50-word descriptions with rationales
  - User selects preferred identity (or requests revision)
  - Generates Organization + Service JSON-LD schema
  - Generates FAQPage schema with 6-8 Q&As
  - Creates atomic claims (≤18 tokens) optimized for AI citation
  - **Uses strong model** (Sonnet 4.5, Opus 4.5, GPT-4.5) for quality identity generation
  - New scenario file: `archondev-scenarios/geo-optimization.md`
  - Trigger phrases: `geo identity`, `geo schema`, `geo faq`, `optimize for AI`
- **Web Optimization Preferences** — User can set preference in `.archon/config.yaml`
  - Options: `yes` (run optimization), `later` (skip now), `no-ask` (never ask again)
  - AI prompts for preference on first website detection
- All 7 lite packages updated with Web Optimization section

### CLI Commands
- `archon seo check` — Run SEO meta tag audit
- `archon seo fix` — Apply recommended SEO fixes
- `archon geo identity` — Generate brand identity phrases
- `archon geo schema` — Generate JSON-LD schemas

---

## [1.7.0] - 2026-01-23

### Added
- **Pre-Deploy Accessibility Check** — Automatic WCAG 2.2 AA compliance checking before deploying live websites
  - Legal liability warnings (ADA, EAA, Section 508)
  - Interactive fix-or-deploy prompt
  - Auto-fix for common issues (contrast, missing alt text, focus outlines)
  - WCAG 2.2 AA badge for compliant sites
  - New scenario file: `archondev-scenarios/pre-deploy-accessibility.md`
  - Trigger phrases: `check accessibility`, `fix accessibility`, `add accessibility badge`
- **CLI Accessibility Commands** (`archon a11y`)
  - `archon a11y check` — Run WCAG 2.2 AA audit on web files
  - `archon a11y fix` — Auto-fix common accessibility issues
  - `archon a11y badge` — Add compliance badge to footer
  - `archon a11y pre-deploy` — Interactive pre-deployment check
- All 7 lite packages updated with accessibility protocol

---

## [1.6.1] - 2026-01-23

### Added
- **Task Extraction Protocol** — When users describe multi-item requests, AI extracts all items, presents a numbered checklist for confirmation, and tracks completion. Prevents lost requirements.
  - New scenario file: `archondev-scenarios/task-extraction.md`
  - New tracking file: `.archon/current-tasks.md`
  - Trigger phrases: `plan these tasks`, `task status`, `what's on my list`
- All 7 lite packages updated with Task Extraction Protocol

---

## [1.6.0] - 2026-01-22

### Added
- **Smart Onboarding** — Three-scenario detection system
  - NEW_PROJECT: Empty folder → Interactive interview
  - ADAPT_EXISTING: Has source files, no progress.txt → Analyze and adapt
  - CONTINUE_SESSION: Has progress.txt entries → Resume with handoff
- **Google Gemini Package** — New lite package with GEMINI.md
- **Scenario Prompts** — `archondev-scenarios/` folder in all 7 packages
- CLI auto-detects project state and routes to appropriate workflow
- File size indicators on download page

---

## [1.5.0] - 2026-01-22

### New Feature: DEPENDENCIES.md
- **File-level dependency tracking** — Track "changing X breaks Y" relationships
- Prevents regressions by warning before changes to files with downstream impacts
- YAML frontmatter format matches ARCHITECTURE.md pattern
- Integrated with ConflictChecker — automatic warnings during `archon execute`

### CLI Commands
- `archon deps list` — View all dependency rules
- `archon deps add --source <path> --dependent <path>` — Add new rule
- `archon deps check --files <list>` — Check files for downstream impacts
- `archon deps graph` — Generate Mermaid diagram of dependencies
- `archon deps init` — Create starter DEPENDENCIES.md

### Lite Package Updates
- All 6 packages now include DEPENDENCIES.md template
- AGENTS.md updated with dependency tracking instructions
- New "🔗 Dependency Tracking" section in workflow

### Core
- `DependencyParser` in `src/core/dependencies/`
- `ConflictChecker` integration for file-level dependency warnings
- 17 new tests for dependency parsing and checking

---

## v1.4.0 — Admin Dashboard & System Monitoring (January 22, 2026)

### Admin Features
- **Daily Stats Email** — Automated daily report sent via SendGrid at 8:00 AM EST
  - User counts by tier (FREE, CREDITS, BYOK)
  - New and active users today
  - Revenue tracking (daily, MTD, all-time)
  - Credit purchases summary
  - Token usage breakdown by model
  - Atom creation/completion stats
  - Execution success/failure rates
- Supabase Edge Function with cron scheduling
- HTML email with styled dashboard layout + plain text fallback

### Infrastructure
- New `supabase/functions/daily-stats/` Edge Function
- SendGrid integration for transactional emails

---

## v1.3.0 — Lite Package Enhancements (January 21, 2026)

### Lite Package Features
- **First-Run Walkthrough** — Guided onboarding when AI detects governance files
- **Code Review Mode** — Structured review for architecture, security, quality, test coverage
- **Local Database** — SQLite atom tracking without CLI (natural language CRUD)
- **Memory Management** — Context handoff protocol with 60%/80% warnings
- **OpenAI Codex Package** — New lite package for Codex CLI (AGENTS.md native support)

### Website
- New animated **AI Problems Story** section on homepage
- Visual problem→solution narrative with CSS animations
- **Dynamic Model Display** — Pricing page fetches current model names from API
- Model names update automatically without website redeployment

### Documentation
- [AI Coding Problems Research](docs/ai-coding-problems-research.md) — Industry statistics from METR, Stack Overflow, Apiiro, CSA, and MIT/Harvard/Microsoft

### Model Registry Updated (January 21, 2026)
**Anthropic:**
- Claude Sonnet 4.5, Claude Opus 4.5 (thinking)
- Claude Haiku 4.5 (fast tier)

**OpenAI:**
- GPT-5.2, o3, o4-mini (thinking)
- GPT-4o Mini (fast tier)

**Google:**
- Gemini 3 Pro, Gemini 2.5 Pro (thinking)
- Gemini 3 Flash, Gemini 2.5 Flash-Lite (fast tier)

---

## v1.1.0 — Existing Projects & Code Review (January 2026)

### New Features
- Interactive Code Review menu option in CLI (option 6)
- Automatic existing project detection — suggests Code Review workflow
- Review progress summary displayed in CLI when database exists
- New "Working with Existing Projects" documentation with 7-step workflow

### Improvements
- CLI detects source files without ARCHITECTURE.md and guides users
- Code Review sub-menu for easier navigation (Analyze, Status, Review next, List)
- Updated README with existing project workflow

---

## v1.0.0 — Initial Release (January 2026)

### New Features
- CLI launch with init, login, plan, execute, list, and show commands
- Architect agent for adversarial planning and debate
- Sentinel agent for architectural validation and gate enforcement
- Executor agent for autonomous code implementation

### Core
- ARCHITECTURE.md governance with YAML frontmatter for invariants and gates
- AGENTS.md learning persistence for cross-session knowledge
- Multi-provider AI support (Anthropic, OpenAI, Google)

---

## v0.9.0 — Beta (December 2024)

### Improvements
- Performance optimizations for large codebases
- Enhanced error handling with detailed feedback
- Improved conflict detection between concurrent changes

### Bug Fixes
- Fixed token counting accuracy for multi-provider setups
- Resolved gate validation edge cases with nested invariants
- Corrected plan serialization for complex dependency graphs

---

## v0.8.0 — Alpha (November 2024)

### New Features
- Basic CLI structure with plan command
- Initial Supabase integration for cloud sync
- Architecture definition parser with validation

### Core
- Initial project setup with TypeScript strict mode
- Foundational agent abstraction layer

---

*ArchonDev by Jumping Ahead Corp.*
