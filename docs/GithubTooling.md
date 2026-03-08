# GitHub Tooling - Conversation Log

**Date:** 2026-03-08

---

## User Request

> I would like your help in determining the best way to use GitHub's features to stage my incremental enhancements and bug fixes to my individual software projects, each being a folder in ~/Code, each being linked and synced to a remote repo on GitHub. I would like the agent team to use this in a simple and task-appropriate and area of responsibility centric manner. I would like to be able to add my agile stories and/or requirements in a kanban and track accordingly. I would like to plan versions as sprints, i.e. Sprint 0.5.0 and have the numbering be the tag we end up using. It would be great to avail branching so we can handle bug fixes while we create new features. Help me plan this. Think about how to make this simple enough to be more helpful than burdensome, and provide me a report and recommendation.

---

## Research Findings

### Project State Summary - ~/Code

**14 projects with .git directories:**

1. **Bot** — No GitHub remote, 2 local branches (master, my-branch), no tags
2. **ClaudeCodingProjectSetup** — GitHub: `ii90475/AgentTeam`, 2 tags (v2.0.0, v3.0.0), 1 local branch + remote
3. **EasyBot** — No GitHub remote, HEAD detached, 13 tags (0.0.0.2→0.0.0.13, master), 1 local branch
4. **RateService** — GitHub: `ii90475/RateService`, Latest tag: v0.44.0 (44 total tags), 2 branches (master + Oanda_History), actively developed
5. **SimpleBotWebHook** — No GitHub remote, master branch, no tags
6. **SimplestWebHookTradingBot** — No GitHub remote, HEAD detached, 13 tags (0.0.0.2→0.0.0.13, master), 1 local branch
7. **Tradernaught_ORIG** — Backup remotes (10.0.0.175 local git server), master branch only, no tags
8. **Tradernaught** — Backup remotes (10.0.0.175 local git server), 2 branches (create, master), no tags
9. **TradingSystem** — GitHub: `ii90475/TradingSystem`, Latest tag: v0.43.0 (37 total tags), actively developed
10. **TradingViewWebHook** — No GitHub remote, detached HEAD, no tags
11. **TSI-Spread_Abbr** — No GitHub remote, HEAD detached, 13 tags (0.0.0.2→0.0.0.13, master)
12. **TSI-Spread** — No GitHub remote, HEAD detached, 13 tags (0.0.0.2→0.0.0.13, master)
13. **WSJ** — GitHub: `ii90475/WSJ`, 1 tag (v0.0.1), 1 main branch, minimal commit history
14. **YTCCSBE** — GitHub: `ii90475/YTCCSBE`, 2 tags (v0.1.0, v0.2.0), 1 main branch

### GitHub Remote Repositories (ii90475 account)

| Project | Remote | Latest Version | Branch Strategy | Status |
|---------|--------|-----------------|-----------------|--------|
| RateService | `ii90475/RateService` | v0.44.0 | master (primary) | Production-ready, 44 versions released |
| TradingSystem | `ii90475/TradingSystem` | v0.43.0 | master (primary) | Production-ready, 37 versions released |
| ClaudeCodingProjectSetup | `ii90475/AgentTeam` | v3.0.0 | main (primary) | Agent framework, 3 versions |
| WSJ | `ii90475/WSJ` | v0.0.1 | main | Early stage (1 commit) |
| YTCCSBE | `ii90475/YTCCSBE` | v0.2.0 | main | Mature (3 commits) |

### Agent Git/GitHub Responsibilities (Current)

**No agent currently performs git operations directly.** Key findings:

- **Context Keeper**: Has Bash access but uses it for reading state and monitoring. No git operations.
- **Project Manager**: Explicitly states "Never modify code files - only documentation." No git operations.
- **Implementer**: Has Bash access and writes code, but no git operations defined.
- **`/release` command**: CLAUDE.md says it should "tag git" but no agent definition implements this.
- **No GitHub integration**: No agent handles pull requests, issue tracking, or GitHub-specific operations.

---

## Recommendation

### Current State

- **5 repos on GitHub** (ii90475): RateService (v0.44.0), TradingSystem (v0.43.0), AgentTeam (v3.0.0), WSJ (v0.0.1), YTCCSBE (v0.2.0)
- **No GitHub features in use** — no Issues, Milestones, Projects, or branching strategies
- **No agent currently handles git/GitHub operations** — this is a gap
- All development happens on `main`/`master` with no branch isolation

---

### Recommended Model: GitHub-Native Sprint Workflow

**Core principle:** One GitHub feature per concern. No duplication between GitHub and local state files.

#### 1. GitHub Features to Use

| Feature | Purpose | Maps To |
|---------|---------|---------|
| **Issues** | Stories, bugs, tasks | BA requirements (REQ-NNN) |
| **Milestones** | Sprint/version grouping | Sprint v0.5.0 |
| **Projects (v2)** | Kanban board | Visual tracking |
| **Labels** | Categorization | Type (feature/bug/chore) |
| **Branches + PRs** | Code isolation & merge gate | Feature/fix work |
| **Tags + Releases** | Version snapshots | `/release` output |

#### 2. Sprint = Version = Milestone = Tag

```
Sprint v0.5.0
  ├── GitHub Milestone: "v0.5.0"
  ├── Issues assigned to milestone (stories + bugs)
  ├── Kanban board filtered by milestone
  ├── Feature/fix branches → PRs → main
  └── When complete: git tag v0.5.0 + GitHub Release
```

The version number IS the sprint name IS the milestone IS the tag. One number, used everywhere.

**GitHub Milestones serve as the sprint container.** No native "Sprint" feature exists in GitHub — Milestones fill this role. They integrate directly with issues, PRs, and `gh` CLI. No special markdown format needed; a milestone is just a title (e.g., `v0.5.0`) and an optional due date.

#### 3. Branching Strategy

Lightweight model — not full GitFlow, just enough structure:

```
main ─────────●────────●────────●──── (always stable, tagged)
               \      /          \
                \    /            \
  feature/123-add-oanda-feed     fix/456-rate-timeout
                  (PR)              (PR)
```

| Branch Pattern | Created From | Merges To | When |
|---------------|-------------|-----------|------|
| `main` | — | — | Always stable, every merge is deployable |
| `feature/{issue#}-short-desc` | `main` | `main` via PR | New functionality |
| `fix/{issue#}-short-desc` | `main` | `main` via PR | Bug fixes |

**PRs are the code merge gate.** When the Implementer finishes work on a feature/fix branch, the PR is how that code gets reviewed by Validator and merged into `main`. The PR description documents what changed, but the PR itself is the mechanism that keeps `main` stable — no unreviewed code reaches `main` without passing through this checkpoint.

**Why not more branches?** Solo developer with agents. Release branches and develop branches add ceremony without value at this scale. Tags on `main` mark releases. If you need to hotfix an old version, branch from the tag.

#### 4. Label Scheme (Minimal)

Three labels only. Version semantics replace priority labels — the SemVer number already communicates scope:

| Label | Color | Version Impact |
|-------|-------|----------------|
| `feature` | green (#0E8A16) | Minor bump |
| `bug` | red (#D93F0B) | Patch bump |
| `chore` | gray (#9E9E9E) | Minor or Patch (user decides) |

User determines Major bumps. No priority labels needed.

#### 5. Kanban Board (GitHub Projects v2)

One project board per repo, four columns:

```
┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
│ Backlog  │→ │ Sprint   │→ │   In     │→ │   Done   │
│          │  │ Planned  │  │ Progress │  │          │
│ Unsorted │  │ Assigned │  │ Branch   │  │ PR merged│
│ ideas &  │  │ to a     │  │ exists,  │  │ or       │
│ future   │  │ milestone│  │ work     │  │ closed   │
│ work     │  │          │  │ active   │  │          │
└──────────┘  └──────────┘  └──────────┘  └──────────┘
```

The "Sprint Planned" column is a fixed name — filter the board by milestone (e.g., `v0.5.0`) to see only the current sprint's issues.

#### 6. Agent Responsibilities (Updated)

| Agent | GitHub Responsibility |
|-------|---------------------|
| **BA** | Creates Issues from requirements. Links REQ-NNN IDs to issue numbers. |
| **Planner** | Adds implementation plan as issue comment. |
| **Implementer** | Creates feature/fix branch. Commits. Opens PR referencing issue (`Closes #123`). |
| **Validator** | Reviews PR. Approves or requests changes via PR comment. |
| **Project Manager** | Creates milestones. Assigns issues to milestones. Moves kanban cards. |
| **Changelog Writer** | Generates changelog from closed issues in milestone. |
| **Context Keeper** | Reads open milestone + issue state at session start. |
| **QA Agent** | Tests, reports results as issue/PR comment. |

All via `gh` CLI — uses whatever auth method is configured via `gh auth login` (SSH key, PAT, etc.).

#### 7. Stories & Requirements

**GitHub Issues ARE the stories.** No separate local markdown library needed.

- **User** creates issues (stories/bugs) via GitHub web UI or `gh issue create`
- **PM** assigns issues to a milestone (sprint)
- **BA** reads issues, writes analysis into `requirements.md` (its workspace for gaps, conflicts, implicit requirements)
- `requirements.md` remains the BA's analytical output, not the source of truth for "what to build" — issues are the source of truth

This avoids duplication between local files and GitHub. One place to look for "what's in this sprint": the milestone.

#### 8. Workflow End-to-End

```
/new-version rateservice v0.45.0
  → PM creates Milestone "v0.45.0" on GitHub
  → User adds stories/requirements as GitHub Issues

/start-session rateservice
  → Context Keeper reads open milestone, lists issues
  → "Sprint v0.45.0: 4 issues, 0 in progress, 0 done"

User: "Work on issue #52"
  → BA evaluates requirements (reads issue body)
  → Planner designs approach (comments on issue)
  → Implementer: git checkout -b feature/52-oanda-feed
  → Implementer: commits, pushes, opens PR "Closes #52"
  → Validator: reviews PR
  → QA: tests, comments results on PR
  → PR merged → Issue auto-closes → Kanban moves to Done

/release rateservice v0.45.0
  → Changelog Writer: generates notes from milestone's closed issues
  → git tag v0.45.0 → GitHub Release created
  → Milestone closed
```

#### 9. Setup Required (One-Time per Repo)

**Prerequisites:**
```bash
brew install gh
gh auth login   # Choose SSH key, PAT, or browser — all work identically
```

**Per repo:**
```bash
# Create GitHub repo (if new project)
gh repo create ii90475/RepoName --private --source . --push

# Create project board
gh project create --title "RepoName" --owner ii90475

# Link project board to repo (use project number from previous command)
gh project link {project-number} --owner ii90475 --repo ii90475/RepoName

# Create labels (3 only)
gh label create feature --color 0E8A16 --repo ii90475/RepoName
gh label create bug --color D93F0B --repo ii90475/RepoName
gh label create chore --color 9E9E9E --repo ii90475/RepoName

# Create first milestone (when starting a sprint)
gh api repos/ii90475/RepoName/milestones -f title="v0.45.0" -f state="open"
```

**This setup is automated by the `/new-project` skill** — the Recruiter agent handles repo creation, project board, linking, and labels as Phase 4 of project scaffolding. See `.claude/commands/new-project.md`.

#### 10. What Changes in Agent Definitions

The following agents need updated definitions to include `gh` CLI operations:

| Agent | Changes Needed |
|-------|---------------|
| project-manager.md | Add: milestone CRUD, issue assignment, kanban management |
| business-analyst.md | Add: create/update GitHub Issues from requirements |
| implementer.md | Add: branch creation, PR creation with `Closes #N` |
| validator.md | Add: PR review comments |
| context-keeper.md | Add: read milestone/issue state at session start |
| changelog-writer.md | Add: pull closed issues from milestone for changelog |
| qa-agent.md | Add: post test results as PR/issue comments |
| recruiter.md | Add: GitHub repo + project board + labels + milestone setup in `/new-project` |

#### 11. What NOT To Do

- **Don't duplicate tracking** — GitHub Issues replace local requirements tracking for active sprints. Keep `requirements.md` as the BA's analysis workspace, but issues are the source of truth for "what's in this sprint."
- **Don't use GitHub Actions** — your agents are the CI/CD. No need to add workflow YAML complexity.
- **Don't use branch protection rules** — solo dev with agents, the validator agent is your review gate.
- **Don't create a monorepo project board** — one board per repo keeps things clean.
- **Don't maintain a local library of story markdown files** — GitHub Issues are the single source of truth. No duplication.

---

## Next Steps

If approved, update the 8 agent definitions and integrate GitHub setup into the `/new-project` skill.
