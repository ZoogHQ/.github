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

Use the format: `REPO-PREFIX-### description`

Set the GitHub Issue Type (Bug, Feature, Task) instead of using title prefixes.

### Repository Prefixes

| Repository | Prefix |
|------------|--------|
| ZoogFrontEnd | ZOOG-FE |
| ZoogCloudFunctions | ZOOG-CF |
| ZoogIOS | ZOOG-IOS |
| Hailey | HAILEY |

### Issue Types

| Type | Use for |
|------|---------|
| Bug | Defects, issues, broken functionality |
| Feature | New functionality |
| Task | Maintenance, refactoring, chores |

### Examples

- `ZOOG-FE-42 Share overlay covers multiple items` (type: Bug)
- `ZOOG-CF-15 Add user analytics endpoint` (type: Feature)
- `HAILEY-8 Update dependencies` (type: Task)

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

## Testing & Verification

### Before Creating a PR

1. **Deploy locally** and test your changes
2. **Use browser automation** (Claude in Chrome) to verify the fix works
3. **Take a screenshot** showing the issue is resolved
4. **Attach the screenshot** to the PR description

### PR Screenshots

When closing a bug, include before/after screenshots in the PR to demonstrate the fix works. Use the GIF recording feature for interaction bugs.

## Issue Workflow

### Creating Issues

1. **Add to project**: All new issues go to the **Zoog R&D** project
2. **Repository**: Infer from context which repo the issue belongs to. If unclear, ask the user
3. **Default status**: Backlog (unless specified otherwise)

### Project Status Workflow

| Status | When to set |
|--------|-------------|
| **Backlog** | Default for new issues |
| **Ready** | Issue is ready to be picked up |
| **In Progress** | Agent picks up the task |
| **In Review** | PR is opened |
| **In QA** | Deployed to QA environment (automated) |

### Workflow Steps

1. **Create issue** → Add to Zoog R&D project with Backlog status
2. **Start work** → Set status to **In Progress**, rename session to issue name
3. **Create PR** → Set status to **In Review**, link with "Closes #XXX"
4. **PR merged** → Wait for deployment to QA
5. **Deployed to QA** → Status automatically set to **In QA**
6. **QA verified** → Close issue
