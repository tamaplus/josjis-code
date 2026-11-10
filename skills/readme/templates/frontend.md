# {{APP_NAME}}

### Contents
- [1. Version](#1-version)
- [2. Description](#2-description)
- [3. Architecture](#3-architecture)
- [4. Technology Stack](#4-technology-stack)
- [5. Pages & Routes](#5-pages--routes)
- [6. API Consumer](#6-api-consumer)
- [7. Components & Design System](#7-components--design-system)
- [8. Project Structure](#8-project-structure)
- [9. Environment Variables](#9-environment-variables)
- [10. Running Application](#10-running-application)
- [11. Build & Deploy](#11-build--deploy)
- [12. Author](#12-author)

---

### 1. Version

| Date | Version | Author | Changelog |
|---|---|---|---|
| {{RELEASE_DATE}} | {{VERSION}} | {{AUTHOR_NAME}} | {{CHANGELOG}} |

[**Back to contents**](#contents)

---

### 2. Description

**{{APP_NAME}}** is {{APP_DESCRIPTION}}.

Features:
{{FEATURE_LIST}}

[**Back to contents**](#contents)

---

### 3. Architecture

| Concern | Approach |
|---|---|
| Rendering | {{RENDERING}} <!-- SPA / SSR / SSG / ISR / hybrid --> |
| Routing | {{ROUTING}} <!-- file-based (app/, pages/), vue-router, react-router --> |
| State management | {{STATE}} <!-- Redux, Zustand, Pinia, React Query, context --> |
| Data fetching | {{DATA_FETCHING}} <!-- fetch/axios wrapper, React Query, SWR, server components --> |
| Auth | {{AUTH}} |
| Styling | {{STYLING}} |

```
{{ARCHITECTURE_ASCII_DIAGRAM}}
```
<!-- Browser → router/page → components → state/data layer → API client → backend. -->

[**Back to contents**](#contents)

---

### 4. Technology Stack

| Component | Technology |
|---|---|
| Framework | {{FRAMEWORK_VERSION}} |
| Language | {{LANGUAGE}} |
| UI library | {{UI_LIBRARY}} |
| Build tool | {{BUILD_TOOL}} |
| Testing | {{TEST_LIBRARY}} |
<!-- Add or remove rows to match package.json. -->

[**Back to contents**](#contents)

---

### 5. Pages & Routes

| Route | Page / Component | Description | Auth |
|---|---|---|---|
| `{{ROUTE}}` | `{{PAGE_FILE}}` | {{DESC}} | {{PUBLIC_OR_PROTECTED}} |

[**Back to contents**](#contents)

---

### 6. API Consumer

Base URL: `{{API_BASE_URL_ENV}}`

**{{BACKEND_LABEL}}**
| Method | Endpoint | Used by | Description |
|---|---|---|---|
| {{HTTP_METHOD}} | `{{ENDPOINT}}` | `{{CALLER_FILE}}` | {{DESC}} |

[**Back to contents**](#contents)

---

### 7. Components & Design System
<!-- optional -->

{{DESIGN_SYSTEM_DESCRIPTION}}
<!-- Where shared components live, naming rules, tokens/theme location, Storybook link if any. -->

[**Back to contents**](#contents)

---

### 8. Project Structure

```
{{PROJECT_TREE}}
```

[**Back to contents**](#contents)

---

### 9. Environment Variables

| Key | Description | Exposed to browser | Required |
|---|---|---|---|
| `{{ENV_KEY}}` | {{ENV_DESC}} | {{YES_NO}} | {{YES_NO}} |
<!-- Mark public prefixes (NEXT_PUBLIC_, VITE_, NUXT_PUBLIC_) as exposed. Never copy real values. -->

[**Back to contents**](#contents)

---

### 10. Running Application

```sh
{{INSTALL_COMMAND}}
{{DEV_COMMAND}}
```

**Test / Lint**
```sh
{{TEST_COMMAND}}
{{LINT_COMMAND}}
```

[**Back to contents**](#contents)

---

### 11. Build & Deploy

```sh
{{BUILD_COMMAND}}
```

{{DEPLOY_DESCRIPTION}}
<!-- Target (Vercel, Netlify, static bucket, Docker, CDN) and how deploys are triggered. -->

[**Back to contents**](#contents)

---

### 12. Author

| Name | Role | Email |
|---|---|---|
| {{AUTHOR_NAME}} | {{AUTHOR_ROLE}} | {{AUTHOR_EMAIL}} |

[**Back to contents**](#contents)
