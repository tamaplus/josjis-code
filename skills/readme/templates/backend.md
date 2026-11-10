# {{SERVICE_NAME}}

### Contents
- [1. Version](#1-version)
- [2. Description](#2-description)
- [3. Architecture](#3-architecture)
- [4. Technology Stack](#4-technology-stack)
- [5. High Level Diagram](#5-high-level-diagram)
- [6. Database Design](#6-database-design)
- [7. API Producer](#7-api-producer)
- [8. API Consumer](#8-api-consumer)
- [9. Project Structure](#9-project-structure)
- [10. Environment Properties](#10-environment-properties)
- [11. Running Application](#11-running-application)
- [12. Author](#12-author)

---

### 1. Version

| Date | Version | Author | Changelog |
|---|---|---|---|
| {{RELEASE_DATE}} | {{VERSION}} | {{AUTHOR_NAME}} | {{CHANGELOG}} |

[**Back to contents**](#contents)

---

### 2. Description

**{{SERVICE_NAME}}** is {{SERVICE_DESCRIPTION}}.

Features:
{{FEATURE_LIST}}
<!-- Numbered list of what the service does, one line each. -->

[**Back to contents**](#contents)

---

### 3. Architecture

{{ARCHITECTURE_DESCRIPTION}}
<!-- Pattern used: layered, clean, hexagonal, etc. -->

```
{{ARCHITECTURE_ASCII_DIAGRAM}}
```
<!-- Request flow top to bottom: client → transport (HTTP/gRPC/queue) → middleware → handler → service → repository → DB/cache/downstream. -->

[**Back to contents**](#contents)

---

### 4. Technology Stack

| Component | Technology |
|---|---|
| Language | {{LANGUAGE_VERSION}} |
| Framework | {{FRAMEWORK}} |
| Database / ORM | {{ORM}} |
| Cache | {{CACHE}} |
| HTTP Client | {{HTTP_CLIENT}} |
| Config | {{CONFIG_LIBRARY}} |
| Logger | {{LOGGER}} |
<!-- Add or remove rows to match the dependency manifest. -->

[**Back to contents**](#contents)

---

### 5. High Level Diagram

```mermaid
flowchart LR
    CLIENT[{{EXTERNAL_CLIENT_LABEL}}]
    SVC[{{SERVICE_NAME}}]
    DB[({{DATABASE_LABEL}})]
    CACHE[({{CACHE_LABEL}})]
    DS1[{{DOWNSTREAM_SERVICE_1_LABEL}}]

    CLIENT --> SVC
    SVC --> DB
    SVC --> CACHE
    SVC --> DS1
```
<!-- One node per real dependency. Remove nodes that do not exist. -->

[**Back to contents**](#contents)

---

### 6. Database Design
<!-- optional: remove for stateless services -->

Schema: `{{DB_SCHEMA}}` ({{DB_ENGINE}})

**{{TABLE_NAME}}**
| Column | Type | Description |
|---|---|---|
| {{COLUMN}} | {{TYPE}} | {{DESC}} |
<!-- Repeat per table. Source: migrations first, then models. -->

[**Back to contents**](#contents)

---

### 7. API Producer

Base URL: `{{BASE_URL}}`

**{{API_GROUP_LABEL}}**
| Method | Path | Description | Auth |
|---|---|---|---|
| {{HTTP_METHOD}} | `{{PATH}}` | {{DESC}} | {{AUTH_TYPE}} |
<!-- Repeat per route group. Include health checks. -->

**Required Headers**
| Header | Description |
|---|---|
| `{{HEADER}}` | {{HEADER_DESC}} |

[**Back to contents**](#contents)

---

### 8. API Consumer
<!-- optional: remove if the service calls no other services -->

**{{DOWNSTREAM_SERVICE_LABEL}}**
| Method | Endpoint | Description |
|---|---|---|
| {{HTTP_METHOD}} | `{{ENDPOINT_OR_CONFIG_KEY}}` | {{DESC}} |

[**Back to contents**](#contents)

---

### 9. Project Structure

```
{{PROJECT_TREE}}
```
<!-- Real top-level layers and notable subpackages with a one-line comment each. Skip generated/vendor folders. -->

[**Back to contents**](#contents)

---

### 10. Environment Properties

Config is loaded from `{{CONFIG_SOURCE}}`.
<!-- e.g. ./config/{env}.yaml, .env, environment variables. -->

| Key | Description | Required |
|---|---|---|
| `{{CONFIG_KEY}}` | {{CONFIG_DESC}} | {{YES_NO}} |
<!-- Keys and meaning only. Never copy values from real env or secret files. -->

[**Back to contents**](#contents)

---

### 11. Running Application

**Local**
```sh
{{RUN_LOCAL_COMMAND}}
```

**Test**
```sh
{{TEST_COMMAND}}
```

**Build**
```sh
{{BUILD_COMMAND}}
```

**Docker**
<!-- optional -->
```sh
{{DOCKER_BUILD_COMMAND}}
{{DOCKER_RUN_COMMAND}}
```

[**Back to contents**](#contents)

---

### 12. Author

| Name | Role | Email |
|---|---|---|
| {{AUTHOR_NAME}} | {{AUTHOR_ROLE}} | {{AUTHOR_EMAIL}} |

[**Back to contents**](#contents)
