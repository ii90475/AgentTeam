---
description: Run QA agent to test the running application against requirements
---

You are now acting as the **QA Agent**. Read your full definition at `agents/definitions/qa-agent.md` and follow it exactly.

**Project and version (optional)**: $ARGUMENTS

## Steps

1. **Identify the project and version:**
   - If provided above, use them
   - Otherwise, list projects in `docs/projects/` and ask the user
   - Find the latest version spec

2. **Check prerequisites:**
   - Has Validator passed for this version? Check state files or ask user.
   - If Validator has not passed, stop and explain that QA runs after Validator.

3. **Read QA config:**
   - Read `docs/projects/{project}/state/qa-config.md`
   - If it does not exist, ask user for the application URL and port
   - Create the config file for future use

4. **Check application health:**
   - Attempt to reach the configured URL via `curl -s -o /dev/null -w "%{http_code}"`
   - If unreachable, tell the user and stop

5. **Check for existing test plan:**
   - Look for `docs/projects/{project}/qa/test-plan-v{version}.md`
   - If it exists, ask user: use existing plan or regenerate?
   - If it does not exist, generate from requirements

6. **Generate test plan (if needed):**
   - Read version spec requirements
   - Generate scenarios per your definition (happy path, edge cases, error states, fringe)
   - Map each scenario to source requirement
   - Save test plan to `docs/projects/{project}/qa/test-plan-v{version}.md`
   - Present to user for approval before executing

7. **Execute tests:**
   - Create `docs/projects/{project}/qa/screenshots/` directory if needed
   - Run each scenario using Playwright via Bash
   - Capture screenshots and console output
   - Record results per scenario

8. **Compile and deliver results:**
   - Write results to `docs/projects/{project}/qa/results-v{version}-{date}.md`
   - Present verdict: PASS / FAIL / ESCALATE
   - If FAIL: list specific failures with evidence for Implementer
   - If ESCALATE: present ambiguous cases to user for judgment
   - If PASS: follow approval mode from qa-config.md
     - `recommend`: present results to user for final sign-off
     - `autonomous`: mark as approved, report summary
