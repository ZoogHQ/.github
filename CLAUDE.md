# Claude Code Instructions for ZoogHQ

## MANDATORY: Before Starting Any Task

**STOP. Complete these steps FIRST before writing any code:**

### 1. Rename Session
Run `/name` immediately and set:
- **Name:** `#<issue_number>: <issue_title>`
- **Color:** Based on repository (see table below)

| Repository | Color |
|------------|-------|
| ZoogIOS | Blue |
| ZoogCloudFunctions | Red |
| ZoogFrontEnd | Yellow |
| Hailey | Purple |
| ZoogDBTools | Green |

### 2. Create Branch
```bash
# ZoogFrontEnd, ZoogCloudFunctions, ZoogIOS:
git checkout develop && git pull && git checkout -b feature/<issue-number>-<short-description>

# Hailey, ZoogDBTools:
git checkout main && git pull && git checkout -b feature/<issue-number>-<short-description>
```

### 3. Update Issue Status
Move the GitHub issue to **In Progress** in the Zoog R&D project using:
```bash
ITEM_ID=$(gh project item-list 2 --owner ZoogHQ --format json --limit 50 | jq -r '.items[] | select(.content.number == <ISSUE_NUMBER>) | .id')
gh project item-edit --project-id PVT_kwDOA-dX_s4BMnIR --id $ITEM_ID --field-id PVTSSF_lADOA-dX_s4BMnIRzg72EK4 --single-select-option-id 47fc9ee4
```

---

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

### Creating Bug Issues

When the user asks to create a bug issue, **collect the following details** before creating:

| Field | Required | Options |
|-------|----------|---------|
| **Platform** | Yes | iOS, Frontend, Backend, Hailey, Landing Page, Unsure |
| **Environment** | Yes | QA, Production |
| **Severity** | Yes | P0 (Critical - Fix Now), P1 (High - Next Release), P2 (Normal - To Be Prioritized) |
| **iOS Version** | If iOS | App version (e.g., 2.5.0) |
| **Title** | Yes | Brief description of the bug |
| **Steps to Reproduce** | Yes | Numbered steps to reproduce |
| **Expected vs Actual** | Optional | What should happen vs what happens |

**Repository Mapping:**

| Platform | Repository |
|----------|------------|
| iOS | ZoogIOS |
| Frontend | ZoogFrontEnd |
| Backend | ZoogCloudFunctions |
| Hailey | Hailey |
| Landing Page | .github |
| Unsure | .github |

**Issue Body Format:**
```markdown
## Description
[Bug title]

## Environment
- **Platform:** [Platform]
- **Environment:** [QA/Production]
- **Severity:** [P0/P1/P2 - Label]
- **iOS Version:** [If applicable]

## Steps to Reproduce
[Numbered steps]

## Expected vs Actual Behavior
[If provided]

---
*Reported via Claude Code*
```

**Labels to Apply:**
- `bug` (always)
- Severity label: `p0`, `p1`, or `p2`

### Project Status Workflow

| Status | When to set |
|--------|-------------|
| **Backlog** | Default for new issues |
| **Ready** | Issue is ready to be picked up |
| **In Progress** | Agent picks up the task |
| **In Review** | PR is opened |
| **In QA** | Deployed to QA environment (automated) |
| **Done** | Issue is closed/completed |

### Workflow Steps

1. **Create issue** → Add to Zoog R&D project with Backlog status
2. **Start work** → Set status to **In Progress**, rename session to issue name
3. **Create PR** → Set status to **In Review**, link with "Closes #XXX"
4. **PR merged** → Wait for deployment to QA
5. **Deployed to QA** → Status automatically set to **In QA**
6. **QA verified** → Set status to **Done**, close issue

### GitHub Project Commands

**IMPORTANT: Always run these commands after creating an issue.**

**Zoog R&D Project Info:**
- Project Number: **2**
- Project ID: `PVT_kwDOA-dX_s4BMnIR`
- Status Field ID: `PVTSSF_lADOA-dX_s4BMnIRzg72EK4`

```bash
# Step 1: Get the issue's node ID
ISSUE_ID=$(gh issue view <ISSUE_NUMBER> --repo ZoogHQ/<REPO_NAME> --json id -q '.id')

# Step 2: Add issue to Zoog R&D project via GraphQL (more reliable than gh project item-add)
ITEM_ID=$(gh api graphql -f query="
mutation {
  addProjectV2ItemById(input: {
    projectId: \"PVT_kwDOA-dX_s4BMnIR\"
    contentId: \"$ISSUE_ID\"
  }) {
    item { id }
  }
}" -q '.data.addProjectV2ItemById.item.id')

# Step 3: Set status to Backlog (default for new issues)
gh project item-edit --project-id PVT_kwDOA-dX_s4BMnIR --id $ITEM_ID --field-id PVTSSF_lADOA-dX_s4BMnIRzg72EK4 --single-select-option-id f75ad846
```

### Status Option IDs (Zoog R&D)

| Status | Option ID |
|--------|-----------|
| Backlog | `f75ad846` |
| Ready | `61e4505c` |
| In Progress | `47fc9ee4` |
| In Review | `df73e18b` |
| In QA | `19d16395` |
| Done | `98236657` |

### Quick Reference: Setting Status

```bash
# Set to Backlog
gh project item-edit --project-id PVT_kwDOA-dX_s4BMnIR --id $ITEM_ID --field-id PVTSSF_lADOA-dX_s4BMnIRzg72EK4 --single-select-option-id f75ad846

# Set to In Progress
gh project item-edit --project-id PVT_kwDOA-dX_s4BMnIR --id $ITEM_ID --field-id PVTSSF_lADOA-dX_s4BMnIRzg72EK4 --single-select-option-id 47fc9ee4

# Set to In Review
gh project item-edit --project-id PVT_kwDOA-dX_s4BMnIR --id $ITEM_ID --field-id PVTSSF_lADOA-dX_s4BMnIRzg72EK4 --single-select-option-id df73e18b

# Set to Done
gh project item-edit --project-id PVT_kwDOA-dX_s4BMnIR --id $ITEM_ID --field-id PVTSSF_lADOA-dX_s4BMnIRzg72EK4 --single-select-option-id 98236657
```
