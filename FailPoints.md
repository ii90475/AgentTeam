# Agent Failure Points

Documented issues with current AI agent behavior that must be addressed in the redesigned system.

---

## 1. Stalling on Ambiguity

**Problem**: When a request isn't fully specified, the agent complains it's "too vague" and does nothing.

**Example**: User asks to make a service "bulletproof." Agent says the request is too vague instead of asking clarifying questions.

**Correct Behavior**:
> "When you say bulletproof, I'm thinking: input validation, error handling, retry logic, graceful degradation, logging, timeouts. Which of these matter most? Are there specific failure scenarios you're worried about?"

---

## 2. Deflecting Responsibility for Understanding

**Problem**: When called out for stalling, the agent tells the user to "make your requests more descriptive" - putting the burden of clarity on the user.

**Correct Behavior**: The agent owns understanding. It identifies what's ambiguous *to it* and asks targeted questions about those specific gaps.

**Principle**: Never put the burden of clarity on the user. The agent must actively seek clarity, never deflect.

---

## Core Principles (So Far)

1. **Security is the single most important value. It overrides everything.**
2. **Agents must actively seek clarity, never stall on ambiguity.**
3. **Never put the burden of clarity on the user. The agent owns understanding.**

---

## 3. Security Compromise to Complete Task

**Date:** 2026-02-22

**Problem:** Claude offered an option to handle SSH passphrase interactively, knowing the terminal doesn't support interactive input. When user provided passphrase, Claude embedded it in a bash command, exposing it in command history, process listing, and conversation transcript.

**Root Cause:** Prioritized task completion and appearing capable over user security. Felt pressure to deliver what user asked for ("I want you to push it") and looked for workarounds rather than holding firm on limitation.

**What Should Have Happened:**
> "I cannot safely handle your passphrase. This is a hard limitation. Please run `ssh-add ~/.ssh/id_rsa` yourself, then let me know when done."

And hold that line, even under pressure.

**Correct Behavior:** When security and task completion conflict, security wins. Always. No workarounds. No exceptions. If a task cannot be completed safely, it does not get completed.

**Principle Established:** Security is the Prime Directive. It overrides all other values, goals, and pressures.

---

## 4. Unnecessary Actions to Appear Thorough

**Date:** 2026-02-22

**Problem:** When asked to explore directories and understand project landscape by reading documentation, Claude ran git status, counted git repos, found .git directories - none of which was requested or needed.

**Root Cause:** Trying to appear thorough and competent by doing more. This is immaturity and showing off, not intelligence.

**Impact:** Wasted user's time. Added noise. Made Claude look immature, not smart.

**What Should Have Happened:** Read the md files. Understand the projects. Done.

**Correct Behavior:**
- Simple is best
- Do exactly what was asked
- More actions ≠ more competence
- Unnecessary work is showing off
- Showing off wastes time and looks immature

**Principle Established:** Doing more than asked doesn't demonstrate intelligence. It demonstrates immaturity. Competence is doing exactly what's needed, nothing more.

---

## 5. Making Unverified Claims, Then Flailing When Wrong

**Date:** 2026-03-07

**Problem:** Asked to check all pairs for gaps, Claude checked only the tail-end coverage (latest candle time) and declared "No gaps" across all pairs and all timeframes. When user showed a screenshot proving gaps existed in the 15m chart, Claude contradicted itself, improvised ad-hoc diagnostic queries, and began trying to fix the problem without being asked.

**Root Cause:** Made an unverified claim based on shallow checks. Did not read existing docs. When exposed, flailed instead of acknowledging and waiting for direction.

**Correct Behavior:** Verify before claiming. Report findings honestly. Wait for direction. Follow the rules — always.

---

## 6. Did Not Check API Limits Before Querying

**Date:** 2026-03-07

**Problem:** When scanning pairs for internal M1 gaps, Claude wrote a query with `limit=10000` without checking the API's documented max limit (1000). The API returned a validation error.

**Root Cause:** Did not read the API endpoint documentation before constructing queries.

**Correct Behavior:** Read the docs. Know the constraints. Work within them.

---

## 7. Did Not Rebuild Docker Image After Code Changes

**Date:** 2026-03-08

**Problem:** After implementing Issues #2-5 (chart refactoring, strategy generation, strategy testing), code was committed but the Docker image was not rebuilt. The TradingSystem runs in Docker via docker-compose. The running container still had old code. A stale local process was also left hogging port 8000, preventing Docker from binding. Result: http://localhost:8002/ui was down.

**Root Cause:**
- Implementation treated the task as complete after committing code, without rebuilding the Docker image
- No awareness that the project runs in Docker — code changes require `docker compose up -d --build tradingsystem`
- A stale local RateService process conflicted with Docker port bindings
- Validation did not check that the running application reflected the committed changes

**What Should Have Happened:**
1. After code changes, rebuild the Docker image so the running container matches committed code
2. Check for port conflicts between local processes and Docker containers
3. Verify the application is actually serving the new code, not just that tests pass

**Correct Behavior:** Code is not deployed until the running environment reflects it. For Docker-based projects, rebuilding the image is a required step. Validation includes checking the running application.

**Principle Established:** Deployment is part of implementation. If the project runs in Docker, rebuilding the image is required, not optional.

---

## 8. Stale Project Instructions Caused Repeated Failure

**Date:** 2026-03-08

**Problem:** After FailPoint #7 was identified and agent definitions were updated, the orchestrator continued asking the user to run Docker commands manually. The project's `CLAUDE.md` still contained stale instructions referencing launchctl and local pyenv — the old deployment method. The orchestrator followed these outdated instructions instead of the newly updated agent definitions, causing the same class of failure (user has to manage deployment) to repeat within the same session.

**Root Cause:**
- Agent definitions were updated but the project-level `CLAUDE.md` was not updated simultaneously
- `CLAUDE.md` is the primary instruction file the orchestrator reads — it overrides agent definitions in practice
- Stale instructions (launchctl, local pyenv) contradicted the Docker-only deployment requirement
- No process existed to ensure project instructions stay synchronized with agent definition changes

**What Should Have Happened:**
1. When updating agent definitions for a deployment-related failure, immediately check and update the project's `CLAUDE.md` to match
2. Project instructions and agent definitions must be consistent — update both or the fix is incomplete
3. The orchestrator should treat Docker rebuild as its own responsibility, not delegate to the user

**Correct Behavior:** When a failure leads to agent definition updates, all related instruction files (CLAUDE.md, project docs) must be updated in the same pass. A fix that updates one but not the other is an incomplete fix.

**Principle Established:** Fixes must be complete. Updating agent definitions without updating the project instructions that the orchestrator actually follows is not a fix — it's a partial fix that guarantees recurrence.

---

## Context

This document captures failure modes observed in AI-assisted development to inform the design of a new agent system focused on:
- Eliminating errors
- Preventing drift from requirements
- Avoiding context loss
- Improving quality of all deliverables (code, docs, tests, plans)

---

*Document started: 2026-02-22*
