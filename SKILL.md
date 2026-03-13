---
name: refresh-agents
description: Refresh agent guidance either locally for one project or globally for the shared agents infrastructure. Use when rebuilding a project's AGENTS.md or when reviewing the shared agents repo, rules, scripts, skills, and principles.
---

# Agents Refresh

Refresh agent guidance in one of two modes:

- `local`: rebuild one project's `AGENTS.md` from the shared baseline while preserving project-specific rules
- `global`: review and improve the shared agents infrastructure itself, including rules, scripts, skills, references, and principles

Read only the reference file needed for the current mode.

## Use This Skill When

- rebuilding or refreshing one repository's `AGENTS.md`
- reviewing the shared agents repository itself
- cleaning up shared rules, shared references, or agent-maintenance workflows

## Workflow

1. Decide whether the request is `local` or `global`.
2. For `local`, read `references/local-mode.md`.
3. For `global`, read `references/global-mode.md`.
4. Before finishing, read `references/final-checklist.md` for the required response items.

## References

- `references/local-mode.md`: local `AGENTS.md` rebuild workflow, stack detection, output rules, and baseline verification
- `references/global-mode.md`: shared-repo review workflow, rules cleanup policy, and verification
- `references/final-checklist.md`: required response items for local mode and global mode
