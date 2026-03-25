---
name: refresh-agents
description: Refresh agent guidance either locally for one project or globally for the shared agents infrastructure. Use when rebuilding a project's AGENTS.md or when reviewing the shared agents repo, rules, scripts, skills, and principles.
---

# Agents Refresh

Refresh agent guidance in one of two modes:

- `local`: rebuild one project's `AGENTS.md` from the shared baseline while preserving project-specific rules and generating `Project Specific Rules`, `Standard Rules`, and `Skills`
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

## Skill References

When you mention other skills, follow these practical rules to avoid wasting context:
  - Mention skills explicitly when they are genuinely repo-relevant.
  - Prefer a short conditional instruction over a bare link dump.
  - Keep operational skill references centralized in `Skills`; avoid scattering them elsewhere except for the required regeneration note.
  - Do not summarize the skill in `AGENTS.md`; let the skill own its own detail.
  
Do not add skill references just for discovery. Assume that the available list of skills is already known.
Point to skills to support selection, not invite eager loading.
Use skill names, not explicit file paths.

Examples:
- Good: `Use the swiftui-pro skill for SwiftUI view work.`
- Bad: `Also consider these 12 related skills...`

## References

- `references/local-mode.md`: local `AGENTS.md` rebuild workflow, three-section output rules, stack detection, and baseline verification
- `references/global-mode.md`: shared-repo review workflow, rules cleanup policy, and verification
- `references/final-checklist.md`: required response items for local mode and global mode
