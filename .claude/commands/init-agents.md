---
description: Initialize agent team for an existing project
---

Initialize the agent team for an existing project so it can use sustained session-based development.

**Project name**: $ARGUMENTS

## Steps

1. **Validate project exists:**
   - If no project name was provided, ask for one
   - Check if `docs/projects/{project}/` exists
   - If not, ask if the user wants to run `/init-project` first

2. **Create state directory and files:**

   Create `docs/projects/{project}/state/` with these files:

   **state/session-log.md:**
   ```markdown
   # Session Log: {project}

   <!-- Context Keeper appends to this file at the end of each session -->
   ```

   **state/decisions.md:**
   ```markdown
   # Decisions: {project}

   <!-- Key decisions made during development. Context Keeper maintains this file. -->

   | Date | Decision | Rationale | Agent |
   |------|----------|-----------|-------|
   ```

   **state/requirements.md:**
   ```markdown
   # Requirements: {project}

   <!-- Current requirements. Business Analyst owns content, Context Keeper syncs. -->

   ## Functional Requirements

   _To be defined by Business Analyst._

   ## Non-Functional Requirements

   _To be defined by Business Analyst._

   ## Success Criteria

   _To be defined by Business Analyst._
   ```

   **state/last-review.md:**
   ```markdown
   <!-- Last periodic review date. Context Keeper checks this at session start. -->
   Never reviewed
   ```

3. **Add agent team reference to project CLAUDE.md (if one exists):**
   - Check if the project has its own CLAUDE.md
   - If yes, append the agent team reference block (see below)
   - If no, note that the project will use the parent CLAUDE.md

   Agent team reference block:
   ```markdown
   ## Agent Team

   This project uses the agent team defined in:
   `~/AI/ClaudeCodingProjectSetup/agents/`

   At session start, run `/start-session {project}` to activate the Context Keeper.

   Agent workflow: Context Keeper → BA → Planner → Implementer → Validator
   ```

4. **Confirm to user:**
   - List all files created
   - Explain that `/start-session {project}` is now available
   - Explain the agent workflow they'll use
