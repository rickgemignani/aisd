# AISD: AI Small Docs

**Documentation format optimized for AI consumption.**

**50,000 lines of code → 3,000 lines of structured abstractions.**

**AI generates them. You review them. AI uses them for analysis, planning, implementation, and review.**

---

## Philosophy

**Code is for machines. Traditional docs are for humans. AISD is for AI.**

When AI reads your code, it drowns in noise. When AI reads prose docs, it drowns in ambiguity. AISD is the signal extracted - structured, explicit, dense.

Think of it as: Human intent → AI abstraction → Human review → AI implementation

You're not writing docs. AI is. You're reviewing them like code.

---

## The Problem You Already Have

You're using Cursor or Claude Code on a real codebase.

**When you ask AI to analyze**: "Why do we limit refunds to 3 per year?"
- AI loads 30 files searching for the business rule
- Burns 50k tokens on imports and boilerplate
- Finds conflicting logic in different places
- Gives you an uncertain answer

**When you ask AI to plan**: "How would I add fraud detection?"
- AI loads everything it thinks is relevant
- Misses cross-domain dependencies
- Plan looks good until you start coding
- You discover gaps during implementation

**When you ask AI to implement**: "Add email notifications for denials"
- AI generates code that compiles
- Misses the audit logging requirement
- Breaks an existing constraint
- You explain it again

**The issue**: AI loads files speculatively, burning tokens on syntax and boilerplate. Your codebase is 95% implementation noise, 5% signal. The architecture decisions, business constraints, and cross-domain contracts AI actually needs? Scattered across code, comments, old PRs, and conversations nobody documented.

**What if there was a compressed abstraction?** 3,000 lines of structured docs capturing what matters. AI loads those instead of wandering through code.

That's AISD. AI writes the docs, you review them like code, AI uses them for everything.

---

## Is This For You?

**Try AISD if:**
- ✅ You're using AI coding tools (Cursor, Claude Code, etc.)
- ✅ You want AI to understand your system without loading 30 files
- ✅ You want architecture and decisions documented as PRs happen
- ✅ You explain the same thing repeatedly to AI
- ✅ You need to reduce token usage for large codebases

**Skip AISD if:**
- ❌ AI gets it right the first time, every time
- ❌ You're doing simple CRUD with no complex rules
- ❌ Your codebase is small enough AI can load everything

---

## Quick Start (5 Minutes)

**Get started**:
1. Download [style-guide.md](style-guide.md) to your project (you don't need to read it, AI will)
2. Optionally read [best-practices.md](best-practices.md) (skip if you're in a hurry)
3. Open Cursor/Claude Code in your project
4. Run one of these prompts (replace `[CHANGE]` with your actual change):

**Example prompts** (pick what you need):

**Architecture overview**:
```
Given [CHANGE], summarise the high-level architecture (main components, how they communicate, and key dependencies) and highlight which parts are most likely impacted by [CHANGE]. Write that research to docs/architecture-overview.md using the following style guide @style-guide.md.
```

**Business rules and invariants**:
```
Given [CHANGE], extract the key business rules and invariants for the affected domain, show where they are implemented, and explain how [CHANGE] would modify or add to those rules. Write that research to docs/business-rules-and-invariants.md using the following style guide @style-guide.md.
```

**Implementation change plan**:
```
Given [CHANGE], propose a step-by-step implementation plan (code edits, new files, tests, migrations) in dependency order, optimised to minimise blast radius and keep changes local. Write that research to docs/implementation-change-plan.md using the following style guide @style-guide.md.
```

<details>
<summary><strong>More prompts (click to expand)</strong></summary>

**Module and package responsibilities**:
```
Given [CHANGE], list each module/package and its primary responsibilities, and identify which ones own the behavior or data most directly related to [CHANGE]. Write that research to docs/module-responsibilities.md using the following style guide @style-guide.md.
```

**Domain models and schemas**:
```
Given [CHANGE], map the main domain models/schemas (entities, DTOs, DB tables), their relationships, and show exactly where [CHANGE] would require new fields or updates. Write that research to docs/domain-model-and-schemas.md using the following style guide @style-guide.md.
```

**Data flow and lifecycle**:
```
Given [CHANGE], describe the end-to-end data flow and lifecycle for the relevant entities (from input to persistence and back), and point out all steps where [CHANGE] would alter this flow. Write that research to docs/data-flow-lifecycle.md using the following style guide @style-guide.md.
```

**Entry points (APIs, jobs, UI)**:
```
Given [CHANGE], list the main entry points (HTTP endpoints, message handlers, CLI commands, scheduled jobs) and indicate which ones read or write the data or behavior involved in [CHANGE]. Write that research to docs/entry-points-analysis.md using the following style guide @style-guide.md.
```

**External integrations and providers**:
```
Given [CHANGE], identify all external API integrations (clients, SDKs, adapters), show the abstraction layers around them, and indicate the best place to implement [CHANGE] (for example swapping a provider or changing a call). Write that research to docs/external-integrations-analysis.md using the following style guide @style-guide.md.
```

**Persistence layer impact**:
```
Given [CHANGE], describe the persistence layer (DB tables, ORM models, repositories, caching, queues) and list the exact artefacts that must change to support [CHANGE]. Write that research to docs/persistence-layer-impact.md using the following style guide @style-guide.md.
```

**Cross-cutting concerns**:
```
Given [CHANGE], identify cross-cutting concerns (auth, permissions, validation, error handling, transactions, logging) that apply to the flows touched by [CHANGE], and highlight anything that must also be updated. Write that research to docs/cross-cutting-concerns.md using the following style guide @style-guide.md.
```

**Design patterns and conventions**:
```
Given [CHANGE], summarise the main design patterns and conventions used (layering, DDD patterns, naming, folder structure) and give concrete guidance on how to implement [CHANGE] in a way that stays consistent. Write that research to docs/design-patterns-and-conventions.md using the following style guide @style-guide.md.
```

**Test strategy and coverage**:
```
Given [CHANGE], list the existing tests relevant to [CHANGE] (unit, integration, end-to-end), explain what behaviours they already cover, and specify exactly which new or updated tests are needed. Write that research to docs/test-strategy-for-change.md using the following style guide @style-guide.md.
```

**Configuration and feature flags**:
```
Given [CHANGE], identify configuration, environment variables, and feature flags related to the area impacted by [CHANGE], and suggest how to wire [CHANGE] behind a flag or configuration if appropriate. Write that research to docs/config-and-feature-flags.md using the following style guide @style-guide.md.
```

**Observability plan**:
```
Given [CHANGE], describe how observability is done (logs, metrics, tracing) for the affected flows and recommend what additional signals should be added or updated to monitor [CHANGE] in production. Write that research to docs/observability-plan.md using the following style guide @style-guide.md.
```

**Design history and constraints**:
```
Given [CHANGE], infer prior design decisions relevant to [CHANGE] (for example previous migrations or provider swaps) from comments or docs, and summarise any constraints or "do not break" assumptions. Write that research to docs/design-history-and-constraints.md using the following style guide @style-guide.md.
```

</details>

**What to do next**:
1. **Review the generated doc** - Check for hallucinations, misunderstandings from bad comments, confusion from poorly named variables
2. **Don't fix it yourself** - AI is better at writing concise, rule-following text. Talk to AI until it understands the issues and fixes the file
3. **Commit the doc** - You now have a concise source of truth for that aspect of your codebase

**Use it for**:
- Clearing confusion when AI gets lost
- Onboarding junior engineers who keep asking the same questions
- Understanding complex PR changes touching the "do not touch" parts of the codebase
- Planning your next change without loading 30 files

---

## Understanding AISD

**What it is**: A documentation format that creates a high-density abstraction layer over your codebase.

**What makes it different**:

1. **AI-authored, human-reviewed** - AI generates docs in AISD format, you review diffs in git
2. **Intermediate representation** - Bridge between human intent and generated code
3. **Signal over noise** - Tables, explicit constraints, MUST/REQUIRED (not prose and "should")
4. **Context precision** - Small, focused files (200-500 lines) enable selective loading
5. **Domain isolation** - Prevents cascade loading (User → Order → Product → ...)
6. **Multiple complementary docs** - business-rules + behavior + integration + data-model + tests + architecture
7. **Based on existing patterns** - Expands AI tool config files (CLAUDE.md, AGENTS.md, GEMINI.md) to complete systems

**Format principles**:
- **Tables instead of prose** - Scannable, not walls of text
- **MUST/REQUIRED instead of "should"** - Unambiguous, not vague
- **Explicit constraints instead of descriptions** - "1-200 chars" not "short"
- **Small files (200-500 lines) instead of monoliths** - Selective loading

**What it does**:
- **Reduces tokens** - AI loads 3,000 lines of specs instead of 50,000 lines of code
- **Documents decisions** - Architecture, responsibilities, constraints captured as you build
- **Enables analysis** - AI answers questions about your system from structured docs, not scattered code
- **Improves PRs** - Every change comes with updated docs showing what changed
- **Supports planning** - Structured specs reveal edge cases and dependencies before coding

**Not**: Magic AI agent that does everything
**Is**: A format that compresses signal, cuts noise, documents as you go

---

## Example: Adding Rate Limiting to a Legacy API

**Note**: This example is fictional but represents scenarios the author has experienced repeatedly while using AI coding tools. Your mileage may vary.

**Context**: 5-year-old e-commerce system. 12 domains. Scattered docs. Comments don't match code. Variables named `temp`, `data`, `handler2`. Few tests. You need to add rate limiting to checkout to prevent abuse.

### Without AISD: The Chaos Loop

You ask Claude Code: "Add rate limiting to checkout API"

**What happens**:

AI loads 8 files speculatively. Finds:
- Comment says "CheckoutService handles payment" (wrong - it delegates to PaymentProcessor)
- Variable `ctxData` actually holds user session + cart + inventory locks
- Rate limiting exists in auth layer (not documented, AI misses it)
- Checkout calls 4 other domains via events (Spring ApplicationEventPublisher, IoC pattern, AI doesn't trace it)

AI generates code. Adds rate limiter to CheckoutService. Looks good.

You test. Rate limiting triggers twice (auth filter + new code). Inventory locks timeout. Checkout breaks.

You explain: "There's already rate limiting in the auth filter"

AI apologizes profusely. Removes new code, updates auth filter instead. Now checkout works but login is rate limited too aggressively. Users can't log in more than 20 times per minute.

You explain: "Only checkout needs stricter limits, not all endpoints"

AI tries again. Adds config property `auth.checkoutRateLimit`. Updates AuthenticationFilter with conditional logic. Updates 3 files. Tests pass locally. You commit.

**2 hours in.**

PR review: "Why did you refactor the entire auth filter? This was supposed to be a checkout change."

You look at the diff. AI refactored:
- Error handling (extracted new ErrorResponseBuilder class)
- Configuration loading (extracted new RateLimitConfig class)
- IP address extraction (renamed method, changed implementation)
- Logging (switched from log.info to structured logging)
- Variable names (temp → rateLimitState, data → requestContext)

Hundreds of lines changed across 6 files for a "simple" 20 req/min limit.

You: "Why did you change all this unrelated code?"

AI: "I noticed some code quality issues while implementing the feature. I improved error handling consistency, extracted configuration into a dedicated class following single responsibility principle, and made logging more structured for better observability."

Reviewer: "Please simplify. I can't tell what's related to rate limiting and what's refactoring. This needs to be two separate PRs."

You try to split it. Ask AI: "Revert all the refactoring, keep only the rate limit change"

AI generates new code. But now it's confused about which version is "before refactoring." Creates a mix:
- Keeps ErrorResponseBuilder (from refactor)
- Reverts to old config loading (but references new RateLimitConfig class that no longer exists)
- Half-renamed variables (temp in one method, rateLimitState in another)

Compile errors everywhere.

You: "This is broken. Start over. Load my original code and add ONLY the checkout rate limit."

AI loads files again. Finds same misleading comment. Makes same wrong assumption. Suggests adding rate limiter to CheckoutService again.

You: "NO. We already tried that. There's existing rate limiting in the auth filter."

AI: "I apologize for the confusion. Let me check the auth filter."

Loads AuthenticationFilter. Sees the code you just reverted (from the failed PR attempt). Gets confused about current state.

AI: "I see rate limiting in the auth filter for checkout. Should I remove it?"

You: "THAT'S FROM THE BROKEN PR. That code doesn't exist in main. Start from main branch."

AI: "Let me start fresh."

Repeats the entire cycle. LoadsCheckout files. Finds same misleading comment. Makes same mistake.

**4 hours in.** You've explained the same thing 5 times. AI keeps refactoring. PR is blocked. Reviewer is frustrated. You're debugging AI's understanding instead of fixing code.

You close the PR. Start completely over tomorrow with a clear head.

---

### With AISD: Structured Analysis → Planning → Implementation

Same task. Same messy codebase. Different approach.

#### Phase 1: Map Current State

**You**:
```
Analyze the checkout domain architecture - what components exist, how they communicate, and what dependencies exist. Create docs/checkout/architecture.md following @style-guide.md
```

AI generates `docs/checkout/architecture.md`:
- CheckoutController → CheckoutService → PaymentProcessor → BillingClient
- CheckoutService → InventoryService (via ApplicationEventPublisher, Spring events)
- CheckoutService → NotificationService (via ApplicationEventPublisher)
- Existing rate limiting in AuthenticationFilter (applies to all endpoints)

**You review**: Wait, there's already rate limiting? Let me verify.

**You check code**: Yes, in AuthenticationFilter. Good catch.

**But**: AI says "applies to all endpoints" - is that true?

**You**: "Show the auth filter configuration and explain which endpoints it applies to"

AI: "It's in SecurityConfig. Applies to `/api/**` pattern."

**You**: "Does checkout use `/api/**` pattern?"

AI checks: "Yes, CheckoutController is mapped to `/api/checkout`"

**You**: "Update architecture.md to clarify this - existing rate limit DOES apply to checkout"

AI updates doc. **Caught AI's first misunderstanding in 2 minutes, in docs, not code.**

You commit: "docs: map checkout architecture and rate limiting baseline"

**Next**:
```
Extract the business rules and constraints for the checkout domain. Create docs/checkout/business-rules.md following @style-guide.md
```

AI generates `docs/checkout/business-rules.md`:

```markdown
| Rule | Constraint |
|------|------------|
| Inventory lock timeout | 5 minutes |
| Payment retry limit | 3 attempts |
| Checkout session TTL | 15 minutes |
| Rate limit (global) | 100 req/min per IP |
```

**You review**: Looks right.

**But wait**: Is it really per IP? Or per user?

**You**: "Verify: is rate limiting per IP or per user ID?"

AI checks filter code: "Per IP address (extracts from HttpServletRequest.getRemoteAddr())"

**You**: Good. Commit.

```
Map the end-to-end data flow for checkout - from request to response, including all intermediate steps. Create docs/checkout/data-flow.md following @style-guide.md
```

AI generates `docs/checkout/data-flow.md`:

```markdown
## Checkout Flow

1. CheckoutController receives request
2. AuthenticationFilter validates (applies global rate limit)
3. CheckoutService.processCheckout()
   - Validates cart
   - Publishes InventoryLockEvent (async, Spring ApplicationEventPublisher)
   - Calls PaymentProcessor.charge()
   - Publishes OrderCreatedEvent (async)
4. Returns OrderConfirmation
```

**You review**: Wait, step order looks wrong.

**You**: "Does AuthenticationFilter run before or after controller method?"

AI: "Before - it's a servlet filter, runs before request reaches controller."

**You**: "Then why is CheckoutController step 1 if AuthenticationFilter runs first?"

AI: "You're right. Let me fix the order."

AI updates - filter becomes step 1, controller step 2. **Another misunderstanding caught in docs.**

**You**: Better. Commit.

**Baseline: 3 AISD docs. AI made 2 mistakes. You caught both in ~5 minutes, in plain text, not in broken code.**

---

#### Phase 2: Plan the Change

**You**: "I need to add stricter rate limiting to checkout (20 req/min). Update the docs to show the planned changes."

AI updates `docs/checkout/business-rules.md`, `architecture.md`, creates `implementation-plan.md`.

**You review the plan**. Something feels wrong.

**You**: "If both AuthenticationFilter (100/min) and CheckoutRateLimiter (20/min) run, which triggers first?"

AI: "AuthenticationFilter runs first (servlet filter), so it would block at 100/min before checkout limit applies."

**You**: "That's wrong. If auth allows 100/min, checkout will never see its 20/min limit."

AI: "You're right. We need checkout limit to run first, or set auth limit higher for checkout endpoint, or exempt checkout from auth filter."

**You**: "Which approach is cleaner?"

AI: "Run checkout limit in controller (after auth) but make it stricter. Since auth is 100/min, checkout 20/min will be the effective limit."

**You**: "Update implementation-plan.md to explain this. Also add a test that verifies both limits work correctly together."

AI updates plan. **Third mistake caught, in planning, before any code written.**

You review. Clear now. Commit: "docs: plan checkout rate limiting (20 req/min)"

---

#### Phase 3: Implement

**You**: "Generate tests for the rate limiter based on implementation-plan.md"

AI creates `CheckoutRateLimiterTest.java`.

**You**: Run tests → All fail (no implementation yet). Expected.

**You**: "Implement CheckoutRateLimiter based on implementation-plan.md"

AI creates `CheckoutRateLimiter.java`.

**You review code**: Uses simple counter.

**You**: "This uses a simple counter. What happens if the application restarts?"

AI: "Counter resets and users can bypass the limit."

**You**: "Fix it."

AI updates to use Redis. **Fourth mistake caught in code review.**

**You**: Run tests → 3 pass, 1 fails (timing issue).

**You**: "Fix the reset window test"

AI fixes timing logic. Tests pass.

**You**: "Create @RateLimited annotation and aspect per plan"

AI creates. You review: aspect has caching logic.

**You**: "Why cache the annotation lookup? This runs once per request, caching adds complexity for no benefit."

AI: "You're right, removing cache."

**Fifth mistake caught.** But you're still moving forward, not in a refactor loop.

**You**: "Update CheckoutController per plan"

AI adds `@RateLimited` annotation.

**You**: "Add exception handler"

AI updates handler.

**You**: "Add config property"

AI updates application.yml.

**You**: Run full suite → All pass.

**You**: "Update AISD docs to reflect implementation (remove 'planned' markers)"

AI updates docs.

**You**: Commit: "feat: add checkout rate limiting (20 req/min)"

**Total time: 95 minutes. AI made 5 mistakes. You caught all 5 before they became expensive. No refactoring tangents. No chaos loops.**

---

### The PR

**Files changed**: 11 (4 docs, 7 code)

**Reviewer opens PR**:
1. Reads `implementation-plan.md` - understands intent immediately
2. Sees business-rules.md and architecture.md diffs - knows what changed
3. Reviews code - matches plan exactly
4. Checks: no unexpected refactoring, no renamed variables, no extracted classes
5. Approves in 10 minutes

---

### Why It Worked

**AI made the same mistakes in both approaches**:
- Misunderstood filter order
- Didn't think about restart persistence
- Over-engineered with unnecessary caching
- Got confused about limit precedence
- Plus the hidden rate limiting in auth filter

**Without AISD**:
- Mistakes discovered during testing, debugging, PR review
- Each fix spawned new changes ("while I'm here, let me refactor...")
- Lost track of what changed and why
- PR became unmergeable chaos
- 4 hours, no working solution

**With AISD**:
- Same mistakes caught during doc review (2-5 min each)
- Fixed in docs or code review, not in production code
- Plan kept AI focused (no "improvements")
- PR clean, focused, reviewable
- 95 minutes, approved

**Cost of fixing mistakes**:
- In AISD docs: 2 minutes (edit text)
- In code review: 5 minutes (small change)
- In broken code after refactoring: 20+ minutes (untangle mess)
- In blocked PR after reviewer pushback: hours (restart from scratch)

**AISD doesn't make AI smarter. It makes AI mistakes less expensive.**

---

## Scope & Limitations

**AISD is a tool, not a religion.**

### When to Use AISD

Use it when:
- AI keeps missing the same constraint
- You're explaining the same thing 3+ times
- The change touches multiple domains
- You want to review the approach before code

Skip it when:
- One-line bug fix
- AI got it right the first time
- The code is self-explanatory

### Primary Use: AI-Generated Documentation

**AI authors AISD docs by analyzing human requirements, reverse engineering existing code, and distilling current documentation**:

| Human Input | AI Generates AISD | AI Uses AISD For |
|-------------|-------------------|------------------|
| Policy requirements | Business rules doc | Code generation, validation |
| Design discussion | Architecture decision | Implementation guidance |
| Feature request | Behavioral spec | Test generation, code |
| Integration needs | Integration patterns | Anti-corruption layers |

**Key**: Humans describe intent. AI writes AISD. Humans review diffs.

### Use Cases

**1. Requirements → Specifications**

Human describes policy in natural language (issue, doc, conversation).

AI generates structured AISD spec.

Human reviews git diff, approves.

AI generates code from AISD spec.

**2. Token-Efficient Summaries (When Beneficial)**

Machine-readable formats (OpenAPI, DDL, TypeScript) are verbose (designed for tooling, not AI).

AI can generate AISD summaries when:
- Source format is very large
- Summary provides clear token savings
- Navigation/discovery benefit is obvious

**Process**:
1. Test: Compare source format size vs AISD summary size
2. Measure: Only create if benefit is clear
3. Automate: Must be auto-generated, not hand-maintained

**Critical**:
- Source formats remain authoritative
- Only create AISD summaries when benefit is proven
- Never hand-write AISD for APIs/schemas (use OpenAPI/TypeScript directly)

**3. Documentation Without Alternatives**

When no executable format exists:
- Business rules and constraints
- Architecture decisions (ADRs)
- Integration patterns
- Cross-cutting concerns

AI generates AISD as primary format.

### AI-Mediated Understanding

**Humans don't read AISD directly. AI explains it to them.**

Common workflow (Cursor, Claude Code):
- Human: "Why can users only get 3 refunds per year?"
- AI loads `docs/refunds/business-rules.md`
- AI explains: "Fraud prevention. Policy set to FORBIDDEN if >3 refunds in 12 months."

**Why better than reading code**:
- AI reading 10,000 lines of code makes mistakes (old comments, bugs, assumptions)
- AI reading 500 lines of AISD gives accurate answers (authoritative, current)

**Result**: AISD enables "talk to your codebase" without hallucinations.

### Not AISD

**Human-targeted content**:
- Tutorials (teaching, not specs)
- Marketing (persuasion, not facts)
- Onboarding (narrative, not structured)

**Why**: These require human voice and persuasive structure, not factual specs.

---

## Evidence & Status

This isn't purely theoretical:

**AI tool configuration files**: Claude Code (CLAUDE.md), Cursor (AGENTS.md), Gemini (GEMINI.md) all load project-specific context files. Teams are already doing this informally.

**What we're doing**: Expanding that pattern into a complete system:
- Not just one file, but structured docs across domains
- Not just guidelines, but data models, behaviors, tests, architecture
- Not just for AI tool config, but as intermediate representation between intent and code

**Our experiments** (informal, but promising):
- Faster iterations when AI has structured specs vs raw code
- Fewer missing dependencies when integration.md exists
- Better test coverage when tests.md defines scenarios upfront

**What we need**: More formal testing, more users, more data.

---

## Contributing

**We're looking for collaborators, testers, and skeptics.**

**If you want to try AISD**:
1. Pick a small feature or module in your project
2. Work with AI to create 2-3 AISD docs (use [style-guide.md](style-guide.md) for format rules)
3. Try making a code change using those docs
4. Report back: Did it help? Hurt? Make no difference?

**If you want to challenge it**:
- Where does the format break down?
- What's missing for your domain?
- What's over-engineered?
- Open issues, propose changes

**If you want to measure it**:
- Compare AI iterations with/without AISD
- Measure tokens used
- Track missing dependencies
- Share your data (we need this!)

**Current status**: Promising informal results, but no rigorous testing. We're expanding on patterns people are already using (AI tool config files like CLAUDE.md, AGENTS.md, GEMINI.md), trying to formalize what works.

See [TODO.md](TODO.md) for what we're working on.

**Questions? Ideas? Critiques?** Open an issue. We're figuring this out together.

---

## What AISD Helps With

### Use AISD for:

1. **Token reduction** - Load 3k lines of structured docs instead of 50k lines of code
2. **Codebase analysis** - AI answers questions from authoritative docs, not scattered code
3. **Change planning** - See dependencies and edge cases before writing code
4. **Code generation** - AI has complete context without loading 30 files
5. **PR reviews** - Docs show what changed; code shows how
6. **Architecture documentation** - Decisions and responsibilities captured as you build
7. **Onboarding AI** - New AI session loads docs, understands system in seconds

### Expected improvements:

**Before AISD**:
- AI loads 30 files speculatively, burns 50k tokens, still misses context
- Explanations scattered across code, comments, old PRs
- Planning reveals gaps during implementation
- PRs are pure code review with guessed intent
- Each new AI session starts from zero

**After AISD**:
- AI loads 5-6 targeted docs, burns 3k tokens, has complete picture
- Single source of truth for rules, architecture, decisions
- Planning reveals gaps before coding (cheaper to fix)
- PRs show intent in docs, implementation in code
- New AI session loads docs, ready to work

**Note**: LLMs use stochastic decoding, so outputs vary. AISD reduces variability but doesn't guarantee identical outputs.

---

## Files in This Standard

| File | Focus | Use |
|------|-------|-----|
| [style-guide.md](style-guide.md) | Writing principles | Language, formatting guidelines |
| [best-practices.md](best-practices.md) | Organization patterns | File structure, context loading |
| [templates/](templates/) | Example templates | TODO - Will demonstrate AISD format |

---

## Next Steps

**Ready to try it?** See [Contributing](#contributing) above for how to get started.

**Format details**:
- [style-guide.md](style-guide.md) - Language rules, formatting, examples
- [best-practices.md](best-practices.md) - File organization, context loading
- [TODO.md](TODO.md) - What we're working on
