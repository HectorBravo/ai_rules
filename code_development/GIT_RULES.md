# Git Rules

- All git operations use `AI_BOT` / `ai_bot@destr0.com` via env vars (never alters global config):
  `$env:GIT_AUTHOR_NAME="AI_bot"; $env:GIT_AUTHOR_EMAIL="ai_bot@destr0.com"; git commit -m "msg"`
- Every change → new branch `feat/ai_job_<short_issue_details>`, then merge into current branch.
- If repo is empty, create initial remote `main` branch first.
