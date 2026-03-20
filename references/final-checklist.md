# Final Response Checklist

Always include:

## Local Mode

- files changed
- modules included and excluded
- evidence used for stack detection
- skills referenced from the `Skills` section
- any shared guidance files explicitly referenced from the `Skills` section
- unresolved local-vs-shared guidance conflicts
- any intentional repository overrides to referenced skills or shared guides
- confirmation that no `Standard Rules` bullet depends on the current wording of an in-scope skill
- confirmation that no `Standard Rules` bullet is a shared-baseline maintenance instruction unless the repository itself owns shared guidance or published shared assets
- a baseline verification matrix with clause, status (`kept`, `rewritten-equivalent`, or `omitted-intentional`), and location in `AGENTS.md`
- any intentionally omitted baseline clauses with rationale

## Global Mode

- rules moved from `default.rules` into shared files
- rules removed from `default.rules` as redundant
- rules removed from `default.rules` as one-off or machine-specific
- sort and de-dup verification result
- symlink verification result
- any ambiguous rules that need user confirmation
- any suggested new shared rule files
- any risky broad approvals that deserve review
- any suggested or implemented improvements to workflows, scripts, skills, references, or principles
- the basis for those suggestions when they come from recent usage, repeated friction, or newer platform guidance
