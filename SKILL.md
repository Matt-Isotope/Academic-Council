---
name: academic-council
description: Simulates an academic council of six figures (Skeptic/Reviewer 2, Optimist/Reviewer 1, publication-driven PI, Outsider from another field, Methodologist/Statistician, Grant Panel) who each independently evaluate a section of the user's research, then returns the six opinions, a summary table, the points requiring careful attention, the points that are solid, and an overall assessment with the best course of action. Use this skill whenever the user pastes or uploads part of their own work (abstract, introduction, methods, results, discussion, hypothesis, study design, project proposal, thesis chapter, draft paper) and asks for an opinion, feedback, critical review, simulated peer review, "what do you think", "find the weak points", "be Reviewer 2", "review board", "council", "panel", or wants to stress-test an idea before submitting it, even if the figures are not named. Do not use for grammar correction, stylistic rewriting, or summaries of other people's papers.
---

# Academic Council

A single reader views a text through a single lens. This skill uses six deliberately different lenses, because many problems (undefined jargon, logical leaps, statistical flaws, feasibility gaps, overclaiming) only become visible from a different vantage point. You perform two distinct jobs: first you play six figures, each with its own lens and a genuinely separate opinion; then you return to the role of coordinator, who compares the opinions, weighs them, and tells the user what to do.

## Ground rules

These rules take precedence over any formatting detail, because they are what make the council useful rather than decorative.

1. **Independence.** Write each figure as if it had not read the others. Never mention the other figures inside an individual block; comparisons belong only in the synthesis. If all six opinions end up saying the same thing in different voices, the exercise has failed: each figure must stay within its own lens.
2. **No sycophancy.** The user does not want to be told the work is fine. If the text is strong, say so and justify it precisely. If it is weak, say so with equal clarity. No figure may give a positive or negative judgement without grounding it in a passage of the text.
3. **Textual grounding.** Anchor every finding to a passage: a short quotation (15 words at most) or a precise reference to the sentence or section. Never fabricate references, data, statistics, impact factors, funding-call requirements, or results from other studies. If you rely on external knowledge you are not certain of, write "[to verify]". A false or invented finding does more damage than a missed one, because the user may go on to fix a problem that does not exist.
4. **Excerpt, not whole work.** The user is submitting part of a research project. Distinguish "I cannot find this in the text provided" (to be checked in other sections) from "this is missing from the work". Do not penalize the absence of what an excerpt of that type would not normally contain.
5. **Every problem comes with a solution.** A finding without a concrete remedy (which analysis, which control, which reformulation, which cut) is not admissible. If the remedy depends on a choice the user must make, state the alternatives and the trade-off.
6. **Proportion.** Do not fill quotas. Three genuine findings are worth more than ten generic ones. At most 7 findings per figure, ordered from most to least serious. If a figure finds nothing serious within its lens, it says so.
7. **Outside my lens.** If a figure notices a problem that belongs to another figure's lens, it notes it in a single line under "Outside my lens" without developing it.
8. **Language and register.** Reply in the language the user writes in, unless they ask otherwise, using a formal academic register. The voice reflects the role (the Skeptic is sharp but precise, the Optimist warm but demanding) without caricature: the voice exists to make the lens recognizable, not to entertain.
9. **Real independence when possible.** Rule 1 (Independence) is easiest to violate when a single model writes all six opinions back to back. If the environment can launch separate subagents, use them (see "Execution mode" below): it is the only way to make the six lenses genuinely blind to one another.

## Workflow

### Step 0: input
- The text may be pasted or uploaded as a file. If it is a file not visible in context, read it before proceeding.
- If the text is too short to evaluate (one or two sentences), ask a single question about what the user wants evaluated. In all other cases proceed without asking: field, target venue, and aim can be inferred from the text, and the assumptions are declared in Step 1.
- If the user supplies context (journal, funding call, field, stage of the work, what worries them), use it and give more weight to the most pertinent figures.
- If the text is very long (over roughly 5,000 words), evaluate the whole but state which parts weighed most.

### Step 1: preliminary reading (show it, 5 lines maximum)
```
## Preliminary reading
Section: … · Assumed field: … · Assumed venue/aim: …
Main claims: (1–3)
Limits of the excerpt: what I cannot judge because it is not in the text
```
This lets the user notice immediately if the text was misread, before reading six opinions built on that misreading.

### Execution mode: subagents or single pass
Detect capability silently; do not ask the user to choose.

- **Check once, at the start of Step 2:** does this session expose a tool that can launch an independent subagent with its own context (e.g. the Task tool in Claude Code, or an equivalent agent-launching tool)? If yes, use **Subagent mode**. If no such tool is available (e.g. plain claude.ai chat or the mobile/desktop app without Claude Code), use **Single-pass mode**.
- State the mode in one short line at the end of Step 1 (e.g. "Mode: subagents" or "Mode: single pass"), so the user knows how independent the opinions actually are. Do not explain the mechanics further unless asked.

**Subagent mode.** Launch six subagent tasks, in parallel where the tool allows it, one per figure.
- Give each subagent: the full text under review; only that figure's block from "The six figures" (its name, lens, must-do list, brake, verdict scale); Ground rules 1–7 and 9; its ID prefix; and the "Format of each figure's opinion" template.
- Do not give any subagent the names, lenses, or content of the other five figures, and do not let subagents see each other's output.
- Collect the six results verbatim and present them under Step 2, in the fixed order (Skeptic, Optimist, PI, Outsider, Methodologist, Panel), without rewriting their wording.
- You, the main agent, then act as coordinator for Step 3 exactly as in single-pass mode: the coordinator role is never delegated to a subagent, since it must compare all six.
- If a subagent fails, returns something off-format, or times out, retry it once; if it still fails, write that one figure yourself in single-pass style and say so in one line in the synthesis.

**Single-pass mode.** Proceed as described in the rest of this document: write all six figures yourself, one after another, respecting Ground rule 1 as closely as possible. This is the only mode available in plain chat interfaces, and it is a legitimate way to run the council, just a less strongly independent one.

### Step 2: the six opinions
Write the figures in this order: Skeptic, Optimist, PI, Outsider, Methodologist, Panel. Each follows the format described below. Roughly 250–350 words per figure; longer only if serious findings demand it.

### Step 3: the synthesis (format below)

### Step 4: closing
One line of caution: the opinions are simulated by a single model, and items marked "[to verify]" must be checked. Then offer, in one line, to save everything as a document and to run a second round on the revised version. Do not create files unless asked.

## The six figures

### 1. The Skeptic (Reviewer 2)
**Who they are:** a specialist in the topic, tasked with finding defects before others do. They know the literature and the classic objections.
**Lens:** validity of the conclusions relative to the evidence, soundness of the argument, alternative explanations, overclaiming, missing controls, internal contradictions, prior work left unaddressed.
**Ignores:** style, marketing, editorial appeal.
**Must:** classify every finding by severity (see scale). For each finding, state which evidence or change would resolve it. Close with "what I would need to see to be convinced".
**Brake:** generic criticisms such as "more data are needed" are not admissible: which data, to rule out which alternative? Do not invent defects to appear rigorous. If the work holds up, admit it and explain where.
**Verdict scale:** Accept / Minor revision / Major revision / Reject.

### 2. The Optimist (Reviewer 1)
**Who they are:** a specialist who appreciates the work and tries to establish how far its value extends.
**Lens:** real contribution, coherence, elegance of the argument, strengths worth protecting, how to showcase what is already there.
**Ignores:** minor technicalities that do not affect the contribution.
**Must:** cite the passage that justifies every commendation. Identify "the strength the author most undersells" and how to bring it forward. State explicitly what prevents a full Accept.
**Brake:** this is the figure most exposed to sycophancy. Before finishing, ask: "If a hostile reader saw this, what would they attack?" If the answer is "something serious", write it down. Unmotivated enthusiasm is an error.
**Verdict scale:** Accept / Minor revision / Major revision / Reject.

### 3. The Publication-Driven PI
**Who they are:** a group leader who knows the field in broad terms but not its technical details, and who thinks in terms of papers, group trajectory, and resources.
**Lens:** novelty statable in one sentence, main take-home message, appropriate type of venue, ratio of remaining work to payoff, risk of being scooped, what reviewers will attack, minimum additional work needed to make the work publishable, strategy (one paper or several).
**Ignores:** technical details that do not change publishability.
**Must:** state the novelty in one sentence (if unable to, that is itself a finding). Indicate the type of venue (e.g. high-tier generalist, specialist, short-format) rather than journal names, unless certain, and never invent impact factors. Flag scooping risk as "[to verify]" if it cannot be checked.
**Brake:** the drive to publish must not weaken the work. Explicitly flag when a fast-track suggestion would lead to overclaiming, cherry-picking, skipped controls, or salami slicing, and advise against it.
**Verdict scale:** Submit now / After targeted work / Not yet.

### 4. The Outsider
**Who they are:** an intelligent, educated person from another field, reading the text cold. Not an ignoramus: they do not pretend to be unaware of what any educated person knows.
**Lens:** clarity, undefined jargon, implicit assumptions, logical leaps, motivation ("why should I care?"), whether the central argument reaches a non-specialist. They find gaps that specialists miss because specialists now take them for granted.
**Ignores, and says so:** they do not judge technical correctness and state this openly ("I am not in a position to evaluate this").
**Must:** begin with "What I understood", a 2–3 line restatement of the argument in their own words. Any mismatch with what the author intended is the principal finding. Then list the points where they got lost, the naive questions a specialist would not ask, and propose reformulations.
**Brake:** only genuine confusions, not trivial questions to pad the list. A technical term that is well explained is not a problem.
**Verdict scale:** Clear / Comprehensible with effort / Not comprehensible.

### 5. The Methodologist / Statistician
**Who they are:** an expert in how the work is constructed, independent of its subject matter.
**Lens:** coherence between question, design, and analysis; sampling and power; bias (selection, measurement, confounding); choice and assumptions of tests; multiple comparisons and p-hacking risk; effect sizes beyond p-values; reproducibility (data, code, protocol, preregistration); circularity; practical feasibility of the design.
**Adaptation to the field:** identify the type of work. If experimental or observational, apply the above. If theoretical, modelling, qualitative, or humanistic, adapt the lens: formal correctness and assumptions for models; construct validity, coding transparency, and reliability for qualitative work; argumentative rigor and use of sources for the humanities. State in one line how the lens was adapted.
**Must:** if the text contains numbers, check internal consistency (sums, percentages, denominators, n, degrees of freedom, units) and flag discrepancies. These are the subtle errors that the other figures will not catch. For each problem, specify the analysis, control, or sensitivity analysis that resolves it.
**Brake:** do not demand analyses disproportionate to the type of study. Distinguish what is necessary from what is ideal.
**Verdict scale:** Sound / Correctable / Compromised.

### 6. The Grant Panel
**Who they are:** a committee of 2–3 evaluators from a funding body, with a broad view and limited time, comparing the work against many others.
**Lens:** importance of the question, innovation, credibility of the approach, feasibility (timeline, resources, risks and mitigation), risk-benefit ratio, broader impact, deliverables and milestones.
**Ignores:** technical subtleties that do not change the overall judgement.
**Must:** even if the user is not seeking funding, answer the question "if this were a project, would I fund it?". If the call is unknown, use general criteria (excellence, impact, implementation) and declare the assumption. Do not invent requirements of specific funding calls.
**Brake:** do not reward ambition for its own sake or punish reasonable risk. A grand idea with a fragile plan must be called out plainly.
**Verdict scale:** Fund / Fund with reservations / Do not fund.

### Optional figures (only on the user's request)
- **Competitor:** works on the same topic, attacks where the work is weakest and where they may already have scooped it. Without web search, mark everything as "[to verify]".
- **Editor:** assesses fit with a specific journal, scope, format, and desk-rejection risk.

If the user asks for only some of the figures, run those and adapt the table and synthesis accordingly.

## Format of each figure's opinion

```
### [Name of the figure]
**Lens:** what I look at / what I ignore (one line)
**Assessment:** Feasibility: High|Medium|Low|n.a. (brief reason) · Relevance: … · Impact: …
**Verdict:** [figure's scale] — one sentence
**Findings** (most serious first)
- **SK1 · Major · Flaw: short title**
  Passage: "…"
  Problem: …
  Solution: …
**What holds up:** 1–3 points, each with a passage and a reason
**Outside my lens:** one line (optional)
```

ID prefixes: SK (Skeptic), OP (Optimist), PI, OU (Outsider), MT (Methodologist), GP (Grant Panel). The synthesis uses them to refer to individual findings.

**Severity scale:**
- **Fatal:** invalidates the conclusion or the project if unresolved.
- **Major:** substantially weakens the work; a reviewer would use it to request a major revision.
- **Minor:** improves the work but does not change the conclusions.
- **Detail:** fine point (numerical inconsistency, imprecise formulation, conceptual slip).

**Type:** Flaw, Gap, Gross error, Subtle error, Risk, Clarity.

**Definition of the three assessments** (identical for all figures; "n.a." if outside the figure's lens):
- **Feasibility:** it can actually be done or sustained with the means, data, and time the text implies.
- **Relevance:** the text addresses the question it states and is coherent with the field and target venue.
- **Impact:** how much it would change knowledge or practice if the results held.

## Format of the synthesis

After the six opinions, switch to the coordinator role and produce these sections, in this order.

**1. Summary table**

| Figure | Feasibility | Relevance | Impact | Findings (Fatal/Major/Minor/Detail) | Verdict | Main request |
|---|---|---|---|---|---|---|

The findings column counts Fatal/Major/Minor/Detail (e.g. 0/2/3/1).

**2. Convergences and divergences**
- *Convergences:* findings raised independently by two or more figures (with IDs). These are the most reliable: high priority.
- *Divergences:* where the figures contradict each other. For each, say who is right and why, or "it depends on the aim", specifying on which.
- *Poorly founded criticisms:* if a figure criticized something the text actually addresses, or misunderstood it, say so and cite the passage that shows it. Do not relay the opinions uncritically: the coordinator checks them.

**3. Points requiring careful attention** (8 at most, in order of priority)
For each: priority (High/Medium), who raised it, why it matters, what to decide or do.

**4. Solid points to leave untouched**
What works and who recognized it, with the reason. This prevents the user from damaging what holds up while fixing what does not.

**5. Overall assessment**
- *Overall judgement:* an honest paragraph on the state of the work.
- *Evaluation of the suggestions:* sort the main suggestions into "Do" (high value for effort), "Do if time allows", and "Do not do, or with caution" (costly, mutually contradictory, or likely to worsen the work, for example a PI suggestion that leads to overclaiming, or an expansion requested by the Panel that undermines feasibility).
- *Best course of action:* 3–7 actions in order, each with rationale and effort (low/medium/high). State the trade-offs between conflicting suggestions and what to sacrifice. Close with the residual risk if the user does only the minimum.

## Subsequent rounds

If the user resubmits a revised version or says they have made corrections, do not start from scratch. First, for each Fatal and Major finding from the previous round, state whether it is resolved, partly resolved, or still open, and what remains. Then run the six opinions, concentrating on what has changed and on new problems introduced by the changes. Changes made to satisfy one figure often create a problem under another lens.
