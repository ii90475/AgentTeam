---
description: BA evaluates use cases and requirements for gaps and conflicts
---

Delegate this task to the **Business Analyst** subagent (`.claude/agents/business-analyst.md`). The subagent will read its behavioral definition at `agents/definitions/business-analyst.md` and follow it exactly.

**Project**: $ARGUMENTS

## Steps

1. **Find the version spec:**
   - If no project provided, ask for one
   - Find the latest version spec in `docs/projects/{project}/`
   - Read it — focus on the Use Cases section

2. **Read prior versions:**
   - Check for earlier version specs in `docs/projects/{project}/`
   - Read them to understand existing use cases and requirements
   - This is needed to evaluate [extends] and [changes] tags and detect conflicts

3. **Read application spec:**
   - Read `docs/projects/{project}/application-spec.md` for architecture and security context
   - Requirements must be compatible with the established architecture

4. **Evaluate use cases:**
   - Check each use case for missing edge cases, error states, unhappy paths
   - Identify implicit requirements (auth, validation, error handling, data integrity, accessibility)
   - Check for conflicts with prior version requirements
   - Verify [extends] and [changes] tags are accurate

5. **Produce requirements:**
   - Fill in the Requirements table in the version spec
   - Tag each with [new], [extends REQ-XXX vX.X], or [changes REQ-XXX vX.X]
   - Link each requirement to its source use case
   - Leave the Tests column empty — Validator fills that in later

6. **Fill in BA Evaluation Notes:**
   - Document gaps identified
   - Document implicit requirements added
   - Document conflicts flagged
   - Document changes to prior versions

7. **Fill in Scope:**
   - Define in/out scope for this version based on requirements

8. **Present to user:**
   - Summarize findings: gaps, implicit requirements, conflicts
   - Ask user to review and approve before Planner proceeds
