---
name: risk-scan
description: Scan code for unhandled errors and crash/panic risks (swallowed errors, nil/null dereference, unchecked casts, out-of-range access, missing timeouts, unhandled async failures) and write a dated report to docs/risk-scan/. Scans the current branch diff by default, the whole repo with --all, or a given path. Runs language linters when installed. Use when the user asks for a risk scan, error-handling audit, panic/crash check, or to find unhandled errors.
argument-hint: "[--all | <path>]"
---

# risk-scan

Find places where the code can fail without handling it, and report them with a concrete failure scenario for each.

## Rule zero: no scenario, no finding

Every finding must state a concrete path to failure: **input/state → line → what breaks**. Example: "`GetUser` returns `nil, nil` when the row is missing (`repo/user.go:41`) → `handler/user.go:27` reads `u.Name` → nil pointer panic → 500 with no log." If you cannot write that sentence, drop the finding. Pattern matches alone are not findings.

## Code navigation

Pick the best tool available, top to bottom. Check once at the start and remember the choice.

| Tier | Tool | How to detect | Use for |
|---|---|---|---|
| 1 | **Codegraph** | codegraph MCP tools available, or a `.codegraph/` folder in the repo | Symbols, callers/callees, call paths, blast radius |
| 2 | **LSP** | An `LSP` tool or a symbol-aware MCP server (such as Serena) is available, and the language server for the repo's language responds | Go to definition, find references, call hierarchy |
| 3 | **ctags** | `command -v ctags` reports universal-ctags (`ctags --version`) | Symbol map: where each type/function is defined |
| 4 | **ripgrep / grep + reading files** | Always available | Text search, then follow imports by reading |

Rules:
- Do not install anything and do not stop to ask. If you are on tier 3 or 4, tell the user in one line, e.g. "No codegraph or LSP found; using ripgrep. Caller lists may be incomplete. Installing codegraph or a language server improves this."
- On tier 3–4, find callers by searching for the symbol name and confirming each hit by reading it. Watch for interface/method dispatch, dependency injection, and string-based routing, which text search misses.
- State the tier used in your final summary.

## Step 1: Scope

| Invocation | Files scanned | Report name |
|---|---|---|
| `risk-scan` | Changed files vs base branch, plus uncommitted changes | `YYYY-MM-DD-diff-<branch>.md` |
| `risk-scan --all` | Whole repo | `YYYY-MM-DD-full.md` |
| `risk-scan <path>` | Files under path | `YYYY-MM-DD-path-<path-slug>.md` |

Base branch: `git merge-base HEAD origin/main`, falling back to `main`, then `master`. In diff mode, scan changed files fully but report only findings in changed lines **or** in code whose behavior the change affects (for example a caller of a function whose return contract changed).

Always skip: vendored deps, `node_modules`, generated code, build output, lockfiles, test fixtures. Deleted files are skipped. List renamed or binary files under "Not scanned".

For `--all`, count source files first. Show the count, the languages found, and an estimate of the effort, then ask the user to confirm before scanning.

If a report with the same date and name already exists, add a suffix (`-2`, `-3`).

## Step 2: Languages and checklists

Detect languages from file extensions in scope. Always load `checklists/core.md`. For each language, load its checklist if one exists:

| Language | Checklist |
|---|---|
| JavaScript / TypeScript (Node, React, Vue, Next, Nuxt) | `checklists/javascript.md` |
| Python | `checklists/python.md` |
| Java / Kotlin (incl. Android) | `checklists/java-kotlin.md` |
| Go | `checklists/go.md` |
| C# | `checklists/csharp.md` |
| PHP | `checklists/php.md` |
| Rust | `checklists/rust.md` |
| Swift | `checklists/swift.md` |

A language without a checklist is scanned with `core.md` only. Note this in the report.

## Step 3: Linters

Each checklist lists linters. For each one relevant to the scope:
1. Check if it is installed (`command -v`, or a local binary such as `node_modules/.bin/eslint`, or configured in the project).
2. If any is missing, tell the user which ones and the install command, and ask whether to continue without them. Do not install anything yourself.
3. If the user continues, mark the report **"Linters skipped: <list>"**.

Run installed linters on the scoped files only. Treat linter output as leads, not findings: confirm each one against rule zero, and drop false positives.

### ast-grep rules

This skill ships cross-language pattern rules in `rules/` (one folder per language, wired by `rules/sgconfig.yml`). They complement language linters and work even where none is configured.

1. Check `command -v ast-grep` (or `sg`). If missing, include it in the missing-tools warning above with the install command: `brew install ast-grep`, `npm i -g @ast-grep/cli`, `pip install ast-grep-cli`, or `cargo install ast-grep --locked`.
2. Run from the target repo root, on the scoped files only:
   ```sh
   ast-grep scan -c <this-skill-dir>/rules/sgconfig.yml --json=stream <files...>
   ```
3. Each hit has a `ruleId`, `severity` (`warning` = likely issue, `hint` = needs context), and a message. Hits are leads like linter output: confirm each against rule zero before it becomes a finding. `hint` rules are noisy by design; most will be dropped.
4. If ast-grep is skipped, list it under "Linters skipped".

## Step 4: Context

- **Docs**: read `AGENTS.md`, `docs/conventions.md`, or similar for the team's error-handling rules (global recover middleware, error boundaries, a result type). A risk already covered by a documented global handler is downgraded, not dropped. Say what covers it.
- **Reachability** (navigation tier chosen above): use callers to rank. Code reachable from an HTTP handler, message consumer, UI event, or many call sites ranks higher than a rarely used helper.

## Step 5: Analyze

Walk each scoped file with the loaded checklists. For each candidate, trace far enough to confirm or reject it: who calls this, can the value actually be nil/empty/error here, is it handled upstream.

Severity:
- **Critical**: crash/panic of a process or app, data corruption or loss, security-relevant failure (auth bypass on error), reachable from external input.
- **High**: request/operation fails with wrong result or wrong status, silent data inconsistency, resource leak under normal load.
- **Medium**: failure only in rare conditions (network error, timeout), poor error surfaced to user, missing timeout on an external call.
- **Low**: defensive gaps unlikely to trigger, error logged but context lost.

## Step 6: Compare with previous reports

Find the most recent earlier report in `docs/risk-scan/` with the same scope type (same branch for diff, `full` for --all, same path). For each of its findings, mark it:
- **Resolved**: the code no longer has the issue
- **Still open**: unchanged
- **New**: a finding not in the previous report

If there is no previous report, mark all findings New.

## Step 7: Write the report

Write `docs/risk-scan/<name>.md` using `report-template.md`. Create the folder if needed. Never edit or delete earlier reports: they are history.

## Finish

Tell the user: report path, counts per severity, the top 3 findings in one line each, linters skipped. Offer to fix findings using the `implement` skill. Do not change source code during the scan. Do not commit.
