---
description: Generate release notes, update changelog, tag release
---

Prepare a release for a project version.

**Project and version**: $ARGUMENTS

## Steps

1. **Parse arguments:**
   - If no arguments provided, ask for project name and version
   - If only project provided, check latest version spec for version number

2. **Validate:**
   - Read `docs/projects/{project}/version-{version}.md`
   - Verify all requirements have status Done or explicitly deferred
   - Verify all tests have status Pass or explicitly skipped with reason
   - If not ready, list what's incomplete and stop

3. **Generate release notes:**
   - Read the version spec's requirements and implementation plan
   - Write the Release Notes section in the version spec
   - Write for end users, not developers

4. **Update changelog:**
   - Read `docs/projects/{project}/changelog.md`
   - Add a new version section following Keep a Changelog format
   - Group changes: Added, Changed, Fixed, Removed, Security
   - Each entry must trace to a requirement

5. **Update version history:**
   - Add entry to version spec's bottom if not already present

6. **Tag git:**
   - Ask user for confirmation before tagging
   - Tag as `{project}-v{version}`

7. **Summarize to user:**
   - Show release notes
   - Show changelog entry
   - Confirm git tag
   - Note any deferred requirements for next version
