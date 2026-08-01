# AI Rules

Centralized ruleset for AI agents.

## Structure

```
ai_rules/
├── README.md
├── AI_RULES.md          # Main entry point
├── HOST_RULES.md        # Host environment detection & rules
├── .env.sample          # Sample config (copy to .env)
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

Copy `.env.sample` to `.env` and adjust as needed:

```bash
cp .env.sample .env
```

- `.env` is **ignored** by git (local-only)
- `MAX_SUBAGENTS=<number>` — max concurrent subagents

## User & Bot Identity Setup

### User Setup (Global)

Set your identity globally so all your commits are attributed to you:

```powershell
# Set your global identity
git config --global user.name "Your Name"
git config --global user.email "your@email.com"

# Set your global credential helper (Windows Keyring)
git config --global credential.helper manager
```

### Bot Setup (Per-Repo)

The bot uses **dynamic injection** to maintain its own identity without polluting your global config:

#### How to get a Bot PAT

**GitHub:**

1. Go to **GitHub Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**.
2. Click **Generate new token**.
3. Name it (e.g., `AI_BOT`).
4. Set expiration (e.g., 90 days).
5. **Repository access:** Select "Only select repositories" and add your repos.
6. **Permissions:**
   - **Contents:** Read & Write
   - **Pull requests:** Read & Write
   - **Administration:** Read & Write (needed to create repos)
   - **Metadata:** Read-only
7. Click **Generate token** and copy it.

**GitLab:**

1. Go to **GitLab Settings** → **Access Tokens**.
2. Click **New personal access token**.
3. Name it (e.g., `AI_BOT`).
4. Set expiration (e.g., 90 days).
5. **Scopes:** Select `api`, `read_api`, `read_repository`, `write_repository`, `sudo`.
6. Click **Create personal access token** and copy it.

1. **Store bot PAT** in a global `.env` file (e.g., `D:\repos\.env`):
   ```
   BOT_TOKEN=glpat_xxxxxxxxxxxx
   AI_BOT_EMAIL=ai_bot@sample.com
   ```

2. **Load bot PAT** in your shell profile (`.bashrc`, `.zshrc`, or `profile.ps1`):
   ```powershell
   $env:BOT_TOKEN = (Get-Content "D:\repos\.env" | Where-Object { $_ -match "^BOT_TOKEN=" }).Split("=")[1]
   ```

3. **Bot pushes** use dynamic injection:
   ```powershell
   # Override identity + inject PAT
   git -c user.name="AI_bot" -c user.email="$env:AI_BOT_EMAIL" commit -m "bot commit"
   git push https://AI_bot:${env:BOT_TOKEN}@github.com/<owner>/<repo>.git
   ```

### Identity Separation

| Action | Identity (Author) | Authentication |
|---|---|---|
| **You push** (`git push`) | Your Name (Global) | Your SSH Key (Global) |
| **Bot pushes** (`git push https://AI_bot:${TOKEN}@...`) | AI_bot (Injected) | Bot PAT (Injected) |
