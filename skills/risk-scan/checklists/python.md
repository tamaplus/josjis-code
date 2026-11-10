# Python checklist

## Linters
| Tool | Install | Run |
|---|---|---|
| ruff | `pip install ruff` | `ruff check <files>` (rules `BLE`, `S110`, `E722`, `TRY`, `B`) |
| mypy or pyright | `pip install mypy` / `npm i -g pyright` | `mypy <files>` / `pyright <files>` |
| bandit | `pip install bandit` | `bandit -r <path>` |

## Checks
- Bare `except:` or `except Exception: pass`.
- `except` that logs and returns `None`, with callers using the result.
- `dict[key]` on external data instead of `.get` + check; `KeyError`.
- `Optional` values used without `None` check (ORM `.first()`, `re.match`, `os.getenv`).
- `int()`, `float()`, `datetime.strptime`, `json.loads` on input without try.
- `requests` calls without `timeout=` (default waits forever); `raise_for_status()` missing.
- Files/connections opened without `with`.
- `asyncio.create_task` result not kept or awaited → exception lost, task may be garbage-collected.
- Blocking calls inside `async def` (requests, time.sleep).
- Mutable default arguments (`def f(x=[])`).
- Django/Flask/FastAPI: `.get()` on models raising `DoesNotExist` unhandled; missing transaction on multi-write; FastAPI background tasks failing silently.
