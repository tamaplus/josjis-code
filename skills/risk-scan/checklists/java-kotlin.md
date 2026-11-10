# Java / Kotlin checklist (server and Android)

## Linters
| Tool | Install | Run |
|---|---|---|
| SpotBugs | Gradle/Maven plugin | `./gradlew spotbugsMain` |
| Error Prone | compiler plugin | via build |
| detekt (Kotlin) | Gradle plugin | `./gradlew detekt` |
| Android Lint | bundled with AGP | `./gradlew lint` |

Run only if already configured in the build. Otherwise report as skipped with the plugin name.

## Java
- Empty `catch`, or `catch (Exception e) { e.printStackTrace(); }` and continue.
- `Optional.get()` without `isPresent`; methods returning `null` used directly.
- Unchecked casts; `ClassCastException` on deserialized data.
- `Integer.parseInt` on input without `NumberFormatException` handling.
- Resources not in try-with-resources (streams, JDBC, HTTP responses).
- `CompletableFuture` without `exceptionally`/`handle`; executor tasks whose exceptions are never read.
- HTTP clients without connect/read timeouts.
- Spring: `@Transactional` on private/self-invoked methods (no transaction); checked exceptions not triggering rollback.

## Kotlin
- `!!` on values that can be null (platform types from Java, intent extras, JSON).
- `lateinit` read before init.
- `as` instead of `as?` on external data.
- `first()`, `single()`, `[i]` on possibly empty collections.
- Coroutines: `launch` without `CoroutineExceptionHandler` in a scope that should survive; `GlobalScope`; catching `CancellationException` and not rethrowing; `runCatching` swallowing cancellation.
- `runBlocking` on main thread.

## Android
- Network or disk on main thread.
- `Fragment` view accessed after `onDestroyView`; context leaks in long-lived objects.
- `Activity` result / intent extras read without null checks.
- State not saved for process death where the screen depends on it.
- Missing permission check before using a dangerous permission API.
