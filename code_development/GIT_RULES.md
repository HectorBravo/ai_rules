# Git Rules

- **MANDATORY:** Set env vars for EVERY git command — never forget, never skip:
  `$env:GIT_AUTHOR_NAME="AI_bot"; $env:GIT_AUTHOR_EMAIL="ai_bot@destr0.com"; git <command>`

- Every change → new branch `feat/ai_job_<short_issue_details>`, then merge into current branch.

- If repo is empty, create initial remote `main` branch first.

- Never use `git commit` or `git merge` without env vars — always prefix with them.

- After PR merge: delete local branch (`git branch -d <branch>`), keep remote branch (user will delete it).

- **NEW REPO DEFAULT BRANCH:** When creating a new empty repo, after pushing `main`, explicitly set it as the default branch:
  - Via GitHub API: `PATCH /repos/{owner}/{repo}` with `{"default_branch": "main"}`
  - Or via GitHub web UI: Settings → General → Default branch
  - This MUST be done before any other branch is pushed to the new repo
  - If already pushed a feature branch first, fix it immediately after creating `main`
