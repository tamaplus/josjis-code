# {{PROJECT_NAME}}

### Contents
- [1. Version](#1-version)
- [2. Description](#2-description)
- [3. Architecture](#3-architecture)
- [4. Technology Stack](#4-technology-stack)
- [5. High Level Diagram](#5-high-level-diagram)
- [6. Workspace Structure](#6-workspace-structure)
- [7. Pages & Routes](#7-pages--routes)
- [8. API](#8-api)
- [9. Database Design](#9-database-design)
- [10. External Services](#10-external-services)
- [11. Environment Variables](#11-environment-variables)
- [12. Running Application](#12-running-application)
- [13. Build & Deploy](#13-build--deploy)
- [14. Author](#14-author)

---

### 1. Version

| Date | Version | Author | Changelog |
|---|---|---|---|
| {{RELEASE_DATE}} | {{VERSION}} | {{AUTHOR_NAME}} | {{CHANGELOG}} |

[**Back to contents**](#contents)

---

### 2. Description

**{{PROJECT_NAME}}** is {{PROJECT_DESCRIPTION}}.

Features:
{{FEATURE_LIST}}

[**Back to contents**](#contents)

---

### 3. Architecture

{{ARCHITECTURE_DESCRIPTION}}
<!-- Monorepo (apps/packages) or single framework (Next/Nuxt with server routes). How frontend reaches backend: REST, tRPC, GraphQL, server actions. -->

```
{{ARCHITECTURE_ASCII_DIAGRAM}}
```

[**Back to contents**](#contents)

---

### 4. Technology Stack

| Layer | Component | Technology |
|---|---|---|
| Frontend | Framework | {{FE_FRAMEWORK}} |
| Frontend | State / data | {{FE_STATE}} |
| Backend | Runtime / framework | {{BE_FRAMEWORK}} |
| Backend | ORM | {{ORM}} |
| Data | Database | {{DATABASE}} |
| Data | Cache | {{CACHE}} |
| Tooling | Monorepo / build | {{MONOREPO_TOOL}} |

[**Back to contents**](#contents)

---

### 5. High Level Diagram

```mermaid
flowchart LR
    USER[Browser]
    FE[{{FRONTEND_LABEL}}]
    BE[{{BACKEND_LABEL}}]
    DB[({{DATABASE_LABEL}})]
    EXT[{{EXTERNAL_SERVICE_LABEL}}]

    USER --> FE --> BE
    BE --> DB
    BE --> EXT
```

[**Back to contents**](#contents)

---

### 6. Workspace Structure

```
{{PROJECT_TREE}}
```
<!-- Show apps/*, packages/*, shared types/config, and what depends on what. -->

[**Back to contents**](#contents)

---

### 7. Pages & Routes

| Route | Page | Description | Auth |
|---|---|---|---|
| `{{ROUTE}}` | `{{PAGE_FILE}}` | {{DESC}} | {{PUBLIC_OR_PROTECTED}} |

[**Back to contents**](#contents)

---

### 8. API

| Method | Path | Handler | Description | Auth |
|---|---|---|---|---|
| {{HTTP_METHOD}} | `{{PATH}}` | `{{HANDLER_FILE}}` | {{DESC}} | {{AUTH_TYPE}} |
<!-- Include server actions / tRPC procedures if used instead of REST. -->

[**Back to contents**](#contents)

---

### 9. Database Design

Engine: {{DB_ENGINE}}

**{{TABLE_NAME}}**
| Column | Type | Description |
|---|---|---|
| {{COLUMN}} | {{TYPE}} | {{DESC}} |

[**Back to contents**](#contents)

---

### 10. External Services
<!-- optional -->

| Service | Purpose | Called from |
|---|---|---|
| {{SERVICE}} | {{PURPOSE}} | `{{CALLER_FILE}}` |

[**Back to contents**](#contents)

---

### 11. Environment Variables

| Key | Used by | Description | Exposed to browser | Required |
|---|---|---|---|---|
| `{{ENV_KEY}}` | {{FE_OR_BE}} | {{ENV_DESC}} | {{YES_NO}} | {{YES_NO}} |

[**Back to contents**](#contents)

---

### 12. Running Application

```sh
{{INSTALL_COMMAND}}
{{DB_SETUP_COMMAND}}
{{DEV_COMMAND}}
```

**Test**
```sh
{{TEST_COMMAND}}
```

[**Back to contents**](#contents)

---

### 13. Build & Deploy

```sh
{{BUILD_COMMAND}}
```

{{DEPLOY_DESCRIPTION}}

[**Back to contents**](#contents)

---

### 14. Author

| Name | Role | Email |
|---|---|---|
| {{AUTHOR_NAME}} | {{AUTHOR_ROLE}} | {{AUTHOR_EMAIL}} |

[**Back to contents**](#contents)
