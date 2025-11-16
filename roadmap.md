# AISD Roadmap

**Future improvements and open questions**

---

## Critical: Evidence Gap

### 1. Build Reference Implementation

**Problem**: Zero evidence that AISD improves AI code generation

**Needed**:
- Build complete example project with AISD docs
- Create equivalent traditional docs (prose-based)
- Test AI code generation from both
- Measure: accuracy, hallucinations, iterations, tokens
- Document honest results (even if mixed)

**Action**: Create `examples/todo-app/` with both AISD and traditional docs, test results

**Why critical**: Without evidence, AISD is just opinions

---

### 2. Validate Context Window Assumptions

**Problem**: Claims optimize for "context windows" but modern models have 200k+ tokens

**Needed**:
- Test file sizes with GPT-4 (128k), Claude (200k), Gemini (1M+)
- Determine if 200-500 line limits still matter
- Find actual optimal file sizes for 2025 models
- Update recommendations with data

**Action**: Test with multiple models, document findings

**Why critical**: May be solving a 2023 problem in 2025

---

## High Priority: Scope Clarity

### 3. Clarify Context Precision Benefits

**Status**: Domain isolation is correctly designed for AI context loading, not architectural purity

**What's correct**:
- Small files enable selective loading (load only what's needed)
- Primitive references prevent cascade loading (User → Order → Product → ...)
- Index files enable navigation without reading full specs
- Mixed context composition (load tasks/model.md + users/behavior.md)

**What needs clarity**:
- Document "when to split" based on independent vs co-loaded concepts
- Explain this is about AI loading flexibility, not project complexity
- Needs empirical measurement to validate benefits

**Action**: Add context loading examples, clarify split criteria (done in best-practices.md)

**Why important**: Teams may dismiss as "over-engineering" without understanding AI context benefits

---

## Medium Priority: Adoption

### 4. Incremental Adoption Path

**Problem**: All-or-nothing approach won't work for existing projects

**Needed**:
- Migration guide (traditional → AISD)
- Incremental adoption strategy
- Coexistence patterns (AISD + existing docs)
- Quick wins list (start here, expand later)

**Action**: Add migration.md guide

**Why useful**: Lowers barrier to entry

---

### 5. Real User Validation

**Problem**: No external users, no feedback, no case studies

**Needed**:
- Find early adopters
- Collect feedback on what works/doesn't
- Document real use cases
- Iterate based on usage

**Action**: Add CONTRIBUTING.md, create feedback issue template

**Why useful**: Validates (or invalidates) assumptions

---

## Low Priority: Refinement

### 6. Metric Validation

**Problem**: 40 chars/line chosen arbitrarily, forbidden words list unvalidated

**Needed**:
- Test different line length targets
- Test if "often/typically" actually harm AI output
- Measure table density vs prose ratio
- Find optimal balance

**Action**: Research and document findings

**Why nice-to-have**: Current metrics work "well enough"

---

### 7. Multi-Model Testing

**Problem**: Optimized for unknown "AI" - which models?

**Needed**:
- Test GPT-4, Claude, Gemini, local models
- Document model-specific quirks
- Identify which principles matter per model
- Create model compatibility matrix

**Action**: Test suite across models

**Why nice-to-have**: Most teams use one primary model

---

### 8. Tooling

**Problem**: Basic shell scripts, no IDE integration

**Needed**:
- Standalone CLI validator
- IDE plugins (VS Code, JetBrains)
- CI/CD integration examples
- Auto-fix suggestions

**Action**: Build `aisd-lint` tool

**Why nice-to-have**: Validation scripts work for now

---

## Research Questions

### 9. Format Experiments

**Questions needing investigation**:
- Do AI models prefer YAML/JSON over markdown tables?
- Is there optimal table width for AI parsing?
- Do code examples in docs help or hurt generation?
- Should we use ASCII diagrams? Mermaid? External images?
- How much redundancy is optimal?

**Action**: Run experiments, document findings in `research/`

---

### 10. Theoretical Limits

**Questions about AI capabilities**:
- Do different architectures (GPT vs Claude vs Gemini) prefer different formats?
- Does fine-tuning change optimal doc format?
- How do multimodal models handle diagrams vs tables?
- Does preventing cascade loading measurably improve code generation quality?

**Action**: Research and share findings

---

## Non-Goals

**What AISD is NOT trying to solve**:
- Human-first documentation (tutorials, guides, marketing)
- Runtime documentation generation (Swagger, JSDoc)
- Automated doc generation from code
- Replacing comments in code
- General writing style guide

---

## Success Metrics (When We Have Evidence)

**How to measure if AISD works**:

| Metric | Target | Current Status |
|--------|--------|----------------|
| AI accuracy | >95% compiles + passes tests | ❌ Not measured |
| Iteration count | <3 prompts to working code | ❌ Not measured |
| Hallucination rate | <5% invented APIs | ❌ Not measured |
| Token efficiency | 50% reduction vs prose | ❌ Not measured |
| External adopters | 10+ projects | ❌ Zero known |

**Action**: Track and publish metrics after building reference implementation

---

## Timeline (Realistic)

**Phase 1: Prove It Works** (Next 1-3 months)
- Build todo app example with AISD + traditional docs
- Test AI generation from both
- Document results
- Iterate based on findings

**Phase 2: Refine & Focus** (After validation)
- Measure context loading benefits empirically
- Document optimal split strategies
- Add migration guides
- Create examples showing context composition

**Phase 3: Scale** (If Phase 1 succeeds)
- Find external users
- Collect real feedback
- Build tooling
- Multi-model optimization

**Phase 4: Polish** (If adopted)
- Metric refinement
- IDE integration
- Community growth

---

## Current State Assessment

**What's working**:
- Clear value proposition (refund policy, ADR examples)
- Self-compliance (docs follow own rules)
- Collaborative tone (not prescriptive)
- Practical templates (architecture, business-rules) aligned with new scope

**What's broken**:
- Zero evidence of benefits (biggest gap)
- Context window assumptions may be outdated (200k+ tokens now common)
- Templates marked as TODO
- Context loading benefits not empirically measured
- No adoption path for existing projects

**Honest next step**: Build one complete example and test it. Everything else is speculation.

---

## Related

- [README.md](README.md) - Standard overview
- [style-guide.md](style-guide.md) - Writing principles
- [best-practices.md](best-practices.md) - Organization patterns
