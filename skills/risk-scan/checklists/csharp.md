# C# checklist

## Linters
| Tool | Install | Run |
|---|---|---|
| Roslyn analyzers | bundled with .NET SDK | `dotnet build -warnaserror` (read warnings) |
| Nullable reference types | project setting | check `<Nullable>enable</Nullable>`; read CS86xx warnings |

## Checks
- Empty `catch` or `catch (Exception) { }`.
- `async void` methods (outside event handlers) → exceptions crash the process.
- `.Result` / `.Wait()` on tasks (deadlocks, AggregateException).
- Fire-and-forget `Task` without observing exceptions.
- `First()`, `Single()` on possibly empty sequences; `dict[key]` without `TryGetValue`.
- `!` null-forgiving on data that can be null.
- `int.Parse` instead of `TryParse` on input.
- `HttpClient` created per request, or without timeout; response status not checked (`EnsureSuccessStatusCode`).
- `IDisposable` not in `using`.
- ASP.NET: no exception middleware / `UseExceptionHandler`; EF `SaveChanges` failures not handled in multi-step writes.
