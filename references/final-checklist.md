# Final Response Checklist

Always include:

## Local Mode

- files changed
- modules included and excluded
- evidence used for stack detection
- shared guidance files and skills referenced from `AGENTS.md`
- unresolved local-vs-shared guidance conflicts
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
