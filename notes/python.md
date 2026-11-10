# Python

## Environments

```bash
python -m venv .venv
.venv\Scripts\activate          # Windows
source .venv/bin/activate       # POSIX
python -m pip install -r requirements.txt
```

`uv` is the faster path: `uv venv`, `uv pip install -r requirements.txt`, `uv run script.py`.

## Paths

```python
from pathlib import Path

root = Path(__file__).resolve().parent
for p in root.rglob("*.json"):
    print(p.relative_to(root))
```

Never join paths with `+` or string formatting — `Path / "sub"` handles separators on every OS.

## Subprocess

```python
import subprocess

result = subprocess.run(
    ["git", "status", "--short"],
    capture_output=True, text=True, check=True,
)
print(result.stdout)
```

Pass a list, not a string: it skips the shell, so quotes and spaces in arguments stay literal. `check=True` raises instead of silently returning a non-zero exit code.

## Gotchas

- Mutable default arguments are created once and shared: use `def f(items=None): items = items or []`.
- `datetime.now(timezone.utc)` gives an aware datetime; naive ones compare and subtract wrong.
- Bare `except Exception:` hides real bugs; catch the narrowest type you can name and re-raise the rest.
- `str.strip()` with no args strips all whitespace; `strip(",")` strips only commas.
- Dictionaries keep insertion order since 3.7 — no need for `OrderedDict`.
