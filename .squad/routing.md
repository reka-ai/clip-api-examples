# Work Routing

How to decide who handles what.

## Routing Table

| Work Type | Route To | Examples |
|-----------|----------|----------|
| Rust implementation | Keaton | clip_generator.rs, check_status.rs, Cargo.toml |
| Code review | Keaton | Review PRs, check Rust quality, correctness |
| Documentation | McManus | README.md files, inline doc comments |
| Scope & priorities | Keaton | What to build next, trade-offs, decisions |
| Session logging | Scribe | Automatic — never needs routing |
| Work queue monitoring | Ralph | Issue triage, PR status, backlog |

## Issue Routing

| Label | Action | Who |
|-------|--------|-----|
| `squad` | Triage: analyze issue, assign `squad:{member}` label | Keaton |
| `squad:keaton` | Pick up issue and complete the work | Keaton |
| `squad:mcmanus` | Pick up issue and complete the work | McManus |

## Rules

1. **Eager by default** — spawn all agents who could usefully start work in parallel.
2. **Scribe always runs** after substantial work, always as `mode: "background"`. Never blocks.
3. **Quick facts → coordinator answers directly.** Don't spawn an agent for status questions.
4. **"Team, ..." → fan-out.** Spawn Keaton + McManus in parallel as `mode: "background"`.
5. **Anticipate downstream work.** When Keaton implements, spawn McManus to draft docs simultaneously.
