# Global Mode

Use global mode when reviewing or improving the shared agents infrastructure itself.

## Scope

- Shared canonical rules live in `~/.local/share/agents/codex/rules/*.rules`.
- Shared canonical reference modules live in `~/.local/share/agents/references/*.md`.
- Local runtime rules live in `<codex-home>/rules/*.rules`.
- `default.rules` is a catch-all and should stay small. It may be empty.

## Decision Rules

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

## Rule Classification

Classify reusable rules by command family:

- `git ...` -> `git.rules`
- `gh ...` -> `github.rules`
- `swift ...` -> `swift.rules`
- `xcodebuild ...` and related Apple build or simulator inspection commands -> `xcode.rules`
- reusable tool wrappers and shared helper CLIs -> `tools.rules`
- non-destructive shell helpers and simple polling helpers -> `misc.rules`

If a command family appears repeatedly and does not fit an existing file cleanly, suggest a new shared rule file rather than stuffing unrelated rules into `default.rules`.

## Workflow

1. Read shared `~/.local/share/agents/codex/rules/*.rules`.
2. Read `<codex-home>/rules/default.rules` and any runtime `*.rules` files that are not symlinks to shared files.
3. Classify each entry in `default.rules`.
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
   - shared references and principles
   - `~/.local/share/agents/references/COMMON.md` and `~/.local/share/agents/references/Principles.md`
8. Base those suggestions on:
   - current industry practice and established engineering guidance
   - observed user behavior and repeated requests
   - common patterns in code and repositories the user has been working with recently
   - new language, tooling, framework, or platform features
   - recurring friction seen in prior rule approvals, scripts, or skill usage
9. Verify the resulting shared files, runtime symlinks, final `default.rules` state, and any concrete repo changes you make.

## Verification

Check all of the following before finishing:

- no duplicate entries remain within or across shared rule files
- each shared rule file has a corresponding runtime symlink
- `default.rules` contains no entries already covered by shared prefixes
- `default.rules` contains no obviously machine-specific or one-off entries
- any suggested workflow or guidance changes are tied to concrete evidence or current best practice, not generic preference
