# Academic-Council

A Claude skill that simulates an academic council of six reviewers — Skeptic (Reviewer 2), Optimist (Reviewer 1), publication-driven PI, Outsider from another field, Methodologist/Statistician, and Grant Panel — who each independently evaluate a piece of research (abstract, methods, hypothesis, proposal, thesis chapter, draft paper, ...) and return separate opinions, a summary table, and an overall recommendation.

It was built with Claude's help, iteratively, and has not yet been tested on a large sample of real texts. Treat the output as a structured starting point for self-review, not as a substitute for human reviewers or advisors.

## What it does

1. Reads the excerpt and shows a short preliminary reading (assumed field, target venue, main claims), so you can catch a misreading before six opinions get built on it.
2. Runs six independent evaluations, each with its own lens, verdict scale, and severity-tagged findings (Fatal / Major / Minor / Detail), each grounded in a quoted or referenced passage.
3. Switches to a coordinator role and produces:
   - a summary table (feasibility, relevance, impact, finding counts, verdict per figure)
   - convergences and divergences across figures, including a check on poorly founded criticisms
   - a prioritized list of points requiring attention
   - a list of solid points to leave untouched
   - an overall assessment that sorts suggestions into *do / do if time allows / do not do*, and a recommended course of action

## Execution mode

- **In Claude Code** (or any environment that can launch subagents): the six figures run as genuinely independent subagents, each seeing only its own instructions and the text, not the other five figures. This is the strongest form of independence the skill supports.
- **In plain Claude (claude.ai, the app, or any chat interface without subagents):** the same six figures are written by a single model pass, following explicit independence rules (no cross-referencing between figures until the synthesis). Weaker independence, but still usable.

The skill detects which mode is available and tells you which one it used; you don't need to choose.

## Installation

1. Download `academic-council.skill` from this repository (or build it yourself from `SKILL.md`, see below).
2. In Claude, add it as a skill (Settings → Capabilities → Skills, or the equivalent in Claude Code / Cowork).
3. Trigger it by pasting or uploading part of your research and asking for feedback, a review, or by naming it directly ("run the academic council on this").

If you only have `SKILL.md`, you can also just paste its content into a Project's custom instructions, or place the folder under your Claude Code skills directory — the file itself is the entire skill, there is no code to run.

## Repository contents

| File | Purpose |
|---|---|
| `SKILL.md` | The skill itself: description, rules, workflow, the six figure definitions, output formats. |
| `academic-council.skill` | Packaged version, ready to install in Claude. |
| `CHANGELOG.md` | What changed between versions. |
| `LICENSE` | MIT license. |

## Known limitations

- In single-pass mode, the six opinions are written by one model in one continuous context, so independence is enforced by instruction, not by architecture — some bleed-through between figures is possible despite the rules against it.
- The skill never verifies external claims (citations, impact factors, funding-call requirements): anything uncertain is marked `[to verify]` and must be checked by the user.
- It evaluates the excerpt given, not the full work; it explicitly avoids penalizing the absence of content that excerpt would not normally contain.
- Tested informally; feedback and issues are welcome.

## License

MIT — see `LICENSE`.
