---
name: implement
description: Add or change a feature by following the project's documented structure first, then the code graph, then existing code patterns. Stops and asks when docs and code disagree, warns before large changes, follows the repo's testing habits, and updates affected docs afterwards. Use when the user asks to implement, add, build, or change a feature, endpoint, screen, or behavior in an existing codebase.
argument-hint: "<what to build or change>"
---

# implement

Make the change the way this codebase already does things. The order of authority is: **docs → code graph → existing code**. Never introduce a new pattern when the repo already has one for the same job.

## Step 1: Understand the request

Restate the change in one or two sentences. If the request is ambiguous about behavior (not about implementation details), ask before reading code.

## Step 2: Read the docs

Look for, in order: `AGENTS.md`, `CLAUDE.md`, `docs/` (especially `conventions.md`, `structure.md`, `architecture.md`, relevant `flows/*.md`), ADRs (`docs/adr/`, `adr/`), `CONTRIBUTING.md`.

From them, extract:
- Where this kind of code goes
- Conventions that apply (naming, error handling, config, tests)
- Decisions that constrain the change

If no docs exist, tell the user once: "No project docs found. I'll follow existing code patterns. Run `docs-init` later so future changes can follow documented rules." Then continue. Do not run `docs-init` yourself.

## Step 3: Read the code

Use the best tool available:
1. **Codegraph** if available: find the symbols the change touches, their callers (blast radius), and the closest existing feature to copy from.
2. Otherwise: search for the closest existing feature (same kind of endpoint, screen, job) and read it end to end.

Always find **one or two existing examples of the same kind of change** and treat them as the template: folder placement, naming, layering, error handling, tests.

## Step 4: Check for conflicts

If docs say one thing and code does another (for example docs say "errors are wrapped with `pkg/errors`" but recent code uses `fmt.Errorf("%w")`), **stop and ask the user** which to follow. Show both with file references. Do not pick one silently.

## Step 5: Size check

Warn the user and wait for a go-ahead before writing code if any of these is true:
- The change touches more than ~8 files or more than one module/service
- It changes a public API, DB schema, shared type, or config contract used by others
- It modifies an existing feature's behavior, not only adds a new one
- You are unsure where it belongs

The warning lists: files to create/modify, existing features affected, and the pattern you will copy. For small, clearly scoped changes, skip the warning and proceed.

## Step 6: Implement

- Mirror the example(s) found in Step 3.
- Follow the documented error-handling convention. Never swallow errors to make code compile.
- Add config keys where existing keys live, and to `.env.example` / sample config if the repo has one.
- Do not refactor unrelated code. Note refactor ideas in your summary instead.

## Step 7: Tests

Follow the repo's habit:
- The touched area has tests → add or update tests in the same style, location, and framework.
- The repo has tests elsewhere but not here → mention it, do not force a new test setup.
- The repo has no tests → do not add a test framework.

Run the relevant tests and linters if commands are documented or obvious (Makefile, package scripts). Report results honestly, including failures.

## Step 8: Update docs

If docs exist, update what the change affects: new route in `api.md`/`routes.md`, new flow or changed step in `flows/`, new config key, new table, new convention. Replaced decisions get struck through (`~~old~~`) with a dated note, not deleted.

If docs do not exist, offer to run `docs-init`. Do not create partial docs on your own.

## Finish

Summarize: what changed (files), which existing example was followed, tests run and results, docs updated, and anything left for the user. Git (branch, commit, push) is the user's job. Do not commit.
