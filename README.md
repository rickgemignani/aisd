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
7. **Based on existing patterns** - Expands CLAUDE.md approach to complete systems

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

## Example: Fraud Detection

**Scenario**: Adding fraud detection to a refund system.

Create high-density maps of what matters. AI loads those instead of wandering through code.

**Step 1: Create AISD docs for the refund system**

Working with AI (using AISD format rules), you generate:

**`docs/refunds/business-rules.md`** (40 lines)
```markdown
| Condition | Rule |
|-----------|------|
| Time window | Within 30 days of purchase |
| Product condition | MUST be unused |
| Refund limit | Max 3 per user per 12 months |
```

**`docs/refunds/behavior.md`** (120 lines)
```markdown
## ProcessRefund

**Preconditions**:
- Purchase within 30 days
- Product unused
- User refund count ≤3 in past 12 months

**Returns**: Success | Denied(reason)

**Side effects**: Records refund in user history
```

**`docs/users/integration.md`** (80 lines)
```markdown
## Refunds Integration

**Provides**: GetRefundHistory(user_id, days) → count

**Required data**:
- user_id
- refund_timestamps[]
```

**`docs/refunds/data-model.md`** (100 lines)
```markdown
## Refund

| Field | Type | Constraints |
|-------|------|-------------|
| id | UUID | Required |
| user_id | UUID | Required, FK to users |
| amount | Decimal | >0 |
| timestamp | DateTime | Required |
| reason | String | 1-500 chars |
```

**`docs/architecture.md`** (updated, 250 lines total)
```markdown
## Cross-Domain Dependencies

- refunds → users (fraud check)
- refunds → payments (transaction reversal)
- refunds → inventory (restock)
```

**`docs/refunds/tests.md`** (60 lines)
```markdown
| Scenario | Refunds (12mo) | Expected |
|----------|----------------|----------|
| New user | 0 | Allow |
| At limit | 3 | Allow |
| Over limit | 4 | Deny |
| Old refunds | 4 (13mo ago) | Allow |
```

**Total**: ~650 lines of AISD docs

**Step 2: Review and commit the abstraction**

You see the complete system design in structured form. Way easier to review than scattered code.

**Step 3: AI uses AISD to generate code**

**Without AISD**: AI loads 30 files (12,000 lines), burns 50k tokens just understanding the system

**With AISD**: AI loads 6 docs (650 lines), burns 3k tokens, has complete picture

Generates:
- Refund service (fraud validation)
- User service updates (history tracking)
- Database migration (refund_history)
- All 4 test scenarios from tests.md
- Integration glue (cross-domain calls)

**The win**: Not about context limits. It's about signal-to-noise ratio.

- 30 code files = 95% noise (imports, syntax, boilerplate)
- 6 AISD docs = 95% signal (rules, constraints, relationships)

AI spends tokens on what matters.

---

## Troubleshooting: AI Keeps Failing

**Scenario**: You're asking AI to make a change. It keeps getting it wrong.

You've tried:
- Explaining it differently
- Resetting context and starting over
- Pointing out the specific mistake
- Re-reading the same code files

**Try this instead**: Create savepoints.

### The Workflow

**1. AI is fucking up on a task**

Example: "Add email notifications when refund is denied"

AI keeps:
- Missing the fraud detection rule
- Breaking the existing refund flow
- Forgetting to log the denial reason

**2. Generate AISD docs with the context AI needs (like explaining to a junior engineer)**

What would you write down? Maybe:

**`docs/refunds/behavior.md`**:
```markdown
## ProcessRefund

**Preconditions**:
- User refund count MUST be ≤3 in past 12 months
- Purchase MUST be within 30 days

**Returns**:
- Success → send confirmation email
- Denied → send denial email with reason

**Side effects**:
- Log refund attempt (success or failure)
- Record denial reason in audit table
```

**`docs/notifications/behavior.md`**:
```markdown
## Email Notifications

**RefundDenied email**:
- Recipient: User email
- Subject: "Refund Request Denied"
- Body MUST include denial reason
- Send async (don't block refund flow)
```

**Format**: Tables, MUST/REQUIRED, explicit constraints. No "should" or vague descriptions.

**3. Add docs to context and ask AI again**

```
I've created docs/refunds/behavior.md and docs/notifications/behavior.md
explaining the refund flow and email requirements.

Read those files. Then add email notifications when refund is denied.
```

**You lose nothing**. If AI still fails, you have:
- Docs that help you understand the system
- A savepoint to reset to (git reset --hard)
- Clear specs to review before code

**4. AI still getting it wrong? Create more docs**

AI is confused about the fraud detection logic?

Create `docs/refunds/business-rules.md`:
```markdown
| Condition | Rule |
|-----------|------|
| Refund limit | FORBIDDEN if user >3 refunds in 12 months |
| Timeframe | Count refunds from current date - 365 days |
```

Add it to context. Reset git changes. Ask again.

**5. Repeat until AI gets it or you realize AI can't do this task**

Each AISD doc is:
- A savepoint (captures what you know)
- Context for AI (structured, explicit)
- Docs for humans (useful even if AI fails)

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

**AISD docs are AI-authored from human input**:

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

**Claude Code's CLAUDE.md pattern**: Anthropic's own tool loads a CLAUDE.md file to understand project-specific context. Teams are already doing this informally.

**What we're doing**: Expanding that idea into a complete system:
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

**Current status**: Promising informal results, but no rigorous testing. We're expanding on patterns people are already using (like CLAUDE.md), trying to formalize what works.

See [roadmap.md](roadmap.md) for what we're still figuring out.

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
- [roadmap.md](roadmap.md) - What we're still figuring out
