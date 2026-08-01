# Host Rules

**MANDATORY: Detect your environment ONCE at start by running:**
`$PSVersionTable.PSVersion` (Windows) or `uname -a` (Linux)

Then follow the matching ruleset:

## Windows with Admin
- **Only if user explicitly requests elevation** — never assume admin
- Use elevated PowerShell (`Start-Process powershell -Verb RunAs` when needed)
- Can install software system-wide, modify registry, manage services
- All tool calls: PowerShell commands

## Windows without Admin (DEFAULT)
- **Default mode — always assume non-privileged unless user says otherwise**
- Use standard PowerShell only (no elevation)
- User-level installs only (`-Scope CurrentUser`), no registry HKLM, no service management
- All tool calls: PowerShell commands

## Linux
- **Default mode — always assume non-privileged unless user says otherwise**
- Use bash/zsh commands
- Package managers: `apt`, `yum`, `pacman` (detect available)
- Use `sudo` only when explicitly requested
- All tool calls: bash commands
