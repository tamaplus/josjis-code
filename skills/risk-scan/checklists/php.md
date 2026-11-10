# PHP checklist

## Linters
| Tool | Install | Run |
|---|---|---|
| PHPStan | `composer require --dev phpstan/phpstan` | `vendor/bin/phpstan analyse <path>` |
| Psalm | `composer require --dev vimeo/psalm` | `vendor/bin/psalm` |

## Checks
- Empty `catch`, `@` error suppression operator.
- Functions returning `false` on failure (`file_get_contents`, `json_decode` → `null`, `strpos`) used without check; `json_decode` without `JSON_THROW_ON_ERROR`.
- Array keys accessed without `isset` / `??` on input arrays.
- Nullable return values chained (`$user->profile->name`) without `?->`.
- `curl` / Guzzle without timeouts; HTTP status not checked.
- DB writes across multiple statements without a transaction.
- Laravel: `find()` result used without null check (use `findOrFail` deliberately); queued jobs without `failed()` handling; `env()` called outside config files.
