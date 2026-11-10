# Go checklist

## Linters
| Tool | Install | Run |
|---|---|---|
| go vet | bundled | `go vet ./...` |
| staticcheck | `go install honnef.co/go/tools/cmd/staticcheck@latest` | `staticcheck ./...` |
| errcheck | `go install github.com/kisielk/errcheck@latest` | `errcheck ./...` |
| nilaway | `go install go.uber.org/nilaway/cmd/nilaway@latest` | `nilaway ./...` |
| golangci-lint (covers several) | see golangci-lint.run | `golangci-lint run` |
| race detector | bundled | `go test -race ./...` (only if tests exist; ask first, it can be slow) |

If `golangci-lint` is configured in the repo, prefer it and its config.

## Errors
- `_ = f()` or `f()` ignoring a returned `error`, including `defer f.Close()` on writers (lost write errors), `json.Unmarshal`, `rows.Err()`, `tx.Rollback()`/`Commit()`.
- `if err != nil { log...; }` with no return.
- Returning `nil, nil` for "not found" and callers dereferencing the result.
- `err` shadowed in an inner scope (`:=`) so the outer `err` checked later is stale.
- Errors compared with `==` instead of `errors.Is` / `errors.As` after wrapping.
- `fmt.Errorf` without `%w` where callers use `errors.Is`.

## Panics
- Nil pointer: methods on possibly nil struct pointers, fields of results from functions that can return nil.
- Nil map write (`var m map[K]V; m[k] = v`).
- Type assertion without `ok`: `v := x.(T)`.
- Index/slice out of range: `s[0]`, `s[i:j]`, `strings.Split(...)[1]`, `os.Args[1]`.
- Closing a closed channel, sending on a closed channel.
- Explicit `panic` / `log.Fatal` / `must*` helpers in request paths.
- Integer division by zero.

## Goroutines and concurrency
- `go func()` without `recover` in a long-running server → one panic kills the process (net/http recovers only in handler goroutines, not ones you spawn).
- Concurrent map read/write without mutex or `sync.Map` → fatal error, not recoverable.
- Goroutine leak: blocked send/receive with no `ctx.Done()` case.
- `sync.WaitGroup.Add` inside the goroutine.
- Loop variable capture in goroutines (Go < 1.22).

## Context and resources
- Outbound calls without `context` deadline; `http.Client{}` with no `Timeout`; `http.Get` default client.
- `ctx` not passed down (using `context.Background()` in a request path).
- `resp.Body` not closed; `rows.Close()` missing; `defer` inside a loop holding resources until function end.
- `sql.Tx` not rolled back on error paths.
