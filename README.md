# Academic Council

A Claude skill that simulates an academic council of six reviewer perspectives:

- Skeptic (Reviewer 2)
- Optimist (Reviewer 1)
- Publication-driven PI
- Outsider from another field
- Methodologist / Statistician
- Grant Panel

The skill evaluates a research excerpt, identifies likely weaknesses and strengths, and produces a coordinated recommendation after comparing the different perspectives. It is designed to help researchers stress-test a draft before submission, not to replace expert human review.

This repository contains the skill prompt itself and the project documentation. The focus is on usability, transparency, and clear installation guidance for Claude users.

This project was developed with the contribution of AI-assisted tooling and iteration, and it is intended to support human academic judgment rather than replace it.

## What it does

1. Reads the excerpt and provides a short preliminary reading: assumed field, likely venue or aim, main claims, and limitations of the excerpt.
2. Runs six evaluations, each with its own lens, verdict scale, and severity-tagged findings.
3. Produces a synthesis with:
   - a summary table
   - convergences and divergences
   - points requiring careful attention
   - points that appear solid
   - an overall recommendation and course of action

Findings are grounded in passages from the submitted text whenever possible. The skill distinguishes between Fatal, Major, Minor, and Detail findings and proposes a concrete remedy for each substantive problem.

## Why use a council instead of one general critique?

The council is structured to make different review criteria explicit rather than asking one model for an undifferentiated list of comments. Each perspective has a defined lens, verdict scale, and set of constraints. The coordinator then compares the results, identifies convergences, checks poorly founded criticisms, and prioritizes actions. This structure does not guarantee better academic judgement, but it makes the review process more inspectable and actionable.

## What it is not

This skill is not:

- a grammar checker
- a stylistic rewriting engine
- a substitute for a supervisor, referee, or academic committee
- a tool that automatically verifies external claims, citations, or funding requirements

The output should be treated as a structured starting point for self-review, not as final expert judgement.

## Execution mode

The skill detects whether the environment supports independent subagents. A **subagent** is a separate AI process or context launched to handle one task independently.

- **Subagent mode:** in Claude Code or a similar environment, the six reviewers can run as genuinely independent subagents. Each reviewer receives only its own instructions and the text, and cannot see the other reviews.
- **Single-pass mode:** in a plain chat interface without subagents, one model writes the six reviews while following explicit separation rules. The perspectives are still useful, but their separation is instruction-based rather than architectural, so some cross-influence may occur.

Claude Code's `Task` tool is one example of a mechanism that can launch a separate context; the exact capability depends on the environment. The mode used is reported in the output, and you do not need to choose it manually.

## Installation

1. Download `academic-council.skill` from this repository, or use `SKILL.md` as the source version.
2. Add the skill to Claude using the relevant skills interface, such as Settings → Capabilities → Skills, or the equivalent workflow in Claude Code or Cowork.
3. Paste or upload an excerpt of your research and ask for feedback, a review, or a stress test. You can also name the skill directly:

   > Run the academic council on this abstract.

If you only have `SKILL.md`, you can also paste its contents into a project's custom instructions or place the skill folder in your Claude Code skills directory. The file contains the complete skill; there is no runtime code to install.

## Quick usage examples

```text
Review this abstract for weaknesses and strengths using the academic council.
```

```text
Run the academic council on this methods section. Focus especially on design, sampling, and analysis.
```

```text
Stress-test this project proposal from multiple perspectives before I submit it.
```

```text
Review this discussion section and tell me which claims are overextended.
```

The skill can be used with abstracts, introductions, methods sections, results, discussions, hypotheses, project proposals, thesis chapters, and draft papers. It is intended for the user's own work, rather than for summarizing or editing somebody else's paper.

## Current evaluation status

The design has been reviewed internally, but the repository does not yet include a systematic benchmark or a published worked example on a real research text. This is an early, openly documented release. If you use it, feedback and example-based evaluation are welcome.

## Roadmap

Planned improvements include:

- adding anonymized worked examples from real research excerpts, with permission
- comparing single-pass and subagent-mode outputs on the same text
- developing a small evaluation set with planted weaknesses and known expectations
- considering optional Editor and Competitor perspectives after the core workflow has been tested

These are future goals, not claims about current capabilities.

## Repository structure

| File | Purpose |
| --- | --- |
| `SKILL.md` | The source prompt: rules, workflow, reviewer definitions, and output format. |
| `academic-council.skill` | Packaged version ready to install as a Claude skill. |
| `README.md` | Project overview, installation, examples, and limitations. |
| `CHANGELOG.md` | Version history and key changes. |
| `CONTRIBUTING.md` | Guidelines for contributing and improving the repository. |
| `LICENSE` | MIT license. |

## Limitations and caveats

- In single-pass mode, independence is enforced by instruction rather than architecture, so some overlap between reviewer voices may still occur.
- The skill does not verify external claims, citations, datasets, funding requirements, or impact factors. Uncertain items are marked `[to verify]` and should be checked by the user.
- It evaluates the excerpt provided, not the full work, and does not penalize the absence of content that would normally not appear in that excerpt.
- The skill has been tested informally and should be treated as a structured review aid rather than validated scientific methodology.
- Recommendations depend on the quality and completeness of the text supplied to Claude.
- The severity counts in the synthesis table are descriptive counts within each reviewer perspective, not a common quantitative score across figures. The figures use different verdict scales and should not be combined mechanically.

## Contributing

Contributions are welcome, especially improvements to clarity, usability, reproducibility, and documentation.

Before proposing changes:

- keep the skill itself stable unless a prompt change is clearly intentional and justified
- do not silently weaken safeguards against fabrication or overclaiming
- prefer focused documentation and practical improvements when possible
- explain the purpose and expected benefit of changes to the skill prompt

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for more information.

## Version history

See [`CHANGELOG.md`](CHANGELOG.md) for the project history.

## License

This project is released under the MIT License. See [`LICENSE`](LICENSE).

## Acknowledgements

This project was created as a practical academic review aid and iteratively refined with AI-assisted prompting and review. The work reflects a combination of human direction and AI contribution, and it is intended to support critical thinking and self-review rather than replace scholarly judgement.
