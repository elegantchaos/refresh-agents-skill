---
name: refresh-agents
description: Refresh agent guidance either locally for one project or globally for the shared agents infrastructure. Use when rebuilding a project's AGENTS.md or when reviewing the shared agents repo, rules, scripts, skills, and principles.
---

# Agents Refresh

Refresh agent guidance in one of two modes:

- `local`: rebuild one project's `AGENTS.md` from the shared baseline while preserving project-specific rules
- `global`: review and improve the shared agents infrastructure itself, including rules, scripts, skills, instructions, templates, and principles

Decide the mode from user intent. If the user asks to update a specific repository's `AGENTS.md`, use `local`. If the user asks to improve the shared setup, shared rules, workflows, or agent infrastructure, use `global`.

## Shared Inputs

Resolve shared guidance from the team's shared agents repository:

- `~/.local/share/agents/instructions/COMMON.md`
- relevant files under `~/.local/share/agents/instructions/`

Required working inputs:

- target project repository
- target project's existing `AGENTS.md`, if present
- repo evidence for project identity and stack detection, such as `README*`, package metadata, manifests, and top-level docs
- for global mode, the shared agents repository itself plus the Codex runtime rules under `<codex-home>/rules`

## Modes

### Local Mode

Use this when refreshing one project's `AGENTS.md`.

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
- Read `~/.local/share/agents/instructions/COMMON.md` and only the instruction modules relevant to the detected stack.
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

- Base this section on `~/.local/share/agents/instructions/COMMON.md`.
- Always preserve the force of the baseline requirements from `~/.local/share/agents/instructions/COMMON.md`.
- Include core guidance from `~/.local/share/agents/instructions/COMMON.md`, including engineering principles, testing and validation expectations, safety, and source-quality rules.
- Add stack-relevant guidance from `~/.local/share/agents/instructions/` modules only when those languages, tools, or services are actually used.
- Exclude unrelated modules.
- Prefer concrete, checkable instructions over narrative explanation.
- Compress for agent ingestion when helpful, but do not weaken meaning.
- If uncertain, preserve shared principles in `AGENTS.md` and point optional detail to shared modules or shared skills.

4. Point to shared guidance

- In each section of `AGENTS.md`, add raw `~/...` paths to the relevant shared `~/.local/share/agents/instructions/` modules and applicable shared skills.
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

### Global Mode

Use this when refreshing the shared agents infrastructure itself.

## Global Scope

- Shared canonical rules live in `~/.local/share/agents/codex/rules/*.rules`.
- Local runtime rules live in `<codex-home>/rules/*.rules`.
- `default.rules` is a catch-all and should stay small. It may be empty.
- The shared agents repository itself should be reviewed for process and guidance improvements.

## Global Decision Rules

Promote a rule into a shared `*.rules` file when all of the following are true:

- it authorizes a reusable command family rather than a one-off task
- it is not tied to a specific repository, branch, PR, issue, URL, path, or local history
- it would still make sense on another machine or in another repository using the same tool

Keep or leave a rule in `default.rules` only when it is genuinely not general enough for a shared file and is not safe to discard.

Remove a rule entirely when it is:

- already covered by an existing shared prefix
- tied to absolute machine paths or hardcoded working directories
- specific to one repository, PR, issue, release, URL, search query, JSON filter, or shell body
- a one-off cleanup, recovery, polling, or migration command that does not represent a reusable approval

## Global Rule Classification

Classify reusable rules by command family:

- `git ...` -> `git.rules`
- `gh ...` -> `github.rules`
- `swift ...` -> `swift.rules`
- `xcodebuild ...` and related Apple build or simulator inspection commands -> `xcode.rules`
- reusable tool wrappers and shared helper CLIs -> `tools.rules`
- non-destructive shell helpers and simple polling helpers -> `misc.rules`

If a command family appears repeatedly and does not fit an existing file cleanly, suggest a new shared rule file rather than stuffing unrelated rules into `default.rules`.

## Global Workflow

1. Read shared `~/.local/share/agents/codex/rules/*.rules`.
2. Read `<codex-home>/rules/default.rules` and any runtime `*.rules` files that are not symlinks to shared files.
3. Classify each entry in `default.rules`:
   - promote reusable entries into the correct shared rule file
   - remove entries already covered by shared prefixes
   - remove clearly one-off or machine-specific entries
   - keep only genuine leftovers
4. Sort each shared rule file lexicographically and remove duplicates within and across shared files.
5. Ensure every shared `*.rules` file has a symlink in `<codex-home>/rules/` pointing to `~/.local/share/agents/codex/rules/<name>.rules`.
6. Rewrite `default.rules` with only the remaining leftovers. If none remain, leave it empty.
7. Review the shared agents repository for worthwhile improvements to:
   - workflows and maintenance procedures
   - shared scripts and automation helpers
   - published skills and skill boundaries
   - copied instruction modules and templates
   - `~/.local/share/agents/instructions/COMMON.md` and `~/.local/share/agents/instructions/Principles.md`
8. Base those suggestions on:
   - current industry practice and established engineering guidance
   - observed user behavior and repeated requests
   - common patterns in code and repositories the user has been working with recently
   - new language, tooling, framework, or platform features
   - recurring friction seen in prior rule approvals, scripts, or skill usage
9. Verify the resulting shared files, runtime symlinks, final `default.rules` state, and any concrete repo changes you make.

## Global Verification

Check all of the following before finishing:

- no duplicate entries remain within or across shared rule files
- each shared rule file has a corresponding runtime symlink
- `default.rules` contains no entries already covered by shared prefixes
- `default.rules` contains no obviously machine-specific or one-off entries
- any suggested workflow or guidance changes are tied to concrete evidence or current best practice, not generic preference

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

- for local mode:
  - files changed
  - modules included and excluded
  - evidence used for stack detection
  - shared guidance files and skills referenced from `AGENTS.md`
  - unresolved local-vs-shared instruction conflicts
  - a baseline verification matrix with clause, status (`kept`, `rewritten-equivalent`, or `omitted-intentional`), and location in `AGENTS.md`
  - any intentionally omitted baseline clauses with rationale
- for global mode:
  - rules moved from `default.rules` into shared files
  - rules removed from `default.rules` as redundant
  - rules removed from `default.rules` as one-off or machine-specific
  - sort and de-dup verification result
  - symlink verification result
  - any ambiguous rules that need user confirmation
  - any suggested new shared rule files
  - any risky broad approvals that deserve review
  - any suggested or implemented improvements to workflows, scripts, skills, instructions, or principles
  - the basis for those suggestions when they come from recent usage, repeated friction, or newer platform guidance
