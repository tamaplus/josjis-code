# JavaScript / TypeScript checklist (Node, React, Vue, Next, Nuxt)

## Linters
| Tool | Install | Run |
|---|---|---|
| tsc | `npm i -D typescript` | `npx tsc --noEmit` (TS only) |
| eslint | `npm i -D eslint` | `npx eslint <files>` using repo config |
| typescript-eslint rules | `npm i -D typescript-eslint` | check `no-floating-promises`, `no-misused-promises`, `no-unsafe-*` |
| eslint-plugin-react-hooks | `npm i -D eslint-plugin-react-hooks` | `rules-of-hooks`, `exhaustive-deps` |
| eslint-plugin-vue | `npm i -D eslint-plugin-vue` | Vue files |

Use the repo's eslint config if one exists. Do not add rules to it.

## All JS/TS
- Promise not awaited and not `.catch`ed (floating promise) → unhandled rejection.
- `async` callback passed where the caller ignores the promise (`array.forEach(async ...)`, event emitters, `setTimeout`).
- `JSON.parse` on external input without try/catch.
- `catch (e) {}` or `catch` that only logs and continues.
- `fetch` result used without checking `res.ok` (fetch does not throw on 4xx/5xx).
- Optional data accessed without guard: `data.items[0].name`, `obj!.x` non-null assertions, `as T` casts on API responses.
- `parseInt`/`Number` without `NaN` check; missing radix.
- `Promise.all` where one rejection should not fail the rest (use `allSettled`).

## Node (server)
- No `process.on('unhandledRejection' | 'uncaughtException')` strategy (log and exit is fine; nothing is not).
- Express: async route handlers without error forwarding (Express < 5) → hanging request or crash.
- Missing error middleware; errors leaking stack traces to clients.
- Outbound HTTP without timeout (axios default has none; `fetch` needs `AbortSignal.timeout`).
- Streams without `'error'` listeners.
- DB transactions not rolled back on throw.

## React
- No error boundary around route-level trees → one render error blanks the app.
- `useEffect` fetching without handling rejection, without abort on unmount, or setting state after unmount.
- Rendering `data.x` before loading finishes (`data` is `undefined` on first render).
- Event handlers calling async functions without catch.
- `key` from index on reorderable lists (state bugs, not crashes; Low).

## Next.js
- Server component / route handler / server action throwing without `error.tsx` at a sensible level.
- `notFound()` vs returning `null` data; `params` used without validation.
- Server-only code (secrets, DB) imported into client components.
- `NEXT_PUBLIC_` env missing at build time → `undefined` at runtime.
- Hydration mismatches from `Date.now()`, `Math.random()`, `window` in render.

## Vue / Nuxt
- No `app.config.errorHandler` / `errorCaptured` / Nuxt `error.vue`.
- Accessing `ref.value.x` / props before data is loaded.
- `watch` / `onMounted` async callbacks without catch.
- Nuxt `useFetch` / `useAsyncData` `error` ref never read.
