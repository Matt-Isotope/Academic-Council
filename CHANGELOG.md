# Changelog

## v0.6.1
- Fixed and completed `CITATION.cff` metadata, including the correct CFF schema version, project version, repository URL, abstract, keywords, and author ORCID.
- Documented the patch release as a metadata and maintenance release.
- The core skill workflow remains unchanged in this patch release.

## v0.6
- Clarified that the six figures are reviewer perspectives, with genuine independence available only in subagent mode.
- Added a glossary explanation for subagents and Claude Code's `Task` tool.
- Added a rationale explaining the value of the council structure beyond a general multi-perspective prompt.
- Added an explicit evaluation-status section stating that no systematic benchmark or published real-text example is included yet.
- Added a roadmap for worked examples, mode comparisons, evaluation data, and optional figures.
- Clarified that severity counts are descriptive within each figure and are not a cross-figure quantitative score.
- Added a demonstration example showing how the skill behaves in single-pass mode without Claude Code.

## v0.5
- Improved repository documentation and installation guidance.
- Clarified the purpose of the skill, its limitations, and the difference between a structured review aid and real peer review.
- Added contribution guidance and a polished project structure description.
- Explicitly acknowledged AI-assisted development and iteration in the project documentation.
- Kept the underlying skill prompt (`SKILL.md`) unchanged, as requested.

## v0.4
- Renamed the skill from `consiglio-accademico` to `academic-council` (frontmatter name, packaged file, and repository references).
- Removed leftover Italian trigger phrases from the description while preserving multilingual response behavior.

## v0.3
- Added subagent execution mode: in Claude Code (or any environment that can launch subagents), the six figures run as genuinely independent subagents instead of a single-pass write-up.
- Added Ground rule 9 on real independence and a new execution-mode section describing subagent handoff and the single-pass fallback.

## v0.2
- Rewrote the entire skill in academic English.

## v0.1
- Initial version: six figures (Skeptic, Optimist, PI, Outsider, Methodologist, Grant Panel), ground rules against sycophancy and fabrication, preliminary reading, structured opinion format, and coordinator synthesis.
