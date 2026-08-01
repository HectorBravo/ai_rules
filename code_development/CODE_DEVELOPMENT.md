# Code Development Rules

## General
- DRY, KISS, SOLID principles
- Comments explain *why*, not *what*
- Profile before optimizing; avoid premature optimization
- Pin dependency versions; document setup steps
- Function length ~50 lines max; cyclomatic complexity ~10 max
- Security: no secrets, validate inputs, least-privilege

## Python
See [PYTHON_RULES.md](./PYTHON_RULES.md)

## Git
See [GIT_RULES.md](./GIT_RULES.md)

## C/C++
See [C_CPP_RULES.md](./C_CPP_RULES.md)

## Verification (Agent-Generated Code Only)

Verify ONLY code you generate — never the existing codebase unless explicitly requested:

- **Python:** `pylint` + `pyright` (linting + type checking)
- **C/C++:** `cppcheck`
- **JavaScript/TypeScript:** `eslint` + `tsc --noEmit`
- **Rust:** `cargo clippy` + `cargo check`
- **Go:** `golangci-lint`
- **Java:** `checkstyle` + `spotbugs`
- **Other:** Use equivalent linter + static analyzer for the language
- Always run existing tests after changes
