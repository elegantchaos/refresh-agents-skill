# Local Mode

Use local mode when refreshing one project's `AGENTS.md`.

## Shared Inputs

Resolve shared guidance from the team's shared agents repository:

- `~/.local/share/agents/references/COMMON.md`
- relevant files under `~/.local/share/agents/references/`

Required working inputs:

- target project repository
- target project's existing `AGENTS.md`, if present
- repo evidence for project identity and stack detection, such as `README*`, package metadata, manifests, and top-level docs

## Target Output

Produce a compact, project-targeted `AGENTS.md` with exactly these sections:

- `Project Specific Rules`
- `Standard Rules`
- `Skills`

When inserting shared references into the `Skills` section:

- use raw home-relative `~/...` paths
- use plain path text, not markdown links

## Workflow

1. Load context.
   - Detect whether the target repository already has an `AGENTS.md`.
   - If it exists, read it first.
   - Read `~/.local/share/agents/references/COMMON.md` and only the reference modules relevant to the detected stack.
   - Detect technologies in use from repo evidence such as `.swift`, `Package.swift`, `.xcodeproj`, `pyproject.toml`, `requirements*.txt`, `package.json`, and `tsconfig.json`.
2. Write `Project Specific Rules`.
   - If `AGENTS.md` already exists, retain project-specific policies, constraints, architecture notes, and workflows at the top.
   - Remove or rewrite only clearly obsolete or contradictory local rules.
   - If `AGENTS.md` does not exist, start `Project Specific Rules` with exactly one bullet by default.
   - Make that bullet a concise, durable statement of what the repository is for.
   - Derive it from current repo evidence such as `README*`, package metadata, manifests, or top-level docs.
   - Keep it short and factual.
   - Do not add extra bullets unless the user explicitly asks for them.
3. Write `Standard Rules`.
   - Base this section on `~/.local/share/agents/references/COMMON.md`.
   - Always preserve the force of the baseline requirements from `~/.local/share/agents/references/COMMON.md`.
   - Include core guidance from `~/.local/share/agents/references/COMMON.md`, including engineering principles, testing and validation expectations, safety, and source-quality rules.
   - Add stack-relevant guidance from `~/.local/share/agents/references/` modules only when those languages, tools, or services are actually used.
   - Exclude unrelated modules.
   - Prefer concrete, checkable instructions over narrative explanation.
   - Compress for agent ingestion when helpful, but do not weaken meaning.
   - Rewrite shared guidance as direct rules instead of citing local guidance files in this section.
   - Do not mention skills, skill names, or raw `~/...` guidance paths directly in this section.
   - Avoid detailed guidance in this section if it would overlap with a skill (and have the effect of pinning the instructions if the skill is later updated)
4. Write `Skills`.
   - Add one bullet per shared skill that is in scope for the project.
   - Use an imperative instruction for each bullet, such as `Use <path> for git operations.` or `Follow <path> for SwiftUI guidance.`
   - Include only the skills relevant to the detected stack and workflows.
   - If the project depends on a shared non-skill guidance file that agents should consult directly, place that explicit path here rather than in `Standard Rules`.
   - Use the root-level reference modules and shared skills only when they are actually relevant to the project.
5. Add the regeneration note.
   - At the bottom of `AGENTS.md`, add `To refresh this file, use the <path-to-skill> skill.` with the actual home-relative path to this skill.
6. Verify baseline requirements.
7. Lint for softened requirement language in mandatory clauses.

## Fresh File Rules

For fresh-file creation, do not put any of the following into `Project Specific Rules`:

- platform versions
- folder layout
- formatter or linter choices
- test framework
- CI details
- current architecture or implementation style
- concurrency settings
- API design preferences
- paths to shared references or shared skills
- validation workflow
- git or GitHub workflow rules
- stack detection evidence

Good sentence patterns:

- `This repository is a <project type> for <project purpose>.`
- `This repository contains <product/system> for <purpose>.`
- `This repository is the <library/service/app/tool> that <does X>.`

## Baseline Verification

Verify that these clauses remain present in `Standard Rules` with equivalent force:

- testing: red/green TDD for non-UI code
- UI expectation: create previews for UI code
- validation discipline: follow the validation workflow and report skipped checks
- safety: do not perform destructive actions without explicit approval
- safety: if unexpected workspace changes appear, pause and confirm direction
- source quality: prefer trusted primary sources for technical decisions

If any required clause is intentionally omitted, record the rationale in the final response.

Also verify that `Standard Rules` does not contain explicit skill references or raw `~/...` guidance paths, and that those explicit references appear under `Skills` instead.

## Softened Requirement Phrases

Rewrite these phrases out of mandatory clauses unless the source baseline explicitly uses them:

- `when practical`
- `where feasible`
- `if possible`
- `try to`
- `ideally`
