# Changelog

## v0.4
- Renamed the skill from `consiglio-accademico` to `academic-council` (frontmatter name, package file, repository references). Removed the leftover Italian trigger phrases from the description; the skill still replies in whatever language the user writes in (Ground rule 8), only its identifiers and packaging are now English.

## v0.3
- Added subagent execution mode: in Claude Code (or any environment that can launch subagents), the six figures run as genuinely independent subagents instead of a single-pass write-up.
- Added Ground rule 9 on real independence, and a new "Execution mode" section describing detection, subagent handoff, and the single-pass fallback.

## v0.2
- Rewrote the entire skill in academic English (was Italian).

## v0.1
- Initial version: six figures (Skeptic, Optimist, PI, Outsider, Methodologist, Grant Panel), ground rules against sycophancy and fabrication, preliminary reading step, per-figure opinion format with severity-tagged findings, and coordinator synthesis (table, convergences/divergences, priorities, solid points, overall assessment).
