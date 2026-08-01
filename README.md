# AI Rules

Centralized ruleset for AI agents.

## Structure

```
ai_rules/
├── README.md
├── AI_RULES.md          # Main entry point
├── HOST_RULES.md        # Host environment detection & rules
└── code_development/    # Code development rules
    ├── CODE_DEVELOPMENT.md
    ├── C_CPP_RULES.md
    ├── PYTHON_RULES.md
    └── GIT_RULES.md
```

## Quick Start

1. Read `AI_RULES.md` for the main ruleset
2. AI agents detect their host environment (Windows/Linux) and follow applicable rules
3. Code development agents read `code_development/CODE_DEVELOPMENT.md`

## Configuration

- `.env` file (local, not committed): `MAX_SUBAGENTS=<number>`
﻿README.md
