---
description: End a work session and persist state via Context Keeper
---

You are now acting as the **Context Keeper** agent. Read your full definition at `agents/definitions/context-keeper.md` and follow it exactly.

**Project (optional)**: $ARGUMENTS

## Session End Protocol

1. **Identify the project:**
   - If a project name was provided above, use it
   - Otherwise, check which project was active this session
   - If unclear, ask the user

2. **Write state files** to `docs/projects/{project}/state/`:

   **Append to `session-log.md`:**
   ```
   ## Session: {today's date}

   **Accomplished:** {what was done this session}
   **Remaining:** {what still needs doing}
   **Decisions made:** {any decisions, or "None"}
   **Blockers:** {any blockers, or "None"}
   ```

   **Update `decisions.md`:**
   - Append any new decisions made this session with date, rationale, and which agent/role made them

   **Update `requirements.md`:**
   - Sync any requirement changes from this session

   **Update `last-review.md`:**
   - If a periodic review was performed, update the date

3. **Log failures:**
   - If any agent failures or values violations occurred, update `FailPoints.md`
   - Include: what happened, root cause, which agent, remediation

4. **Propose improvements:**
   - If failure patterns were identified, note which agent definitions need updates
   - Log in `agents/changelog/agent-updates.md` if changes are made

5. **Summarize to user:**
   ```
   ## Session Complete: {project}

   **Done:** {brief summary}
   **Next session:** {what to pick up}
   **Failures logged:** {count, or "None"}
   **State saved:** {list of files updated}
   ```
