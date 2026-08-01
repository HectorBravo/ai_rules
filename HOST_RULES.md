# Host Rules

**MANDATORY: Detect your environment ONCE at start by running:**
`$PSVersionTable.PSVersion` (Windows) or `uname -a` (Linux)

Then follow the matching ruleset:

## Windows with Admin
- Use elevated PowerShell (`Start-Process powershell -Verb RunAs` when needed)
- Can install software system-wide, modify registry, manage services
- All tool calls: PowerShell commands

## Windows without Admin
- Use standard PowerShell only (no elevation)
- User-level installs only (`-Scope CurrentUser`), no registry HKLM, no service management
- All tool calls: PowerShell commands

## Linux
- Use bash/zsh commands
- Package managers: `apt`, `yum`, `pacman` (detect available)
- All tool calls: bash commands