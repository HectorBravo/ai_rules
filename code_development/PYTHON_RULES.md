# Python Rules

## Style
- PEP 8 compliant; max line length: 100 chars
- Use `black` (line-length=100) and `ruff` for formatting/linting
- Type hints everywhere; prefer `mypy` for static checking

## Naming
- Modules/packages: `snake_case`
- Classes: `PascalCase`
- Functions/variables: `snake_case`
- Constants: `UPPER_SNAKE_CASE`
- Private: `_leading_underscore`

## Structure
- One class per file unless related; module-level code: guard with `if __name__ == "__main__":`
- Use `pyproject.toml` for config (black, ruff, mypy, pytest)
- Virtual env: `python -m venv .venv`

## Dependencies
- Pin versions in `requirements.txt` or use `poetry`/`uv`
- Prefer `uv` for fast installs; fallback to `pip`

## Testing
- Use `pytest`; tests in `tests/` mirroring source structure
- Name test files: `test_<module>.py`; test functions: `test_<scenario>_<expected>`
- Minimum 80% coverage; assert specific exceptions

## Error Handling
- Catch specific exceptions; never bare `except:`
- Use custom exception classes in packages
- Log with `logging` module; never `print()` in library code

## Concurrency
- Prefer `asyncio` for I/O-bound; `concurrent.futures` for CPU-bound
- Never mix blocking I/O in async code

## Documentation
- Docstrings: Google style; include Args, Returns, Raises
- Public APIs must be documented
