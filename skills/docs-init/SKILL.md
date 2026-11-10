---
name: docs-init
description: Bootstrap agent-ready project documentation in docs/ plus an AGENTS.md entry point, tailored to the project type (backend, frontend, fullstack, mobile). Focuses on flows and conventions an AI agent needs before changing code. Marks anything that cannot be derived from code and asks the user about it. Use when a repo has no docs, when the user asks to initialize, generate, or bootstrap docs, or when another skill reports missing docs.
argument-hint: "[--type backend|frontend|fullstack|mobile]"
---

# docs-init

Write the documentation an AI agent (and a new teammate) needs to change this codebase safely. The README is for humans browsing the repo. These docs go deeper: how requests and screens flow, where things live, and which rules the code follows.

## Output layout

```
AGENTS.md                  # entry point for any agent; short, links into docs/
docs/
├── overview.md            # what the project is, who uses it, glossary
├── architecture.md        # layers, dependency direction, diagram
├── structure.md           # folder map: what lives where, where new code goes
├── conventions.md         # naming, error handling, logging, testing, config
├── flows/
│   └── <flow-name>.md     # one file per important flow, end to end
├── <type-specific>.md     # see references/<type>.md
└── open-questions.md      # everything not derivable from code, for the user
```

Keep each file short and factual. Prefer tables and file paths over prose. Every claim should point to a file (`path/to/file.go:42`) so an agent can verify it.

If the repo already has `CLAUDE.md` and no `AGENTS.md`, create `AGENTS.md` and add one line to `CLAUDE.md` pointing to it. Never overwrite existing `CLAUDE.md` content.

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

## Step 1: Detect the type

Use `--type` if given. Otherwise detect with the same signals as the `readme` skill (mobile, fullstack, frontend, backend). If unclear, ask the user once. Then read `references/<type>.md` for the type-specific files and what each flow doc must cover.

## Step 2: Check what exists

- `docs/` exists: read every file. Only create files that are missing and only fill sections that are empty. Do not rewrite existing docs. If an existing doc contradicts the code, add an entry to `open-questions.md` instead of editing it.
- `AGENTS.md` exists: append a "Docs" section linking to the new files if it lacks one. Leave the rest alone.

## Step 3: Read the code

Start from the dependency manifest, entry files (`main.go`, `cmd/`, `src/main.*`, `app/`, `pages/`, `MainActivity`, `@main`), and router/navigation registration. Then trace each flow from entry point to storage with the navigation tier chosen above (callers/callees on tiers 1–2, search and read on tiers 3–4).

Pick the flows to document: the 3–7 most important user-facing operations, chosen from route groups, screens, or queue consumers. Prefer flows that touch the most layers. List the candidates to the user and let them adjust before writing flow docs, if there are more than 7.

## Step 4: Write

For each file, write only what the code shows. Use these markers:

- `> TODO(ask): <question>`: needs the user's knowledge (business reason, why a design was chosen, expected behavior). Add the same question to `open-questions.md`.
- `> UNVERIFIED: <claim>`: inferred but not confirmed (for example a naming pattern seen in most but not all files).

### conventions.md must cover

Derive each from the code by looking at several examples, not one:
- Naming (files, types, functions, routes, DB tables)
- Error handling: how errors are created, wrapped, returned, mapped to responses, and logged; is there a global recover / error boundary
- Logging: library, fields, levels
- Config: how it is loaded, where new keys go
- Testing: framework, file placement, naming, fixtures/mocks, how to run
- Where new code goes: "to add an endpoint, touch X, Y, Z" style checklists

### Flow docs must cover

```
# <Flow name>
Trigger: <route / screen / event>
Steps:
1. <layer> `<file:line>`: what happens
2. ...
Data touched: <tables / stores / external calls>
Failure paths: <what happens on each error, and where it is handled>
Related: <other flows>
```

## Step 5: Ask

After writing, show the user the contents of `open-questions.md` grouped by file. Ask them in batches of at most 5. As they answer, write the answer into the relevant doc, remove the `TODO(ask)` marker, and remove the item from `open-questions.md`. Items the user skips stay in `open-questions.md`.

## Finish

Report: files created, files left untouched, number of open questions remaining. Do not commit.

## Keeping docs current

Other skills (such as `implement`) update these docs after changing code. When editing docs later, if a decision is replaced, do not delete the old text: strike it (`~~old~~`) and add a dated note with the new decision, so agents can see why things changed.
