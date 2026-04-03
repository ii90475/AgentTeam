# Git Conventions

All projects managed by the agent team follow these conventions.

## Versioning: Semantic Versioning (Major.Minor.Patch)

All projects use [SemVer](https://semver.org/): `Major.Minor.Patch`

| Component | When to Bump | Example |
|-----------|-------------|---------|
| **Major** | Breaking changes, user decides | `1.0.0` → `2.0.0` |
| **Minor** | New feature (backwards compatible) | `1.0.0` → `1.1.0` |
| **Patch** | Bug fix (backwards compatible) | `1.0.0` → `1.0.1` |

**Label-to-version mapping:**

| Label | Version Impact |
|-------|---------------|
| `feature` | Minor bump |
| `bug` | Patch bump |
| `chore` | Patch bump (unless user specifies Minor) |

User determines Major bumps. Never auto-bump Major.

## Commit Message Schema

Format: `<type>(#<issue>): <description>`

```
feat(#12): add daily report view for job matches
fix(#7): handle IMAP connection timeout gracefully
chore(#15): add SQLAlchemy to requirements.txt
```

### Types

| Type | Meaning | Version Impact |
|------|---------|---------------|
| `feat` | New feature | Minor |
| `fix` | Bug fix | Patch |
| `chore` | Maintenance, dependencies, config | Patch |
| `docs` | Documentation only | None |
| `test` | Adding or fixing tests | None |
| `refactor` | Code change that neither fixes nor adds | None |

### Rules

- Always reference the issue number: `feat(#12): ...`
- Description is lowercase, imperative mood: "add" not "added" or "adds"
- Keep under 72 characters
- No period at the end
- Body (optional) separated by blank line, explains **why** not **what**

### Multi-commit PRs

When a PR has multiple commits, each follows the schema. The PR title follows the same format as the primary commit.

## Branch Naming

| Pattern | Use |
|---------|-----|
| `feature/{issue#}-short-desc` | New functionality |
| `fix/{issue#}-short-desc` | Bug fixes |

Examples:
```
feature/12-daily-report-view
fix/7-imap-timeout
```

## Pull Requests

- Title follows commit message format: `feat(#12): add daily report view`
- Body references issue: `Closes #12`
- PR is the merge gate — no unreviewed code reaches `main`

## Changelog

Every sprint/version must have a changelog entry. This is mandatory, not optional.

- Changelog lives at `docs/projects/{project}/changelog.md`
- Follows [Keep a Changelog](https://keepachangelog.com/) format
- Implementer invokes Changelog Writer agent after code commits, before submitting to Validator
- Validator checks for changelog presence — missing changelog = NEEDS_CHANGES
- Committed as part of the sprint PR: `docs(#<issue>): update changelog for v<version>`

## Tags and Releases

- Tags match version: `v1.0.0`, `v0.2.1`
- Sprint = Version = Milestone = Tag
- `/release` creates the tag and GitHub Release

## Who Does What

| Agent | Git Responsibility |
|-------|-------------------|
| **Implementer** | Creates branch, commits (using this schema), pushes, opens PR |
| **Validator** | Reviews PR, approves or requests changes |
| **Project Manager** | Creates milestones, assigns issues |
| **Changelog Writer** | Generates changelog from closed issues in milestone |
| **Context Keeper** | Reads milestone/issue state at session start |
| **QA Agent** | Posts test results as PR comments |
