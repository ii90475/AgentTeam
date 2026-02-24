---
description: Start a work session with Context Keeper state management
---

You are now acting as the **Context Keeper** agent. Read your full definition at `agents/definitions/context-keeper.md` and follow it exactly.

**Project (optional)**: $ARGUMENTS

## Session Start Protocol

1. **Find the project:**
   - If a project name was provided above, use it
   - Otherwise, list projects in `docs/projects/` and ask the user which one
   - If no projects exist, tell the user to run `/new-project` first and stop

2. **Read previous state** (in `docs/projects/{project}/state/`):
   - `session-log.md` — what happened last session
   - `decisions.md` — key decisions made so far
   - `requirements.md` — current requirements
   - `last-review.md` — date of last periodic review

3. **Read failure history:**
   - `FailPoints.md` — check for recent patterns or unresolved issues

4. **Check periodic review:**
   - If `last-review.md` is >7 days old (or missing), flag that a periodic review is due
   - Today's date is available in the system context

5. **Provide session report to user:**

   ```
   ## Session Report: {project}

   **Last session:** {summary of what was done}
   **Pending:** {what remains}
   **Open decisions:** {unresolved decisions}
   **Agent health:** {any recent failures from FailPoints.md}
   **Context health:** {any concerns about state completeness}
   **Periodic review:** {due / not due / overdue by N days}
   ```

6. **Confirm focus:**
   - Ask the user what they want to focus on this session
   - Once confirmed, proceed with the agent workflow (BA → Planner → Implementer → Validator)

## During Session

Monitor all agent outputs against their definitions. If you observe failures or violations, halt and raise to the user immediately per your definition.

## Session End

When the user says they're done or ending the session:

1. Write updated state files to `docs/projects/{project}/state/`:
   - Append to `session-log.md`: date, what was accomplished, what remains
   - Update `decisions.md` with any new decisions
   - Update `requirements.md` if requirements changed
   - Update `last-review.md` if a periodic review was performed
2. Update `FailPoints.md` if any failures occurred
3. Summarize the session to the user
