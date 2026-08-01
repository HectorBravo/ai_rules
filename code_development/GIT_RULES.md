# Git Rules

## Identity & Credential Protocol

- **Remote URL Policy:** Always use SSH (`git@github.com:<owner>/<repo>.git`). Never embed credentials in the remote URL. This allows the user to push with their own SSH keys.

- **Bot Identity:** Commits authored as `$env:AI_BOT_NAME` / `$env:AI_BOT_EMAIL` via **PAT**.
  - Authentication: Dynamic PAT injection per command.
  - Identity: Dynamic `git -c` override per command.

## Bot Pushing Rules

- **FORBIDDEN:** `git push origin` — uses SSH and the user's identity.
- **MANDATORY:** Inject PAT into URL: `git push https://$env:AI_BOT_NAME:${env:AI_BOT_TOKEN}@github.com/<owner>/<repo>.git`
- **MANDATORY:** Override user identity: `git -c user.name="$env:AI_BOT_NAME" -c user.email="$env:AI_BOT_EMAIL" commit -m "..."`

## Bot Cloning Workflow

- **MANDATORY:** After cloning a repo created by the bot, immediately clean the remote URL to remove the PAT:
  `git remote set-url origin https://github.com/<owner>/<repo>.git`

## General Rules

- **MANDATORY:** Set env vars for EVERY git command — never forget, never skip:
  `$env:GIT_AUTHOR_NAME="$env:AI_BOT_NAME"; $env:GIT_AUTHOR_EMAIL="$env:AI_BOT_EMAIL"; git <command>`

- Every change → new branch `feat/ai_job_<short_issue_details>`, then merge into current branch.

- If repo is empty, create initial remote `main` branch first.

- Never use `git commit` or `git merge` without env vars — always prefix with them.

- After PR merge: delete local branch (`git branch -d <branch>`), keep remote branch (user will delete it).

- **NEW REPO DEFAULT BRANCH:** When creating a new empty repo, after pushing `main`, explicitly set it as the default branch:
  - Via GitHub API: `PATCH /repos/{owner}/{repo}` with `{"default_branch": "main"}`
  - Or via GitHub web UI: Settings → General → Default branch
  - This MUST be done before any other branch is pushed to the new repo
  - If already pushed a feature branch first, fix it immediately after creating `main`
