# Example: single-pass design review

This example shows how the skill behaves in a standard chat environment without Claude Code or subagent support. It is included to illustrate the output structure, reviewer separation rules, and transparency about limitations.

This example reviews the design of the Academic Council skill itself, not a real research abstract or manuscript. It should not be interpreted as evidence that the skill is empirically validated or that it improves peer review in a proven way.

---

## Preliminary reading

Section: full SKILL.md v0.4, plus its README — the whole project, not an excerpt
Assumed field: prompt engineering / applied LLM tooling for academic self-review
Assumed venue/aim: public release as an installable Claude skill, published on GitHub for other researchers
Main claims:
1. six differently-lensed personas surface more than one reviewer would;
2. real subagents give genuine independence, single-pass is a legitimate fallback;
3. the grounding/severity/no-fabrication rules keep output non-sycophantic and checkable.
Limits of the excerpt: this is a design document with no usage data — the project itself states it has not been tested on a real text yet, so this is an evaluation of the design, not evidence of real-world performance.

Mode: single pass — no subagent-launching tool is exposed in this session.

---

## 1. The Skeptic (Reviewer 2)

Lens: validity of the design's claims relative to what's actually verifiable · Ignores: presentation, README polish.
Assessment: Feasibility: Medium (untested) · Relevance: High · Impact: Medium
Verdict: Major revision — the architecture is sound, but its central claim (that the council improves review quality) is not yet supported by evidence.

Findings
- **SK1 · Major · Gap: no empirical validation.**
  Passage: "it has not yet been tested on a large sample of real texts."
  Problem: The README itself admits that the core premise is unverified. Everything else follows from an untested claim.
  Solution: Run the skill on a real excerpt, keep the transcript, and check whether the six opinions diverge meaningfully or simply echo the same critique in different wording.

- **SK2 · Major · Flaw: independence is asserted, not architecturally true in single-pass mode.**
  Passage: "write each figure as if it had not read the others"
  Problem: In a single continuous completion, the model's hidden state is shared across all six by construction. This is discipline, not a guarantee.
  Solution: Reframe single-pass mode as "instructed to stay separate" rather than "independent." Reserve the stronger claim for subagent mode.

- **SK3 · Minor · Flaw: the severity table looks quantitative but is not.**
  Passage: "Fatal / Major / Minor / Detail"
  Problem: Counts are being compared across figures with different verdict scales, which can be read as a misleading composite score.
  Solution: Add a note stating that counts are descriptive within a figure and not comparable across figures.

What holds up:
- The "[to verify]" convention is a real safeguard against fabricated citations and unsupported external claims.

Outside my lens:
- The cost and latency of six subagent calls.

---

## 2. The Optimist (Reviewer 1)

Lens: what the design gets right and how far it can go · Ignores: unproven-ness as a standalone objection.
Assessment: Feasibility: High · Relevance: High · Impact: Medium
Verdict: Minor revision — the structure is more disciplined than a typical “critique this from six angles” prompt.

Findings
- **OP1 · Minor · The one thing that would stop a full accept.**
  Passage: "the skill detects which mode is available"
  Problem: Nothing forces the model to verify its own compliance with word counts, quote lengths, or the seven-finding cap. This is self-reported discipline rather than guaranteed compliance.
  Solution: For a first version, a light spot-check is enough; it is useful to verify the first few runs, not to build a full governance layer around them.

What holds up:
- Rule 5 — every problem must come with a remedy — is the strongest design choice in the document.
- The synthesis stage with a “poorly founded criticisms” check is a genuine differentiator from a naive multi-persona prompt.

If a hostile reader saw this, they would say: “this is elaborate scaffolding for something a single good prompt might approximate.” That is a fair criticism, but the scaffolding is exactly what a bare prompt would not reliably do.

---

## 3. The Publication-Driven PI

Lens: is this ready to put a name on and share · Ignores: theoretical elegance.
Assessment: Feasibility: High · Relevance: High · Impact: Medium
Verdict: After targeted work — do not publish a repo with zero worked examples.

Findings
- **PI1 · Major · Gap: no demo output.**
  Passage: "the README itself admits..."
  Problem: A GitHub visitor sees formatting rules and a workflow description, but not what the output actually looks like.
  Solution: Run the skill once and publish a transcript as an example file.

- **PI2 · Detail: the differentiation is underclaimed.**
  Passage: "Council of expert personas"
  Problem: That phrase sounds familiar. The README does not explain why this design is different enough to merit attention beyond a generic prompt pattern.
  Solution: Add a short paragraph explaining why the grounding rule, severity taxonomy, and synthesis checks matter.

Brake applied to myself: the temptation is to ship now and iterate live. But publishing strong language about “genuine independence” without observed evidence would itself be overclaiming. I will not recommend that.

---

## 4. The Outsider

Lens: would this make sense to someone who has never used Claude Code · Ignores: prompt quality.
Assessment: Feasibility: n.a. · Relevance: High · Impact: n.a.
Verdict: Comprehensible with effort.

What I understood: a document that tells an AI to role-play six reviewer types with different priorities, merge their notes into one report, and use real separate agents instead of one when the technical option exists.

Findings
- **OU1 · Minor · Clarity: subagent and Task tool are unexplained.**
  Passage: "subagent mode"
  Problem: Readers who have never used Claude Code will hit technical jargon without a gloss.
  Solution: Add a one-line explanation: “a separate AI process with a different context.”

- **OU2 · Detail: Reviewer 2 assumes shared academic folklore.**
  Passage: “Reviewer 2”
  Problem: This is understandable for a researcher audience, but the README does not explain it.
  Solution: Add one clause explaining that the labels map to different review roles and priorities.

Outside my lens:
- Whether the personas' content is technically accurate.

---

## 5. The Methodologist

Adaptation: this is not an empirical study; it is a specification for an LLM's behaviour. I therefore check instruction consistency, testability, and reproducibility rather than statistics.
Assessment: Feasibility: Medium · Relevance: High · Impact: Medium
Verdict: Correctable.

Findings
- **MT1 · Major · Gap: no evaluation harness.**
  Passage: "it has not yet been tested on a large sample of real texts"
  Problem: There is no explicit way to check whether the skill behaves as specified, especially in single-pass mode.
  Solution: Add a minimal evaluation step: one or two worked examples reviewed by the author, with attention to cross-bleed between figures.

- **MT2 · Minor · Gap: the template is not fully illustrative.**
  Passage: "SK1 · Major · Flaw: short title"
  Problem: The multi-finding numbering convention is inferable but not shown clearly enough in the example format.
  Solution: Show at least two example entries rather than one.

- **MT3 · Detail: same comparability issue as the Skeptic flagged.**
  Passage: summary table
  Problem: The counts are not comparable across figures with different verdict scales.
  Solution: Add the same caveat the Skeptic suggested.

Brake applied to myself: do not demand a benchmark suite for a v1 prompt-only project. A full planted-flaw benchmark would be disproportionate.

---

## 6. The Grant Panel

Assessment: Feasibility: High · Relevance: Medium · Impact: Medium-low (a real but niche need)
Verdict: Fund with reservations.

Findings
- **GP1 · Minor · Gap: no roadmap.**
  Passage: “Repository contents”
  Problem: The README explains what exists but not what comes next. A funder-style reviewer wants a milestone plan.
  Solution: Add a roadmap section explaining worked examples, mode comparisons, and optional reviewer figures.

Would I fund it? Yes, at low risk — it is a text file, not a system with substantial deployment cost — but I would withhold the “ready to share” milestone until at least one real example exists.

---

## Summary table

| Figure | Feasibility | Relevance | Impact | Findings (F/Major/Minor/Detail) | Verdict | Main request |
| --- | --- | --- | --- | --- | --- | --- |
| Skeptic | Medium | High | Medium | 0/2/1/0 | Major revision | Validate the independence claim and test the design once |
| Optimist | High | High | Medium | 0/0/1/0 | Minor revision | Acknowledge the “elaborate scaffolding” objection |
| PI | High | High | Medium | 0/1/0/1 | After targeted work | Ship a worked example before publishing |
| Outsider | n.a. | High | n.a. | 0/0/1/1 | Comprehensible with effort | Gloss subagent / Task tool |
| Methodologist | Medium | High | Medium | 0/1/1/0 | Correctable | Add a minimal evaluation step and fix the template |
| Grant Panel | High | Medium | Medium-low | 0/0/1/0 | Fund with reservations | Add a roadmap before wider release |

---

## Convergences and divergences

Convergence: SK1, PI1, MT1, and GP1 all independently land on the same gap — the skill has not been run on a real text. This is the priority issue.
Convergence: SK3 and MT3 both flag the same issue — the summary-table counts are not comparable across figures with different verdict scales.
Divergence: the PI wants to ship after one example; the Methodologist would prefer a small evaluation set before release. I side with the PI here, because a v1 prompt-only skill does not need a full benchmark suite.
No poorly founded criticisms were found.

---

## Points requiring careful attention

- **High — Run it once on a real excerpt and keep the transcript.** (SK1, PI1, MT1, GP1)
  Why it matters: this is the single biggest open question.
  Decision: Do it before the next public-facing release.

- **High — Soften the independence claim for single-pass mode.** (SK2)
  Why it matters: current wording overstates what is actually guaranteed.
  Decision: Distinguish “instructed to stay separate” from “genuinely independent.”

- **Medium — Add the cross-comparability caveat to the summary-table instructions.** (SK3, MT3)
  Why it matters: counts can otherwise be misread as a quantitative score.
  Decision: state clearly that counts are descriptive within figure, not across figures.

- **Medium — Gloss subagent / Task tool in the README.** (OU1)
  Why it matters: the audience includes non-expert Claude Code users.
  Decision: add a one-line explanation.

- **Medium — Add a short roadmap section.** (GP1)
  Why it matters: it makes the project look intentional and not static.
  Decision: include the next milestones and optional figures.

- **Low — Show two example findings in the format template instead of one.** (MT2)
  Why it matters: it reduces ambiguity for new users.
  Decision: add a second entry as a simple example.

- **Low — Add a paragraph on why the council is different from a generic “ask for six perspectives” prompt.** (PI2)
  Why it matters: it makes the design rationale more legible.
  Decision: add one succinct paragraph.

---

## Solid points to leave untouched

- Rule 5 — every finding needs a concrete remedy — is the strongest design principle in the whole project.
- The synthesis step that checks for poorly founded criticisms is a real differentiator from a naive multi-persona prompt.
- The severity and type taxonomy is structurally sensible; it only needs a caveat about comparability, not redesign.
- The subagent-mode isolation and retry-once fallback logic is reasonable and not the core issue at this stage.

---

## Overall assessment

The document is a thoughtfully built specification for something that has never been run. That is not a contradiction: the instructions are cautious, they require textual grounding, they forbid fabrication, and they force concrete remedies. However, every reviewer that touched the question of readiness landed on the same point: there is no evidence yet that the six voices actually diverge in the intended manner, and the README currently states some independence claims more confidently than the evidence supports.

Evaluation of the suggestions:
- **Do:** run the skill once on a real excerpt and save the transcript; soften the independence claim for single-pass mode; add the cross-comparability caveat.
- **Do if time allows:** gloss the Claude Code terminology; add a roadmap paragraph; add a second example in the template.
- **Do not do, or with caution:** do not build a full benchmark suite for a v1 prompt-only skill; do not publish the stronger “genuinely independent” phrase without qualification.

Best course of action:
1. Run the council on one real text in single-pass mode and save the transcript. (low effort)
2. Edit the wording around single-pass and subagent independence to distinguish “instructed to stay separate” from “genuinely independent.” (low effort)
3. Add the caveat on the summary-table counts. (low effort)
4. Add a one-line explanation of subagent and Task tool, plus a short roadmap paragraph. (low-medium effort)
5. When Claude Code is available, run one subagent-mode comparison to see whether the gap between modes is meaningful. (medium effort)

Residual risk if only the minimum is done: the repository goes public with an unqualified independence claim and no visible proof it works, which is not catastrophic for a prompt-based tool, but it is exactly the kind of issue a skeptical reader would raise first.

---

## Final note

This example is intentionally a design review of the skill itself. It demonstrates how the skill behaves when used in a standard chat setting, and it clarifies the difference between a single-pass fallback and a genuinely independent subagent setup. It is useful as a documentation artifact, but it is not a substitute for a real-world benchmark.
