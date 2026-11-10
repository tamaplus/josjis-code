# Mobile docs (Android / iOS / cross-platform)

Extra files:

| File | Contents |
|---|---|
| `docs/screens.md` | Every screen: file, ViewModel/presenter, navigation route, deep links, arguments. |
| `docs/data.md` | Repositories, remote API calls, local storage (DB, preferences, keychain), caching and offline rules, sync. |
| `docs/build.md` | Build variants/flavors/schemes, config sources (gradle properties, xcconfig, .env), signing (by reference only), CI/release lanes. |
| `docs/platform.md` | Permissions requested and where, background work, push notifications, lifecycle handling. |

Flow docs: follow a user action from screen → ViewModel → use case → repository → API/local store → UI state. Always state loading/error/empty UI states, offline behavior, and process-death/state restoration if handled.

Conventions to check specifically:
- Threading/dispatchers (main vs IO), structured concurrency
- How errors become UI state (sealed result types, `Result`, exceptions)
- DI module locations and scopes
