# Rust checklist

## Linters
| Tool | Install | Run |
|---|---|---|
| clippy | `rustup component add clippy` | `cargo clippy -- -W clippy::unwrap_used -W clippy::expect_used -W clippy::indexing_slicing` |

## Checks
- `.unwrap()` / `.expect()` on `Result`/`Option` from I/O, parsing, or external input in non-test code.
- Indexing `v[i]`, slicing `&s[a..b]` (also panics on non-char-boundary for `str`).
- `panic!`, `unreachable!`, `todo!`, `unimplemented!` in reachable paths.
- Integer overflow in release (wraps) or debug (panics) on arithmetic with external values; use `checked_*`.
- `let _ = fallible()` discarding errors.
- Spawned tokio tasks whose `JoinHandle` is dropped → panics and errors lost.
- `Mutex` lock poisoning ignored via `unwrap()` after a panic in another thread.
- Blocking calls inside async runtime.
- `unsafe` blocks: check invariants are documented and upheld.
- reqwest clients without timeout.
