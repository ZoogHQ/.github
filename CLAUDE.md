# Claude Code Instructions for ZoogHQ

## Git Workflow

### Environments by Repository

| Repository | Branches | Environments |
|------------|----------|--------------|
| ZoogFrontEnd | `develop` → `main` | QA → Production |
| ZoogCloudFunctions | `develop` → `main` | QA → Production |
| ZoogIOS | `develop` → `main` | QA → Production |
| Hailey | `main` only | Production only |
| ZoogDBTools | `main` only | Single environment |

### Branching Rules

**ZoogFrontEnd, ZoogCloudFunctions, ZoogIOS:**
- Branch from `develop`
- Create PRs against `develop`

**Hailey, ZoogDBTools:**
- Branch from `main`
- Create PRs against `main`

## GitHub Issue Naming Convention

Use a clear, descriptive title for issues. Set the GitHub Issue Type (Bug, Feature, Task) instead of using title prefixes.

### Issue Types

| Type | Use for |
|------|---------|
| Bug | Defects, issues, broken functionality |
| Feature | New functionality |
| Task | Maintenance, refactoring, chores |

### Examples

- `Share overlay covers multiple items` (type: Bug)
- `Add user analytics endpoint` (type: Feature)
- `Update dependencies` (type: Task)

## Session Naming & Colors

When starting work on an issue, **immediately rename your terminal session** using `/name`.

### Naming Format

```
#<issue_number>: <issue_title>
```

**Example:** `#2173: Support relative paths for profile pictures`

### Color by Repository

| Repository | Terminal Color |
|------------|----------------|
| ZoogIOS | Blue |
| ZoogCloudFunctions | Red |
| ZoogFrontEnd | Yellow |
| Hailey | Purple |
| ZoogDBTools | Green |

### Example

Working on issue #42 "Share overlay covers multiple items" in ZoogFrontEnd:
→ Run `/name` and set name to `#42: Share overlay covers multiple items` with **yellow** color

## Worktree Policy (Local CLI Sessions Only)

> **Note:** Worktrees and lock files apply to local CLI sessions only. All other policies (session naming, colors, git workflow, testing, issue workflow) apply to **both local and web sessions**.

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
| ZoogDBTools | 2 | Yes |

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

## ZoogDBTools Operations

ZoogDBTools is used for company-wide data operations: DB queries, updates, analysis, and one-off tasks.

### Workflow

No strict PR review process required. Operations follow this sequence:

1. **Dry run on QA** — Run operation with no changes (log only)
2. **Test on QA user** — Execute on a specific test user in QA
3. **User approval** — Get explicit approval before proceeding to production
4. **Run on Production** — Execute on production after approval

### Guidelines

- Always start with a dry run
- Never run directly on production without QA validation
- Document what the operation does before running
- Keep operations idempotent when possible

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
