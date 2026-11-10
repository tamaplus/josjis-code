# {{APP_NAME}}

### Contents
- [1. Version](#1-version)
- [2. Description](#2-description)
- [3. Architecture](#3-architecture)
- [4. Technology Stack](#4-technology-stack)
- [5. Screens & Navigation](#5-screens--navigation)
- [6. API Consumer](#6-api-consumer)
- [7. Local Storage](#7-local-storage)
- [8. Project Structure](#8-project-structure)
- [9. Build Variants & Configuration](#9-build-variants--configuration)
- [10. Running Application](#10-running-application)
- [11. Release](#11-release)
- [12. Author](#12-author)

---

### 1. Version

| Date | Version | Build | Author | Changelog |
|---|---|---|---|---|
| {{RELEASE_DATE}} | {{VERSION_NAME}} | {{BUILD_NUMBER}} | {{AUTHOR_NAME}} | {{CHANGELOG}} |

[**Back to contents**](#contents)

---

### 2. Description

**{{APP_NAME}}** is {{APP_DESCRIPTION}}.

| Platform | Minimum version | Target version |
|---|---|---|
| {{PLATFORM}} | {{MIN_VERSION}} | {{TARGET_VERSION}} |
<!-- Android: minSdk / targetSdk. iOS: deployment target. -->

Features:
{{FEATURE_LIST}}

[**Back to contents**](#contents)

---

### 3. Architecture

| Concern | Approach |
|---|---|
| Pattern | {{PATTERN}} <!-- MVVM, MVI, Clean, TCA, BLoC --> |
| UI | {{UI_TOOLKIT}} <!-- Jetpack Compose, XML views, SwiftUI, UIKit, Flutter, React Native --> |
| Dependency injection | {{DI}} |
| Async | {{ASYNC}} <!-- Coroutines/Flow, Combine, async/await, Rx --> |
| Navigation | {{NAVIGATION}} |

```
{{ARCHITECTURE_ASCII_DIAGRAM}}
```
<!-- Screen → ViewModel/presenter → use case → repository → remote API / local storage. -->

[**Back to contents**](#contents)

---

### 4. Technology Stack

| Component | Technology |
|---|---|
| Language | {{LANGUAGE_VERSION}} |
| Networking | {{NETWORK_LIBRARY}} |
| Local storage | {{STORAGE_LIBRARY}} |
| Image loading | {{IMAGE_LIBRARY}} |
| Analytics / crash reporting | {{ANALYTICS}} |
| Testing | {{TEST_LIBRARY}} |

[**Back to contents**](#contents)

---

### 5. Screens & Navigation

| Screen | File | Description | Entry points |
|---|---|---|---|
| {{SCREEN}} | `{{SCREEN_FILE}}` | {{DESC}} | {{FROM_WHERE_OR_DEEPLINK}} |
<!-- Include deep links / universal links. -->

[**Back to contents**](#contents)

---

### 6. API Consumer

Base URL: `{{API_BASE_URL_CONFIG}}`

| Method | Endpoint | Used by | Description |
|---|---|---|---|
| {{HTTP_METHOD}} | `{{ENDPOINT}}` | `{{CALLER_FILE}}` | {{DESC}} |

[**Back to contents**](#contents)

---

### 7. Local Storage
<!-- optional -->

| Store | Technology | Contents |
|---|---|---|
| {{STORE_NAME}} | {{TECH}} <!-- Room, Core Data, SwiftData, SharedPreferences, DataStore, Keychain, Hive --> | {{WHAT_IS_STORED}} |

[**Back to contents**](#contents)

---

### 8. Project Structure

```
{{PROJECT_TREE}}
```

[**Back to contents**](#contents)

---

### 9. Build Variants & Configuration

| Variant / scheme | API environment | Notes |
|---|---|---|
| {{VARIANT}} | {{ENVIRONMENT}} | {{NOTES}} |

| Config key | Source | Description |
|---|---|---|
| `{{CONFIG_KEY}}` | {{SOURCE}} <!-- gradle.properties, local.properties, xcconfig, .env --> | {{DESC}} |
<!-- Keys and meaning only. Never copy keystore passwords, API keys, or signing values. -->

[**Back to contents**](#contents)

---

### 10. Running Application

**Requirements**: {{TOOLCHAIN}} <!-- Android Studio / JDK version, Xcode version, Flutter SDK -->

```sh
{{SETUP_COMMAND}}
{{RUN_COMMAND}}
```

**Test**
```sh
{{TEST_COMMAND}}
```

[**Back to contents**](#contents)

---

### 11. Release

{{RELEASE_PROCESS}}
<!-- How a release build is produced and shipped (Fastlane, CI, manual), where signing material lives (by reference, not value), store tracks. -->

[**Back to contents**](#contents)

---

### 12. Author

| Name | Role | Email |
|---|---|---|
| {{AUTHOR_NAME}} | {{AUTHOR_ROLE}} | {{AUTHOR_EMAIL}} |

[**Back to contents**](#contents)
