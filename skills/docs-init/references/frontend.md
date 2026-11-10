# Frontend docs

Extra files:

| File | Contents |
|---|---|
| `docs/routes.md` | Every route: path, page file, layout, auth guard, data loaded on entry. |
| `docs/state.md` | Stores/contexts/query keys: what each holds, who writes it, who reads it, persistence. |
| `docs/api-client.md` | API client setup: base URL, auth header injection, error/401 handling, retries. Every endpoint used and its caller. |
| `docs/components.md` | Shared component locations, design tokens/theme, naming, when to make a new shared component vs local. |

Flow docs: follow a user action from UI event → handler → state/data layer → API → UI update. Always state loading, empty, and error states, and where errors are shown to the user.

Framework specifics to record:
- Next.js / Nuxt: server vs client components, where data is fetched (server component, route handler, server action, `getServerSideProps`, `useFetch`), caching/revalidation.
- React: error boundaries location, Suspense usage.
- Vue: composables location, `errorCaptured` / global error handler.
