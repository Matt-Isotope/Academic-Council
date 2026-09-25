# Maintenance notes for the packaged skill

The repository contains two related representations of the skill:

- `SKILL.md` is the human-readable source prompt.
- `academic-council.skill` is the installable package.

When the source prompt changes, regenerate the package from the updated source before publishing a release. The package should contain the same current `SKILL.md` and any intended accompanying files; do not publish a package built from an older release.

For single-pass use, remember that reviewer agreement is a concordance rather than independent confirmation. Only subagent mode provides architectural separation between reviewer contexts. The coordinator should check whether one reviewer refers to another before treating an apparent convergence as especially reliable.

The packaged file is a binary archive and should be validated by opening it and checking its embedded files after regeneration.
