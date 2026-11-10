---
name: readme
description: Generate or update a project README from a template matched to the project type (backend, frontend, fullstack, mobile). Fills only what is missing in an existing README, or with --diff updates only the sections touched by the current branch's changes. Use when the user asks to create, generate, complete, or update a README.
argument-hint: "[--type backend|frontend|fullstack|mobile] [--diff]"
---

# readme

Produce a README that follows a fixed template, filled with facts read from the repository. Never invent facts.

## Arguments

- `--type <backend|frontend|fullstack|mobile>`: use this template. Skips detection.
- `--diff`: update only the sections affected by changes on the current branch.
- No arguments: detect the type, then create or complete the README.

## Step 1: Pick the template

Use the first that applies:

1. A repo-provided template: `.github/README_TEMPLATE.md`, `docs/README_TEMPLATE.md`, or `README.template.md`. The team's template always wins.
2. `--type` flag → `templates/<type>.md` in this skill folder.
3. Detect the type from the repo:

| Signal | Type |
|---|---|
| `AndroidManifest.xml`, `build.gradle(.kts)` with `com.android.application`, `*.xcodeproj`, `*.xcworkspace`, `Package.swift` with an iOS target, `pubspec.yaml` with `flutter`, `react-native` / `expo` in `package.json` | mobile |
| Both a server (Go/Java/Python/Node API, DB migrations) and a web UI in one repo, or a monorepo with `apps/web` + `apps/api`, or Next.js with API routes / server actions **and** a database client | fullstack |
| `package.json` with `react`, `vue`, `next`, `nuxt`, `svelte`, `angular` and no server/DB layer | frontend |
| `go.mod`, `pom.xml`, `build.gradle` (non-Android), `requirements.txt` / `pyproject.toml`, `Cargo.toml`, `*.csproj`, `composer.json`, or Node with `express` / `fastify` / `nest` | backend |

If signals conflict or are weak, ask the user once, showing what you found. Do not guess silently.

## Step 2: Choose the mode

### No README exists → generate

1. Read the template.
2. Gather facts for each section from the repo (see "Where facts come from").
3. Replace every `{{PLACEHOLDER}}` you can fill. Remove authoring `<!-- -->` comments.
4. For a section with no facts available, keep the heading and write `> TODO: <what is needed>`. Do not delete required sections and do not fill them with plausible fiction.
5. Drop optional sections (marked `<!-- optional -->` in the template) only if they truly do not apply, such as Database Design for a stateless service.

### README exists, no `--diff` → complete

1. Map the existing README's headings to template sections, matching by meaning, not exact title.
2. Leave every existing section's content untouched, even if you would phrase it differently.
3. Add the missing sections in template order, filled from the repo.
4. If an existing section contradicts the code (for example a documented env var no longer exists), do not edit it. List it in your summary as a suspected stale section.

### `--diff` → update from changes

1. Find the base: `git merge-base HEAD origin/main` (fall back to `main`, then `master`). Collect `git diff <base>...HEAD` plus uncommitted changes.
2. Map changed files to README sections:

| Change | Section |
|---|---|
| New/changed routes, handlers, controllers | API Producer / Pages & Routes |
| New outbound HTTP/gRPC clients or base URLs | API Consumer |
| Migrations, model/entity/schema files | Database Design / Local Storage |
| New env vars, config keys, `.env.example` | Environment |
| Dependency manifest changes | Technology Stack |
| New top-level folders or modules | Project Structure |
| Dockerfile, Makefile, scripts, build configs | Running Application / Build |
| New screens, navigation entries | Screens & Navigation |

3. Edit only those sections, and only the rows/lines related to the change. Add a row to the Version table if the template has one and the user confirms a version.
4. If the README does not follow a template yet, run "complete" mode first and tell the user.

## Where facts come from

- **Description, features**: existing docs (`docs/`, `AGENTS.md`), package description fields, top-level route/screen groups. If the purpose is not stated anywhere, ask the user instead of summarizing code.
- **Tech stack**: dependency manifests only. Include versions from the manifest.
- **Architecture, diagram**: folder layout and import direction between layers. Use codegraph if available to confirm call direction.
- **API Producer**: route registrations (router files, decorators, `app/api/**`, OpenAPI spec if present).
- **API Consumer**: outbound clients, base URL config keys.
- **Database**: migrations first, then ORM models.
- **Environment**: `.env.example`, config files, and code that reads env/config. List keys and meaning, **never values** from real `.env` or secret files.
- **Running**: Makefile, `package.json` scripts, Dockerfile, CI config. Only commands that exist.
- **Author**: ask the user, or leave TODO. Do not pull names from git log without asking.

## Finish

Tell the user: the template and mode used, sections added or updated, sections left as TODO, and any suspected stale sections. Do not commit.
