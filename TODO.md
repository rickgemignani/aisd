# TODO +AISD

**Future improvements and open questions**

---

## Critical: Evidence Gap #critical

- [ ] (A) Build complete example project with AISD docs +examples type:evidence ~16h
  - [ ] Create examples/todo-app/ directory structure ~1h
  - [ ] Write AISD-format docs for todo app ~6h
  - [ ] Create equivalent traditional prose docs ~6h
  - [ ] Document both approaches ~3h

- [ ] (A) Test AI code generation from both doc formats +examples type:evidence ~8h
  - [ ] Test GPT-4 code generation ~2h
  - [ ] Test Claude code generation ~2h
  - [ ] Test Gemini code generation ~2h
  - [ ] Measure accuracy, hallucinations, iterations, tokens ~2h

- [ ] (A) Document honest results even if mixed +examples type:evidence ~4h

- [ ] (A) Validate context window assumptions with 2025 models type:evidence ~6h
  - [ ] Test file sizes with GPT-4 (128k tokens) ~2h
  - [ ] Test file sizes with Claude (200k tokens) ~2h
  - [ ] Test file sizes with Gemini (1M+ tokens) ~2h
  - [ ] Determine if 200-500 line limits still matter ~1h
  - [ ] Update recommendations with data ~1h

---

## High Priority: Scope Clarity #scope

- [ ] (B) Document "when to split" based on independent vs co-loaded concepts +guides ~4h
  notes:"Based on AI loading flexibility not project complexity"

- [ ] (B) Add context loading examples showing selective loading benefits +guides ~3h

- [ ] (B) Clarify split criteria with empirical measurement +guides type:evidence ~4h

---

## Medium Priority: Adoption #adoption

- [ ] (C) Create migration guide (traditional → AISD) +guides ~6h
  - [ ] Document incremental adoption strategy ~2h
  - [ ] Define coexistence patterns (AISD + existing docs) ~2h
  - [ ] Create quick wins list (start here expand later) ~2h

- [ ] (C) Add CONTRIBUTING.md with feedback process +meta ~2h

- [ ] (C) Create feedback issue template +meta ~1h

- [ ] (C) Find early adopters for real user validation +community ~8h

- [ ] (C) Collect feedback on what works and what doesn't +community repeat:monthly ~2h

- [ ] (C) Document real use cases from adopters +community ~4h

---

## Low Priority: Refinement #refinement

- [ ] Test different line length targets (40 chars baseline) type:research ~4h

- [ ] Test if "often/typically" actually harm AI output type:research ~3h

- [ ] Measure table density vs prose ratio type:research ~3h

- [ ] Test AISD across multiple models +testing ~12h
  - [ ] Test GPT-4 compatibility ~3h
  - [ ] Test Claude compatibility ~3h
  - [ ] Test Gemini compatibility ~3h
  - [ ] Test local models compatibility ~3h

- [ ] Document model-specific quirks +guides ~4h

- [ ] Create model compatibility matrix +guides ~2h

- [ ] Build standalone CLI validator tool +tooling ~16h
  - [ ] Design aisd-lint architecture ~2h
  - [ ] Implement forbidden words check ~2h
  - [ ] Implement line count validation ~2h
  - [ ] Implement avg line length check ~2h
  - [ ] Add auto-fix suggestions ~4h
  - [ ] Package and publish ~4h

- [ ] Create VS Code extension +tooling ~24h

- [ ] Create JetBrains plugin +tooling ~24h

- [ ] Add CI/CD integration examples +tooling ~4h

---

## Research Questions #research

- [ ] Test if AI models prefer YAML/JSON over markdown tables type:experiment ~6h

- [ ] Determine optimal table width for AI parsing type:experiment ~4h

- [ ] Test if code examples in docs help or hurt generation type:experiment ~6h

- [ ] Evaluate ASCII diagrams vs Mermaid vs external images type:experiment ~6h

- [ ] Measure optimal redundancy level type:experiment ~4h

- [ ] Research if different architectures prefer different formats type:theoretical ~8h
  notes:"GPT vs Claude vs Gemini architecture differences"

- [ ] Research if fine-tuning changes optimal doc format type:theoretical ~8h

- [ ] Test how multimodal models handle diagrams vs tables type:theoretical ~6h

- [ ] Measure if preventing cascade loading improves code quality type:theoretical ~8h

---

## Success Metrics (When We Have Evidence) #metrics

- [ ] Track AI accuracy (target >95% compiles + passes tests) type:metric repeat:monthly ~1h

- [ ] Track iteration count (target <3 prompts to working code) type:metric repeat:monthly ~1h

- [ ] Track hallucination rate (target <5% invented APIs) type:metric repeat:monthly ~1h

- [ ] Track token efficiency (target 50% reduction vs prose) type:metric repeat:monthly ~1h

- [ ] Track external adopters (target 10+ projects) type:metric repeat:monthly ~30m

- [ ] Publish metrics dashboard after reference implementation type:metric ~8h

---

## Templates #templates

- [ ] Create templates/index.md +templates ~2h

- [ ] Create business-rules template +templates ~4h

- [ ] Create architecture-adr template +templates ~4h

- [ ] Create integration-pattern template +templates ~4h

- [ ] Create behavioral-spec template +templates ~4h

- [ ] Mark each template as Core or Experimental +templates ~1h

---

## Related

- [README.md](README.md) - Standard overview
- [style-guide.md](style-guide.md) - Writing principles
- [best-practices.md](best-practices.md) - Organization patterns
- [AGENTS.md](AGENTS.md) - Agent instructions
