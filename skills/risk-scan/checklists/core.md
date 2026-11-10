# Core checklist (all languages)

Apply to every file. Language checklists add specifics.

## Errors
- Error/exception returned or thrown and then ignored, discarded, or caught with an empty handler.
- Error logged, then execution continues as if the operation succeeded (caller gets a zero value / partial result).
- Error mapped to a success response (HTTP 200 with an error body, `true` from a failed save).
- Error context lost: original error replaced by a generic one with no cause attached.
- Catch-all handlers that hide programmer bugs (catching everything around large blocks).

## External calls (HTTP, DB, cache, queue, file, subprocess)
- Result/status not checked (non-2xx treated as success, affected rows not checked when it matters).
- No timeout or deadline.
- Retry without backoff, or retry of a non-idempotent operation.
- Resource not released on the error path (connection, file handle, response body, lock, transaction).
- Partial failure in multi-step writes with no transaction or compensation.

## Missing / empty values
- Value that can be null/nil/undefined/None used without a check (lookup results, optional fields, decoded payloads, env vars).
- First element / index / key access on a collection that can be empty.
- Parsing (numbers, dates, JSON, enums) without handling invalid input.
- Division or modulo by a value that can be zero.

## Input from outside
- Request bodies, query params, headers, messages, files, deep links used without validation of presence, type, and range.
- Size/length not bounded (unbounded reads, pagination limits).

## Concurrency and async
- Background task / thread / goroutine / coroutine whose failure is not observed.
- Shared mutable state written from multiple tasks without synchronization.
- Cancellation not propagated, or work continuing after the caller gave up.

## Process level
- No top-level handler for crashes where the platform expects one (HTTP recover middleware, error boundary, uncaught exception handler) — note once, not per call site.
- `TODO` / `FIXME` / `XXX` on an error path.
