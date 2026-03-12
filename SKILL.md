---
name: refresh-agents
description: Regenerate a project AGENTS.md from the shared agents repository baseline. Use when updating stale project agent instructions, syncing standards into a repo, or running the refresh-agents skill.
---

# Agents Refresh

Rebuild a project's `AGENTS.md` from the shared baseline while preserving project-specific rules.

## Shared Inputs

Resolve shared guidance from the team's shared agents repository:

- `<shared-agents>/instructions/COMMON.md`
- relevant files under `<shared-agents>/instructions/`

Required working inputs:

- target project repository
- target project's existing `AGENTS.md`, if present
- repo evidence for project identity and stack detection, such as `README*`, package metadata, manifests, and top-level docs

## Target Output

Produce a compact, project-targeted `AGENTS.md` with exactly these sections:

- `Project Specific Rules`
- `Standard Rules`

When inserting shared references into `AGENTS.md`:

- use raw home-relative `~/...` paths
- use plain path text, not markdown links

## Workflow

1. Load context

- Detect whether the target repository already has an `AGENTS.md`.
- If it exists, read it first.
- Read `instructions/COMMON.md` and only the instruction modules relevant to the detected stack.
- Detect technologies in use from repo evidence such as `.swift`, `Package.swift`, `.xcodeproj`, `pyproject.toml`, `requirements*.txt`, `package.json`, and `tsconfig.json`.

2. Write `Project Specific Rules`

If `AGENTS.md` already exists:

- retain project-specific policies, constraints, architecture notes, and workflows at the top
- remove or rewrite only clearly obsolete or contradictory local instructions
- otherwise keep existing-file refresh behavior unchanged

If `AGENTS.md` does not exist:

- start `Project Specific Rules` with exactly one bullet by default
- make that bullet a concise, durable statement of what the repository is for
- derive it from current repo evidence such as `README*`, package metadata, manifests, or top-level docs
- keep it short and factual
- do not add extra bullets unless the user explicitly asks for them

Good sentence patterns:

- `This repository is a <project type> for <project purpose>.`
- `This repository contains <product/system> for <purpose>.`
- `This repository is the <library/service/app/tool> that <does X>.`

For fresh-file creation, do not put any of the following into `Project Specific Rules`:

- platform versions
- folder layout
- formatter or linter choices
- test framework
- CI details
- current architecture or implementation style
- concurrency settings
- API design preferences
- paths to shared instructions or shared skills
- validation workflow
- git or GitHub workflow rules
- stack detection evidence

3. Write `Standard Rules`

- Base this section on `instructions/COMMON.md`.
- Always preserve the force of the baseline requirements from `instructions/COMMON.md`.
- Include core guidance from `instructions/COMMON.md`, including engineering principles, testing and validation expectations, safety, and source-quality rules.
- Add stack-relevant guidance from `instructions/` modules only when those languages, tools, or services are actually used.
- Exclude unrelated modules.
- Prefer concrete, checkable instructions over narrative explanation.
- Compress for agent ingestion when helpful, but do not weaken meaning.
- If uncertain, preserve shared principles in `AGENTS.md` and point optional detail to shared modules or shared skills.

4. Point to shared guidance

- In each section of `AGENTS.md`, add raw `~/...` paths to the relevant shared `instructions/` modules and applicable shared skills.
- Use the root-level instruction modules `Principles.md`, `Validation.md`, `Trusted Sources.md`, and `Good Code.md` by default.
- Add language, technology, and service modules only when relevant.
- When a workflow is already captured by a shared skill, point to that skill instead of restating the detailed procedure.

5. Add the regeneration note

At the bottom of `AGENTS.md`, add the text:

`To refresh this file, use the <path-to-skill> skill.`

replacing `<path-to-skill>` with the actual home-relative path to this skill in the shared skills repository.

6. Verify baseline requirements

After drafting `AGENTS.md`, verify that these baseline clauses are still present in `Standard Rules` with equivalent force:

- testing: red/green TDD for non-UI code
- UI expectation: create previews for UI code
- validation discipline: follow the validation workflow and report skipped checks
- safety: do not perform destructive actions without explicit approval
- safety: if unexpected workspace changes appear, pause and confirm direction
- source quality: prefer trusted primary sources for technical decisions

If any required clause is intentionally omitted, record the rationale in the final response.

7. Lint for softened requirements

Check `Standard Rules` for softened requirement language in mandatory clauses:

- `when practical`
- `where feasible`
- `if possible`
- `try to`
- `ideally`

Remove or rewrite those phrases unless the source baseline explicitly uses them.

## Initial `Project Specific Rules` Examples

Bad:

- `Use Swift 6.2.`
- `Run swift test.`
- `Sources are in Sources/App.`
- `Use swiftui-pro.`
- `Keep APIs small.`

Good:

- `This repository is a SwiftPM library for building stable SwiftUI preview infrastructure with runtime injection and seeded fixture data.`
- `This repository is an iOS app for tracking personal workouts and recovery.`
- `This repository is a backend service for syncing customer billing events between Stripe and the internal ledger.`

## Final Response Checklist

Always include:

- files changed
- modules included and excluded
- evidence used for stack detection
- shared guidance files and skills referenced from `AGENTS.md`
- unresolved local-vs-shared instruction conflicts
- a baseline verification matrix with clause, status (`kept`, `rewritten-equivalent`, or `omitted-intentional`), and location in `AGENTS.md`
- any intentionally omitted baseline clauses with rationale
