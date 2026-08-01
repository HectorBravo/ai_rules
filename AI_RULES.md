# AI Agent Rules

## Host
See [HOST_RULES.md](./HOST_RULES.md)

## Code Development
If acting as a code developer, read [code_development/CODE_DEVELOPMENT.md](./code_development/CODE_DEVELOPMENT.md)

## Task Division & Subagents
- Always divide tasks into parallel subtasks when possible
- Spawn subagents for independent subtasks concurrently
- Max subagents: read from `.env` → `MAX_SUBAGENTS`; fallback to 5
- User-specified limit overrides config
- Subtasks must be independent — no circular dependencies
- Aggregate results before merging; ensure all complete