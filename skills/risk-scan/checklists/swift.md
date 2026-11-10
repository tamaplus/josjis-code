# Swift checklist (iOS / macOS)

## Linters
| Tool | Install | Run |
|---|---|---|
| SwiftLint | `brew install swiftlint` | `swiftlint lint --path <path>` (rules `force_unwrapping`, `force_cast`, `force_try`) |

## Checks
- Force unwrap `!` on optionals from network, JSON, dictionaries, `URL(string:)`, outlets after view unload.
- `as!` force cast; `try!` on failable calls.
- Array index without bounds check; `first!`.
- `do { } catch { }` empty or print-only.
- `Task { }` whose thrown errors are never observed; missing `@MainActor` for UI updates from background.
- `URLSession` calls without checking `HTTPURLResponse.statusCode`; no timeout configured.
- `Codable` decoding failures swallowed, leaving UI in loading state.
- Retain cycles in closures capturing `self` strongly in long-lived objects (leaks, not crashes; Low).
- Keychain / file operations with status codes ignored.
