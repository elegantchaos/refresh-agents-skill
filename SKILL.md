---
name: refresh-agents
description: Regenerate a project AGENTS.md from the shared agents repository baseline. Use when updating stale project agent instructions, syncing standards into a repo, or running the refresh-agents skill.
---

# Agents Refresh

Rebuild project instruction artifacts from shared guidance while preserving project-specific rules.

## Shared Location

Shared baseline files live in the team's shared agents repository.

When refreshing another repository, resolve shared inputs from that configured location.

Required shared inputs:

- `<shared-agents>/instructions/COMMON.md`
- `<shared-agents>/instructions/`

## Goal

Produce a compact, project-targeted `AGENTS.md` for agents, while preserving project-local instructions and pointing directly to shared guidance files and skills for full detail.

The rebuilt agents file should contain two main sections:

- `Project Specific Rules`
- `Standard Rules`

## Required Inputs

- target project repository
- target project's existing `AGENTS.md`, if present
- shared `instructions/COMMON.md` and relevant files under `instructions/` (including subfolders such as `languages/`, `technologies/`, and `services/`)
- repo evidence for fresh-file identity statements (for example `README*`, package metadata, manifests, or top-level docs)

## Rebuild Workflow

1. Load context

- Detect whether the target project already has an `AGENTS.md`.
- If it exists, read the target project's existing `AGENTS.md`.
- Read shared common files and relevant instruction modules from the configured shared agents repository.
- Detect technologies in use from repo evidence (for example: `.swift`, `Package.swift`, `.xcodeproj`, `pyproject.toml`, `requirements*.txt`, `package.json`, `tsconfig.json`).
- For fresh-file creation, read current repo evidence such as `README*`, package metadata, manifests, or top-level docs to derive the repository identity statement.

2. Seed Project Specific Rules for fresh-file creation

- If no `AGENTS.md` exists, start `Project Specific Rules` with exactly one bullet by default.
- That bullet should be a concise, durable description of what the repository is for.
- The sentence should describe the project's purpose or role, not its tooling, layout, CI, implementation details, or coding conventions.
- Prefer patterns such as:
  - `This repository is a <project type> for <project purpose>.`
  - `This repository contains <product/system> for <purpose>.`
  - `This repository is the <library/service/app/tool> that <does X>.`
- Derive the sentence from current repo evidence such as `README*`, package metadata, manifests, or top-level docs.
- Prefer a sentence that will remain true even if implementation details or workflows change.
- Keep it short and factual.
- Do not add extra bullets unless the user explicitly asks for them during initial creation.
- For fresh-file creation, do not put platform versions, folder layout, formatter/linter choices, test framework, CI details, current architecture, implementation style, concurrency settings, API design preferences, links to shared instructions or shared skills, validation workflow, git or GitHub workflow rules, or stack detection evidence into `Project Specific Rules`.

3. Preserve Project Specific Rules for existing files

- Retain project-specific policies, constraints, architecture notes, and workflows at the top of rebuilt `AGENTS.md`.
- Remove or rewrite only clearly obsolete or contradictory local instructions.
- Existing-file refresh behavior is otherwise unchanged.

4. Rewrite Standard Rules

- Replace the rest of the file with compact agent guidance, based on `instructions/COMMON.md`.
- Always include core guidance from `instructions/COMMON.md` in rebuilt `AGENTS.md` (for example engineering principles, testing/validation expectations, safety, and source-quality rules).
- Add stack-relevant guidance from `instructions/` modules only when those languages/tools/services are used by the project.
- Prefer concrete, checkable instructions over narrative explanation.
- Ensure compact instructions preserve enough context for an agent to locate and load full detail from shared guidance files and shared skills.
- Apply the shared-guidance path rules in step 6 when referencing those materials from `AGENTS.md`.
- Exclude unrelated language/framework/service modules.
- You may compress guidance for agent ingestion, but must preserve intent and principles.
- Do not weaken mandatory baseline requirements with hedging language (for example: `when practical`, `where feasible`, `if possible`) unless the baseline itself includes such qualifiers.

5. Add regeneration note

- At the bottom of `AGENTS.md`, add this exact note: `To refresh this file, use the refresh-agents skill.`

6. Point to shared guidance

- In each section of the new `AGENTS.md`, add raw home-relative `~/...` paths to the relevant shared `instructions/` modules and applicable shared skills.
- Use plain path text, not markdown links, for those inserted paths.
- Include core cross-cutting modules by default (`Principles.md`, `Validation.md`, `Trusted Sources.md`, `Good Code.md`), then add only relevant language/technology/service modules.
- Prefer inserting raw `~/...` paths to shared skills for specialized workflows such as git, GitHub, validation, or framework-specific guidance.
- When a workflow is already captured by a shared skill, point to that skill rather than reproducing detailed procedure text in `AGENTS.md`.

7. Optional notes

- If needed, include in the final response:
- included and excluded modules
- detected stack assumptions
- unresolved local-vs-shared instruction conflicts

8. Verify mandatory baseline clauses

- After drafting `AGENTS.md`, verify that mandatory baseline clauses from `instructions/COMMON.md` are still present in `Standard Rules` with equivalent force.
- Required clauses (semantic equivalent wording allowed):
  - testing: red/green TDD for non-UI code
  - UI testing expectation: create previews for UI code
  - validation discipline: follow testing/validation workflow and report skipped checks
  - safety: do not perform destructive actions without explicit approval
  - safety: if unexpected workspace changes appear, pause and confirm direction
  - source quality: prefer trusted primary sources for technical decisions
- If any required clause is intentionally omitted, record it in notes with a rationale.

9. Run a hedging-language lint on Standard Rules

- Check for requirement-softening terms in mandatory clauses, including:
  - `when practical`
  - `where feasible`
  - `if possible`
  - `try to`
  - `ideally`
- Remove or rewrite hedged phrasing unless the source baseline explicitly uses it.

10. Produce a baseline verification summary

- In the final response, include a short matrix:
  - required clause
  - status (`kept`, `rewritten-equivalent`, `omitted-intentional`)
  - location in rebuilt `AGENTS.md`

## Project Specific Rules: Fresh-File Examples

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

## Selection Rules

- Treat `instructions/COMMON.md` as mandatory baseline guidance for every refresh.
- Treat `instructions/` files as detailed, context-specific guidance.
- Include non-specific principles in final `AGENTS.md` even when compacting text.
- Prefer root-level instruction modules (`Principles.md`, `Validation.md`, `Trusted Sources.md`, `Good Code.md`) as the default linked set for agent consumption.
- Include language modules only when that language is present.
- Include technology/service modules only when actively used.
- If uncertain, preserve shared principles in `AGENTS.md` and point optional detail to shared modules or shared skills using raw `~/...` paths.
- Preserve mandatory baseline obligations explicitly; compacting must not reduce requirement strength.
- Prefer one-way tightening over weakening: clarify or make rules stricter when needed, but do not silently relax shared requirements.

## Output Checklist

In the final response, always include:

- Files changed
- Modules included and excluded
- Evidence used for stack detection
- What shared guidance files and skills were referenced from `AGENTS.md`
- Any unresolved local-vs-shared instruction conflicts
- Mandatory baseline clause verification results
- Any intentionally omitted baseline clauses with rationale
