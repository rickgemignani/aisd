# AISD Style Guide

**Format principles for AI-authored documentation**

---

## Core Philosophy

**Primary Author**: AI (generates docs from human requirements)
**Primary Reader**: AI (generates code from docs)
**Secondary Reader**: Humans (review diffs, approve changes)
**Target Audience**: AI-targeted, human-readable
**Goal**: Unambiguous intermediate representation

---

## Format Principles

**Note**: These principles guide AI when generating AISD docs. Humans review the output, not write it directly.

### 1. Brutal Conciseness

AI generates only essential content.

Context windows are finite. Every word costs tokens.

**Examples** (showing what AI generates, not what humans write):

❌ "The system should validate that the user has provided a valid email address"
✅ "Email MUST be valid"

❌ "When the user attempts to create a new task, the system will check if..."
✅ "CreateTask validates inputs before storing"

❌ "It is recommended that passwords contain at least 8 characters"
✅ "Password MUST be 8-128 characters"

❌ "Note: File naming conventions are project-specific"
✅ (omit - not specified by standard = project choice)

### 2. Authoritative Language

AI generates MUST/REQUIRED/FORBIDDEN (no ambiguity).

Never should/might/could/typically/usually/often.

**RFC 2119 keywords**:

| Keyword | Meaning |
|---------|---------|
| MUST, REQUIRED, SHALL | Absolute requirement |
| MUST NOT, SHALL NOT, FORBIDDEN | Absolute prohibition |
| MAY, OPTIONAL | Truly optional |

**Why**:
- "should" → AI interprets differently each time
- "reasonable" → Undefined for AI
- MUST → Unambiguous for code generation

**Examples**:

❌ "Passwords should be at least 8 characters"
✅ "Password MUST be 8-128 characters"

❌ "The API might return an error"
✅ "API returns 400 on invalid input"

❌ "Titles are typically short"
✅ "Title MUST be 1-200 characters"

### 3. Technical Precision

Use exact types, ranges, formats, and algorithms.

**Vague → Precise**:

| ❌ Vague | ✅ Precise |
|---------|-----------|
| "short string" | "1-200 characters" |
| "valid email" | "MUST match regex: ^[^@]+@[^@]+\\.[^@]+$" |
| "recent timestamp" | "ISO 8601 datetime, UTC" |
| "positive number" | "Integer, 1-1000000" |
| "unique ID" | "UUID v4" |
| "sorted list" | "Array sorted by created_at ASC" |

### 4. Tables Over Prose

Use structured data (tables, lists, code blocks) not paragraphs.

**Prose → Table example**:

❌ **Prose**:
```markdown
Refunds are allowed within 30 days of purchase for unused products.
The customer must have the original packaging and receipt.
Users who have requested more than 3 refunds in the past year are not eligible.
```

✅ **Table**:
```markdown
| Condition | Rule |
|-----------|------|
| Purchase date | MUST be within 30 days |
| Product condition | MUST be unused (verified by serial scan) |
| Original packaging | REQUIRED |
| Refund limit | FORBIDDEN if >3 refunds in past 12 months |
```

### 5. No "Why" Explanations

Document WHAT happens and WHEN it happens.

Omit rationale, motivation, history, or background.

**Examples**:

❌ "We use UUIDs instead of auto-increment IDs because they're globally unique and work better in distributed systems"
✅ "ID: UUID v4"

❌ "The system validates email addresses to prevent users from entering invalid data"
✅ "Email MUST match regex: ^[^@]+@[^@]+\\.[^@]+$"

**Why**: Rationale is for humans. AI only needs specs.

---

## File Organization

### Size Guidelines

| Type | Target Lines | Rationale |
|------|--------------|-----------|
| Index | <100 | Quick navigation |
| Spec | 200-500 | Fits AI context windows, single responsibility |

**If file grows large** (>500 lines):
- Split by domain (separate entities)
- Split by operation (create vs update vs delete)
- Extract to separate file (validation.md, integration.md)

**Note**: Targets, not hard limits. Optimize for AI comprehension.

### Single Responsibility

One concept per file.

**Good file splits**:
- `refunds/business-rules.md` - Eligibility, limits, fraud prevention
- `refunds/processing.md` - Workflow, timelines, notifications
- `tasks/validation.md` - Cross-system validation constraints

**Bad file design**:
- `refunds/everything.md` - Rules + processing + integration + edge cases (too broad)

---

## Formatting Rules

### Headers

- **H1** (`#`): File title (one per file)
- **H2** (`##`): Major sections
- **H3** (`###`): Subsections
- **Never skip levels** (no H1 → H3 without H2)

### Emphasis

- **Bold** (`**text**`): Keywords, field names, entity names (first mention only)
- **Code** (`` `text` ``): Types, values, commands, file paths, error codes
- **Italic**: Rarely used (prefer bold or code)

### Lists

- **Unordered** (`-`): Requirements, constraints, features
- **Ordered** (`1.`): Sequential steps, algorithms

### Code Blocks

Always specify language for syntax highlighting:

````markdown
```python
def create_task(title: str) -> Task:
    return Task(id=uuid4(), title=title)
```
````

### Tables

Use for structured data (entities, operations, test cases).

**Alignment**:
- Left-align text columns
- Right-align numeric columns (if needed)
- Keep columns narrow (avoid wide cells)

**Example**:
```markdown
| Field | Type | Required | Constraints |
|-------|------|----------|-------------|
| id | UUID | Y | - |
| count | Integer | Y | 1-1000 |
```

---

## Cross-References

### Linking

**Within same directory**:
```markdown
See [model.md](model.md) for entity definitions
```

**Cross-directory**:
```markdown
See [tasks/model.md](../tasks/model.md)
```

**Index-style references** (preferred for lists):
```markdown
## Related

- **model.md** - Entity definitions
- **behavior.md** - Operations and rules
- **../auth/model.md** - Authentication entities
```

---

## Anti-Patterns

### ❌ Bad Examples

1. **Vague requirements**:
   ```markdown
   Password should be reasonably long and secure
   ```

2. **Prose explanations**:
   ```markdown
   The system validates email addresses to ensure users
   enter valid data and prevent errors later in the flow.
   ```

3. **Missing structure**:
   ```markdown
   Tasks have an id, title, and status field.
   ```

4. **Weak language**:
   ```markdown
   The API might return an error if the input is invalid.
   ```

5. **Implementation details in spec**:
   ```markdown
   Store tasks in a PostgreSQL database using SQLAlchemy ORM.
   ```

### ✅ Good Examples

1. **Explicit constraints**:
   ```markdown
   Password MUST be 8-128 characters
   ```

2. **Pure specification**:
   ```markdown
   Email MUST match regex: ^[^@]+@[^@]+\.[^@]+$
   ```

3. **Structured data**:
   ```markdown
   | Field | Type | Required |
   |-------|------|----------|
   | id | UUID | Y |
   | title | String | Y |
   | status | String | Y |
   ```

4. **Authoritative language**:
   ```markdown
   API returns 400 when input validation fails
   ```

5. **Behavior, not implementation**:
   ```markdown
   Tasks MUST persist across application restarts
   ```

---

## Validation Checklist

**Before approving AI-generated docs, verify**:

**Language**:
- [ ] No forbidden words (should/might/could/typically/usually)
- [ ] Only MUST/REQUIRED/FORBIDDEN for requirements
- [ ] Explicit types (UUID, String, Integer, not "ID" or "text")
- [ ] Explicit constraints (1-200, not "short")

**Structure**:
- [ ] Tables/lists/code blocks (not prose paragraphs)
- [ ] One concept per file
- [ ] Under 500 lines (split if exceeded)
- [ ] Headers follow hierarchy (no level skipping)

**Content**:
- [ ] What and when (not why)
- [ ] Behavior (not implementation)
- [ ] Testable specifications

**Links**:
- [ ] All cross-references work
- [ ] No broken links
- [ ] Relative paths (not absolute)

---

## Enforcement Tools

### Line Count Check

```bash
wc -l docs/**/*.md | awk '$1 > 500 {print $2 ": " $1 " lines (max 500)"}'
```

### Average Line Length Check

```bash
for file in docs/**/*.md; do
  non_empty=$(grep -c '[^[:space:]]' "$file")
  chars=$(wc -c < "$file")
  avg=$(( chars / non_empty ))
  [ $avg -gt 40 ] && echo "$file: $avg chars/line (max 40, non-empty lines)"
done
```

### Forbidden Words Check

```bash
grep -rn "should\|might\|could\|typically\|usually\|often" docs/ --include="*.md"
```

### Combined Pre-commit Hook

Add to `.git/hooks/pre-commit`:

```bash
#!/bin/bash
set -e

echo "Checking AISD docs..."

# Check for forbidden words
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

## Examples in the Wild

**Good AISD documentation**:
- [Stripe API Reference](https://stripe.com/docs/api) - Tables, explicit types, authoritative
- [GitHub API Docs](https://docs.github.com/en/rest) - Structured, precise constraints
- [Kubernetes API Reference](https://kubernetes.io/docs/reference/) - YAML schemas, exact specs

**Bad for AI** (but good for humans):
- Tutorial-style guides ("Let's build a todo app!")
- Conceptual overviews with metaphors
- Marketing documentation

---

## Quick Reference

**Forbidden words**: should, might, could, typically, usually, often, reasonable

**Required keywords**: MUST, REQUIRED, FORBIDDEN, SHALL, SHALL NOT

**File limits**: Index <100 lines, Spec 200-500 lines, Max 1000 lines

**Line length**: Max 40 chars/line (non-empty lines only)

**Format preference**: Tables > Lists > Code blocks > Prose

---

## Related

- [README.md](README.md) - Overview of AISD documentation standard
- [templates/](templates/) - Example templates (TODO - to be created)
- [best-practices.md](best-practices.md) - File organization and context loading

---

**Next**: Read [best-practices.md](best-practices.md) for file organization patterns.
