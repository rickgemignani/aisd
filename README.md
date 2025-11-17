# AISD: AI Small Docs

**Stop writing docs for AI. Let AI write them for itself.**

*Because if AI is going to hallucinate anyway, at least make it hallucinate in a review-friendly format first.*

---

## Why?

AI keeps missing your requirements. You explain the constraints again. It breaks something else. You reset and try different words.

**What if you wrote down what you'd tell a junior engineer, then gave that to AI instead?**

That's AISD. A format for those docs.

---

## Is This For You?

**Try AISD if:**
- ✅ You're using Cursor, Claude Code, or similar AI coding tools
- ✅ AI keeps missing constraints or breaking things
- ✅ You explain the same thing 3+ times per task

**Skip AISD if:**
- ❌ AI gets it right the first time
- ❌ You're doing simple CRUD with no complex rules
- ❌ Your code is already self-documenting

---

## What Is AISD?

A format for writing the docs you'd give a junior engineer - but structured for AI.

**Key ideas:**
- **Tables instead of prose** - Scannable, not walls of text
- **MUST/REQUIRED instead of "should"** - Unambiguous, not vague
- **Explicit constraints instead of descriptions** - "1-200 chars" not "short"
- **Small files (200-500 lines) instead of monoliths** - Selective loading

**Not**: Magic AI agent that does everything
**Is**: A format that compresses signal, cuts noise

**Think compression ratios:**
- **Your codebase**: 50,000 lines across 200 files
- **Traditional docs**: 15,000 lines of prose (if you even have them)
- **AISD abstraction**: 3,000 lines of structured specs

**Result**: AI gets the context it needs without drowning in code.

## The Problem

You're using Cursor or Claude Code on a real codebase.

**Scenario**: Add fraud detection to your refund system

**What AI does**:
- Loads 30 files trying to understand the refund flow
- Finds the refund service, payment processor, user management
- Reads database schemas, config files, tests
- Burns 50,000 tokens just to understand what's there
- Still misses the business rules buried in comments
- Generates code that "works" but violates policies

**Why**: Even with 200k token windows, AI loads files speculatively. Most of what it loads is noise (imports, boilerplate, implementation details). The signal is scattered.

## The AISD Approach

Create high-density maps of what matters. AI loads those instead of wandering through code.

**Example: Adding fraud detection**

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

## Core Principles

**What makes AISD different**:

1. **AI-authored, human-reviewed** - AI generates docs in AISD format, you review diffs in git
2. **Intermediate representation** - Bridge between human intent and generated code
3. **Signal over noise** - Tables, explicit constraints, MUST/REQUIRED (not prose and "should")
4. **Context precision** - Small, focused files (200-500 lines) enable selective loading
5. **Domain isolation** - Prevents cascade loading (User → Order → Product → ...)
6. **Multiple complementary docs** - business-rules + behavior + integration + data-model + tests + architecture
7. **Based on existing patterns** - Expands CLAUDE.md approach to complete systems

---

## Try It (When AI Keeps Failing)

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

## Why This Works

**Without AISD**:
- You: "Add email notifications"
- AI loads 10 files, misses the fraud rule buried in RefundService line 247
- You: "No, check the fraud detection logic"
- AI: "Oh right" (hallucinates the rule)

**With AISD**:
- You create docs/refunds/business-rules.md with the fraud rule in a table
- AI loads 1 doc (50 lines), sees the exact rule
- AI implements correctly or you catch the mistake in the doc review

**The docs are your savepoint**. If AI fucks up, reset and try again with better context.

---

## You Don't Need to Use AISD for Everything

Use it when:
- AI keeps missing the same constraint
- You're explaining the same thing 3+ times
- The change touches multiple domains
- You want to review the approach before code

Skip it when:
- One-line bug fix
- AI got it right the first time
- The code is self-explanatory

**AISD is a tool, not a religion.**

---

## Real-World Evidence

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

## Want to Help?

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

## Format Principles

**Why these principles matter when AI writes docs**:

### 1. Brutal Conciseness
AI doesn't get tired of verbosity, but context windows are finite.

Every word costs tokens. AI generates only essential content.

### 2. Tables Over Prose
AI parses structured data more reliably than prose.

Tables = unambiguous. Prose = interpretation needed.

### 3. Authoritative Language
MUST/REQUIRED/FORBIDDEN removes ambiguity.

AI doesn't interpret "should" the same way twice.

### 4. Explicit Constraints
AI needs exact specifications, not fuzzy concepts.

"1-200 characters" generates correct validation. "Reasonable length" doesn't.

### 5. File Size Limits
200-500 lines per file enables selective loading.

AI loads files programmatically. Small files = flexible context composition.

### 6. Context Precision
Prevents cascade loading and context explosion.

Primitive references = Self-contained files, no chain dependencies (User → Order → Product → ...).

---

## File Structure

### Standard Layout

```
docs/
├── index.md              # System overview (<100 lines)
├── domain-a/
│   ├── index.md          # Domain overview (<100 lines)
│   ├── model.md          # Entities, fields, constraints (200-500 lines)
│   └── behavior.md       # Operations, rules, scenarios (200-500 lines)
└── domain-b/
    ├── index.md
    ├── model.md
    └── behavior.md
```

### File Types

| Type | Size | Purpose | Example |
|------|------|---------|---------|
| Index | <100 lines | Navigation, orientation | `docs/index.md`, `docs/tasks/index.md` |
| Spec | 200-500 lines | Entities, behaviors, tests | `model.md`, `behavior.md` |
| Max | 1000 lines | Hard limit, split if exceeded | N/A |

---

## What AISD Helps With

### Goals:

1. **Reduce hallucinations** - Explicit constraints guide AI
2. **Improve consistency** - Structured docs reduce variability
3. **Optimize context** - Selective loading prevents over-loading
4. **Enable mixed context** - Load tasks/model.md + users/behavior.md (impossible with large files)
5. **Prevent cascade loading** - Self-contained files, no chain dependencies
6. **Catch errors early** - Explicit constraints reveal edge cases

### Expected improvements:

**Before AISD**:
- AI generates 10 different implementations from vague spec
- Code compiles but uses nonexistent APIs
- Large multi-responsibility files force AI to load everything
- Cross-domain references cause cascade loading (User → Order → Product → ...)

**After AISD**:
- AI generates more consistent implementations
- Explicit constraints reduce invalid code
- Small files enable precise loading (load only needed entities)
- Mixed context composition (tasks/model.md + users/behavior.md, skip unneeded files)

**Note**: LLMs use stochastic decoding, so outputs vary between runs. AISD reduces variability but doesn't guarantee identical outputs.

---

## Files in This Standard

| File | Focus | Use |
|------|-------|-----|
| [style-guide.md](style-guide.md) | Writing principles | Language, formatting guidelines |
| [best-practices.md](best-practices.md) | Organization patterns | File structure, context loading |
| [templates/](templates/) | Example templates | TODO - Will demonstrate AISD format |

---

## When to Use AISD

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

## Validation

### Optional Automated Checks

```bash
# Line count check
wc -l docs/**/*.md | awk '$1 > 500 {print $2 ": " $1 " lines (max 500)"}'

# Average line length check (max 40 chars/line, non-empty lines)
for file in docs/**/*.md; do
  non_empty=$(grep -c '[^[:space:]]' "$file")
  chars=$(wc -c < "$file")
  avg=$(( chars / non_empty ))
  [ $avg -gt 40 ] && echo "$file: $avg chars/line (max 40)"
done

# Forbidden words
grep -rn "should\|might\|could\|typically\|usually" docs/ --include="*.md"
```

### Pre-commit Hook

Add to `.git/hooks/pre-commit`:

```bash
#!/bin/bash
set -e

echo "Checking AISD docs..."

# Check for forbidden words in staged docs
if git diff --cached --name-only | grep '\.md$' | xargs grep -n "should\|might\|could\|typically\|usually" 2>/dev/null; then
  echo "❌ ERROR: Found forbidden words in docs"
  echo "Use MUST/REQUIRED/FORBIDDEN instead"
  exit 1
fi

# Check line counts
git diff --cached --name-only | grep '\.md$' | while read file; do
  lines=$(wc -l < "$file")
  if [ $lines -gt 500 ]; then
    echo "⚠️  WARNING: $file has $lines lines (max 500)"
  fi
done

# Check average line length (max 40 chars/line, non-empty)
git diff --cached --name-only | grep '\.md$' | while read file; do
  non_empty=$(grep -c '[^[:space:]]' "$file" || echo 1)
  chars=$(wc -c < "$file")
  avg=$(( chars / non_empty ))
  if [ $avg -gt 40 ]; then
    echo "⚠️  WARNING: $file has $avg chars/line (max 40)"
  fi
done

echo "✅ Docs OK"
```

---

## Philosophy

**Code is for machines. Traditional docs are for humans. AISD is for AI.**

When AI reads your code, it drowns in noise. When AI reads prose docs, it drowns in ambiguity. AISD is the signal extracted - structured, explicit, dense.

Think of it as: Human intent → AI abstraction → Human review → AI implementation

You're not writing docs. AI is. You're reviewing them like code.

---

## Quick Links

**Ready to try it?** See ["Want to Help?"](#want-to-help) above for how to get started.

**Format details**:
- [style-guide.md](style-guide.md) - Language rules, formatting, examples
- [best-practices.md](best-practices.md) - File organization, context loading
- [roadmap.md](roadmap.md) - What we're still figuring out
