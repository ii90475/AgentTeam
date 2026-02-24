---
description: Create a new version spec for a project
---

Create a new version spec for a project release.

**Project and version**: $ARGUMENTS

## Steps

1. **Parse arguments:**
   - If no arguments provided, ask for project name and version number
   - If only project provided, ask for version number

2. **Validate project:**
   - Check `docs/projects/{project}/` exists
   - Check `docs/projects/{project}/application-spec.md` exists — if not, ask if user wants to create one first

3. **Check for prior versions:**
   - Look for existing version specs in `docs/projects/{project}/`
   - If prior versions exist, read the most recent to understand current use cases and requirements

4. **Create version spec:**
   - Copy `docs/templates/version-spec-template.md` to `docs/projects/{project}/version-{version}.md`
   - Fill in project name, version, and date

5. **Prompt user for use cases:**
   - Tell user to add their use cases to the new version spec
   - Remind them to tag with [new], [extends UC-XXX vX.X], or [changes UC-XXX vX.X]
   - When user is done, run `/evaluate-requirements {project}` to have BA evaluate
