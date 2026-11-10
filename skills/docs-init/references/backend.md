# Backend docs

Extra files:

| File | Contents |
|---|---|
| `docs/api.md` | Every route: method, path, handler `file:line`, auth, request/response shape, error codes. Note OpenAPI spec location if one exists. |
| `docs/data.md` | Tables/collections from migrations: columns, indexes, relations. Which repository/model owns each. Migration tool and how to add one. |
| `docs/integrations.md` | Outbound calls (HTTP, gRPC, queues, cache): client file, config key, timeout, retry, what happens on failure. |
| `docs/jobs.md` (if any) | Cron jobs, queue consumers, background workers: trigger, handler, idempotency. |

Flow docs: follow a request from transport to storage and back. Always state transactions (where they begin and end), cache reads/writes, and every external call.

Conventions to check specifically:
- Response envelope and error code mapping
- Context/cancellation propagation
- Transaction boundaries
- Auth middleware and how a handler reads the current user
