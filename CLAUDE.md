# Claude Code Instructions for ZoogHQ

## Git Workflow

### Environments by Repository

| Repository | Branches | Environments |
|------------|----------|--------------|
| ZoogFrontEnd | `develop` → `main` | QA → Production |
| ZoogCloudFunctions | `develop` → `main` | QA → Production |
| ZoogIOS | `develop` → `main` | QA → Production |
| Hailey | `main` only | Production only |

### Branching Rules

**ZoogFrontEnd, ZoogCloudFunctions, ZoogIOS:**
- Branch from `develop`
- Create PRs against `develop`

**Hailey:**
- Branch from `main`
- Create PRs against `main`

## GitHub Issue Naming Convention

Use the format: `[TYPE] REPO-PREFIX-### description`

Types: `[BUG]`, `[FEATURE]`, `[TASK]`

### Repository Prefixes

| Repository | Prefix |
|------------|--------|
| ZoogFrontEnd | ZOOG-FE |
| ZoogCloudFunctions | ZOOG-CF |
| ZoogIOS | ZOOG-IOS |
| Hailey | HAILEY |

### Examples

- `[BUG] ZOOG-FE-42 Share overlay covers multiple items`
- `[FEATURE] ZOOG-CF-15 Add user analytics endpoint`
- `[TASK] HAILEY-8 Update dependencies`

## Session Naming & Colors

When starting work on an issue, rename your session to match the issue name using `/name`.

### Color Scheme by Repository

| Repository | Color |
|------------|-------|
| ZoogIOS | Blue |
| ZoogCloudFunctions | Red |
| ZoogFrontEnd | Yellow |
| Hailey | Purple |

Example: Working on `[BUG] ZOOG-FE-42 Share overlay bug`
→ Rename session to: `ZOOG-FE-42 Share overlay bug` with yellow color

## Worktree Policy (Local CLI Sessions Only)

> **Note:** This policy applies to local CLI sessions only. Web sessions run in isolated cloud containers and manage their own resources independently.

### Session Detection

Before starting a task, check for `.claude-session-lock` in repo root:
- If lock exists → another session is active → create worktree
- If no lock → create lock file and work directly in repo

### Lock File Format

```
branch: feature/my-branch
started: 2026-01-14T10:30:00Z
```

### Creating a Worktree

```bash
# For ZoogFrontEnd, ZoogCloudFunctions, ZoogIOS:
git worktree add ../[repo]-worktree-[branch] -b [branch] develop

# For Hailey:
git worktree add ../[repo]-worktree-[branch] -b [branch] main

cd ../[repo]-worktree-[branch]
npm install  # if applicable
```

### Cleanup

When task completes:
1. Delete `.claude-session-lock` (if you created it)
2. Remove worktree: `git worktree remove ../[repo]-worktree-[branch]`

### Repository Limits (Local Sessions)

| Repository | Max Sessions | Use Worktrees |
|------------|--------------|---------------|
| ZoogFrontEnd | 2 | Yes |
| ZoogCloudFunctions | 3 | Yes |
| ZoogIOS | 1 | No (Xcode issues) |
| Hailey | 2 | Yes |

### Exceptions

- **ZoogIOS**: Never use worktrees (Xcode compatibility)
- If at max sessions, inform user and wait
