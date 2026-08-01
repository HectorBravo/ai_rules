# Git Rules

- **MANDATORY:** Set env vars for EVERY git command — never forget, never skip:
  `$env:GIT_AUTHOR_NAME="AI_bot"; $env:GIT_AUTHOR_EMAIL="ai_bot@destr0.com"; git <command>`

- Every change → new branch `feat/ai_job_<short_issue_details>`, then merge into current branch.

- If repo is empty, create initial remote `main` branch first.

- Never use `git commit` or `git merge` without env vars — always prefix with them.

- After PR merge: delete local branch (`git branch -d <branch>`), keep remote branch (user will delete it).
