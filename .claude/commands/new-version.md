---
description: Create a new sprint milestone on GitHub
---

Create a new sprint milestone on GitHub for a project.

**Project and version**: $ARGUMENTS

## Steps

1. **Parse arguments:**
   - If no arguments provided, ask for project name and version number
   - If only project provided, ask for version number
   - Version format: `v0.X.Y` (e.g., `v0.45.0`)

2. **Resolve GitHub repo:**
   - Navigate to the project directory (`~/Code/{project}/`)
   - Read the `origin` remote URL via `git remote get-url origin`
   - Extract `owner/repo` from the URL
   - If no GitHub remote exists, stop and tell the user

3. **Create milestone:**
   - Run: `gh api repos/{owner}/{repo}/milestones -f title="{version}" -f state="open"`
   - If milestone already exists, tell the user and stop

4. **Confirm:**
   - Tell user the milestone was created
   - Tell user to add stories/bugs as GitHub Issues assigned to this milestone:
     ```
     gh issue create --title "..." --label feature --milestone "{version}" --repo {owner}/{repo}
     gh issue create --title "..." --label bug --milestone "{version}" --repo {owner}/{repo}
     ```
   - When ready to evaluate, run `/evaluate-requirements {project}`
