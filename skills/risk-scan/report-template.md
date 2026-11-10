# Risk scan: {{SCOPE_LABEL}}

| | |
|---|---|
| Date | {{DATE}} |
| Scope | {{diff vs <base> on <branch> / full repo / path <path>}} |
| Commit | `{{SHORT_SHA}}` |
| Files scanned | {{COUNT}} |
| Languages | {{LANGUAGES}} (checklists: {{CHECKLISTS_USED}}) |
| Linters run | {{LINTERS_RUN}} (incl. ast-grep rules if run) |
| Code navigation | {{NAV_TIER}} <!-- codegraph / LSP / ctags / ripgrep --> |
| Linters skipped | {{LINTERS_SKIPPED_OR_NONE}} |
| Previous report | {{PREVIOUS_REPORT_LINK_OR_NONE}} |

## Summary

| Severity | New | Still open | Resolved |
|---|---|---|---|
| Critical | 0 | 0 | 0 |
| High | 0 | 0 | 0 |
| Medium | 0 | 0 | 0 |
| Low | 0 | 0 | 0 |

## Findings

### [CRITICAL] {{SHORT_TITLE}}  ·  New
- **Where**: `{{file:line}}`
- **Type**: {{unhandled error / nil dereference / unchecked cast / out of range / missing timeout / unhandled async / ...}}
- **Scenario**: {{input/state}} → {{line}} → {{what breaks}}
- **Reachable from**: {{entry point, e.g. POST /orders, CheckoutScreen, consumer X}}
- **Covered by**: {{global handler if any, or "nothing"}}
- **Fix**: {{concrete suggestion in the repo's own style}}

<!-- Repeat per finding, ordered Critical → Low, then by reachability. -->

## Resolved since previous report

| Finding | Where it was | Previous report |
|---|---|---|
| {{TITLE}} | `{{file:line}}` | {{LINK}} |

## Not scanned

| File / area | Reason |
|---|---|
| {{PATH}} | {{renamed / binary / generated / no checklist for language}} |
