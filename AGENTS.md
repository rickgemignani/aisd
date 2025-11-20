# AGENTS: AISD – AI Small Docs

This repo defines the **AISD (AI Small Docs)** standard.

Docs here are meta: they teach AI how to read and write AISD-style documentation so AI can reason about real codebases with less noise and fewer tokens.

**Status**: Early stage, no empirical evidence. Core idea: AISD is intermediate representation between human intent and generated code.

**Repository structure**:
- `README.md` - Overview, philosophy, when to use
- `style-guide.md` - Writing principles, validation
- `best-practices.md` - File organization, context loading
- `TODO.md` - Task tracking, future work
- `templates/` - Templates (TODO - to be created)

---

## 1. How AI should behave in this repo

- Audience: senior engineers and AI agents.
- Voice: clear, direct, low-fluff. No hype, no marketing tone.
- Goal: increase **signal density** and **structural clarity**, not word count.
- Prefer:
  - lists over paragraphs
  - schemas and examples over abstract prose
  - explicit constraints over vague “best practices”
- When editing:
  - Preserve existing structure and headings where possible.
  - Tighten and clarify; avoid rewriting everything unless necessary.
  - If something is ambiguous, propose 2–3 concrete options instead of inventing new concepts silently.

---

## 2. Commit messages (AI + humans)

All commit messages must be **English**, **single line**, and follow:

`<type>[<area>]: <short-message>`

- `type` ∈ `spec`, `docs`, `chore`, `refactor`, `test`
  - `spec` – changes to AISD spec / formats
  - `docs` – guides, examples, explanations
  - `chore` – repo hygiene, tooling, config
  - `refactor` – structural changes without behavior change
  - `test` – test cases, validation docs, fixtures
- `area` ∈ `core`, `examples`, `prompts`, `guides`, `meta`
  - `core` – core AISD concepts and spec
  - `examples` – example docs, reference cases
  - `prompts` – prompt templates and patterns
  - `guides` – how-to, usage guides, workflows
  - `meta` – README, contribution notes, project meta
- `<short-message>`:
  - plain English phrase
  - max 20 words
  - imperative
  - lowercase
  - words separated by spaces
  - no trailing period

**Examples**

- `spec[core]: tighten aisd file schema`
- `docs[guides]: add cursor integration section`
- `docs[examples]: add refund rule case study`
- `chore[meta]: update repo structure notes`
- `refactor[prompts]: normalize agent instruction format`
- `test[core]: add schema validation cases`

---

## 3. AISD-specific editing rules

When changing any AISD-related doc:

- Make the **intent, constraints, and contracts** more explicit.
- Prefer:
  - "AI can assume X" over "usually X"
  - "Never do Y" over "avoid Y where possible"
- Protect the **3,000-line abstraction** idea:
  - Avoid adding low-signal commentary.
  - Move long narrative examples into dedicated example files if needed.
- Keep examples realistic:
  - Use scenarios like refunds, fraud detection, email notifications, etc.
  - Show how AISD helps AI consume a large codebase through a small, structured surface.

**AISD principles** (apply to all AISD docs):

- **Language**: MUST/REQUIRED/FORBIDDEN (never should/might/could/typically/usually)
- **Explicit constraints**: "1-200 chars" not "short"
- **Format**: Tables/lists/code blocks (not prose)
- **File size**: Index <100 lines, Spec 200-500 lines, target 40 chars/line (non-empty)
- **Structure**: One concept per file, H1 → H2 → H3 (never skip levels), relative paths only

---

## 4. File-specific notes

- `README.md`
  - Explains **why AISD exists** and when to use it.
  - Keep it focused on philosophy and problem framing.
- Spec files (AISD formats, schemas)
  - Treat them as **source of truth**.
  - Update spec first, then examples, then guides.
- Example / guide files
  - Show end-to-end flows:
    - analysis → planning → implementation → review
  - Highlight how AISD replaces “load 30 files” with “load 1–3 AISD docs”.

---

## 5. When in doubt

- Default to **shorter, sharper, more explicit**.
- If a change doesn't help an AI agent answer, plan, or implement better, don't add it.

---

## 6. Validation

**Forbidden words**:
```bash
grep -rn "should\|might\|could\|typically\|usually" . --include="*.md"
```

**Line counts**:
```bash
wc -l *.md | awk '$1 > 500 {print $2 ": " $1}'
```

**Avg line length**:
```bash
for file in *.md; do
  non_empty=$(grep -c '[^[:space:]]' "$file")
  chars=$(wc -c < "$file")
  avg=$(( chars / non_empty ))
  [ $avg -gt 40 ] && echo "$file: $avg chars/line"
done
```

---

## 7. Scope

**Primary use**: AI-authored specs from human requirements.

| Human Input | AI Generates | Purpose |
|-------------|--------------|---------|
| Policy requirements | Business rules | Code generation |
| Design discussion | Architecture ADRs | Implementation guidance |
| Feature request | Behavioral spec | Test + code generation |

**Use cases**:
- Business rules, ADRs, integration patterns, behavioral specs
- Token-efficient summaries (only when benefit is clear, source formats remain authoritative)

**Not AISD**: Tutorials, marketing, onboarding (human-targeted content)

---

## 8. Common tasks

**Add template**:
1. Create in `templates/`
2. Use tables, MUST/REQUIRED, conciseness
3. Keep under 500 lines
4. Mark "Core" (proven) or "Experimental" (unproven)
5. Add to `templates/index.md`

**Update core docs**:
1. Edit `README.md`, `style-guide.md`, `best-practices.md`
2. Use tables, explicit constraints, no prose
3. Add ❌ bad and ✅ good examples
4. Validate (line length, forbidden words)

**Update TODO**:
1. Edit `TODO.md`
2. Follow todo-md format (checkboxes, priorities, metadata)
3. Use hierarchical structure (Critical → High → Medium → Low → Research)
4. Add time estimates where helpful (~2h, ~4h, etc)

---

## 9. Tone

**For meta-docs** (this file, README, etc.):
- Use "Consider", "Target", "Example"
- Not "MUST", "Standard", "Enforce"
- Acknowledge uncertainty
- Invite community validation

**For AISD docs** (style-guide, best-practices, etc.):
- Use MUST/REQUIRED/FORBIDDEN per AISD principles

---

## 10. Key principles

1. **AI-authored** - Docs generated by AI, reviewed by humans
2. **Intermediate representation** - Bridge between human intent and code
3. **Self-compliance** - Follow own rules
4. **Honest** - Acknowledge uncertainty
5. **Focused** - Business rules/ADRs (not replacing OpenAPI/DDL)
6. **Git-reviewed** - Humans approve AI-generated diffs
7. **Context optimized** - File sizes for AI loading

**Critical gaps** (no evidence yet):
- No before/after AI tests
- No token efficiency data
- No proof 40 chars/line or 200-500 lines matter
- No multi-model testing