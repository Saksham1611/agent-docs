---
name: "create-pr"
description: "Create a high-quality pull request for any project type (frontend or backend). Handles multi-repo workspaces, branch safety, dev-config audits, quality gates, conventional commits, and a clear PR description. Use when the user asks to open or prepare a PR."
---

## Overview

This skill produces a PR that is easy to review and safe to merge:
scoped changes, green quality gates, and a clear description with validation steps.

It works in **multi-folder workspaces** where each folder is its own git repository,
and adapts its quality gates based on the detected project type.

---

## Step 1 — Resolve the Target Repository

In a workspace with multiple git repos, first confirm which repo the PR belongs to.

```bash
# From the current working directory, find the repo root
git rev-parse --show-toplevel
```

- If the result is **ambiguous** (user hasn't navigated into a repo), ask:
  > "Which project should the PR target?" and list the repo folders found.
- If clear, proceed with that repo root as the working directory for all subsequent git commands.

---

## Step 2 — Branch Safety Check

```bash
git -C <repo-root> branch --show-current
```

| Current branch | Action |
|---------------|--------|
| `main` / `master` / `develop` | **STOP.** See recovery below. |
| Any other branch | Proceed to Step 3. |

**Recovery when on a protected branch:**

> ⚠️ Branch Protection Triggered: You are on `<branch>`.

Suggest a branch name derived from the staged changes (e.g., `feat/add-user-auth`, `fix/login-redirect`), then provide:

```bash
git -C <repo-root> checkout -b <suggested-branch>
```

---

## Step 3 — Dev-Config Audit

Scan `git diff --cached` (and `git diff`) for patterns that must not reach the PR.

**Universal patterns to flag:**

- `localhost` or `127.0.0.1` outside of test/config files
- Hardcoded secrets, API keys, tokens, or passwords
- `DEBUG=True` / `debug: true` in non-dev config files

If found:
> ⚠️ Found potential dev-only configuration in `<file>`. Exclude before committing?

Suggest: `git restore --staged <file>`

---

## Step 4 — Detect Project Type

Check the repo root for these indicators (evaluate in order):

| Indicator | Project Type |
|-----------|-------------|
| `pyproject.toml` or `requirements.txt` | **Backend (Python)** |
| `package.json` with `next` / `react` / `vite` in deps | **Frontend** |
| `package.json` only | **Frontend / Node** |
| Both present | **Full-stack** — run both gate sets |

---

## Step 5 — Run Quality Gates

### Backend (Python)

| Gate | Command | Required |
|------|---------|----------|
| Tests | `uv run pytest` | Yes |
| Pre-commit hooks | `uv run pre-commit run --all-files` | Yes |
| DB migrations | `uv run alembic upgrade head` | If models changed |

### Frontend / Node

| Gate | Command | Notes |
|------|---------|-------|
| Install deps | `bun install` (preferred) or `npm install` | If lockfile changed |
| Lint | `bun lint` → `npm run lint` → `npx eslint .` | First available |
| Type-check | `bun run type-check` → `npx tsc --noEmit` | If TypeScript |
| Tests | `bun test` → `npm test` | If test suite exists |
| Build | `bun run build` → `npm run build` | Yes |

> **bun preference:** If `bun.lock` or `bun.lockb` exists, use `bun` for all commands.
> If `bun` is not available, inform the user and ask whether to install it or fall back to `npm`/`pnpm`.

If any gate **fails**, stop and show the error. Do not proceed to commit until resolved or explicitly waived by the user.

---

## Step 6 — Conventional Commit

Generate a commit message from the diff:

```
<type>(<scope>): <summary>

Types: feat | fix | chore | refactor | test | docs | perf | style
Scope: optional module or layer name

Examples:
  feat(auth): add OAuth2 provider support
  fix(cart): correct total price calculation on quantity change
  chore: update dependencies to latest patch versions
```

---

## Step 7 — PR Description

Use the template below, adapting the "Files Impacted" section to the project type.

```markdown
## Summary
<!-- 2 sentences: what changed and why -->

## Files Impacted
<!-- Backend: group by Model / Repository / Service / Route -->
<!-- Frontend: group by Component / Hook / Store / Page / API -->

## Validation Steps
<!-- How a reviewer can verify this works locally -->
1. ...
2. ...

## Checklist
- [ ] Quality gates passed (lint / tests / build)
- [ ] No dev-only config in diff
- [ ] PR is scoped to a single concern
- [ ] Migrations generated (backend, if models changed)
- [ ] Screenshots attached (if UI changed)
```

---

## Step 8 — Execute

Run only after all gates pass and the user confirms:

```bash
# Stage and commit
git -C <repo-root> add .
git -C <repo-root> commit -m "<conventional-commit-message>"

# Push and open PR
git -C <repo-root> push -u origin $(git -C <repo-root> branch --show-current)
gh pr create \
  --title "<commit-message>" \
  --body "<pr-description>"
```

> **gh CLI:** If `gh` is not authenticated, run `gh auth status` first.
> If not installed, inform the user and provide manual PR steps.

---

## Notes

- Do not force-push unless the branch is a personal branch and you are certain it is safe.
- If the PR changes any UI, attach screenshots or a short screen recording.
- Keep PRs scoped to a single concern — split unrelated changes into separate PRs.
- For backend-specific details, see `@global_workflows/create-pr-backend.md`.
